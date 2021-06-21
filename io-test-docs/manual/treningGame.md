# Rozgrywka treningowa

>Scenariusz testowy wykonał: Piotr Biazik  
Testy manualne przeprowadził: Piotr Biazik  
Poprawy finalne testów: Gabriela Stefaniak

### Przypadki Testowe

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
        <td>Rozpoczęcie rozgrywki w trybie treningowym</td>
        <td>Znajdowanie się w Menu Głównym jako gość</td>
        <td>
            <ol>
                <li>Kliknięcie przycisku "Jednoosobowa"</li>
            </ol>
        </td>
        <td>
            <p>Rozpoczyna się rozgrywka</p>
            <p>Wygląd kart jest taki sam jak bazowy motyw</p>
            <p>Zaczyna się odtwarzanie muzyki</p>
            <p>Zaczyna się odliczanie czasu</p></td>
        <td><p><strong>Zgodny z oczekiwaniem</strong></p>
            <p>Rozpoczyna się rozgrywka</p>
            <p>Wygląd kart jest taki sam jak bazowy motyw,</p>
            <p>Muzyka nie odtwarza się sama z siebie (#36 pkt 4.)</p>
            <p>Zaczyna się odliczanie czasu</p></td>
    </tr>
    <tr>
        <td>2</td>
        <td>Poprawne działanie wskaźnika możliwych ruchów</td>
        <td>-</td>
        <td>-</td>
        <td>Wskaźnik możliwych ruchów wskazuje ilość możliwych do wykonania ruchów</td>
        <td><p><strong>Zgodny z oczekiwaniem</strong></p></td>
    </tr>
    <tr>
        <td>3</td>
        <td>Przegranie gry</td>
        <td>Ustawienie kart pozwalające na uniemożliwienie jakichkolwiek ruchów</td>
        <td>
            <ol>
                <li>Wykonanie ruchu uniemożliwiającego wykonanie innych ruchów</li>
            </ol>
        </td>
        <td><p>Wskaźnik istnienia wykonywalnych ruchów zmienia się na 0</p>
            <p>Uruchamia się animacja przegranej</p></td>
        <td><p><strong>Zgodny z oczekiwaniem</strong></p></td>
    </tr>
    <tr>
        <td>4</td>
        <td>Próba przeciągnięcia karty</td>
        <td>Obecność co najmniej jednej karty</td>
        <td>
            <ol>
                <li>Kliknięcie i przytrzymanie na karcie</li>
                <li>Poruszanie kursorem</li>
            </ol>
        </td>
        <td>Karta &nbsp;podąża za kursorem&nbsp;</td>
        <td><p><strong>Zgodny z oczekiwaniem</strong></p>
            <p>Karta &nbsp;podąża za kursorem&nbsp;</p></td>
    </tr>
    <tr>
        <td>5</td>
        <td>Próba przeciągnięcia stosu kart (czyli karty, na której znajdują się inne karty)</td>
        <td>Obecność co najmniej jednego stosu kart</td>
        <td>
            <ol>
                <li>Kliknięcie i przytrzymanie na wybranej karcie ze stosu</li>
                <li>Poruszanie kursorem</li>
            </ol>
        </td>
        <td>Wybrana karta i wszystkie znajdujące się nad nią podążają za kursorem&nbsp;</td>
        <td>
            <p><strong>Zgodny z oczekiwaniem</strong></p>
            <p>Wybrana karta i wszystkie znajdujące się nad nią podążają za kursorem&nbsp;</p></td>
    </tr>
    <tr>
        <td>6</td>
        <td>Próba poprawnego przeniesienia karty na inną</td>
        <td>Obecność na różnych polach co najmniej dwóch odsłoniętych kart na, których kolor jest przeciwny, wartość
            różni się o 1. Mniejsza karta może znajdować się na polu 'z talii'
        </td>
        <td>
            <ol>
                <li>Przeniesienie mniejszej z dwóch kart na większą</li>
            </ol>
        </td>
        <td>Karta zostaje przeniesiona</td>
        <td><p><strong>Zgodny z oczekiwaniem</strong></p>
            Karta zostaje przeniesiona</td>
    </tr>
    <tr>
        <td>7</td>
        <td>Próba przeniesienia karty na inną z tym samym kolorem</td>
        <td>Obecność na różnych polach &nbsp;co najmniej dwóch odsłoniętych kart na, których kolor jest taki sam,</td>
        <td>
            <ol>
                <li>Przeniesienie karty na drugą</li>
            </ol>
        </td>
        <td>Karta zostaje zostaje na swoim miejscu</td>
        <td><p><strong>Zgodny z oczekiwaniem</strong></p>
            Karta zostaje zostaje na swoim miejscu</td>
    </tr>
    <tr>
        <td>8</td>
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
        <td><p><strong>Zgodny z oczekiwaniem</strong></p>
            Karta zostaje zostaje na swoim miejscu</td>
    </tr>
    <tr>
        <td>9</td>
        <td>Odkrycie zakrytej karty</td>
        <td>Obecność co najmniej jednej zakrytej karty</td>
        <td>
            <ol>
                <li>Kliknięcie i przytrzymanie karty, pod którą znajduje się zakryta karta</li>
                <li>Poprawne przeniesienie tej karty na inną</li>
            </ol>
        </td>
        <td>Zakryta karta się odkrywa</td>
        <td><p><strong>Zgodny z oczekiwaniem</strong></p>
            Zakryta karta się odkrywa</td>
    </tr>
    <tr>
        <td>10</td>
        <td>Próba poprawnego przeniesienia karty na stos zwycięstwa</td>
        <td>Obecność na 'stosie zwycięstwa' o tym samym kolorze karty o jeden mniejszej niż przenoszona (dla asa jest to
            puste pole)
        </td>
        <td>
            <ol>
                <li>Przeniesienie karty na opisany stos</li>
            </ol>
        </td>
        <td><p>Karta zostaje przeniesiona na stos</p>
            <p>Licznik puntów zwiększa się o 10</p></td>
        <td><p><strong>Zgodny z oczekiwaniem</strong></p>
            <p>Karta zostaje przeniesiona na stos</p>
            <p>Licznik puntów zwiększa się o 10</p></td>
    </tr>
    <tr>
        <td>11</td>
        <td>Próba przeniesienia<i> </i>karty na stos zwycięstwa odpowiedniego koloru na którym nie ma karty mniejszej o
            1
        </td>
        <td>Obecność jakiejkolwiek karty na polu</td>
        <td>
            <ol>
                <li>Przeniesienie karty na opisany stos</li>
            </ol>
        </td>
        <td>Karta zostaje na swoim miejscu</td>
        <td><p><strong>Zgodny z oczekiwaniem</strong></p>
            Karta zostaje na swoim miejscu</td>
    </tr>
    <tr>
        <td>12</td>
        <td>Próba przeniesienia<i> </i>karty na stos zwycięstwa o innym kolorze</td>
        <td>Obecność jakiejkolwiek karty na polu</td>
        <td>
            <ol>
                <li>Przeniesienie karty na stos o innym kolorze</li>
            </ol>
        </td>
        <td>Karta zostaje na swoim miejscu</td>
        <td><p><strong>Zgodny z oczekiwaniem</strong></p>
            Karta zostaje na swoim miejscu</td>
    </tr>
    <tr>
        <td>13</td>
        <td>Zdjęcie karty z talii</td>
        <td>Obecność co najmniej jednej karty w talii</td>
        <td>
            <ol>
                <li>Kliknięcie na talię</li>
            </ol>
        </td>
        <td>Karta znajdująca się na szczycie talii przenosi się na pole obok</td>
        <td><p><strong>Zgodny z oczekiwaniem</strong></p>
            Karta znajdująca się na szczycie talii przenosi się na pole obok</td>
    </tr>
    <tr>
        <td>14</td>
        <td>Poprawne przeniesienie karty z talii</td>
        <td>Obecność co najmniej jednej karty w talii</td>
        <td>
            <ol>
                <li>Poprawne przeniesienie karty na drugą</li>
            </ol>
        </td>
        <td><p>Karta przenosi się na wybraną inną kartę.</p>
            <p>Jeżeli w talii znajdują się inne karty, wyświetla się <strong>poprzednia</strong> karta</p></td>
        <td><p><strong>Zgodny z oczekiwaniem</strong></p>
            <p>Karta przenosi się na wybraną inną kartę.</p>
            <p>Jeżeli w talii znajdują się inne karty, wyświetla się <strong>następna</strong> karta</p></td>
    </tr>
    <tr>
        <td>15</td>
        <td>Wygranie gry</td>
        <td>Możliwość wykonania zwycięskiego ruchu</td>
        <td>
            <ol>
                <li>Przeniesienie ostatniej karty na stos zwycięstwa</li>
            </ol>
        </td>
        <td><p>Uruchamia się animacja zwycięstwa</p>
            <p>Możliwy jest powrót do menu lub analiza rozgrywki</p></td>
        <td><p><strong>Zgodny z oczekiwaniem</strong></p>
            <p>Uruchamia się animacja zwycięstwa</p>
            <p>Możliwy jest powrót do menu lub analiza rozgrywki</p></td>
    </tr>
    </tbody>
</table>