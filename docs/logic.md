# Logic.js
Sekcja odpowiada za wyznaczenie ilości możliwych do wykonania ruchów oraz sprawdzenie czy grę da się wygrać.

`nummov` - zmienna przechowująca ilość możliwych ruchów

`columnList` - dwu-wymiarowa tablica przechowująca kolumnami z kartami

`revealedCardStack` - zmienna przechowująca stos kart do odkrywania

`foundationList` - dwu-wymiarowa tablica przechowująca stosy kart zwycięstwa

Funkcja `isDroppable(k1,k2)` sprawdza czy kartę k2 można zrzucić na kartę k1

Funkcja `check4Stack(k1,k2)` sprawdza czy kartę k2 można zrzucić na kartę k1 znajdującą się na stosie zwycięstwa

Funkcja sprawdzająca, czy możliwe jest wygranie gry:
```js
export const gameWinable = function(numMoves) {
    if (numMoves==0)
    {
        return false;
    }
    return true;
};
```
Funkcja zwróci true, jeśli grę da się wygrać lub false gdy jest to niemożliwe