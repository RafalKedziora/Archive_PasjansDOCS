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

`const cards` to wszystkie dostępne karty w talii. `const testCards` oraz `const testCard2` są specjalnie ułożonymi taliami, które nie wymagają tasowania;służą do testowania.

`shuffleCards` tasuje karty. W pętli losowo wybierana jest karta i wrzucana na stos, po czym jest wyrzucana z talii, aby nie została wylosowana ponownie.

```js
for (let i = 0; i < 24; i++) {
  const random = Math.floor(Math.random() * deck.length);
  const card = { ...deck[random] };
  card.isVisible = false;
  startColumn1.push(card);
  deck.splice(random, 1);
}
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

Oblicza punkty w zależności od warunków. W tym przypadku, w momencie przenoszenia karty z jednej z 4 miejsc na górze, odejmuje 10 punktów.

```js
if (draggingCards.title.includes("finalColumn")) {
      const newPoints = points - 10;
      if (newPoints < 0) setPoints(0);
      else setPoints(newPoints);
```

` if (draggingCards.title === "startColumn2")` oznacza, że karta jest pobrana z talii, więc przerzucana jest do odpowiedniej, nowej kolumny, a w talii pobierana jest nowa.

```js
const source = columns["startColumn1"].get;
      const index = draggingCard.cardIndex;
      source.splice(index - 1, 1);
      columns[draggingCard.title].set([]);
      columns["startColumn1"].set(source);
      columns[currentCards.title].set([
        ...currentCards.array,
        ...draggingCards.array,
```

Ostatnie prawidłowe przenoszenie to z kolumny do kolumny. Po dodaniu do nowej kolumny,

```js

      columns[currentCards.title].set([
        ...currentCards.array,
        ...draggingCards.array,
```

"Obcinany" jest z tablicy fragment kolumny,

```js
const reducedColumn = carriedArray.slice(0, sliceEnd);
```

Sprawdzane jest czy pod spodem nie ma odwróconych kart, a jeśli są to stają się widoczne.

```js
if (
  reducedColumn.length > 0 &&
  !reducedColumn[reducedColumn.length - 1].isVisible
) {
  reversed = reducedColumn.length - 1;
}
if (reducedColumn.length > 0)
  reducedColumn[reducedColumn.length - 1].isVisible = true;
```

Przy każdym prawidłowym odłożeniu karty zapisywany jest krok w `newHistoryStep`, aby mogło funkcjonować cofanie ruchu oraz działała analiza rozgrywki, po ukończeniu gry.

```js
newHistoryStep = {
  source: draggingCard.title,
  target: currentCards.title,
  draggedCards: draggingCard.array,
  reversed,
};
```

Jeżeli karta zostanie odłożona poprawnie zostanie wywołany efekt dźwiękowy `cardSound(cardRight);` w przeciwnym przypadku, kiedy nie można odłożyć karty w dane miejsce, wraca ona na swoją pozycje.

```js
carriedTarget.style.opacity = 1;
    let sibling = carriedTarget.nextElementSibling;
    while (sibling !== null) {
      sibling.style.opacity = 1;
      sibling = sibling.nextElementSibling;
```
