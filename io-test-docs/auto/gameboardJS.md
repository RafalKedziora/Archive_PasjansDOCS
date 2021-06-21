# Plansza gry

>Testy wykonali: Jakub Podsiadły oraz Damian Bugaj

Plansza jest kluczowym elementem rozgrywki, na niej odbywa się gra. 
Plansza składa się z kilku kluczowych miejsc tj. stos, z którego pobieramy nowe karty, 
7 stosów kart ułożonych w kolumnach rosnąco od lewej do prawej zaczynając od jednej karty w pierwszej kolumnie 
i siedmiu kart ułożonych na sobie w ostatniej kolumnie oraz stosu kart ułożonych już w odpowiedniej sekwencji.

Gra zostaje zakończona, gdy wszystkie karty wylądują na stosach rezultatu w odpowiedniej sekwencji. 
Dlatego też pierwszym testem, jaki przeprowadziliśmy, było sprawdzenie, czy gra na początku nie jest zakończona:

```javascript
test('state is not finish on start', () => {
    let board = new Board();
    expect(board.finishState).toBe(false);
});
```

Następnie sprawdziliśmy, czy stos dostępnych kart istnieje:
```javascript
test("Checking if card deck exists", () => {
    let board = new Board();
    expect(board.deck).toBeDefined();
});
```

Czy stos kart odwróconych istnieje:
```javascript
test("Checking if revealed card stack exists", () => {
    let board = new Board();
    expect(board.revealedCardStack).toBeDefined();
});
```

Czy istnieją stosy rezultatów kart oraz, czy jest ich odpowiednio dużo (powinno być ich 4):
```javascript
test("Checking if result stacks exists", () => {
    let board = new Board();
    expect(board.resultStacks).toBeDefined();
});

test("Checking number of result stacks", () => {
    let board = new Board();
    expect(board.resultStacks.length).toEqual(4);
});
```

Analogicznie zostały sprawdzone stosy kart uczestniczących w grze wraz z ich ilością w każdej z kolumn:
```javascript
test("Checking if game stacks exists", () => {
    let board = new Board();
    expect(board.gameStacks).toBeDefined();
});

test("Checking number of game stacks", () => {
    let board = new Board();
    expect(board.gameStacks.length).toEqual(7);
});

test("Checking if number of cards in game stack 0 is correct", () =>{
    let board = new Board();
    expect(board.gameStacks[0].length).toEqual(1)
});

test("Checking if number of cards in game stack 1 is correct", () =>{
    let board = new Board();
    expect(board.gameStacks[1].length).toEqual(2)
});

test("Checking if number of cards in game stack 2 is correct", () =>{
    let board = new Board();
    expect(board.gameStacks[2].length).toEqual(3)
});

test("Checking if number of cards in game stack 3 is correct", () =>{
    let board = new Board();
    expect(board.gameStacks[3].length).toEqual(4)
});

test("Checking if number of cards in game stack 4 is correct", () =>{
    let board = new Board();
    expect(board.gameStacks[4].length).toEqual(5)
});

test("Checking if number of cards in game stack 5 is correct", () =>{
    let board = new Board();
    expect(board.gameStacks[5].length).toEqual(6)
});

test("Checking if number of cards in game stack 6 is correct", () =>{
    let board = new Board();
    expect(board.gameStacks[6].length).toEqual(7)
});
```

Ostatecznie należało przetestować logikę samej rozgrywki:
```javascript
test("Checking if function to passing card to reveal stack passes the card", () => {
    let board = new Board();

    board.passCardToRevealedStack();
    expect(board.revealedCardStack.length).toEqual(1);
});

test("Making revealed stack full", () => {
    let board = new Board();

    let i = 0;
    while (i < 24){
        board.passCardToRevealedStack();
        i++;
    }
    expect(board.revealedCardStack.length).toEqual(24);
});

test("Passing one more card when the revealed stack full", () => {
    let board = new Board();

    let i = 0;
    while (i < 25){
        board.passCardToRevealedStack();
        i++;
    }
    expect(board.revealedCardStack.length).toEqual(0);
});

test("Checking if stack after reset is the same as before", () => {
    let board = new Board();

    let original_stack = board.deck;

    let i = 0;
    while (i < 25){
        board.passCardToRevealedStack();
        i++;
    }

    i = 0;
    while (i<24){
        expect(board.deck[i]).toBe(original_stack[i])
        i++;
    }
});

test('Passing a card from one game stack to the other', () => {
    let board = new Board();

    board.gameStacks[0][0] = new Card(14); // Dwójka kier
    let card_from_gamestack0 = board.gameStacks[0][0];
    board.gameStacks[1][board.gameStacks[1].length - 1] = new Card(28); // trójka pik

    board.moveBetweenGameStacks(0, 1, 1);

    expect(board.gameStacks[0].length).toEqual(0);
    expect(board.gameStacks[0][0]).toBeUndefined();
    expect(board.gameStacks[1].length).toEqual(3);
    expect(board.gameStacks[1][board.gameStacks[1].length - 1]).toBe(card_from_gamestack0);
});

test('Passing a King card from reveal deck to an empty game stack', () => {
    let board = new Board();

    board.gameStacks[0] = []; //pusty stos
    board.revealedCardStack = [ new Card(12) ]; //Król karo
    
    board.moveFromRevealedToGameStack(0);
    let gamestack0_length = board.gameStacks[0].length;

    expect(gamestack0_length).toEqual(1);
    expect(board.gameStacks[0][0].rank).toBe('K');
    expect(board.revealedCardStack.length).toEqual(0);
});

test('Passing a card other than a King card from reveal deck to an empty game stack', () => {
    let board = new Board();

    board.gameStacks[0] = []; //pusty stos
    board.revealedCardStack = [ new Card(10) ]; //Walet karo
    
    board.moveFromRevealedToGameStack(0);

    let gamestack0_length = board.gameStacks[0].length;

    expect(gamestack0_length).toEqual(0);
    expect(board.revealedCardStack[0].rank).toBe('J');
    expect(board.revealedCardStack.length).toEqual(1);
});

test('Passing correct card from reveal deck to a game stack', () => {
    let board = new Board();

    board.revealedCardStack = [ new Card(14) ]; // Dwójka kier
    let card_from_revealedCardStack = board.revealedCardStack[0];
    board.gameStacks[0] = [ new Card(28) ]; // trójka pik 

    board.moveFromRevealedToGameStack(0);

    let gamestack0_length = board.gameStacks[0].length;

    expect(gamestack0_length).toEqual(2);
    expect(board.gameStacks[0][board.gameStacks[0][board.gameStacks[0].length - 1]]).toBe(card_from_revealedCardStack);
    expect(board.revealedCardStack[0]).toBeUndefined();
    expect(board.revealedCardStack.length).toEqual(0);
});

test('Passing incorrect card from reveal deck to a game stack', () => {
    let board = new Board();

    board.revealedCardStack = [new Card(28) ]; // Dwójka kier
    let card_from_revealedCardStack = board.revealedCardStack[0];
    board.gameStacks[0] = [  new Card(14) ]; // trójka pik 
    let card_from_gamestack0 = board.gameStacks[0][0];

    board.moveFromRevealedToGameStack(0);

    let gamestack0_length = board.gameStacks[0].length;

    expect(gamestack0_length).toEqual(1);
    expect(board.gameStacks[0][board.gameStacks[0][board.gameStacks[0].length - 1]]).toBe(card_from_gamestack0);
    expect(board.revealedCardStack[0]).toBe(card_from_revealedCardStack);
    expect(board.revealedCardStack.length).toEqual(1);
});

test('Passing two cards from one game stack to the other', () => {
    let board = new Board();

    board.gameStacks[0][0] = new Card(14); // Dwójka kier
    let card_from_gamestack0 = board.gameStacks[0][0];
    board.gameStacks[1][board.gameStacks[1].length - 1] = new Card(28); // trójka pik

    board.moveBetweenGameStacks(0, 1, 1);

    board.gameStacks[2][board.gameStacks[2].length - 1] = new Card(16) // czwórka kier

    board.moveBetweenGameStacks(1, 2, 2);

    expect(board.gameStacks[0].length).toEqual(0);
    expect(board.gameStacks[1].length).toEqual(1);
    expect(board.gameStacks[2].length).toEqual(5);
    expect(board.gameStacks[2][board.gameStacks[2].length - 1]).toBe(card_from_gamestack0);
});

test('Passing a card other than King from one game stack to the other empty game stack', () => {
    let board = new Board();

    board.gameStacks[0] = []; //pusty stos
    board.gameStacks[1] = [ new Card(10) ]; //Walet karo
    
    board.moveBetweenGameStacks(1, 1, 0);

    let gamestack0_length = board.gameStacks[0].length;

    expect(gamestack0_length).toEqual(0);
    expect(board.gameStacks[1][0].rank).toBe('J');
    expect(board.gameStacks[1].length).toEqual(1);
});

test('Passing a King card from one game stack to the other empty game stack', () => {
    let board = new Board();

    board.gameStacks[0] = []; //pusty stos
    board.gameStacks[1] = [ new Card(12) ]; //Król karo
    
    board.moveBetweenGameStacks(1, 1, 0);

    expect(board.gameStacks[0].length).toEqual(1);
    expect(board.gameStacks[0][0].rank).toBe('K');
    expect(board.gameStacks[1].length).toEqual(0);
});

test('Passing a Ace card from revealed stack to the empty result stack', () => {
    let board = new Board();

    board.revealedCardStack = [ new Card(0) ]; //As kier

    board.moveFromRevealedToResultStack(0);

    expect(board.revealedCardStack.length).toEqual(0);
    expect(board.resultStacks[0].length).toEqual(1);
    expect(board.resultStacks[0][0].rank).toBe('A');
});

test('Passing a card other than Ace from revealed stack to the empty result stack', () => {
    let board = new Board();

    board.revealedCardStack = [ new Card(1) ]; //Dwójka kier

    board.moveFromRevealedToResultStack(0);

    expect(board.revealedCardStack.length).toEqual(1);
    expect(board.resultStacks[0].length).toEqual(0);
    expect(board.revealedCardStack[0].rank).toBe('2');
});

test('Adding correct card to the result stack, where is an Ace card', () => {
    let board = new Board();

    board.revealedCardStack = [ new Card(0) ]; //As kier

    board.moveFromRevealedToResultStack(0);

    board.revealedCardStack = [ new Card(1) ]; //Dwójka kier
    board.moveFromRevealedToResultStack(0);

    expect(board.revealedCardStack.length).toEqual(0);
    expect(board.resultStacks[0].length).toEqual(2);
    expect(board.resultStacks[0][0].rank).toBe('A');
    expect(board.resultStacks[0][1].rank).toBe('2');
});

test('Adding incorrect card to the result stack, where is an Ace card', () => {
    let board = new Board();

    board.revealedCardStack = [ new Card(0) ]; //As kier

    board.moveFromRevealedToResultStack(0);

    board.revealedCardStack = [ new Card(2) ]; //Trójka kier
    board.moveFromRevealedToResultStack(0);

    expect(board.revealedCardStack.length).toEqual(1);
    expect(board.resultStacks[0].length).toEqual(1);
    expect(board.resultStacks[0][0].rank).toBe('A');
    expect(board.revealedCardStack[0].rank).toBe('3');
});
```