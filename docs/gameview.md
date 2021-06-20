# Buttons.js

Sekcja odpowiada za odtwarzanie dźwięków związanych z ruchem i klikaniem myszką oraz za obsługiwanie logiki cofania ruchu kart.

`startColumn1` - Zawiera zakryte karty ze stosu.
 
`startColumn2` - Zawiera odkryte karty ze stosu do wybierania kart.

`startCardIndex` - Indeks pierwszej karty na stosie.

`history` - Tabela z historią ruchów kart.

`points` - Ilość punktów.

`columns` - Zawiera karty na kolumnach.

`buttonUndo` - Odtwarza dźwięk cofnięcia ruchu.

`buttonHover` - Odtwarza dźwięk podczas najechania myszką na obiekt.

`handleMouseOver` - Wykonuje zespół czynności związanych z najechaniem myszką na dany element.
<div>

  `stepBack` -  Odpowiada za logikę stojącą za cofnięciem ruchu karty.

  Warunek `if (lastStep.source === "startColumn1")` obsługuje przypadek gdy poprzedni ruch to odkrycie karty ze stosu. 

  `previousIndex` - Indeks poprzedniej karty

  `previousCard` - Zawiera informacje o poprzedniej karcie

  `else if (lastStep.source === "startColumn2")` warunkuje działanie funkcji gdy kartę przeniesiono ze stosu do wybierania.

  `column` - Wszystkie karty na stosie

  `finalColumn` - Miejsce, w które karta została przeniesiona

  natomiast instrukcja warunkowa `else` obsługuje pozostałe przypadki ruchów kart.

  `sourceColumn` - Kolumna, z której zostały przerzucone karty

  `draggedCardLength` - Ilość przerzucanych kart

  `targetColumn` - Kolumna na którą została przerzucana karta

  `targetColumnLength` - Długość kolumny na którą została przerzucona karta

  `targetColumnStartSlice` - Kolumna pomniejszona o karty, które zostały zabrane do nowej kolumny
</div>


Uruchomienie cofnięcia ruchu:
```js
onClick={stepBack}
``` 
Uruchomienie `handleMouseOver`:
```js
onMouseOver={handleMouseOver}
``` 
Zrestartowanie gry:
```js
onClick={() => setGameNumber((prev) => prev + 1)}
``` 

# Card.js

`Card` zwraca div wyświetlający tył karty z ustalonymi danymi zdefiniowanymi w "Card Motives"
```js
  const Card = ({ top, index }) => {
  return (
    <div className={styles.card} style={{ top: top + "%", zIndex: index + 1 }}>
      <div className="card back">
        <span className="card__value"></span>
        <span className="card__minisuit"></span>
        <span className="card__mainsuit"></span>
      </div>
    </div>
  );
};
  }
``` 
# Custom.js

Sektor odpowiada za logikę podążania karty za kursorem podczas przenoszenia.

`initialOffset` - Wartości przesunięcia początkowego.
 
`currentOffset` - Aktualna pozycja.

Funkcja `getItemStyles(initialOffset, currentOffset, isSnapToGrid)` tworzy style dzięki którym karta podąża za kursorem.

Obliczenie pozycji kart podążających za kursorem:
```js
    x -= initialOffset.x;
    y -= initialOffset.y;
    [x, y] = snapToGrid(x, y);
    x += initialOffset.x;
    y += initialOffset.y;
```

Poniższe wyrażenie `Custom` renderuje karty idące za kursorem.

```js
const Custom = ({ draggingCard }) => {
  const { itemType, isDragging, item, initialOffset, currentOffset } =
    useDragLayer((monitor) => ({
      item: monitor.getItem(),
      itemType: monitor.getItemType(),
      initialOffset: monitor.getInitialSourceClientOffset(),
      currentOffset: monitor.getSourceClientOffset(),
      isDragging: monitor.isDragging(),
    }));
```

# snapToGrid.js

Funkcja zmieniające wprowadzone wartości na podzielne przez 32. Potrzebna do przenoszenia kart.

```js
  export function snapToGrid(x, y) {
    const snappedX = Math.round(x / 32) * 32
    const snappedY = Math.round(y / 32) * 32
    return [snappedX, snappedY]
  }
```

# Deck.js

Segment odpowiada za logikę odkrywania kart ze stosu.

`handleDrop` - obsługa przerzucania karty do kolumn.

`draggingCard` - przenoszona w aktualnym momencie karta.

`revealTheCard` - odpowiada za odkrycie karty ze stosu kart do wybierania oraz dodanie nowego kroku do historii ruchu kart.



Zaktualizowanie historii:
```js
  const newHistoryStep = {
      source: "startColumn1",
      target: "startColumn2",
      draggedCards: [startColumn1[startCardIndex]],
    };
    setHistory([...history, newHistoryStep]);
```

Uruchomienie `revealTheCard`:
```js
  <div className={styles.cardShadow} onClick={revealTheCard}>
```


# DraggableCard

Sektor obsługuje logikę przenoszenia kart.
 
`top` - pozycja karty względem elementu zerowego.

`index` - Indeks karty.

`item` - Zawiera informacje o karcie.

`handleDrag` - obsługa przenoszenia kart.

Obsługa błędu niezawierania karty:
```js
  if (!e.target.classList.contains("card-parent")) {
      el = e.target.closest(".card-parent");
    
```

Pobranie danych o przenoszonej karcie:
```js
  let rank = el.attributes.getNamedItem("data-rank").value;
    let shape = el.attributes.getNamedItem("data-shape").value;
    let color = el.attributes.getNamedItem("data-color").value;
    let isVisible = el.attributes.getNamedItem("data-visible").value;
    let cardIndex = el.attributes.getNamedItem("data-index")?.value;
```

`rank` - ranga karty np 8, 10, A.
 
`shape` - kształt karty.

`color` - pobranie koloru karty.

`isVisible` - określa czy karta jest widoczna.

`cardIndex` - Indeks karty.

`sibling` - kolejna karta o tym samym rodzicu. 

`let arr = [];` - Utworzenie tablicy potrzebnej do składowania danych przenoszonych kart.

Pobranie danych o kolejnej karcie:
```js
      rank = sibling.attributes.getNamedItem("data-rank").value;
      shape = sibling.attributes.getNamedItem("data-shape").value;
      color = sibling.attributes.getNamedItem("data-color").value;
      isVisible = sibling.attributes.getNamedItem("data-visible").value;
```

Zapisanie przenoszonej karty:
```js
    setDraggingCard({
      title: name,
      array: arr,
      target: el,
      cardIndex: cardIndex,
    });  
```

`handleDragEnd` - Służy do zapisania kart, które zostaną podniesione i nigdzie nie wrzucone.

# game_end_animations

`game_end_animations` odpowiada za animacje po wygranej, przegranej lub remisie. Obsługiwane jest przez `animation.js`.

# Animation.js

Zwraca komponent w zależności od wartości `action`. Zawsze pojawia się animacja zrobiona w `Animation.css`, która jest wzbogacona o jedną z 3 animacji w zależności od rezultatu rozgrywki.

# Firework.js

Zwraca komponent w momencie wygranej, który jest animacją fajerwerków.

# Fog.js

Zwraca komponent w momencie remisu, który jest animacją mgły.

# Rain.js

Zwraca komponent w momencie przegranej, który jest animacją deszczu.

# drop.js

Funkcja `drop.js` obsługuje możliwość odkładania kart na wybrane miejsce. 

Przyjmuje parametry:
- accept - określa typ elementu na który obiekt może być upuszony.
- onDrop - przenosi obiekty z jednego miejsca na inne wybrane miejsce.
- top - jest to punkt startowy stosu z którego została pobrana karta. 
- currentArr - tablica, z której pobrany zostaje obiekt do odłożenia.
- draggingArr - tablica obiektów, które zostają przenesone na miejsce docelowe.
- name - zawiera nazwę obiektu na który obiekt jest odkładany.
- isDragActive - sprawdza czy obiekt jest możliwy do przesunięcia, jeżeli jest zwraca `activeStyles`, jeżeli nie zwraca `style`.

`activeStyles` - obiekt zawierający wartości top i zIndex:
```js
const activeStyles = {
    top: top + "%",
    zIndex: "100",
};
```
`style` - obiekt zawierający wartość top:
```js
const style = {
    top: top + "%",
};
```

Funkcja zwraca `div` z ustlonymi wartościami:

```js
<div
    className={styles.drop}
    onDrop={() => onDrop({ title: name, array: currentArr }, draggingArr)}
    ref={drop}
    style={isDragActive ? activeStyles : style}
></div>
```

# FinalColumnItem.js

Funkcja zwraca wszystkie informacje o karcie na szczycie stosu zwycięstwa w sformatowanym `div`.

# FinalColumns.js

Zawiera informacje o stanie stosów zwycięstwa

Przyjmuje parametry:
- finalColumns - 
- columns - 
- draggingCard - 
- setHistory - 
- history - 
- setDraggingCard - 
- setMoveNumbers - 
- setPoints - 
- handleDrop - 

# MainColumns.js


