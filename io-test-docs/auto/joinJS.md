# Dołączenie do pokoju

>Testy wykonała: Paulina Gayny

W grze multiplayer dołączamy do pokoi i tam "spotykamy" się z rywalami.
Testowany komponent sprawdzał jakość działania dołączania do pokoju oraz innych cech związanych z tą cechą aplikacji.
Wszystko to działa na podstawie socket.io, który również został zmockowany.

Sprawdzamy czy nasz pokój istnieje na starcie:
```javascript
test('Export room on start', () => {

    jest.mock('./../socketConfig.js');

    socket.emit = jest.fn();

    act(() => {
        ReactDOM.render(<BrowserRouter><JoinRoom/></BrowserRouter>, container);
    });

    expect(socket.emit).toHaveBeenCalledWith("export-room");
});
```

Sprawdzamy cechę aplikacji jaką jest wyrzucenie użytkownika z danego pokoju:
```javascript
test('User can be kicked', () => {
    jest.mock('./../socketConfig.js');
    socket.on = jest.fn();
    socket.emit = jest.fn();

    socket.emit.mockImplementation((eventKey, ...args) => {
        socketMock.socketClient.emit(eventKey, ...args)
    });
    socket.on.mockImplementation((evt, cb) => {
        socketMock.on(evt, cb)
    });

    act(() => {
        ReactDOM.render(<BrowserRouter><JoinRoom/></BrowserRouter>, container);
    });

    let lobbyModal = container.querySelector('.lobby__modal-container');
    expect(lobbyModal.classList.contains('active')).toBeFalsy();

    socket.on('kicked', () => {
        console.log(lobbyModal.classList.toString())
        expect(lobbyModal.classList.contains('active')).toBeTruthy();
    });

    socket.emit('kicked');
});
```

Sprawdzamy czy pokój jest poprawnie ustawiony przed utworzeniem:
```javascript
test('Inintial data (room name, empty array for players) is properly set before joining the room', () => {
    jest.mock('./../socketConfig.js');
    socket.on = jest.fn();
    socket.emit = jest.fn();

    socket.emit.mockImplementation((eventKey, ...args) => {
        socketMock.socketClient.emit(eventKey, ...args)
    });
    socket.on.mockImplementation((evt, cb) => {
        socketMock.on(evt, cb)
    });

    act(() => {
        ReactDOM.render(<BrowserRouter><JoinRoom/></BrowserRouter>, container);
    });

    //room's name
    let list = container.querySelector('#lobby__created-data_name');
    expect(list).not.toBeNull();

    let listItems = list.querySelectorAll('p');
    expect(listItems.length).toBe(2); //"Nazwa" tag and the room's name

    let room_name = listItems[1].innerHTML;
    expect(room_name).toEqual('test');
    
    //players array
    list = container.querySelector('#lobby__created-data_players');
    expect(list).not.toBeNull();

    listItems = list.querySelectorAll('ul');
    expect(listItems.length).toBe(1);

    let players = listItems[0].innerHTML;
    expect(players).toBe("");
});
```

Sprawdzamy czy przenoszenie do widoku gry działa prawidłowo:
```javascript
test('It is possible to start a room; Current window has changed to game view', () => {
    jest.mock('./../socketConfig.js');
    socket.on = jest.fn();
    socket.emit = jest.fn();

    socket.emit.mockImplementation((eventKey, ...args) => {
        socketMock.socketClient.emit(eventKey, ...args)
    });
    socket.on.mockImplementation((evt, cb) => {
        socketMock.on(evt, cb)
    });

    act(() => {
        ReactDOM.render(<BrowserRouter><JoinRoom/></BrowserRouter>, container);
    });
    

    socket.on('start', (time) => {

        var pathname = window.location.pathname;

        expect(pathname).toEqual("/game-view");
    });

    socket.emit('start', (3000)); //3000 is some "time"
});
```

Sprawdzamy czy pokój jest aktualizowany w sposób prawidłowy, ponieważ ważne jest wyświetlanie poprawnej nazwy etc:
```javascript
test('It is possible to update Room"s state', () => {
    jest.mock('./../socketConfig.js');
    socket.on = jest.fn();
    socket.emit = jest.fn();

    socket.emit.mockImplementation((eventKey, ...args) => {
        socketMock.socketClient.emit(eventKey, ...args)
    });
    socket.on.mockImplementation((evt, cb) => {
        socketMock.on(evt, cb)
    });

    act(() => {
        ReactDOM.render(<BrowserRouter><JoinRoom/></BrowserRouter>, container);
    });

    socket.on('pass-room', ({room, users}) => {

    //room's name
    let list = container.querySelector('#lobby__created-data_name');
    expect(list).not.toBeNull();

    let listItems = list.querySelectorAll('p');
    expect(listItems.length).toBe(2); //"Nazwa" tag and the room's name

    let room_name = listItems[1].innerHTML;
    expect(room_name).toEqual('room_updated');
    
    //players array
    list = container.querySelector('#lobby__created-data_players');
    expect(list).not.toBeNull();

    listItems = list.querySelectorAll('ul');
    expect(listItems.length).toBe(1);

    let players = listItems[0].innerHTML;
    expect(players).not.toBe(""); //it is a sign that something changed; it is no longer an empty array. I believe that in this very moment players "exist" so in the original script, in "lobby_created-data" class, so they can be mapped into player rows. Thus it is no longer an empty string. However it is just my assumption - I think it would be better to use "real fake" players in this test.
    });

    let room_2 = {room: "room_updated", users: "players_update"};

    socket.emit('pass-room', room_2); 
});
```