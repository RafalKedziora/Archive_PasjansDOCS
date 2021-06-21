# Ustawienia gościa

>Scenariusz testowy wykonał: Gabriel Seroczyński  
Testy manualne przeprowadził: Piotr Czajkowski

### Przypadki testowe

<table>
    <tbody>
    <tr>
        <td>Lp.</td>
        <td>Opis&nbsp;</td>
        <td>Kroki do wykonania</td>
        <td>Oczekiwany rezultat</td>
        <td>Uzyskany rezultat</td>
    </tr>
    <tr>
        <td>1</td>
        <td>Gość może wejść w ustawienia gry.</td>
        <td>
            <ol>
                <li>Wybranie z listy rozwijanej opcji "Ustawienia"</li>
            </ol>
        </td>
        <td>Przejście do widoku ustawień</td>
        <td><strong>Zgodnie z oczekiwanym</strong></td>
    </tr>
    <tr>
        <td>2</td>
        <td>Gość może zmieniać głośność oraz efekty dźwiękowe.</td>
        <td>
            <ol>
                <li>Wybranie z listy rozwijanej opcji "Ustawienia".</li>
                <li>Zmiana ustawień dźwięku poprzez przesunięcie kółeczka na pasku.</li>
            </ol>
        </td>
        <td>Ustawienia dźwiękowe się zmieniają, np. dźwięk po najechaniu na przycisk "Logowanie" jest teraz głośniejszy
            albo muzyka podczas rozgrywki.
        </td>
        <td><strong>Zgodnie z oczekiwanym</strong></td>
    </tr>
    <tr>
        <td>3</td>
        <td>Ustawienia zapisują się dla gościa.</td>
        <td>
            <ol>
                <li>Wybranie z listy rozwijanej opcji "Ustawienia".</li>
                <li>Zmiana ustawień dźwięku poprzez przesunięcie kółeczka na pasku.</li>
                <li>Wyjście z aplikacji.</li>
                <li>Odpalenie jej ponownie.</li>
                <li>Wybranie z listy rozwijanej opcji "Ustawienia".</li>
                <li>Sprawdzenie czy ustawienia pozostały bez zmian.</li>
            </ol>
            <p>&nbsp;</p></td>
        <td>Ustawienia dźwiękowe pozostają bez zmian.&nbsp;</td>
        <td><strong>Zgodnie z oczekiwanym</strong></td>
    </tr>
    <tr>
        <td>4</td>
        <td>Gość może sprawdzić autorów gry.</td>
        <td>
            <ol>
                <li>Wybranie z listy rozwijanej opcji "Autorzy".</li>
            </ol>
        </td>
        <td>Przejście do widoku o autorach.</td>
        <td><strong>Zgodnie z oczekiwanym</strong></td>
    </tr>
    <tr>
        <td>5</td>
        <td>Gość może dowiedzieć się więcej o grze.</td>
        <td>
            <ol>
                <li>Wybranie z listy rozwijanej opcji "Autorzy".</li>
            </ol>
        </td>
        <td>Przejście do widoku informacyjnego o grze</td>
        <td><strong>Zgodnie z oczekiwanym</strong></td>
    </tr>
    <tr>
        <td>6</td>
        <td>Gość ma możliwość zarejestrowania się.</td>
        <td>
            <ol>
                <li>Wybranie z listy rozwijanej opcji "Statystyki" lub "Konto" lub kliknięcie w przycisk w prawym górnym
                    rogu "Logowanie/Rejestracja".
                </li>
                <li>Kliknięcie przycisku "Zarejestruj się".</li>
            </ol>
        </td>
        <td>Przejście do widoku rejestracji</td>
        <td><strong>Zgodnie z oczekiwanym</strong></td>
    </tr>
    <tr>
        <td>7</td>
        <td>Gość ma możliwość rozgrywania w gier w trybie jednoosobowym.</td>
        <td>
            <ol>
                <li>Kliknięcie przycisku "Jednoosobowa".</li>
            </ol>
        </td>
        <td>Przejście do widoku gry.</td>
        <td><strong>Zgodnie z oczekiwanym</strong></td>
    </tr>
    <tr>
        <td>8</td>
        <td>Gościowi nie zapisują się statystyki oraz nie wyświetlają się po ukończonej rozgrywce.</td>
        <td>
            <ol>
                <li>Kliknięcie przycisku "Jednoosobowa".</li>
                <li>Rozegranie gry.</li>
                <li>Powrót do strony głównej aplikacji.</li>
                <li>Wybranie z listy rozwijanej opcji "Statystyki".</li>
            </ol>
        </td>
        <td>Po rozegraniu gry statystyki się nie pokazują oraz po wejściu w opcję "Statystyki" również się one nie
            zapisują.
        </td>
        <td><strong>Zgodnie z oczekiwanym</strong></td>
    </tr>
    </tbody>
</table>