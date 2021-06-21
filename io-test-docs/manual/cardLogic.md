# Logika kart

>Scenariusz testowy wykonał: Piotr Biazik  
Testy manualne przeprowadził: Gabriel Seroczyński  
Poprawy finalne testów: Gabriela Stefaniak

<table>
    <tbody>
    <tr>
        <td>Lp.</td>
        <td>Opis</td>
        <td>Warunki wstępne</td>
        <td>Kroki do wykonania</td>
        <td>Oczekiwany rezultat</td>
        <td>Uzyskany rezultat</td>
    </tr>
    <tr>
        <td>1</td>
        <td>Próba przeciągnięcia karty</td>
        <td>Obecność co najmniej jednej karty</td>
        <td>
            <ol>
                <li>Kliknięcie i przytrzymanie na karcie</li>
                <li>Poruszanie kursorem</li>
            </ol>
        </td>
        <td>Karta zostaje podąża za kursorem&nbsp;</td>
        <td><strong>Zgodny z oczekiwaniami</strong></td>
    </tr>
    <tr>
        <td>2</td>
        <td>Próba przeciągnięcia stosu kart (czyli karty, na której znajdują się inne karty)</td>
        <td>Obecność co najmniej jednego stosu kart</td>
        <td>
            <ol>
                <li>Kliknięcie i przytrzymanie na wybranej karcie ze stosu</li>
                <li>Poruszanie kursorem</li>
            </ol>
        </td>
        <td>Wybrana karta i wszystkie znajdujące się nad nią podążają za kursorem&nbsp;</td>
        <td><strong>Zgodny z oczekiwaniami</strong></td>
    </tr>
    <tr>
        <td>3</td>
        <td>Próba poprawnego przeniesienia karty na inną</td>
        <td>Obecność na różnych polach co najmniej dwóch odsłoniętych kart na, których kolor jest przeciwny, wartość
            różni się o 1. Mniejsza karta może znajdować się na polu 'z talii'
        </td>
        <td>
            <ol>
                <li>Przeniesienie mniejszej z dwóch kart na większą</li>
            </ol>
        </td>
        <td>Mniejsza karta zostaje przeniesiona na większą</td>
        <td><strong>Zgodny z oczekiwaniami</strong></td>
    </tr>
    <tr>
        <td>4</td>
        <td>Próba przeniesienia karty na inną z tym samym kolorem</td>
        <td>Obecność na różnych polach &nbsp;co najmniej dwóch odsłoniętych kart na, których kolor jest taki sam,</td>
        <td>
            <ol>
                <li>Przeniesienie karty na drugą</li>
            </ol>
        </td>
        <td>Karta zostaje zostaje na swoim miejscu</td>
        <td><strong>Zgodny z oczekiwaniami</strong></td>
    </tr>
    <tr>
        <td>5</td>
        <td>Próba przeniesienia karty na inną z wartością inną niż o 1 większą</td>
        <td>Obecność na różnych polach &nbsp;co najmniej dwóch odsłoniętych kart. Jedna z kart może znajdować się na
            polu 'z talii'
        </td>
        <td>
            <ol>
                <li>Przeniesienie karty o wartości innej niż o 1 mniejsza na drugą</li>
            </ol>
        </td>
        <td>Karta zostaje zostaje na swoim miejscu</td>
        <td><strong>Zgodny z oczekiwaniami</strong></td>
    </tr>
    <tr>
        <td>6</td>
        <td>Odkrycie zakrytej karty</td>
        <td>Obecność na polu zakrytej karty</td>
        <td>
            <ol>
                <li>Kliknięcie zakrytej karty</li>
            </ol>
        </td>
        <td>Zakryta karta się odkrywa</td>
        <td><strong>Zgodny z oczekiwaniami</strong></td>
    </tr>
    <tr>
        <td>7</td>
        <td>Próba poprawnego przeniesienia karty na stos zwycięstwa</td>
        <td>Obecność na 'stosie zwycięstwa' o tym samym kolorze karty o jeden mniejszej niż przenoszona (dla asa jest to
            puste pole)
        </td>
        <td>
            <ol>
                <li>Przeniesienie karty na adekwatny stos</li>
            </ol>
        </td>
        <td>Karta zostaje przeniesiona na stos</td>
        <td><strong>Zgodny z oczekiwaniami</strong></td>
    </tr>
    <tr>
        <td>8</td>
        <td>Próba przeniesienia<i> </i>karty na stos zwycięstwa odpowiedniego koloru na którym nie karty mniejszej o 1
        </td>
        <td>Obecność jakiejkolwiek karty na polu</td>
        <td>
            <ol>
                <li>Przeniesienie karty na opisany stos</li>
            </ol>
        </td>
        <td>Karta zostaje na swoim miejscu</td>
        <td><strong>Zgodny z oczekiwaniami</strong></td>
    </tr>
    <tr>
        <td>9</td>
        <td>Próba przeniesienia<i> </i>karty na stos zwycięstwa o innym kolorze</td>
        <td>Obecność jakiejkolwiek karty na polu</td>
        <td>
            <ol>
                <li>Przeniesienie karty na stos o innym kolorze</li>
            </ol>
        </td>
        <td>Karta zostaje na swoim miejscu</td>
        <td><strong>Zgodny z oczekiwaniami</strong></td>
    </tr>
    <tr>
        <td>10</td>
        <td>Po wzięciu karty ze stosu kart do wzięcia na miejsce wziętej karty NIE powinna wejść jej poprzedniczka z tego
            stosu.
        </td>
        <td>Przynajmniej dwie karty na stosie do dobrania.</td>
        <td>
            <ol>
                <li>Użycie karty ze stosu.</li>
            </ol>
        </td>
        <td>Poprzednia karta "wskakuje" na miejsce do dobrania.</td>
        <td><strong>Zgodny z oczekiwaniami</strong></td>
    </tr>
    <tr>
        <td>11</td>
        <td>Podczas przytrzymania karty lub paru kart, karty na stosie zwycięstwa powinny pokazywać obecny stan.</td>
        <td>Przynajmniej dwie karty na danym stosie zwycięstwa.</td>
        <td>
            <ol>
                <li>Ułożenie dwóch kart na stosie zwycięstwa, tj. np. AS oraz 2.
                    <ol>
                        <li>Przytrzymanie karty, tzw. czynność "drag".</li>
                    </ol>
                </li>
            </ol>
        </td>
        <td>Na stosie zwycięstwa pokazywana jest najwyższa obecnie karta na nim się znajdująca.</td>
        <td><strong>Zgodny z oczekiwaniami</strong></td>
    </tr>
    </tbody>
</table>
