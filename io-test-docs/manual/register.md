# Panel rejestracji

>Scenariusz testowy wykonał: Damian Bugaj   
Testy manualne przeprowadził: Gabriel Seroczyński  
Poprawy finalne testów: Gabriela Stefaniak

<table>
    <tbody>
    <tr>
        <td>Lp.</td>
        <td>Opis</td>
        <td>Kroki do wykonania</td>
        <td>Oczekiwany rezultat</td>
        <td>Otrzymany rezultat</td>
    </tr>
    <tr>
        <td>1.</td>
        <td>Wejście do panelu rejestracji</td>
        <td>
            <ol>
                <li>Otworzenie aplikacji</li>
                <li>Naciśnięcie na przycisk przekierowujący do panelu rejestracji użytkownika</li>
                <li>Przejście do panelu rejestracji</li>
            </ol>
        </td>
        <td>Jest możliwość przejścia i ukazuje nam się formularz rejestracyjny</td>
        <td><strong>Otrzymano oczekiwany rezultat</strong></td></tr>
    <tr>
        <td>2.</td>
        <td>Sprawdzenie czy wszystkie wymagane pola nie przyjmują pól pustych</td>
        <td>
            <ol>
                <li>Wysłanie pola pustego loginu</li>
                <li>Wysłanie pola pustego hasła</li>
                <li>Wysłanie pola pustego maila</li>
                <li>Wysłanie pola pustego loginu i hasła</li>
                <li>Wysłanie pola pustego loginu i maila</li>
                <li>Wysłanie pola pustego hasła i maila</li>
                <li>Wysłanie wszystkich pól pustych</li>
            </ol>
        </td>
        <td>Ukazanie się w każdym przypadku, oznaczenia świadczącego o tym, że wymagane puste pola nie zostały
            zaakceptowane przez system
        </td>
        <td><strong>Otrzymano oczekiwany rezultat</strong></td>
    </tr>
    <tr>
        <td>3.</td>
        <td>Testowanie walidacji danych - login</td>
        <td>
            <ol>
                <li>Sprawdzenie, czy system akceptuje spore nadużycia, w kwestii ilości wprowadzonych znaków, poprzez
                    wpisanie bardzo dużej ilości znaków
                </li>
            </ol>
        </td>
        <td>Ukazanie się w każdym przypadku, oznaczenia świadczącego o tym, że wpisywane dane, nie są akceptowane, przez
            system nadzorujący poprawność wprowadzanych danych
        </td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p>
            <p><strong>Input</strong>:</p>
            <p>'a'x21 nie-przeszedł</p>
            <p>'a'x20 przeszedł</p>
            <p>' ' przeszedł (spacja)</p></td>
    </tr>
    <tr>
        <td>4.</td>
        <td>Testowanie walidacji danych - hasło</td>
        <td>
            <ol>
                <li>Sprawdzenie, czy system akceptuje zbyt słabe hasła, poprzez wpisywanie różnych wersji hasła, które
                    według ustaleń nie powinny zostać zaakceptowane przez system (o zbyt małej ilości znaków, bez znaków
                    specjalnych, bez cyfr, bez liter dużych, bez liter małych)
                </li>
                <li>Sprawdzenie, czy system akceptuje spore nadużycia, w kwestii ilości wprowadzonych znaków, poprzez
                    wpisanie bardzo dużej ilości znaków
                </li>
            </ol>
        </td>
        <td>Ukazanie się w każdym przypadku, oznaczenia świadczącego o tym, że wpisywane dane, nie są akceptowane, przez
            system nadzorujący poprawność wprowadzanych danych
        </td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p>
            <p><strong>Input</strong>:</p>
            <p>'abcde' nie-przeszedł</p>
            <p>'ABCdefGHIJ123456' nie-przeszedł</p>
            <p>'password' przeszedł)</p></td>
    </tr>
    <tr>
        <td>5.</td>
        <td>Testowanie walidacji danych - E-mail</td>
        <td>
            <ol>
                <li>Sprawdzenie, czy system akceptuje wersje e-mailu o cechach niecharakterystycznych dla e-mailu,
                    poprzez wpisanie e-mailu w wersji: bez znaku „@”, z więcej niż jednym znakiem „@” , bez znaku „.”, z
                    innymi znakami niż: cyfry, małe litery, duże litery, cyfry, małpa, kropki, myślniki, podkreślenia
                </li>
                <li>Sprawdzenie, czy system akceptuje spore nadużycia, w kwestii ilości wprowadzonych znaków, poprzez
                    wpisanie bardzo dużej ilości znaków (stosując się do cech charakterystycznych e-mailu)
                </li>
            </ol>
        </td>
        <td>Ukazanie się w każdym przypadku, oznaczenia świadczącego o tym, że wpisywane dane, nie są akceptowane, przez
            system nadzorujący poprawność wprowadzanych danych
        </td>
        <td><p>System akceptuje dowolnie długie emaile</p>
            <p><strong>Input</strong>:</p>
            <p>'test@.net' nie-przeszedł</p>
            <p>'@email.net' nie-przeszedł</p>
            <p>'test@email.' nie-przeszedł</p>
            <p>'test@emailnet' nie-przeszedł</p>
            <p>'test test@email.net' nie-przeszedł</p>
            <p>'test_test@email.net' przeszedł</p>
            <p>'test@email.net' przeszedł</p>
            <p>'a{x3000}@email.net' przeszedł</p></td>
    </tr>
    <tr>
        <td>6.</td>
        <td>Próba poprawnej rejestracji konta</td>
        <td>
            <ol>
                <li>Wprowadzenie wszystkich danych poprawnie</li>
                <li>Naciśnięcie przycisku odpowiadającego za wysłania formularza</li>
                <li>Przejście do panelu informującego, że dane zostały wprowadzone poprawnie, a mail z linkiem
                    weryfikacyjnym został wysłany na nasz e-mail
                </li>
                <li>Sprawdzenie otrzymania maila z linkiem weryfikacyjnym oraz wejście w niego</li>
            </ol>
        </td>
        <td>Otrzymanie informacji, że rejestracja przebiegła pomyślnie</td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p>
            <p><strong>Input</strong>:</p>
            <p>email: test@email.com</p>
            <p>username: test</p>
            <p>password: password</p></td>
    </tr>
    <tr>
        <td>7.</td>
        <td>Próba logowania na założone konto</td>
        <td>
            <ol>
                <li>Wejście w panel logowania</li>
                <li>Logowanie za pomocą loginu i hasła</li>
                <li>Otrzymanie dostępu w aplikacji do konta</li>
                <li>Wylogowanie z aplikacji</li>
            </ol>
        </td>
        <td>Udana próba otrzymania dostępu w aplikacji do zarejestrowanego konta</td>
        <td><strong>Otrzymano oczekiwany rezultat</strong></td>
    </tr>
    <tr>
        <td>8.</td>
        <td>Sprawdzenie czy jest możliwość wprowadzania danych użytkownika który już istnieje</td>
        <td>
            <ol>
                <li>Wejście do panelu rejestracji</li>
                <li>Próba rejestracji korzystając z danych użytkownika, wykorzystanych e-mail już podczas poprzedniej
                    rejestracji
                </li>
            </ol>
        </td>
        <td>Nieudane próby rejestracji</td>
        <td><p><strong>Otrzymano oczekiwany rezultat</strong></p>
            <p>otrzymano komentarz 'Email jest zajęty' i nie pozwolono utworzyć konta</p>
            <p><strong>Input</strong>:</p>
            <p>email: test@email.com</p>
            <p>username: test</p>
            <p>password: password</p>
            <p>Poprawnie założono nowe konto</p>
            <p><strong>Input</strong>:</p>
            <p>email: test@email.com</p>
            <p>username: test</p>
            <p>password: password</p></td>
    </tr>
    </tbody>
</table>