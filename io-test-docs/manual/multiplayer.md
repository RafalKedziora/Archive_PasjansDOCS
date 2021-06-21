# Rozgrywka multiplayer

>Scenariusz testowy wykonał: Piotr Czajkowski oraz Piotr Biazik   
Testy manualne przeprowadzili: Piotr Czajkowski oraz Damian Bugaj

### Przypadki testowe

<table>
    <tbody>
    <tr>
        <td>Lp.</td>
        <td>Opis</td>
        <td>Kroki do wykonania</td>
        <td>Oczekiwany rezultat</td>
        <td>Uzyskany rezultat</td>
    </tr>
    <tr>
        <td>1</td>
        <td>Przejście do widoku gry wieloosobowej</td>
        <td>
            <ol>
                <li>Kliknięcie w przycisk "WIELOOSOBOWA".</li>
            </ol>
        </td>
        <td>Przejście do widoku gry wieloosobowej.</td>
        <td>Zgodny z oczekiwanym</td>
    </tr>
    <tr>
        <td>2</td>
        <td>Utworzenie nowego pokoju gry</td>
        <td>
            <ol>
                <li>Kliknięcie w przycisk "Stwórz nowy pokój".</li>
            </ol>
        </td>
        <td>Przejście do widoku tworzenia nowego pokoju.</td>
        <td>Zgodny z oczekiwanym</td>
    </tr>
    <tr>
        <td>3</td>
        <td>Pokój jest widoczny dla innych graczy zaraz po utworzeniu</td>
        <td>
            <ol>
                <li>Kliknięcie w przycisk "WIELOOSOBOWA".</li>
            </ol>
        </td>
        <td>Zobaczenie pokoju o danej nazwie chwilę wcześniej utworzonego przez danego użytkownika.</td>
        <td>Zgodny z oczekiwanym</td>
    </tr>
    <tr>
        <td>4</td>
        <td>Inni gracze mogą dołączyć do nowo utworzonego pokoju</td>
        <td>
            <ol>
                <li>Kliknięcie w przycisk "WIELOOSOBOWA".</li>
                <li>Kliknięcie w przycisk "Dołącz" obok nazwy pokoju.</li>
            </ol>
        </td>
        <td>Dołączenie do pokoju o danej nazwie.</td>
        <td>Zgodny z oczekiwanym</td>
    </tr>
    <tr>
        <td>5</td>
        <td>Można modyfikować ustawienia pokoju</td>
        <td>
            <ol>
                <li>Kliknięcie w przycisk "WIELOOSOBOWA".</li>
                <li>Kliknięcie w przycisk "Stwórz nowy pokój".</li>
                <li>Kliknięcie w przycisk "Modyfikuj".</li>
                <li>Zmień nazwę pokoju lub czas rozgrywki.</li>
            </ol>
        </td>
        <td>Ustawienia pokoju się zmieniają</td>
        <td>Zgodny z oczekiwanym</td>
    </tr>
    <tr>
        <td>6</td>
        <td>Po upływie czasu rozgrywka kończy się dla wszystkich użytkowników.</td>
        <td>
            <ol>
                <li>Kliknięcie w przycisk "WIELOOSOBOWA".</li>
                <li>Kliknięcie w przycisk "Dołącz" obok nazwy pokoju.</li>
                <li>Host zaczyna grę.</li>
                <li>Rozegranie partii o określonej wcześniej przez hosta długości.</li>
            </ol>
        </td>
        <td>Gra kończy się po określonym czasie dla wszystkich graczy.</td>
        <td>Zgodny z oczekiwanym</td>
    </tr>
    <tr>
        <td>7</td>
        <td>Po rozgrywce wyświetlana jest animacja z uzyskanym rezultatem.</td>
        <td>
            <ol>
                <li>Kliknięcie w przycisk "WIELOOSOBOWA".</li>
                <li>Kliknięcie w przycisk "Dołącz" obok nazwy pokoju.</li>
                <li>Host zaczyna grę.</li>
                <li>Rozegranie partii o określonej wcześniej przez hosta długości.</li>
            </ol>
        </td>
        <td>Pokazuje się właściwa animacja w zależności od uzyskanego rezultatu.</td>
        <td>Zgodny z oczekiwanym</td>
    </tr>
    <tr>
        <td>8</td>
        <td>Po rozgrywce wyświetlana jest plansza win/lose</td>
        <td>
            <ol>
                <li>Kliknięcie w przycisk "WIELOOSOBOWA".</li>
                <li>Kliknięcie w przycisk "Dołącz" obok nazwy pokoju.</li>
                <li>Host zaczyna grę.</li>
                <li>Rozegranie partii o określonej wcześniej przez hosta długości.</li>
            </ol>
        </td>
        <td>Plansza pokazuje się właściwie, tytułem jest uzyskany rezultat (wygrałeś, remis, przegrałeś) oraz wszyscy
            gracze z rozgrywki oraz ich wynik.
        </td>
        <td>Niezgodny z oczekiwanym. Rezultat nie zawsze jest prawidłowy, np. podczas wygranej otrzymujemy rezultat
            "przegrałeś". Nie zawsze wyświetlają się wszyscy gracze, zdarza się, że nie wyświetla się żaden gracz.
        </td>
    </tr>
    </tbody>
</table>