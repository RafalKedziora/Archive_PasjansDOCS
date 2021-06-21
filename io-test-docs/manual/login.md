# Test logowania

>Scenariusz testowy wykonał: Paweł Tuzinowski  
Testy manualne przeprowadził: Paweł Tuzinowski  
Poprawy finalne testów: Gabriela Stefaniak

<table>
    <tbody>
    <tr>
        <td><strong>Warunek wstępny generalny</strong></td>
        <td>
            <ul>
                <li>Aplikacja jest otwarta w przeglądarce z widocznym menu głównym.</li>
                <li>Żaden użytkownik nie jest zalogowany.</li>
            </ul>
        </td>
    </tr>
    </tbody>
</table>


<table>
    <tbody>
    <tr>
        <td>Lp</td>
        <td><h3><strong>Przypadek testowy</strong></h3></td>
        <td><h3><strong>Warunki wstępne</strong></h3></td>
        <td><h3><strong>Kroki</strong></h3></td>
        <td><h3><strong>Oczekiwany rezultat</strong></h3></td>
        <td><h3><strong>Otrzymany rezultat</strong></h3></td>
    </tr>
    <tr>
        <td>1</td>
        <td>Zalogowanie się z poprawnymi danymi</td>
        <td>
            <ul>
                <li>Użytkownik ma dostęp do danych logowania dla istniejącego użytkownika (login i hasło).</li>
            </ul>
        </td>
        <td>
            <ol>
                <li>Naciśnij przycisk 'Login'.</li>
                <li>Wprowadź istniejący login (patrz: warunki wstępne).</li>
                <li>Wprowadź poprawne hasło (patrz: warunki wstępne).</li>
                <li>Naciśnij przycisk 'Log in'.</li>
            </ol>
        </td>
        <td>
            <ul>
                <li>Użytkownik zalogował się do swojego konta.</li>
            </ul>
        </td>
        <td><p><strong>Zgodny z oczekiwanym.</strong></p>
            <p>[test poprawny dla danych logowania 'random@mail.com' + '123123' oraz 'rand@mail.com' + 'rand123']</p>
        </td>
    </tr>
    <tr>
        <td>2</td>
        <td>Próba zalogowania się z prawidłowym loginem, ale nieprawidłowym hasłem</td>
        <td>
            <ul>
                <li>Użytkownik ma dostęp do danych logowania dla istniejącego użytkownika (login i hasło).</li>
            </ul>
        </td>
        <td>
            <ol>
                <li>Naciśnij przycisk 'Login'.</li>
                <li>Wprowadź istniejący login (patrz: warunki wstępne).</li>
                <li>Wprowadź do pola hasła inny tekst niż poprawne hasło dla logującego się użytkownika (patrz: warunki
                    wstępne).
                </li>
                <li>Naciśnij przycisk 'Log in'.</li>
            </ol>
        </td>
        <td>
            <ul>
                <li>Użytkownik nie zalogował się do swojego konta.</li>
                <li>Wyświetla się komunikat o błędnym haśle.</li> 
            </ul>
        </td>
        <td><p><strong>Zgodny z oczekiwanym.</strong></p>
            <p>[test przeprowadzony dla loginu: 'random@mail.com' i nieprawidłowych haseł: 'asddsa', '321321']</p>
            <ul>
                <li>Użytkownik zgodnie z oczekiwaniem nie zalogował się do konta i wyskakuje komunikat o błędnych
                    danych.
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>3</td>
        <td>Próba zalogowania się z nieprawidłowym loginem, ale prawidłowym hasłem</td>
        <td>
            <ul>
                <li>Użytkownik ma dostęp do danych logowania dla istniejącego użytkownika (login i hasło).</li>
                <li>Użytkownik ma dostęp do loginu, który na pewno nie istnieje w bazie użytkowników.</li>
            </ul>
        </td>
        <td>
            <ol>
                <li>Naciśnij przycisk 'Login'.</li>
                <li>Wprowadź do pola loginu nieistniejący w bazie użytkowników login (patrz: warunki wstępne).</li>
                <li>Wprowadź hasło dla istniejącego użytkownika (patrz: warunki wstępne).</li>
                <li>Naciśnij przycisk 'Log in'.</li>
            </ol>
        </td>
        <td>
            <ul>
                <li>Użytkownik nie zalogował się do swojego konta.</li>
                <li>Wyświetla się komunikat o nieistniejącym użytkowniku.</li>
            </ul>
        </td>
        <td><p><strong>Zgodny z oczekiwanym.</strong></p>
            <p>[test przeprowadzony dla nieistniejącego loginu: 'xxxxxx@mail.com' i hasła: '123123' oraz nieistniejącego
                loginu 'xyzxyz@o2.pl' i hasła 'rand123']</p>
            <ul>
                <li>Użytkownik zgodnie z oczekiwaniem nie zalogował się do konta i wyskakuje komunikat o błędnych
                    danych.
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>4</td>
        <td>Próba zalogowania się z nieprawidłowymi obiema danymi</td>
        <td>
            <ul>
                <li>Użytkownik ma dostęp do danych logowania dla istniejącego użytkownika (login i hasło).</li>
                <li>Użytkownik ma dostęp do loginu, który na pewno nie istnieje w bazie użytkowników.</li>
            </ul>
        </td>
        <td>
            <ol>
                <li>Naciśnij przycisk 'Login'.</li>
                <li>Wprowadź do pola loginu nieistniejący w bazie użytkowników login (patrz: warunki wstępne).</li>
                <li>Wprowadź do pola hasła inny tekst niż poprawne hasło dla istniejącego użytkownika (patrz: warunki
                    wstępne).
                </li>
                <li>Naciśnij przycisk 'Log in'.</li>
            </ol>
        </td>
        <td>
            <ul>
                <li>Użytkownik nie zalogował się do swojego konta.</li>
                <li>Wyświetla się komunikat o nieistniejącym użytkowniku.</li>
            </ul>
        </td>
        <td><p><strong>Zgodny z oczekiwanym.</strong></p>
            <p>[test przeprowadzony dla nieistniejących danych: 'trial@o2.pl' + 'xyz123']</p>
            <ul>
                <li>Użytkownik zgodnie z oczekiwaniem nie zalogował się do konta i wyskakuje komunikat o błędnych
                    danych.
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>5</td>
        <td>Zmiana hasła</td>
        <td>
            <ul>
                <li>Użytkownik zalogował się na swoje konto.</li>
                <li>W panelu konta użtkownika widoczny jest przycisk 'Edycja'.</li>
                <li>Użytkownik ma dostęp do adresu e-mail i hasła przypisanego do konta, na które próbował się zalogować.</li>
            </ul>
        </td>
        <td>
            <ol>
                <li>Naciśnij przycisk 'Edycja' w panelu konta użytkownika.</li>
                <li>Wpisz poprawną nazwę użytkownika, stare hasło
                    oraz podwójnie nowe hasło w pole do tego przeznaczone (patrz: warunki wstępne).</li>
                <li>Zatwierdź przyciskiem 'Ok'.</li>
            </ol>
        </td>
        <td>
            <ul>
                <li>W aplikacji pojawia się komunikat o zmianie hasła.</li>
            </ul>
        </td>
        <td><p><strong>Zgodny z oczekiwanym.</strong></p>
            <ul>
                <li>Użytkownik pozytywnie zmienił swoje hasło.
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>6</td>
        <td>Logowanie się z nowymi danymi logowania</td>
        <td>
            <ul>
                <li>Użytkownik przeszedł pozytywnie przypadek testowy 'Zmiana hasła'.</li>
                <li>Użytkownik ma dostęp do nowych/aktualnych danych logowania.</li>
            </ul>
        </td>
        <td>
            <ol>
                <li>Naciśnij przycisk 'Zaloguj się'.</li>
                <li>Wprowadź aktualny email (patrz: warunki wstępne).</li>
                <li>Wprowadź nowe/aktualne hasło (patrz: warunki wstępne).</li>
                <li>Naciśnij przycisk 'Zaloguj się'.</li>
            </ol>
        </td>
        <td>
            <ul>
                <li>Użytkownik zalogował się do swojego konta.</li>
            </ul>
        </td>
        <td><p><strong>Zgodny z oczekiwanym.</strong></p>
            <ul>
                <li>Użytkownik pomyślnie się zalogował.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>7</td>
        <td>Próba przypomnienia hasła z nieprawidłowym adresem e-mail</td>
        <td>
            <ul>
                <li>Użytkownik przeszedł pozytywnie któryś z przypadków testowych kończących się niezalogowaniem się do
                    konta.
                </li>
                <li>Niewidoczny jest przycisk 'Przypomnij dane logowania'.</li>
                <li>Użytkownik ma dostęp do adresu e-mail, który nie jest przypisany do żadnego z kont użytkowników.
                </li>
            </ul>
        </td>
        <td>
            <ol>
                <li>Naciśnij przycisk 'Zaloguj się'.</li>
                <li>Wprowadź adres e-mail nieprzypisany do żadnego konta (patrz: warunki wstępne).</li>
                <li>Zatwierdź przyciskiem 'Ok'.</li>
                <li>Sprawdź, czy na pewno nie zostałeś zalogowany.</li>
            </ol>
        </td>
        <td>
            <ul>
                <li>W aplikacji pojawia się komunikat o niepoprawnym adresie e-mail.</li>
            </ul>
        </td>
        <td><p><strong>Zgodny z oczekiwanym.</strong></p>
            <ul>
                <li>
                    Użytkownik nie zalogował się.
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>8</td>
        <td>Próba zalogowania się do usuniętego konta</td>
        <td>
            <ul>
                <li>Użytkownik posiada dostęp do danych logowania do konta (login, hasło), które usunięto z bazy
                    użytkowników.
                </li>
            </ul>
        </td>
        <td>
            <ol>
                <li>Naciśnij przycisk 'Logowanie'.</li>
                <li>Wprowadź login do usuniętego konta (patrz: warunki wstępne).</li>
                <li>Wprowadź hasło do usuniętego konta (patrz: warunki wstępne).</li>
                <li>Naciśnij przycisk 'Zaloguj się'.</li>
            </ol>
        </td>
        <td>
            <ul>
                <li>Użytkownik nie zalogował się do konta.</li>
                <li>Wyświetla się komunikat o błędnych danych.</li>
            </ul>
        </td>
        <td><p><strong>Zgodny z oczekiwanym.</strong></p>
            <p>[stworzono użytkownika z danymi 'new@mail.com' + 'new_user' + hasło:'new321', a następnie usunięto go z
                bazy użytkowników; później próba zalogowania z wymienionymi wyżej danymi]</p>
            <ul>
                <li>Użytkownik zgodnie z oczekiwaniem nie zalogował się do konta i wyskakuje komunikat o błędnych
                    danych, ale niepoprawne dane nie znikają oraz nie pojawia się funkcjonalność przypominania danych
                    logowania.
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>9</td>
        <td>Próba zalogowania się bez wpisania hasła</td>
        <td>
            <ul>
                <li>Użytkownik ma dostęp do danych logowania dla istniejącego użytkownika (login i hasło).</li>
            </ul>
        </td>
        <td>
            <ol>
                <li>Naciśnij przycisk 'Login'.</li>
                <li>Wprowadź poprawny login (patrz: warunki wstępne).</li>
                <li>Naciśnij przycisk 'Log in'.</li>
            </ol>
        </td>
        <td>
            <ul>
                <li>Użytkownik nie zalogował się do konta.</li>
                <li>Wyświetla się komunikat o niewpisaniu hasła.</li>
            </ul>
        </td>
        <td><p><strong>Zgodny z oczekiwanym.</strong></p>
            <p>[test przeprowadzony dla loginu 'rand@mail.com']</p></td>
    </tr>
    <tr>
        <td>10</td>
        <td>Próba zalogowania się bez wpisania loginu</td>
        <td>
            <ul>
                <li>Użytkownik ma dostęp do danych logowania dla istniejącego użytkownika (login i hasło).</li>
            </ul>
        </td>
        <td>
            <ol>
                <li>Naciśnij przycisk 'Login'.</li>
                <li>Wprowadź istniejące hasło (patrz: warunki wstępne).</li>
                <li>Naciśnij przycisk 'Log in'.</li>
            </ol>
        </td>
        <td>
            <ul>
                <li>Użytkownik nie zalogował się do konta.</li>
                <li>Wyświetla się komunikat o niewpisaniu loginu.</li>
            </ul>
        </td>
        <td><p><strong>Zgodny z oczekiwanym.</strong></p>
            <p>[test przeprowadzony dla hasła 'rand123']</p></td>
    </tr>
    <tr>
        <td>11</td>
        <td>Próba zalogowania się bez wpisywania danych</td>
        <td>&nbsp;</td>
        <td>
            <ol>
                <li>Naciśnij przycisk 'Login'.</li>
                <li>Naciśnij przycisk 'Log in' bez wpisywania danych.</li>
            </ol>
        </td>
        <td>
            <ul>
                <li>Użytkownik nie zalogował się do konta.</li>
                <li>Wyświetlają się 2 komunikaty o niewpisaniu loginu i hasła.</li>
            </ul>
        </td>
        <td><strong>Zgodny z oczekiwanym.</strong></td>
    </tr>
    </tbody>
</table>