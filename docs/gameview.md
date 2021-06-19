## Buttons

## game_end_animations

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

Funkcja zwraca wszystkie informacje o karcie na szczycie stosu zwycięstwa w zformatowanym `div`.

# FinalColumns.js


# MainColumns.js