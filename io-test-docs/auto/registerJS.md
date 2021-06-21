# Panel rejestracji

>Testy wykonał: Jakub Podsiadły

Panel rejestracji jest miejscem, w którym użytkownik może rozpocząć swoją przygodę z rozgrywką online.
Sam panel składa się głównie formularza, który posiada walidację.\
Aby zarejestrować się w systemie, niezbędne jest podanie takich danych jak:

- adres email
- nazwa użytkownika
- hasło wraz z jego potwierdzeniem

Testy formularza zaczęliśmy od adresu email, czyli sprawdziliśmy, czy system wyświetli komunikat, gdy użytkownik poda nieprawidłowy adres email:

```javascript
test("incorrect mail causes emailError", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let invalidEmail = "funny mail"
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Email"]');

    fireEvent.change(input,{target: {value: invalidEmail}});
    fireEvent.submit(form);

    expect(input.value).toBe(invalidEmail);
    expect(input.nextElementSibling.textContent.length).toBeGreaterThanOrEqual(1);
});
```

Jak widać powyżej, w pierwszym kroku renderujemy komponent panelu rejestracji, 
następnie znajdujemy takie elementy jak formularz czy pole adresu email,
symulujemy wypełnienie pola wartością `funny mail` i oczekujemy od systemu, że 
wartość wypełnionego pola będzie równa tej wartość oraz że zawartość testu w 
następnym elemencie, obok tego pola będzie większa lub równa 1. 
Dzieje się tak, ponieważ dokładnie w tamtym miejscu znajduje się komunikat o błędzie o nieprawidłowym adresie email.

Analogicznie sprawdzamy, czy dla prawidłowego adresu email nie ma błędów:

```javascript
test("correct mail causes no emailError", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let validEmail = "abc@abc.com";
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Email"]');

    fireEvent.change(input,{target: {value: validEmail}});
    fireEvent.submit(form);

    expect(input.value).toBe(validEmail);
    expect(input.nextElementSibling.textContent.length).toBeLessThanOrEqual(0);
});
```

Staraliśmy się również sprawdzić trochę bardziej wyłuskane przypadki testowe dla adresu mail, 
ponieważ staramy się patrzeć szeroko.\
Maile takie jak `@abc.com`, `abc@.com`, `abc@abc.` nie są prawidłowe i nasz system zdaje sobie z tego sprawę:

```javascript
test("Testing email walidation with email like '@abc.com'", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let invalidEmail = "@abc.com";
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Email"]');

    fireEvent.change(input,{target: {value: invalidEmail}});
    fireEvent.submit(form);

    expect(input.value).toBe(invalidEmail);
    expect(input.nextElementSibling.textContent).not.toBe("");
});

test("Testing email walidation with email like 'abc@.com'", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let invalidEmail = "abc@.com";
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Email"]');

    fireEvent.change(input,{target: {value: invalidEmail}});
    fireEvent.submit(form);

    expect(input.value).toBe(invalidEmail);
    expect(input.nextElementSibling.textContent).not.toBe("");
});

test("Testing email walidation with email like 'abc@abc.'", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let invalidEmail = "abc@abc.";
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Email"]');

    fireEvent.change(input,{target: {value: invalidEmail}});
    fireEvent.submit(form);

    expect(input.value).toBe(invalidEmail);
    expect(input.nextElementSibling.textContent).not.toBe("");
});
```

W następnych testach skupiliśmy się na nazwie użytkownika. Tu do tematu również podchodziliśmy szeroko,
sprawdzaliśmy jednakowo przypadki, w których to nazwa użytkownika jest pusta:

```javascript
test("Testing empty user name input", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let username = "";
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Nazwa użytkownika"]');

    fireEvent.change(input,{target: {value: username}});
    fireEvent.submit(form);

    expect(input.value).toBe(username);
    expect(input.nextElementSibling.textContent).not.toBe("");
});
```

Jak i te, w których jest ona zupełnie normalna:
```javascript
test("Testing normal user name input", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let username = "Kuba";
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Nazwa użytkownika"]');

    fireEvent.change(input,{target: {value: username}});
    fireEvent.submit(form);

    expect(input.value).toBe(username);
    expect(input.nextElementSibling.textContent).toBe("");
});
```

Nazwa użytkownika **nie posiada minimalnej** liczby znaków, posiada jednak **maksymalną** i wynosi ona 20. To również zostało uwzględnione w testach:

```javascript
test("Testing short user name input", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let username = "K";
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Nazwa użytkownika"]');

    fireEvent.change(input,{target: {value: username}});
    fireEvent.submit(form);

    expect(input.value).toBe(username);
    expect(input.nextElementSibling.textContent).toBe("");
});

test("Testing 20-letters user name input", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let username = "aaaaabbbbbcccccddddd";
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Nazwa użytkownika"]');

    fireEvent.change(input,{target: {value: username}});
    fireEvent.submit(form);

    expect(input.value).toBe(username);
    expect(input.nextElementSibling.textContent).toBe("");
});

test("Testing 21-letters user name input", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let username = "aaaaabbbbbcccccddddde";
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Nazwa użytkownika"]');

    fireEvent.change(input,{target: {value: username}});
    fireEvent.submit(form);

    expect(input.value).toBe(username);
    expect(input.nextElementSibling.textContent).not.toBe("");
});
```

Na koniec zostało nam przetestować pola do hasła i jego powtórzenia, głównym założeniem hasła jest nie mniej niż 8 znaków i nie więcej niż 15.
Hasło musi zostać również potwierdzone przez użytkownika poprzez wpisanie go ponownie w przeznaczonym do tego polu.\
To również sprawdziliśmy w naszych testach:

```javascript
test("Testing 5-letters password input", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let password = "aaaaa";
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Hasło"]');

    fireEvent.change(input,{target: {value: password}});
    fireEvent.submit(form);

    expect(input.value).toBe(password);
    expect(input.nextElementSibling.textContent).not.toBe("");
});

test("Testing 6-letters password input", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let password = "aaaaab";
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Hasło"]');

    fireEvent.change(input,{target: {value: password}});
    fireEvent.submit(form);

    expect(input.value).toBe(password);
    expect(input.nextElementSibling.textContent).toBe("");
});

test("Testing 15-letters password input", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let password = "aaaaabbbbbccccc";
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Hasło"]');

    fireEvent.change(input,{target: {value: password}});
    fireEvent.submit(form);

    expect(input.value).toBe(password);
    expect(input.nextElementSibling.textContent).toBe("");
});

test("Testing 16-letters password input", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let password = "aaaaabbbbbcccccd";
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Hasło"]');

    fireEvent.change(input,{target: {value: password}});
    fireEvent.submit(form);

    expect(input.value).toBe(password);
    expect(input.nextElementSibling.textContent).not.toBe("");
});

test("Checking if repeated password matches password", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let password = "aaaaabb";
    let repeated_password = "aaaaabb";
    let form = container.querySelector('form');
    let input_password= container.querySelector('input[placeholder="Hasło"]');
    let input_repeated = container.querySelector('input[placeholder="Powtórz hasło"]');

    fireEvent.change(input_password,{target: {value: password}});
    fireEvent.change(input_repeated,{target: {value: repeated_password}});
    fireEvent.submit(form);

    expect(input_password.value).toBe(password);
    expect(input_repeated.value).toBe(repeated_password);
    expect(input_repeated.nextElementSibling.textContent).toBe("");
});

test("Checking if incorrect repeated password matches password", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let password = "aaaaabb";
    let repeated_password = "aaaaabbc";
    let form = container.querySelector('form');
    let input_password= container.querySelector('input[placeholder="Hasło"]');
    let input_repeated = container.querySelector('input[placeholder="Powtórz hasło"]');

    fireEvent.change(input_password,{target: {value: password}});
    fireEvent.change(input_repeated,{target: {value: repeated_password}});
    fireEvent.submit(form);

    expect(input_password.value).toBe(password);
    expect(input_repeated.value).toBe(repeated_password);
    expect(input_repeated.nextElementSibling.textContent).not.toBe("");
});
```

Jako końcowy test sprawdziliśmy, czy podając wszystkie dane prawidłowo, jesteśmy w stanie zarejestrować się bezbłędnie:

```javascript
test("Simulating correct registration", () => {
    act(() => {
        ReactDOM.render(<Register/>, container);
    });

    let email = "abc@abc.com";
    let nickname = "Kuba";
    let password = "aaaaabb";
    let repeated_password = "aaaaabb";
    let form = container.querySelector('form');
    let input_email= container.querySelector('input[placeholder="Email"]');
    let input_nickname= container.querySelector('input[placeholder="Nazwa użytkownika"]');
    let input_password= container.querySelector('input[placeholder="Hasło"]');
    let input_repeated = container.querySelector('input[placeholder="Powtórz hasło"]');

    fireEvent.change(input_email,{target: {value: email}});
    fireEvent.change(input_nickname,{target: {value: nickname}});
    fireEvent.change(input_password,{target: {value: password}});
    fireEvent.change(input_repeated,{target: {value: repeated_password}});
    fireEvent.submit(form);

    expect(input_email.value).toBe(email);
    expect(input_nickname.value).toBe(nickname);
    expect(input_password.value).toBe(password);
    expect(input_repeated.value).toBe(repeated_password);
    expect(input_email.nextElementSibling.textContent).toBe("");
    expect(input_nickname.nextElementSibling.textContent).toBe("");
    expect(input_password.nextElementSibling.textContent).toBe("");
    expect(input_repeated.nextElementSibling.textContent).toBe("");
});
```