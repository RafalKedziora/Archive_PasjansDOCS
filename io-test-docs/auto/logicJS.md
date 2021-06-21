# Logika kart

>Testy wykonali: Gabriel Seroczyński oraz Paweł Tuzinowski

Karty w grze są układane na stosach według ścisłej sekwencji. 
Napisaliśmy testy, które sprawdzają, czy zasady sekwencji są utrzymane:

Z przygotowanej wczesnej talii kart wybieramy co poniektóre i sprawdzamy, czy system potrafi wyłuskać ich figurę:

```javascript
test('"processRank" works properly', () => {
    expect(processRank(hearts2.rank)).toBe(2);
    expect(processRank(spades10.rank)).toBe(10);
    expect(processRank(hearts4.rank)).toBe(4);
    expect(processRank(clubs3.rank)).toBe(3);
    expect(processRank(clubs4.rank)).toBe(4);
    expect(processRank(spades8.rank)).toBe(8);
    expect(processRank(spades9.rank)).toBe(9);
    expect(processRank(hearts3.rank)).toBe(3);
    expect(processRank(diamondsK.rank)).toBe(13);
    expect(processRank(diamondsA.rank)).toBe(1);
    expect(processRank(clubs5.rank)).toBe(5);
});
```

Następnie dla tej samej karty sprawdzaliśmy czy możliwy jest dany ruch:
```javascript
test('"isDroppable" works properly', () => {
    expect(isDroppable(hearts2, spadesK)).toBeFalsy(); // król pik
    expect(isDroppable(hearts2, spadesA)).toBeTruthy(); // as pik

    expect(isDroppable(hearts3,diamondsA)).toBeFalsy(); // as karo
    expect(isDroppable(hearts3,spades2)).toBeTruthy(); // 2 pik

    expect(isDroppable(hearts4,spades2)).toBeFalsy(); // 2 pik
    expect(isDroppable(hearts4,spades3)).toBeTruthy(); // 3 pik

    expect(isDroppable(hearts5,spades3)).toBeFalsy(); // 3 pik
    expect(isDroppable(hearts5,spades4)).toBeTruthy(); // 4 pik

    expect(isDroppable(hearts6,clubs4)).toBeFalsy(); // 4 trefl
    expect(isDroppable(hearts6,clubs5)).toBeTruthy(); // 5 trefl

    expect(isDroppable(hearts7,clubs5)).toBeFalsy(); // 5 trefl
    expect(isDroppable(hearts7,clubs6)).toBeTruthy(); // 6 trefl
})
```

Przetestowaliśmy każdą kartę z tali oraz każdą możliwą jej drogę na stosie.
Napisaliśmy również testy, które sprawdzają czy wyliczenie możliwych ruchów do wykonania przy różnych sekwencjach oraz kombinacjach jest prawidłowe:

```javascript
test('numMoves ([2pik] na [asaPik] na stosie końcowym)', () => { 
    const columnList = [[spades2],[],[],[],[],[],[]]; // 7 głównych
    const foundationList = [[spadesA],[],[],[]]; // 4 górne
    const revealedCardStack = []; // talia
    expect(numMoves(columnList,foundationList,revealedCardStack)).toBe(1);
});

test('numMoves ([asPik] na stos końcowy)', () => { 
    const columnList = [[spadesA],[],[],[],[],[],[]]; // 7 głównych
    const foundationList = [[],[],[],[]]; // 4 górne
    const revealedCardStack = []; // talia
    expect(numMoves(columnList,foundationList,revealedCardStack)).toBe(4);
});

test('numMoves ([6pik] na [7kier])', () => { 
    const columnList = [[],[],[spades6],[],[],[],[hearts7]]; // 7 głównych
    const foundationList = [[],[],[],[]]; // 4 górne
    const revealedCardStack = []; // talia
    expect(numMoves(columnList,foundationList,revealedCardStack)).toBe(1);
});

test('numMoves ([6pik] [królKier] [damaKier] [7pik])', () => { 
    const columnList = [[],[],[spades6],[heartsK],[heartsQ],[],[spades7]]; // 7 głównych
    const foundationList = [[],[],[],[]]; // 4 górne
    const revealedCardStack = []; // talia
    expect(numMoves(columnList,foundationList,revealedCardStack)).toBe(0);
});
```
Oraz testy które sprawdzają czy tasowanie kart jest na pewno losowe:
```javascript
describe('"shuffleCards":', () => {

    const shuffledCards = shuffleCards();
    const mainColumns = [
        shuffledCards.mainColumn1,
        shuffledCards.mainColumn2,
        shuffledCards.mainColumn3,
        shuffledCards.mainColumn4,
        shuffledCards.mainColumn5,
        shuffledCards.mainColumn6,
        shuffledCards.mainColumn7
    ];
    // łączę wszystkie tablice zwrócone przez shuffleCards w jedną
    const allCards = shuffledCards.startColumn1.concat(
        mainColumns[0],
        mainColumns[1],
        mainColumns[2],
        mainColumns[3],
        mainColumns[4],
        mainColumns[5],
        mainColumns[6],
    );

    it('moves correct number of cards to each initial pile', () => {
        expect(shuffledCards.startColumn1).toHaveLength(24);
        expect(shuffledCards.mainColumn1).toHaveLength(1);
        expect(shuffledCards.mainColumn2).toHaveLength(2);
        expect(shuffledCards.mainColumn3).toHaveLength(3);
        expect(shuffledCards.mainColumn4).toHaveLength(4);
        expect(shuffledCards.mainColumn5).toHaveLength(5);
        expect(shuffledCards.mainColumn6).toHaveLength(6);
        expect(shuffledCards.mainColumn7).toHaveLength(7);
    });

    it('makes cards visible or invisible in a proper way', () => {
        // startColumn1
        let visible = 0, invisible = 0;
        shuffledCards.startColumn1.forEach(card => {
            if (card.isVisible === true) {
                visible++;
            } else {
                invisible++;
            }
        });
        expect(visible).toBe(0);
        expect(invisible).toBe(24);

        // mainColumns
        for (let i = 0; i < 7; i++) {
            visible = 0, invisible = 0;
            mainColumns[i].forEach(card => {
                if (card.isVisible === true) {
                    visible++;
                } else {
                    invisible++;
                }
            });
            expect(visible).toBe(1);
            expect(invisible).toBe(i);
        };
    });

    it('does not allow cards to duplicate anywhere', () => {
        for (let i = 0; i < 52; i++) {
            let isDuplicate = false;
            for (let j = i + 1; j < 52; j++) {
                if (allCards[i] === allCards[j]) {
                    isDuplicate = true;
                    break;
                }
            };
            expect(isDuplicate).toBeFalsy();
        };
    });

    it('does not allow to change any card property into Null nor Undefined', 
    () => {
        let isNull = false, isUndefined = false;
        for (let i = 0; i < 52; i++) {
            if (allCards[i].rank === null
                || allCards[i].color === null
                || allCards[i].shape === null) {
                isNull = true;
            };
            if (allCards[i].rank === undefined
                || allCards[i].color === undefined
                || allCards[i].shape === undefined) {
                isUndefined = true;
            };
        };
        expect(isNull).toBeFalsy();
        expect(isUndefined).toBeFalsy();
    });

    it('shuffles cards correctly', () => {
        // wielokrotne wywoływanie shuffleCards (2*50 razy) i porównywanie
        for (let k = 0; k < 50; k++) {
            let shuffleCardsTest1 = shuffleCards(); // tasowanie 1.
            let allCardsTest1 = shuffleCardsTest1.startColumn1.concat(
                shuffleCardsTest1.mainColumn1,
                shuffleCardsTest1.mainColumn2,
                shuffleCardsTest1.mainColumn3,
                shuffleCardsTest1.mainColumn4,
                shuffleCardsTest1.mainColumn5,
                shuffleCardsTest1.mainColumn6,
                shuffleCardsTest1.mainColumn7
            );
            let shuffleCardsTest2 = shuffleCards(); // tasowanie 2.
            let allCardsTest2 = shuffleCardsTest2.startColumn1.concat(
                shuffleCardsTest2.mainColumn1,
                shuffleCardsTest2.mainColumn2,
                shuffleCardsTest2.mainColumn3,
                shuffleCardsTest2.mainColumn4,
                shuffleCardsTest2.mainColumn5,
                shuffleCardsTest2.mainColumn6,
                shuffleCardsTest2.mainColumn7
            );

            let areIdentical = false;
            let i = 0;
            while (allCardsTest1[i] === allCardsTest2[i]) {
                if(i + 1 !== 52) {
                    i++;
                } else {
                    areIdentical = true;
                }
            }
            expect(areIdentical).toBeFalsy();
        };
    });
```