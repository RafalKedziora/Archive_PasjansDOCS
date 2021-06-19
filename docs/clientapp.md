## App.js

Główny komponent, który jest kontenerem dla każdego innego komponentu.

Dla gościa ustawiane są głośność efektów, muzyki, motyw kard oraz user ID.

```js
const [eff, setEffect] = useState(
  JSON.parse(localStorage.getItem("guestEffect")) ?? 20
);
const [vol, setVolume] = useState(
  JSON.parse(localStorage.getItem("guestMusic")) ?? 20
);
const [cardset, setCardSet] = useState(2);
const [userId, setUserId] = useState(localStorage.getItem("userId"));
```

Pobierane są z bazy danych informacje o `cardset_id, volume, effect`.

Przy pobraniu `auth/verify` przez `agent` następuje ustawienie statusu logowania.

```js
agent
  .get("auth/verify")
  .then(() => {
    localStorage.setItem("isLogged", true);
  })
  .catch(() => {
    localStorage.setItem("isLogged", false);
    localStorage.setItem("userId", 0);
  });
```

Zwracany jest switch, który zawiera wiele komponentów aktywowanych w zależności od `path`.

```js
<Switch>
  <Route exact path="/" component={() => <MainMenu effect={eff} />} />
  <AuthRoute path="/login" component={Login} />
  <AuthRoute path="/register" component={Register} />
  <Route path="/settings" component={() => <Settings ID={userId} />} />
  <PrivateRoute
    path="/global-stats"
    component={() => <GlobalStats effect={eff} />}
  />
  <Route path="/game-view" component={() => <GameViewRoute />} />
  <PrivateRoute
    path="/multiplayer"
    component={() => <LobbyMultiplayer userId={userId} />}
  />
  <PrivateRoute
    path="/account"
    component={() => <Account effect={eff} userId={userId} />}
  />
  <PrivateRoute path="/game-lobby" component={JoinRoom} />
  <PrivateRoute
    path="/create-room"
    component={() => <CreateRoom userId={userId} />}
  />
  <Route path="/app-info" component={AppInfo} />
  <Route path="/authors" component={Authors} />
</Switch>
```

`login` - logowanie. `register` - rejestracja. `settings` - ustawienia. `global-stats` - statystyki dla wszystkich graczy. `game-view` - widok gry. `multiplayer` - wejście do gry wieloosobowej. `account` - widok konta. `game-lobby` - dołączenie do lobby. `create-room` - tworzenie lobby. `app-info` - informacje o grze. `authors` - informacje o autorach.

`GameViewRoute` to komponent odpowiadający za
