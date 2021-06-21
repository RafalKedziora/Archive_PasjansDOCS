# Gracze w pokoju

>Testy wykonała: Paulina Gayny

Podczas rozgrywki multiplayer gracze umieszczani są w pokojach. 
Napisaliśmy testy, które sprawdzają, czy możliwe jest dołączenie do pokoju, jego modyfikacja oraz opuszczenie go.

Sprawdźmy więc, czy użytkownik może dołączyć do dowolnego pokoju:
```javascript
test('Users array is longer after adding a new user', () => {
    users.userJoin(999, 'Paulina', 'name_of_the_room')
    expect(users.getAllUsers()).toHaveLength(1);
});
```

Zaraz po tym potwierdzamy, że użytkownik z tym samym **id** nie może znajdować się w tym samym pokoju:
```javascript
test('It is not possible to add two users with the same id', () => {
    users.userJoin(1000, 'user1', 'name_of_the_room')
    users.userJoin(1000, 'user2', 'name_of_the_room')
    expect(users.getAllUsers()).toHaveLength(1);
});
```

Sprawdzamy również, czy możliwe jest wejście, jak i wyjście wielu użytkowników jednocześnie:
```javascript
test('It is possible to add several users at once', () => {
    users.userLeave(1000);
    users.userLeave(1000);
    let i;
    for (i = 0; i < 100; i++) {
        users.userJoin(i, 'user' + i, 'name_of_the_room')
    }
    expect(users.getAllUsers()).toHaveLength(100);
});

test('It is possible to delete several users at once', () => {
    let i;
    for (i = 0; i < 100; i++) {
        users.userLeave(i, 'user' + i, 'name_of_the_room')
    }
    expect(users.getAllUsers()).toHaveLength(0);
});
```

Na końcu sprawdziliśmy czy jest możliwość zmiany nazwy pokoju:
```javascript
test('Modyfing room results in changing a name for this room', () => {
    users.modifyRoom('r1', 'new_name');
    expect(users.getRoomUsers('new_name')).toStrictEqual([{"id": 0, "room": "new_name", "username": "user1"}, {
        "id": 1,
        "room": "new_name",
        "username": "user2"
    }]);
});
```