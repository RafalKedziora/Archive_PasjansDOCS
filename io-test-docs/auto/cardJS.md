# Układanie kart

>Testy wykonali: Piotr Czajkowski oraz Robert Ciołek

Karty zostały przez deweloperów ujęte jako liczba od 0 do 51 włącznie. 
Na podstawie tej liczby karta jest w stanie określić, jaką jest figurą oraz w jakim kolorze.

Sprawdzamy więc, czy zostanie rzucony wyjątek, kiedy podamy nieprawidłowy numer karty:
```javascript
test('throw exception when invalid ID', () => {
    expect(() => {
        new Card(52);
    }).toThrow();
});
```

Następie sprawdzamy działanie funkcji, która zwraca nam figurę:
```javascript
describe("Checking rank getter while id=13, expected:A", () => {
    let card = new Card(13);
    test("Should return A", () => {
        expect(card.rank).toBe("A");
    });
});

describe("Checking rank getter while id=23, expected:J", () => {
    let card = new Card(23);
    test("Should return J", () => {
        expect(card.rank).toBe("J");
    });
});

describe("Checking rank getter while id=24, expected:Q", () => {
    let card = new Card(24);
    test("Should return Q", () => {
        expect(card.rank).toBe("Q");
    });
});

describe("Checking rank getter while id=25, expected:K", () => {
    let card = new Card(25);
    test("Should return K", () => {
        expect(card.rank).toBe("K");
    });
});

describe("Checking rank getter while id=32, expected:7", () => {
    let card = new Card(32);
    test("Should return 7", () => {
        expect(card.rank).toBe("7");
    });
});
```

Oraz działanie funkcji, która zwraca nam kolor:
```javascript
describe("Checking suite() getter while id=12, expected: diamonds", () => {
    let card = new Card(12);
    test("Should return diamonds", () => {
        expect(card.suite).toBe("diamonds");
    });
});

describe("Checking suite() getter while id=13, expected: hearts", () => {
    let card = new Card(13);
    test("Should return hearts", () => {
        expect(card.suite).toBe("hearts");
    });
});

describe("Checking suite() getter while id=38, expected: spades", () => {
    let card = new Card(38);
    test("Should return spades", () => {
        expect(card.suite).toBe("spades");
    });
});

describe("Checking suite() getter while id=51, expected: clubs", () => {
    let card = new Card(51);
    test("Should return clubs", () => {
        expect(card.suite).toBe("clubs");
    });
});
```

Karty mają w sobie również wiedze na temat tego, czy mogą byc kładzione na sobie, tj. czy ruch, który chcemy wykonać, jest prawidłowy:
```javascript

test("Checking isAscendingCardInSuiteTo function", () => {
    let card = new Card(7);
    let card1 = new Card(6);

    expect((card.isAscendingCardInSuiteTo(card1))).toBeTruthy();
});

test("Checking isAscendingCardInSuiteTo function", () => {
    let card = new Card(7);
    let card1 = new Card(19);
    expect((card.isAscendingCardInSuiteTo(card1))).toBeFalsy();
});

test("Checking isAscendingCardInSuiteTo function", () => {
    let card = new Card(33);
    let card1 = new Card(47);
    expect((card.isAscendingCardInSuiteTo(card1))).toBeFalsy();
});

test("Checking isDescendingAndOppositeTo function", () => {
    let card = new Card(12);
    let card1 = new Card(12);
    expect((card.isDescendingAndOppositeTo(card1))).toBeFalsy();
});

test("Checking isDescendingAndOppositeTo function", () => {
    let card = new Card(12);
    let card1 = new Card(12);
    expect((card.isDescendingAndOppositeTo(card1))).toBeFalsy(); //tutaj test był źle ułożony - poprawiłem - Dawid W
});

test("Checking isDescendingAndOppositeTo function", () => {
    let card = new Card(12);
    let card1 = new Card(12);
    expect((card.isDescendingAndOppositeTo(card1))).toBeFalsy();
});
```