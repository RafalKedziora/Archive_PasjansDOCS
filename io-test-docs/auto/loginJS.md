# Panel logowania

>Testy wykonał: Piotr Czajkowski  
> Poprawki wykonała: Gabriela Stefaniak

Panel logowania umożliwia uwierzytelnienie użytkownika w systemie, wymagane jest podanie prawidłowego adresu email, jak i hasła.  
Napisaliśmy testy, które sprawdzają, czy komunikaty błędów się wyświetlają, jeśli dane są nieprawidłowe:

```javascript
test("Incorrect email causes email Error", () => {
    act(() => {
        ReactDOM.render(<Login/>, container);
    });

    let invalidEmail = "tost mail"
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Email"]');

    fireEvent.change(input,{target: {value: invalidEmail}});
    fireEvent.submit(form);

    expect(input.value).toBe(invalidEmail);
    expect(input.nextElementSibling.textContent.length).toBeGreaterThanOrEqual(1);
});

test("Empty mail causes email Error", () => {
    act(() => {
        ReactDOM.render(<Login/>, container);
    });

    let invalidEmail = ""
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Email"]');

    fireEvent.change(input,{target: {value: invalidEmail}});
    fireEvent.submit(form);

    expect(input.value).toBe(invalidEmail);
    expect(input.nextElementSibling.textContent.length).toBeGreaterThanOrEqual(1);
});

test("Empty password causes password Error", () => {
    act(() => {
        ReactDOM.render(<Login/>, container);
    });

    let invalidPassword = ""
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Hasło"]');

    fireEvent.change(input,{target: {value: invalidPassword}});
    fireEvent.submit(form);

    expect(input.value).toBe(invalidPassword);
    expect(input.nextElementSibling.textContent.length).toBeGreaterThanOrEqual(1);
});
```

Sprawdziliśmy również, czy nie ma komunikatów, jeśli dane są prawidłowe:

```javascript
test("Correct maill does not cause email Error", () => {
    act(() => {
        ReactDOM.render(<Login/>, container);
    });

    let invalidEmail = "tost@mail.com"
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Email"]');

    fireEvent.change(input,{target: {value: invalidEmail}});
    fireEvent.submit(form);

    expect(input.value).toBe(invalidEmail);
    expect(input.nextElementSibling.textContent.length).toBeGreaterThanOrEqual(0);
});

test("Correct password does not cause password Error", () => {
    act(() => {
        ReactDOM.render(<Login/>, container);
    });

    let invalidPassword = "1234"
    let form = container.querySelector('form');
    let input = container.querySelector('input[placeholder="Hasło"]');

    fireEvent.change(input,{target: {value: invalidPassword}});
    fireEvent.submit(form);

    expect(input.value).toBe(invalidPassword);
    expect(input.nextElementSibling.textContent.length).toBeGreaterThanOrEqual(0);
});
```