## card.js

Plik odpowiadający za poprawne działanie kart w rozgrywce i wszelkiej związanej z nimi logiki. Umożliwia poprawne działanie algorytmów związanych z kartami.

`processRank` odpowiada za zwrócenie odpowiedniej wartości rangi, która pobrana była z karty.
`isDroppable` ustala czy podniesiona karta może zostać upuszczona na odpowiednią kartę leżącą na stole. Rozpatrzane w tym celu są zagnieżdżone przypadki, rozpatrujące ranking i kolor. Ustawianie króla na pustym miejscu

```js
if (dropTarget == null && selectedCard.rank === "K") return true;
```

Uniknięcie kładzenia jakiejkolwiek karty na pustym miejscu

```js
if (dropTarget == null) return false;
```

Sprawdzenie poprawności różnicy rang

```js
if (
    processRank(dropTarget.rank) - processRank(selectedCard.rank) === 1)
```

Jeżeli powyższy warunek jest spełniony następuje sprawdzenie czy kolor jest odpowiedni

```js
if (dropTarget.color !== selectedCard.color) {
  return true;
} else {
  return false;
}
```

`isMovable` zwraca wartość `boolean`, która informuje o tym czy karta może być przesunięta.

O co chodzi w pętli?

`check4Stack` to funkcja sprawdzająca czy na czterech polach u góry planszy można położyć kartę.
Przypadek w którym nic nie leży na polu:

```js
if (foundation === null && card.rank === "A") {
  return true;
} else if (foundation === null) return false;
```

przypadek w którym na polu leży już karta:

```js
if (
  foundation.shape === card.shape &&
  processRank(card.rank) - processRank(foundation.rank) === 1
) {
  return true;
} else {
  return false;
}
```

const cards?
const testCards ?
const testCard2 ?

`shuffleCards` tasuje karty.
W pętli losowo wybierana jest karta i wrzucana na stos, po czym jest wyrzucana z talii, aby nie została wylosowana ponownie.

```js
for (let i = 0; i < 24; i++) {
  const random = Math.floor(Math.random() * deck.length);
  const card = { ...deck[random] };
  card.isVisible = false;
  startColumn1.push(card);
  deck.splice(random, 1);
}
```

Co robi ten fragment?

```js
Object.entries(mainColumns).map(([key, item], index) => {
  for (let j = 0; j < index + 1; j++) {
    const random = Math.floor(Math.random() * deck.length);
    const card = { ...deck[random] };
    if (j === index) {
      card.isVisible = true;
    } else card.isVisible = false;
    item.push(card);
    deck.splice(random, 1);
  }
});
```

`numMoves` na podstawie ustawienia kart zwraca ilość możliwych ruchów. Zagnieżdżone pętle w tej funkcji na podstawie `isDroppable` obliczają ilość możliwych ruchów do wykonania przechodząc przez wszystkie kolumny oraz '4stack'.

`gameResult` na podstawie `finalColumns` zwraca `"lose"` lub `"win"` w zależności od spełnionych warunków w pętli.

```js
for (const column of finalColumns) {
  if (column.length < 13) return "lose";
}
return "win";
```

`drop` odpowiada za upuszczenie karty, a dokładniej jest wywoływane po upuszczeniu. Zmienia wartości zmiennych

```js
currentCards,
  draggingCards,
  columns,
  draggingCard,
  setMoveNumbers,
  setPoints,
  points,
  revealCardRef,
  cardSound,
  setHistory,
  history,
  cardRight,
  setDraggingCard;
```

Zwiększa ilość wykonanych ruchów `letMoveNumbers((prev) => prev + 1);`

Oblicza punkty w zależności od warunku

```js
if (draggingCards.title.includes("finalColumn")) {
      const newPoints = points - 10;
      if (newPoints < 0) setPoints(0);
      else setPoints(newPoints);
```

OD 430 linijki
