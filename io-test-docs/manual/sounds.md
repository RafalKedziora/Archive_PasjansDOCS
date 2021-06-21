# Ścieżki dźwiękowe

>Scenariusz testowy wykonał: Robert Ciołek  
Testy manualne przeprowadził: Piotr Biazik  
Poprawy finalne testów: Gabriela Stefaniak

<table>
    <tbody>
    <tr>
        <td>L.P</td>
        <td>Nazwa</td>
        <td>Kroki wykonania</td>
        <td>Oczekiwany rezultat</td>
        <td>Uzyskany Rezultat</td>
    </tr>
    <tr>
        <td>1</td>
        <td>Dźwięk najechania kursorem na element w menu</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Najechanie kursorem na któryś z elementów</li>
            </ol>
        </td>
        <td>Dźwięk się odtwarza</td>
        <td><p><strong>Zgodny z oczekiwanym.</strong></p>
    </tr>
    <tr>
        <td>2</td>
        <td>Szybkie najeżdżanie kursorem na jeden z elementów w menu</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Szybkie, wielokrotne najeżdżanie kursorem na jeden z elementów w menu</li>
            </ol>
        </td>
        <td>Dźwięki nadążają za ponownymi ruchami kursora</td>
        <td><strong>Zgodny z oczekiwanym.</strong></td>
    </tr>
    <tr>
        <td>3</td>
        <td>Dźwięk kliknięcia na element w menu</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Kliknięcie na jeden z elementów</li>
            </ol>
        </td>
        <td>Dźwięk się odtwarza</td>
        <td>
            <p><strong>Zgodny z oczekiwanym.</strong></p></td>
    </tr>
    <tr>
        <td>4</td>
        <td>Muzyka podczas rozpoczęcia rozgrywki</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie jednej z form rozgrywki</li>
            </ol>
        </td>
        <td>
            <p>Utwór z rozgrywki nie zaczyna grać sam z siebie.</p>
            <p>Utwór zaczyna grać ~2s po kliknięciu gdziekolwiek na oknie gry, poza kliknięciami, które:</p>
            <ul>
                <li>wykonały operację przeciągnięcia karty</li>
                <li>zaczęły lub skończyły się na przycisku 'undo'</li>
                <li>zaczęły i skończyły się na przycisku 'undo'</li>
                <li>zaczęły lub skończyły się na przycisku 'reset'</li>
                <li>zaczęły się poza ekranem gry, a skończyły na nim</li>
            </ul>
        </td>
        <td><strong>Zgodny z oczekiwanym.</strong>
        </td>
    </tr>
    <tr>
        <td>5</td>
        <td>Zapętlanie muzyki podczas rozgrywki</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie jednej z form rozgrywki</li>
                <li>Zaczekanie aż utwór się skończy</li>
            </ol>
        </td>
        <td>Utwór jest zapętlony</td>
        <td><strong>Zgodny z oczekiwanym.</strong></td>
    </tr>
    <tr>
        <td>6</td>
        <td>Dźwięk kliknięcia przycisku “cofnij”</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie jednej z form rozgrywki</li>
                <li>Kliknięcie na przycisk “cofnij”</li>
            </ol>
        </td>
        <td>Dźwięk się odtwarza</td>
        <td><strong>Zgodny z oczekiwanym.</strong></td>
    </tr>
    <tr>
        <td>7</td>
        <td>Dźwięk odkrycia karty ze stosu</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie jednej z form rozgrywki</li>
                <li>Odkrycie karty ze stosu</li>
            </ol>
        </td>
        <td>Dźwięk się odtwarza</td>
        <td><strong>Zgodny z oczekiwanym.</strong></td>
    </tr>
    <tr>
        <td>8</td>
        <td>Dźwięk podniesienia jednej z odkrytych kart</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie jednej z form rozgrywki</li>
                <li>Kliknięcie i przytrzymanie na jedną z odkrytych kart</li>
                <li>Przeciągnięcie karty</li>
            </ol>
        </td>
        <td>Dźwięk się odtwarza</td>
        <td><strong>Zgodny z oczekiwanym.</strong></td>
    </tr>
    <tr>
        <td>9</td>
        <td>Dźwięk przekładania karty</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie jednej z form rozgrywki</li>
                <li>Poprawne wykonanie na karcie operacji “drag and drop”</li>
            </ol>
        </td>
        <td>Dźwięk się odtwarza</td>
        <td><strong>Zgodny z oczekiwanym.</strong></td>
    </tr>
    <tr>
        <td>10</td>
        <td>Dźwięk próby przełożenia karty w niepoprawne miejsce</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie jednej z form rozgrywki</li>
                <li>Próba przełożenia karty w jedno ze złych miejsc</li>
            </ol>
        </td>
        <td>Dźwięk się odtwarza</td>
        <td><strong>Zgodny z oczekiwanym.</strong></td>
    </tr>
    <tr>
        <td>11</td>
        <td>Dźwięk podczas przytrzymania kursora na którymś z elementów</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie jednej z form rozgrywki</li>
                <li>Przytrzymanie wciśniętego kursora na jednym z elementów</li>
            </ol>
        </td>
        <td>Dźwięk zostaje odtworzony tylko jeden raz</td>
        <td><strong>Zgodny z oczekiwanym.</strong></td>
    </tr>
    <tr>
        <td>12</td>
        <td>Dźwięk szybkiego odkrywania kart ze stosu</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie jednej z form rozgrywki</li>
                <li>Szybkie wielokrotne odkrywanie kart ze stosu</li>
            </ol>
        </td>
        <td>Dźwięk następnego odkrycia karty występuje dopiero po skończeniu poprzedniego.</td>
        <td><strong>Zgodny z oczekiwanym.</strong></td>
    </tr>
    <tr>
        <td>13</td>
        <td>Szybkie klikanie jednej z odkrytych kart</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie jednej z form rozgrywki</li>
                <li>Szybkie, wielokrotne kliknięcie na jedną z odkrytych kart</li>
            </ol>
        </td>
        <td>Dźwięki nadążają za ponownymi kliknięciami</td>
        <td><strong>Zgodny z oczekiwanym.</strong></td>
    </tr>
    <tr>
        <td>14</td>
        <td>Dźwięk podczas kliknięcia w miejsce w którym nie ma żadnej karty</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie jednej z form rozgrywki</li>
                <li>Kliknięcie w miejsce w którym nie ma karty</li>
            </ol>
        </td>
        <td>Dźwięk się nie odtwarza</td>
        <td><strong>Zgodny z oczekiwanym.</strong></td>
    </tr>
    <tr>
        <td>15</td>
        <td>Muzyka przy powrocie do menu</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie jednej z form rozgrywki</li>
                <li>Powrót do menu po rozpoczęciu muzyki w rozgrywce</li>
            </ol>
        </td>
        <td>Utwór z rozgrywki przestaje być odtwarzany</td>
        <td><strong>Zgodny z oczekiwanym.</strong></td>
    </tr>
    </tbody>
</table>
