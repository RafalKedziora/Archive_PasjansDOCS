# Profil użytkownika

>Scenariusz testowy wykonał: Piotr Czajkowski  
Testy manualne przeprowadził: Piotr Biazik  
Poprawy finalne testów: Gabriela Stefaniak

### Warunek testowy

<table>
    <tbody>
    <tr>
        <td>ID</td>
        <td>Opis</td>
        <td>Przygotowanie do rozpoczęcia testu</td>
        <td>Oczekiwany rezultat końcowy</td>
        <td>Otrzymany rezultat końcowy</td>
    </tr>
    <tr>
        <td>1</td>
        <td>Otworzenie okna "Konto"</td>
        <td>
            <ol>
                <li>Otworzenie aplikacji.</li>
                <li>Zalogowanie się do już istniejącego konta.</li>
                <li>Przejście z okna "Konto" do okna "Konto".</li>
            </ol>
        </td>
        <td>Jest możliwość przejścia do okna "Konto".</td>
        <td>Jest możliwość przejścia do okna "Konto".</td>
    </tr>
    </tbody>
</table>

### Przypadki testowe

<table>
    <tbody>
    <tr>
        <td>Lp.</td>
        <td>Opis</td>
        <td>Warunki wstępne</td>
        <td>Kroki do wykonania</td>
        <td>Oczekiwany rezultat</td>
        <td>Otrzymany rezultat</td>
    </tr>
    <tr>
        <td>1</td>
        <td>Zmiana avatara użytkownika</td>
        <td>Stworzenie co najmniej jednego konta, na którym można to przetestować</td>
        <td>
            <ol>
                <li>Kliknięcie przycisku "Edycja"</li>
                <li>Klikanie strzałek w celu wyboru avatara</li>
                <li>Kliknięcie przycisku "Ok"</li>
            </ol>
        </td>
        <td>Zmiana obecnego avatara.</td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p>
            Zmiana obecnego avatara.</td>
    </tr>
    <tr>
        <td>2</td>
        <td>Zmiana nazwy użytkownika</td>
        <td>Stworzenie co najmniej jednego konta, na którym można to przetestować</td>
        <td>
            <ol>
                <li>Kliknięcie w przycisk "Edycja".</li>
                <li>Wpisanie w okienku tekstowym nowej nazwy użytkownika i kliknięcie "Save".</li>
            </ol>
        </td>
        <td>Zmiana obecnej nazwy użytkownika na nową.</td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p>
            Zmiana obecnej nazwy użytkownika na nową</td>
    </tr>
    <tr>
        <td>3</td>
        <td>Zmiana hasła użytkownika</td>
        <td>Stworzenie co najmniej jednego konta, na którym można to przetestować</td>
        <td>
            <ol>
                <li>Kliknięcie w przycisk "Edycja" .</li>
                <li>Wpisanie w okienko tekstowe starego hasła.</li>
                <li>Wpisanie w okienko tekstowe nowego hasła.</li>
                <li>Powtórne wpisanie nowego hasła w następnym okienku tekstowym.</li>
                <li>Kliknięcie przycisku "Ok".</li>
            </ol>
        </td>
        <td>Zmiana obecnego hasła użytkownika na nowe.</td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p>
        <p>Zmiana obecnego hasła użytkownika na nowe.</p></td>
    </tr>
    <tr>
        <td>4</td>
        <td>Poprawny format wyświetlania daty założenia konta</td>
        <td>Stworzenie co najmniej jednego konta, na którym można to przetestować</td>
        <td>-</td>
        <td>Data wyświetla się w formacie "yyyy-mm-dd"</td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p>
            Data wyświetla się w formacie "yyyy-mm-dd"&nbsp;</td>
    </tr>
    <tr>
        <td>5</td>
        <td>Prawidłowe wyświetlanie się flagi kraju użytkownika</td>
        <td>Stworzenie co najmniej jednego konta, na którym można to przetestować</td>
        <td>-</td>
        <td>Flaga powinna się wyświetlać prawidłowo jako flaga danego kraju, powinna być widoczna.</td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p>
            Wyświetla się flaga wybranego państwa</td>
    </tr>
    <tr>
        <td>6</td>
        <td>Zmiana flagi kraju użytkownika</td>
        <td>Stworzenie co najmniej jednego konta, na którym można to przetestować</td>
        <td>
            <ol>
                <li>Kliknięcie w przycisk "Edit".</li>
                <li>Wybór kraju z listy rozwijanej.</li>
                <li>Kliknięcie "Accept'.</li>
            </ol>
        </td>
        <td>Zmiana flagi kraju użytkownika na flagę wybranego kraju.</td>
        <td>
            <p><strong>NIE otrzymano oczekiwanego rezultatu</strong></p>
            <p>Zmiana flagi kraju użytkownika na flagę wybranego kraju</p>
            <p>Niektóre kraje mają niepoprawne flagi (np. Rep. Zielonego Przylądka ma flagę Kanady)</p></td>
    </tr>
    <tr>
        <td>7</td>
        <td>Działanie licznika odbytych gier</td>
        <td>Stworzenie co najmniej jednego konta, na którym można to przetestować</td>
        <td>
            <ol>
                <li>Zapamiętać licznik odbytych gier.</li>
                <li>Przejść do panelu rozgrywki.</li>
                <li>Rozegrać jedną grę.</li>
                <li>Wrócić do "Profilu użytkownika".</li>
                <li>Sprawdzić czy licznik zwiększył się o jeden.</li>
            </ol>
        </td>
        <td>Zwiększenie licznika odbytych gier po zagraniu gry o jeden.</td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p></td>
    </tr>
    <tr>
        <td>8</td>
        <td>Działanie licznika wygranych gier</td>
        <td>Stworzenie co najmniej jednego konta, na którym można to przetestować</td>
        <td>
            <ol>
                <li>Zapamiętać licznik wygranych gier.</li>
                <li>Po wygranej grze wrócić do "Profilu użytkownika".</li>
                <li>Sprawdzić czy licznik wygranych zwiększył się o jeden.</li>
            </ol>
        </td>
        <td>Zwiększenie licznika wygranych&nbsp;gier po wygraniu gry o jeden.</td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p></td>
    </tr>
    <tr>
        <td>9</td>
        <td>Działanie licznika przegranych gier</td>
        <td>Stworzenie co najmniej jednego konta, na którym można to przetestować</td>
        <td>
            <ol>
                <li>Zapamiętać licznik przegranych&nbsp;gier.</li>
                <li>Po przegranej grze wrócić do "Profilu użytkownika".</li>
                <li>Sprawdzić czy licznik przegranych&nbsp;zwiększył się o jeden.</li>
            </ol>
        </td>
        <td>Zwiększenie licznika przegranych&nbsp;gier po przegraniu gry o jeden.</td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p></td>
    </tr>
    <tr>
        <td>10</td>
        <td>Działanie licznika zremisowanych gier</td>
        <td>Stworzenie co najmniej jednego konta, na którym można to przetestować</td>
        <td>
            <ol>
                <li>Zapamiętać licznik zremisowanych&nbsp;gier.</li>
                <li>Po zremisowanej grze wrócić do "Profilu użytkownika".</li>
                <li>Sprawdzić czy licznik remisów zwiększył się o jeden.</li>
            </ol>
        </td>
        <td>Zwiększenie licznika zremisowanych&nbsp;gier po zremisowaniu gry o jeden.</td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p></td>
    </tr>
    <tr>
        <td>11</td>
        <td>Działanie licznika punktów konta użytkownika.</td>
        <td>Stworzenie co najmniej jednego konta, na którym można to przetestować</td>
        <td>
            <ol>
                <li>Zapamiętać licznik punktów.</li>
                <li>Wrócić po zagranej grze do "Profilu użytkownika".</li>
                <li>Sprawdzić czy punkty naliczyły się poprawnie.</li>
            </ol>
        </td>
        <td>Prawidłowa zmiana licznika punktów uzyskanych po odbytej partii.</td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p></td>
    </tr>
    <tr>
        <td>12</td>
        <td>Działanie licznika łącznego czasu gry.</td>
        <td>Stworzenie co najmniej jednego konta, na którym można to przetestować</td>
        <td>
            <ol>
                <li>Zapamiętać łączny czas gry.</li>
                <li>Wrócić po zagranej grze do "Profilu użytkownika".</li>
                <li>Sprawdzić czy łączny czas gry zwiększył się o czas zagranej rozgrywki.</li>
            </ol>
        </td>
        <td>Prawidłowa zmiana łącznego czasu gry o czas ostatnio zagranej gry.</td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p></td>
    </tr>
    <tr>
        <td>13</td>
        <td>Działanie licznika średniego czasu gry.</td>
        <td>Stworzenie co najmniej jednego konta, na którym można to przetestować</td>
        <td>
            <ol>
                <li>Zapamiętać średni czas gry.</li>
                <li>Wrócić po zagranej grze do "Profilu użytkownika".</li>
                <li>Sprawdzić czy średni czas gry zmienił się w zależności od czasu zagranej rozgrywki. Jeżeli gra była
                    dłuższa niż średni czas, średni czas powinien wzrosnąć, a jeżeli krótsza to zmaleć.
                </li>
            </ol>
        </td>
        <td>Prawidłowa zmiana średniego czasu po zagranej grze.</td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p></td>
    </tr>
    <tr>
        <td>14</td>
        <td>Działanie licznika "Porzuconych gier"</td>
        <td>Stworzenie co najmniej jednego konta, na którym można to przetestować</td>
        <td>
            <ol>
                <li>Zapamiętać obecny licznik.</li>
                <li>Wrócić po przegranej grze, gdzie wyszliśmy przed końcem rozgrywki do "Profilu użytkownika".</li>
                <li>Sprawdzić czy licznik zwiększył się o jeden po wyjściu z rozgrywki.</li>
            </ol>
        </td>
        <td>Prawidłowa zmiana licznika po przedwczesnym wyjściu z gry.</td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p></td>
    </tr>
    </tbody>
</table>