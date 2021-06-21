# Lobby multiplayer

>Testy wykonali: Paulina Gayny


Lobby multiplayer jest miejscem, z którego możemy stworzyć nowy pokój lub też dołączyć do istniejącego. 
Jest sercem rozgrywki multiplayer. Przetestowaliśmy tworzenie nowego pokoju, jak i dołączanie do istniejącego już.

Na początku testujemy czy liczba dostępnych pokoi jest zgodna z liczbą renderowanych na ekranie pokoi:
```javascript
test('The number of rooms is consistent with the number of elements', () => {
    jest.mock('./socketConfig.js');
    socket.on = jest.fn();
    socket.emit = jest.fn();

    let socketMock = new SocketMock();

    socket.emit.mockImplementation((eventKey, ...args) => {
        socketMock.socketClient.emit(eventKey, ...args)
    });
    socket.on.mockImplementation((evt, cb) => {
        socketMock.on(evt, cb)
    });

    act(() => {
        ReactDOM.render(<BrowserRouter><LobbyMultiplayer/></BrowserRouter>, container);
    });

    const usersArray = [{room: 2}, {room: 2}, {room: 3}];
    socket.emit('pass-users', usersArray);

    let roomRows = container.querySelectorAll('.row1');

    socket.on('pass-users', () => {
        expect(roomRows.length).toBe(2);

        expect(roomRows[0].querySelector('.Name').innerHTML).toBe('2');
        expect(roomRows[0].querySelector('.Ppl1').innerHTML).toBe('2');

        expect(roomRows[1].querySelector('.Name').innerHTML).toBe('3');
    });
});
```

A następnie testujemy tworzenie nowego pokoju:

```javascript
test('Clicking create room button results in moving to create room window', () => {

    act(() => {
        ReactDOM.render(<BrowserRouter><LobbyMultiplayer/></BrowserRouter>, container);
    });

    var pathname = window.location.pathname;
    
    expect(pathname).not.toEqual("/create-room"); //it would be better to first emit an event such as start, to fix the pathname so we know it for sure, not to take chances, but I think it would require access to JoinRoom.js script and maybe it wouldn't be neccesary a good thing to do it in unit tests

    fireEvent.click(container.querySelector('#create-room-btn')); //clicking the button

    pathname = window.location.pathname;

    expect(pathname).toEqual("/create-room"); //current window is /create-room
});
```

Jak i dołączenie do jednego, konkretnego:
```javascript
test('Clicking join room button results in moving to game lobby window', () => {

    jest.mock('./socketConfig.js');
    socket.on = jest.fn();
    socket.emit = jest.fn();

    let socketMock2 = new SocketMock();

    socket.emit.mockImplementation((eventKey, ...args) => {
        socketMock2.socketClient.emit(eventKey, ...args)
    });
    socket.on.mockImplementation((evt, cb) => {
        socketMock2.on(evt, cb)
    });

    act(() => {
        ReactDOM.render(<BrowserRouter><LobbyMultiplayer/></BrowserRouter>, container);
    });

    var pathname = window.location.pathname;

    pathname = window.location.pathname;

    expect(pathname).not.toEqual("/game-lobby"); //current window is not /game-lobby

    const usersArray = [{room: 2}];

    socket.emit('pass-users', usersArray);

    socket.on('pass-users', () => {
        let roomRows = container.querySelectorAll('.row1');
        
        expect(roomRows.length).toBe(1);

        expect(roomRows[0].querySelector('.Name').innerHTML).toBe('2');
        expect(roomRows[0].querySelector('.Ppl1').innerHTML).toBe('1');

        fireEvent.click(container.querySelector('#join-btn')); //clicking the button

        expect(pathname).toEqual("/game-lobby"); //current window is /game-lobby
    });

});
```