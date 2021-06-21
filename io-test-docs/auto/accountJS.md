# Profil użytkownika

>Testy wykonali: Piotr Czajkowski oraz Robert Ciołek

Profil użytkownika jest miejscem, w którym może on dokonać modyfikacji swoich ustawień w grze, 
to tutaj użytkownik może zmienić swoją nazwę avatar czy też hasło.

Na pierwszy ogień w testach chwyciliśmy nazwę użytkownika. Sprawdziliśmy, czy użytkownik może zmienić nazwę, jeśli jest ona poprawna 
oraz czy system wyświetli komunikat, jeśli nazwa będzie nieprawidłowa:

```javascript
test('New user name is set after user name edition.', () => {
    act(() => {
        ReactDOM.render(<Account/>, container);
    });

    let profileUserName = container.querySelector('.profile-username');
    let editButton = container.querySelector('.edition-text');
    let editUserName = container.querySelector('.account_modal-nick-input');
    let okButton = container.querySelector('.modal-button-save');
    let newUserName = "newUserName";

    fireEvent.click(editButton);
    fireEvent.change(editUserName, {target: {value: newUserName}});
    fireEvent.click(okButton);

    expect(profileUserName.innerHTML).toBe(newUserName);
});

test('EMPTY new user name is NOT set after user name edition.', () => {
    act(() => {
        ReactDOM.render(<Account/>, container);
    });

    let profileUserName = container.querySelector('.profile-username');
    let editButton = container.querySelector('.edition-text');
    let editUserName = container.querySelector('.account_modal-nick-input');
    let okButton = container.querySelector('.modal-button-save');
    let newUserName = '';

    fireEvent.click(editButton);
    fireEvent.change(editUserName, {target: {value: newUserName}});
    fireEvent.click(okButton);

    expect(profileUserName.innerHTML).not.toBe(newUserName);
});
```

Podobne testy przeprowadziliśmy dla zmiany hasła, uwzględniając oczywiście to, że hasło posiada swoją specyficzną logikę.
Mianowicie, musi zostać ono powtórzone, aby była możliwa jego zmiana. W związku z tym powstały następujące testy:

```javascript
test('Enter the CORRECT password to old password', () => {
    act(() => {
        ReactDOM.render(<Account/>, container);
    });

    let oldPassInput = container.querySelector('.account_modal-password-old-input');
    let correctOldPassword = "admin"

    fireEvent.change(oldPassInput, {target: {value: correctOldPassword}})
    
    expect(oldPassInput.nextElementSibling).toBeNull();
})

test('Enter the WRONG password to old password', () => {
    act(() => {
        ReactDOM.render(<Account/>, container);
    });

    let oldPassInput = container.querySelector('.account_modal-password-old-input');
    let correctOldPassword = "wrongPass"

    fireEvent.change(oldPassInput, {target: {value: correctOldPassword}})

    expect(oldPassInput.nextElementSibling).not.toBeNull();
})

test('Enter the CORRECT new password twice', () => {
    act(() => {
        ReactDOM.render(<Account/>, container);
    });

    let newPassInput = container.querySelector('.account_modal-password-input-new');
    let correctNewPassword = "admin123"

    let newPassInputRepeat = container.querySelector('.account_modal-password-input-new-repeat')
    let correctNewPasswordRepeat = correctNewPassword;

    fireEvent.change(newPassInput, {target: {value: correctNewPassword}})
    fireEvent.change(newPassInputRepeat, {target: {value: correctNewPasswordRepeat}})
    
    expect(newPassInputRepeat.nextElementSibling).toBeNull();
})

test('Enter the CORRECT new password and WRONG password as a repeated', () => {
    act(() => {
        ReactDOM.render(<Account/>, container);
    });

    let newPassInput = container.querySelector('.account_modal-password-input-new');
    let correctNewPassword = "admin123"

    let newPassInputRepeat = container.querySelector('.account_modal-password-input-new-repeat')
    let correctNewPasswordRepeat = "admin1233";

    fireEvent.change(newPassInput, {target: {value: correctNewPassword}})
    fireEvent.change(newPassInputRepeat, {target: {value: correctNewPasswordRepeat}})

    expect(newPassInputRepeat.nextElementSibling).not.toBeNull();
})

test('Enter the CORRECT new password and EMPTY password as a repeated', () => {
    act(() => {
        ReactDOM.render(<Account/>, container);
    });

    let newPassInput = container.querySelector('.account_modal-password-input-new');
    let correctNewPassword = "admin123"

    let newPassInputRepeat = container.querySelector('.account_modal-password-input-new-repeat')
    let correctNewPasswordRepeat = " ";

    fireEvent.change(newPassInput, {target: {value: correctNewPassword}})
    fireEvent.change(newPassInputRepeat, {target: {value: correctNewPasswordRepeat}})

    expect(newPassInputRepeat.nextElementSibling).not.toBeNull();
})

test('Enter the EMPTY new password and CORRECT password as a repeated', () => {
    act(() => {
        ReactDOM.render(<Account/>, container);
    });

    let newPassInput = container.querySelector('.account_modal-password-input-new');
    let correctNewPassword = " "

    let newPassInputRepeat = container.querySelector('.account_modal-password-input-new-repeat')
    let correctNewPasswordRepeat = "admin123";

    fireEvent.change(newPassInput, {target: {value: correctNewPassword}})
    fireEvent.change(newPassInputRepeat, {target: {value: correctNewPasswordRepeat}})

    expect(newPassInputRepeat.nextElementSibling).not.toBeNull();
})
```

Powstały również testy sprawdzające zmianę avataru użytkownika:

```javascript
test('After the last avatar, the first one appears.', () => {
    act(() => {
        ReactDOM.render(<Account/>, container);
    });

    let nextAvatarButton = container.querySelector('.modal-right-arrow');
    let avatar = container.querySelector('.modal-avatar-image');

    //z avatar1 na avatar2
    fireEvent.click(nextAvatarButton);
    //z avatar2 na avatar3
    fireEvent.click(nextAvatarButton);
    //z avatar3 na avatar4
    fireEvent.click(nextAvatarButton);
    //z avatar4 na avatar5
    fireEvent.click(nextAvatarButton);
    //z avatar5 na avatar6
    fireEvent.click(nextAvatarButton);
    //z avatar6 na avatar1
    fireEvent.click(nextAvatarButton);

    expect(avatar.src).toBe('http://localhost/images/avatar1.png')
})
```

Na samym końcu przetestowaliśmy czy dane są zmienione, jeśli zostały wprowadzone poprawnie oraz sytuacje analogicznie odwrotną:

```javascript
test('New data is set when data is CORRECT', () => {
    act(() => {
        ReactDOM.render(<Account/>, container);
    });

    let profileUserName = container.querySelector('.profile-username');
    let editButton = container.querySelector('.edition-text');
    let editUserName = container.querySelector('.account_modal-nick-input');
    let okButton = container.querySelector('.modal-button-save');
    let newUserName = "newUserName";

    fireEvent.click(editButton);
    fireEvent.change(editUserName, {target: {value: newUserName}});

    let oldPassInput = container.querySelector('.account_modal-password-old-input');
    let correctOldPassword = "admin"

    fireEvent.change(oldPassInput, {target: {value: correctOldPassword}})

    let newPassInput = container.querySelector('.account_modal-password-input-new');
    let correctNewPassword = "admin123"

    let newPassInputRepeat = container.querySelector('.account_modal-password-input-new-repeat')
    let correctNewPasswordRepeat = "admin123";

    fireEvent.change(newPassInput, {target: {value: correctNewPassword}})
    fireEvent.change(newPassInputRepeat, {target: {value: correctNewPasswordRepeat}})
    fireEvent.click(okButton);

    //Czy zmieniła się nazwa?
    expect(profileUserName.innerHTML).toBe(newUserName);
    //Czy hasło zostało zmienione?
    fireEvent.change(oldPassInput, {target: {value: correctNewPassword}})
    expect(oldPassInput.nextElementSibling).toBeNull();
})

test('New data is NOT set when data is WRONG', () => {
    act(() => {
        ReactDOM.render(<Account/>, container);
    });

    let profileUserName = container.querySelector('.profile-username');
    let editButton = container.querySelector('.edition-text');
    let editUserName = container.querySelector('.account_modal-nick-input');
    let okButton = container.querySelector('.modal-button-save');
    let newUserName = "newUserName";

    fireEvent.click(editButton);
    fireEvent.change(editUserName, {target: {value: newUserName}});

    let oldPassInput = container.querySelector('.account_modal-password-old-input');
    let correctOldPassword = "admin"

    fireEvent.change(oldPassInput, {target: {value: correctOldPassword}})

    let newPassInput = container.querySelector('.account_modal-password-input-new');
    let correctNewPassword = "admin123"

    let newPassInputRepeat = container.querySelector('.account_modal-password-input-new-repeat')
    let wrongNewPasswordRepeat = "";

    fireEvent.change(newPassInput, {target: {value: correctNewPassword}})
    fireEvent.change(newPassInputRepeat, {target: {value: wrongNewPasswordRepeat}})
    fireEvent.click(okButton);

    fireEvent.click(editButton);
    //  Czy zmieniła się nazwa?
    //  Nazwa się zmieni, ponieważ nie potrzebuje walidacji hasła - możemy "od tak" zmienić nick
    expect(profileUserName.innerHTML).toBe(newUserName);
    //Czy hasło zostało zmienione?
    fireEvent.change(oldPassInput, {target: {value: correctNewPassword}})
    expect(oldPassInput.nextElementSibling).not.toBeNull();
})
```