# Animacje, plansze win/lose

>Scenariusz testowy wykonał: Robert Ciołek  
Testy manualne przeprowadził: Gabriel Seroczyński  
Poprawy finalne testów: Gabriela Stefaniak

# Plansza win/lose

<table>
    <tbody>
    <tr>
        <td><strong>L.P.</strong></td>
        <td><strong>Nazwa</strong></td>
        <td><strong>Kroki wykonania</strong></td>
        <td><strong>Oczekiwany rezultat</strong></td>
        <td><strong>Uzyskany rezultat testu</strong></td>
    </tr>
    <tr>
        <td>1</td>
        <td>Wyświetlenie się planszy po wygranej</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie dowolnej formy rozgrywki</li>
                <li>Wygranie gry</li>
            </ol>
        </td>
        <td>Plansza się wyświetla</td>
        <td><strong>Otrzymano oczekiwany rezultat</strong></td>
    </tr>
    <tr>
        <td>2</td>
        <td>Wyświetlenie się planszy po zakończeniu gry nie będąc wygranym</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie dowolnej formy rozgrywki</li>
                <li>Skończenie gry nie będąc na szczycie tabeli</li>
            </ol>
        </td>
        <td>Plansza się wyświetla</td>
        <td><strong>Otrzymano oczekiwany rezultat</strong></td>
    </tr>
    <tr>
        <td>3</td>
        <td>Działanie przycisku przejścia do analizy partii</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie dowolnej formy rozgrywki</li>
                <li>Zakończenie rozgrywki</li>
                <li>Kliknięcie przycisku przejścia do analizy partii</li>
            </ol>
        </td>
        <td>Następuje przejście do analizy partii</td>
        <td><strong>Otrzymano oczekiwany rezultat</strong></td>
    </tr>
    <tr>
        <td>4</td>
        <td>Wyświetlenie statystyk innego gracza</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie rozgrywki multiplayer</li>
                <li>&nbsp;Zakończenie rozgrywki</li>
                <li>Kliknięcie na imię jednego z graczy</li>
            </ol>
        </td>
        <td>Następuje wyświetlenie statystyk innego gracza</td>
        <td><strong>Otrzymano oczekiwany rezultat</strong></td>
    </tr>
    <tr>
        <td>5</td>
        <td>Działanie przycisku “zagraj ponownie”</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie dowolnej formy rozgrywki</li>
                <li>Zakończenie rozgrywki</li>
                <li>Kliknięcie przycisku “zagraj ponownie”</li>
            </ol>
        </td>
        <td>Gra rozpoczyna się ponownie</td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p>
            <p><strong>(</strong>przycisk znajduje się w widoku rozgrywki nie na planszy końcowej)</p></td>
    </tr>
    <tr>
        <td>6</td>
        <td>Działanie przycisku “zakończ”</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie dowolnej formy rozgrywki</li>
                <li>Zakończenie rozgrywki</li>
                <li>Kliknięcie przycisku “zakończ”</li>
            </ol>
        </td>
        <td>Następuje powrót do menu głównego</td>
        <td><strong>Otrzymano oczekiwany rezultat</strong></td>
    </tr>
    </tbody>
</table>

# Animacje

<table>
    <tbody>
    <tr>
        <td><strong>L.P.</strong></td>
        <td><strong>Nazwa</strong></td>
        <td><strong>Kroki wykonania</strong></td>
        <td><strong>Oczekiwany rezultat</strong></td>
        <td><strong>Uzyskany rezultat testu</strong></td>
    </tr>
    <tr>
        <td>1</td>
        <td>Wystąpienie odpowiedniej animacji będąc w środku tabeli</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie rozgrywki multiplayer</li>
                <li>Zakończenie rozgrywki będąc w środku tabeli</li>
            </ol>
        </td>
        <td>Animacja się odtwarza</td>
        <td><strong>Otrzymano oczekiwany rezultat</strong></td>
    </tr>
    <tr>
        <td>2</td>
        <td>Wystąpienie odpowiedniej animacji po przegranej rozgrywce</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie jednej z form rozgrywki</li>
                <li>Wygranie rozgrywki</li>
            </ol>
        </td>
        <td>Animacja się odtwarza</td>
        <td><strong>Otrzymano oczekiwany rezultat</strong></td>
    </tr>
    <tr>
        <td>3</td>
        <td>Wystąpienie odpowiedniej animacji po wygranej rozgrywce</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie jednej z form rozgrywki</li>
                <li>Przegranie rozgrywki</li>
            </ol>
        </td>
        <td>Animacja się odtwarza</td>
        <td><strong>Otrzymano oczekiwany rezultat</strong></td>
    </tr>
    <tr>
        <td>4</td>
        <td>Czas trwania animacji</td>
        <td>
            <ol>
                <li>Wejście do menu</li>
                <li>Wybranie jednej z form rozgrywki</li>
                <li>Zakończenie rozgrywki</li>
                <li>Zaczekanie, aż animacja się skończy</li>
            </ol>
        </td>
        <td>Animacja się odtwarza</td>
        <td><strong>Otrzymano oczekiwany rezultat</strong></td>
    </tr>
    </tbody>
</table>