# Login

Plik `Login.js` zawiera dwa główne elementy. Pierwszy z nich to `function Login()`, która odpowiada za porawne zalogowanie się do naszego konta.
Stałe wprowadzane bezpośrednio przez użytkownika to `email` i `password`.
```js
function Login() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [emailError, setEmailError] = useState("");
  const [passwordError, setPasswordError] = useState("");
  const [serverError, setServerError] = useState("");
  const [isLoggedIn, setLoggedIn] = useState(false);

  const handleSubmit = async (e) => {
    e.preventDefault();
    setServerError("");
    if (isValid()) {
      agent
        .post("auth/login", {
          email,
          password,
        })
        .then((resp) => {
          if (resp.status === 200) {
            localStorage.setItem('isLogged', true);
            localStorage.setItem('user', JSON.stringify(resp.data));
            setLoggedIn(true);
            window.location.href = '/';
          }
        })
        .catch((err) => {
          if (err.response.data) setServerError(err.response.data);
        });
    }
  };
```
Drugi równie ważny element pliku to walidacja wprowadzonego łańcucha znaków. Sprawdzany jest tutaj wprowadzony `email` przez `emailRegex`, oraz czy hasło nie jest puste.

```js
  const isValid = () => {
    setEmailError("");
    setPasswordError("");
    let isValid = true;
    const emailRegex =
      /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    if (!email.match(emailRegex)) {
      setEmailError("Email jest niepoprawny");
      isValid = false;
    }
    if (!password) {
      setPasswordError("Hasło nie może być puste");
      isValid = false;
    }
    return isValid;
  };
```