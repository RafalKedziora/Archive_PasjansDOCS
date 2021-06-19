# GameBoard.js

Klasa `Board` przedstawia planszę do gry w Pasjans Klondike. Przechowuje aktualny stan gry oraz zapewnia wszystkie metody potrzebne do przemieszczania kart na planszy.

Pola:
- `deck` - przedstawia talię kart do gry.
- `revealedCardStack` - sklada się z kart, które można jescze dobrać.
- `resultStacks` - przedstawia stosy zwycięstwa.
- `gameStacks` - przedstawia miejsca na których rozgrywany jest pasjans.

Metody:
- `passCardToRevealedStack` - służy do przenoszenia kart na stos kart odkrytych do dobrania.
- `moveFromRevealedToGameStack` - służy do przenoszenia karty ze stosu kart odkrytych na jeden ze stosów do gry.
    - Przyjmuje parametry:
        - stackNumber - numer stosu na który ma zostać przeniesiona karta.
- `moveBetweenGameStacks` -  służy do przenoszenia stosów kart pomiędzy stosami do gry.
   - Przyjmuje parametry:
        - sourceStackIndex - numer stosu z którego ma zostać pobrana karta.
        - movingCardsAmount - ilość kart do przeniesienia.
        - targetStackIndex - numer stosu na który ma zostać przeniesiona karta.
- `moveFromRevealedToResultStack` - służy do przenoszenia karty ze stosu kart odkrytych na jeden ze stosów zwycięstwa.
    - Przyjmuje parametry:
        - targetStackIndex - numer stosu zwycięztwa na który ma zostać przeniesiona karta.