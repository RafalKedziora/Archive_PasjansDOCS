# Tworzenie pokoju

>Testy wykonał: Damian Bugaj

W grze multiplayer pokoje są miejscem rozgrywki. 
Komponent, który testowaliśmy, wpuszczał graczy do środka i zarządzał stanem pokoju:
Wszystko to działa na podstawie socket.io, który również został zmockowany.

Sprawdźmy więc, czy możliwe jest wejście do pokoju:
```javascript
test('Update users data with new data', () => {
    act(() => {
        ReactDOM.render(<BrowserRouter><CreateRoom/></BrowserRouter>, container);
    });

    // definuje że socket bedzie mockowany
    jest.mock('./../socketConfig.js');

    // Tworzę pokój
    const initialRoom = {room: 3, users: 2};

    socket.emit('pass-room', initialRoom);
    socket.on('pass-room', ({room, users}) => {
        expect(users).toBe(initialRoom.users);
    });

    const updateRoomData = {room: 3, users: 6};

    socket.emit('pass-room', updateRoomData);
    socket.on('pass-room', ({room, users}) => {
        expect(users).toBe(6);
    });
});
```

Oraz czy po tym liczba graczy się zgadza:
```javascript
test('Compatibility of the number of generated players', () => {
    act(() => {
        ReactDOM.render(<BrowserRouter><CreateRoom/></BrowserRouter>, container);
    });

    // definuje że socket bedzie mockowany
    jest.mock('./../socketConfig.js');

    // Tworzę pokój
    const initialRoom = {room: 1, users: 5};

    let playerRows = container.querySelectorAll('.player-row');

    socket.emit('pass-room', initialRoom);
    socket.on('pass-users', () => {

        //  Sprawdza czy wyrenderowała się piątka graczy
        expect(playerRows.length).toBe(5);

    });
});
```

Każdy z pokoi może również zostać zmodyfikowany, więc sprawdzamy, czy sama gra to umożliwia:
```javascript
test('Checks if room rename is working', () => {
    act(() => {
        ReactDOM.render(<BrowserRouter><CreateRoom/></BrowserRouter>, container);
    });

    let NameRoom = "NameRoom1"
    let input = container.querySelector('input[name="room-name"]');

    fireEvent.change(input,{target: {value: NameRoom}});

    expect(input.value).toBe(NameRoom);

    let form = container.querySelector('form');
    fireEvent.submit(form);

    let Name = container.querySelector('#Name');
    expect(Name.innerHTML).toBe("NameRoom1");
});
```

Pozostało nam przetestować jedynie tworzenie i zapisywanie pokoju:
```javascript
test('Checks if room creation is working', () => {
    act(() => {
        ReactDOM.render(<BrowserRouter><CreateRoom/></BrowserRouter>, container);
    });

    let NameRoom = "Pokoiczek1"
    let input = container.querySelector('input[name="room-name"]');

    fireEvent.change(input,{target: {value: NameRoom}});

    expect(input.value).toBe(NameRoom);


    let GameTime = "5";
    let select = container.querySelector('select[name="game-time"]');

    fireEvent.change(select,{target: {value: GameTime}});
    expect(select.value).toBe(GameTime);

    let StanowoPokoju = container.querySelector('h1[class="lobby__headline"]')
    expect(StanowoPokoju.innerHTML).toBe("Tworzenie pokoju");

    let form = container.querySelector('form');
    fireEvent.submit(form);

    let StanowoPokoju2 = container.querySelector('h1[class="lobby__headline"]')
    expect(StanowoPokoju2.innerHTML).toBe("Pokój utworzony");
});

test('Checks if changes have been saved after creating a room', () => {
    act(() => {
        ReactDOM.render(<BrowserRouter><CreateRoom/></BrowserRouter>, container);
    });

    let NameRoom = "NameRoom1"
    let input = container.querySelector('input[name="room-name"]');

    fireEvent.change(input,{target: {value: NameRoom}});

    expect(input.value).toBe(NameRoom);


    let GameTime = "5";
    let select = container.querySelector('select[name="game-time"]');

    fireEvent.change(select,{target: {value: GameTime}});
    expect(select.value).toBe(GameTime);

    let StanowoPokoju = container.querySelector('h1[class="lobby__headline"]')
    expect(StanowoPokoju.innerHTML).toBe("Tworzenie pokoju");

    let form = container.querySelector('form');
    fireEvent.submit(form);

    let StanowoPokoju2 = container.querySelector('h1[class="lobby__headline"]')
    expect(StanowoPokoju2.innerHTML).toBe("Pokój utworzony");

    let Name = container.querySelector('#Name')
    expect(Name.innerHTML).toBe("NameRoom1");

    let Minutes = container.querySelector('#Minutes')
    expect(Minutes.innerHTML).toBe("5");
});
```