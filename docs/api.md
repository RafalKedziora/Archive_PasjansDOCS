# accountRoute.js
Sekcja odpowiada za weryfikację i pobranie danych użytkownika podczas logowania oraz za wprowadzenie danych z rejestracji do bazy.

`UserID` - zmienna przechowująca ID użytkownika.

`icon_id` - zmienna przechowująca ID awataru.

`username` - zmienna przechowująca nazwę użytkownika.

`password` - zmienna przechowująca hasło.

`country` - zmienna przechowująca kraj.

Weryfikacja istnienia użytkownika:
```js
 let resp = await mysqlQuery(userExistQuery, [userId]);
    if (resp.length == 0) return res.status(404).json("user doesn't exist");
```
Pobranie odpowiedniej kwerendy:
```js
  const query = fs
    .readFileSync(path.join(__dirname, "../../database/queries/account_select.sql")) 
    .toString();
```
Wprowadzenie danych do bazy:
```js
await mysqlQuery(query, [icon_id,username,password,country, userId]);
```

# authRoute.js
Następuje tu proces autoryzacji danych.

`username` - zmienna przechowująca nazwę użytkownika.

`email` - zmienna przechowująca email użytkownika.

`password` - zmienna przechowująca hasło użytkownika.

`hashedpassword` - zmienna przechowująca zaszyfrowane hasło.

`key` - zmienna przechowująca klucz tokena.

Weryfikacja wprowadzonych danych:
```js
const emailRegex =
    /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
  if (!email.match(emailRegex)) return res.status(400).json("email is invalid");
  if (!username) return res.status(400).json("username cannot be empty");
  if (username.length > 20) return res.status(400).json("username is too long");
  if (password.length < 6) return res.status(400).json("password is too short");
  if (password.length > 15) return res.status(400).json("password is too long");
```
Pobranie odpowiedniej kwerendy i sprawdzenie, czy wprowadzony e-mail jest wolny:
```js
const checkIfUserExistsQuery = fs
    .readFileSync(
      path.join(
        __dirname,"../../database/queries/check_if_user_exists_by_email.sql"
      )
    )
    .toString();

  let resp = await mysqlQuery(checkIfUserExistsQuery, [email]);
    return res.status(403).json({ email: "Email jest zajęty" });
```
Zaszyfrowanie hasła:
```js
const hashedPassword = await bcrypt.hash(password, saltRounds);
```
Dodanie danych nowego użytkownika do bazy:
```js
resp = await mysqlQuery(query, [username, email, hashedPassword]);
```
Weryfikacja danych wprowadzanych podczas logowania:
```js
const emailRegex =
    /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
   
  if (!email.match(emailRegex)) return res.status(400).json("email is invalid");
  if (!password) return res.status(400).json("Password is empty");
```
Pobranie danych na podstawie e-maila i ich weryfikacja:
```js
const query = fs
    .readFileSync(path.join(__dirname, "../../database/queries/login.sql"))
    .toString();
  let resp = await mysqlQuery(query, [email]);

  if (resp.length == 0)
    return res.status(401).json("Email lub hasło jest niepoprawne");
```
Weryfikacja wprowadzonego hasła:
```js
const isPasswordCorrect = await bcrypt.compare(password, hashedPassword);
if (!isPasswordCorrect)
    return res.status(401).json("Email lub hasło jest niepoprawne");
```

Stworzenie tokenu:
```js
const key = process.env.TOKEN_KEY;
  const token = jwt.sign(
    {
      id,
      username,
      email,
    },
    key,
    { expiresIn: 60 * 60 * 24 * 7 }
  );
```

Stworzenie ciasteczka:
```js
res.cookie("token", token, {
    httpOnly: true,
    secure: true,
    maxAge: 3600000,
    sameSite: true,
  });
```

# settingsRoute.js
Odpowiada za zmianę ustawień użytkownika.

`cardset_id` - zmienna przechowująca ID motywu kart.

`music` - zmienna przechowująca wartość głośności muzyki.

`effect` - zmienna przechowująca wartość głośności efektów.


Weryfikacja zmiennych:
```js
if (!card[cardset_id]) return res.status(400).json("invalid cardset_id");
  if (isNaN(music) || music < 0 || music > 100)
    return res.status(400).json("invalid music volume");
  if (isNaN(effect) || effect < 0 || effect > 100)
    return res.status(400).json("invalid effect volume");
```
Wprowadzenie nowych zmiennych do bazy danych:
```js
await mysqlQuery(query, [cardset_id, music, effect, userId]);
```
Jeśli użytkownik nie istnieje, wystąpi określony komunikat:
```js
if (resp.length == 0) return res.status(404).json("user doesn't exist");
```
# statsRoute.js
Służy do pobierania z bazy danych statystyk graczy:
```js
router.get("/getStats", async (req, res) => {
  const query = fs
    .readFileSync(path.join(__dirname, "../../database/queries/get_stats.sql"))
    .toString();

  const resp = await mysqlQuery(query);

  res.status(200).json(resp);
});
```