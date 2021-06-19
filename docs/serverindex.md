## index.js

Główny plik 'spajający' ze sobą pliki serwerowe. Posiada fragmenty potrzebne do komunikacji komponentów ze sobą, zawiera struktury socketów oraz część funkcjonalności logowania.

Struktura plików serwera:

```js
const exampleRoute = require("./api/example/exampleRoute");
const roomsRoute = require("./api/rooms/roomsRoute");
const settingsRoute = require("./api/settings/settingsRoute");
const statsRoute = require("./api/stats/statsRoute");
const authRoute = require("./api/auth/authRoute");
const accountRoute = require("./api/account/accountRoute");
const path = require("path");
```

Stałe potrzebne do obsługi logiki socketowej.

```js
const {
  userJoin,
  getCurrentUser,
  userLeave,
  getRoomUsers,
  modifyRoom,
  getAllUsers,
  setUsersInGame,
} = require("./utils/users");
```

Zmienne socketowe

```js
const { Server } = require("socket.io");
const io = new Server(server);
```

Za logowanie odpowiada ten fragment `index.js`.

```js
app.use(function (req, res, next) {
  res.setHeader("Access-Control-Allow-Origin", process.env.CLIENT_URL);

  res.setHeader(
    "Access-Control-Allow-Methods",
    "GET, POST, OPTIONS, PUT, PATCH, DELETE"
  );

  res.setHeader(
    "Access-Control-Allow-Headers",
    "X-Requested-With,content-type"
  );

  res.setHeader("Access-Control-Allow-Credentials", true);

  next();
});
```

Przy połączeniu socket umożliwia korzystanie z kilku funkcjonalności. Po poprawnym podłączeniu wywoływane jest `console.log("a user connected");`.
Wysyłanie informacji do clienta o wszystkich graczach, którzy nie są w grze:

```js
socket.on("export-users", () => {
  socket.emit(
    "pass-users",
    getAllUsers().filter((user) => !user.inGame)
  );
});
```

Wysyłanie przez socket informacji do klienta o pokoju:

```js
socket.on("export-room", () => {
  const user = getCurrentUser(socket.id);

  if (user) {
    socket.emit("pass-room", {
      room: user.room,
      users: getRoomUsers(user.room),
    });
  }
});
```

Za wysyłanie przez socket informacji o starcie gry i czasie wystartowania gry w danym pokoju odpowiada

```js
socket.on("game-start", ({ room, time }) => {
  setUsersInGame(room);
  io.to(room).emit("start", { time });
});
```

Modyfikacja nazwy lobby i synchronizacja z innymi graczami

```js
socket.on("lobby-modify", ({ room, newName }) => {
  const user = getCurrentUser(socket.id);

  modifyRoom(room, newName);

  if (user) {
    io.to(newName).emit("pass-room", {
      room,
      users: getRoomUsers(newName),
    });
  }
});
```

Dołączanie gracza do pokoju

```js
socket.on("lobby-join", ({ player, room }) => {
  const user = userJoin(socket.id, player, room);

  console.log("a user joined the room");
  socket.join(user.room);

  if (user) {
    io.to(room).emit("pass-room", {
      room,
      users: getRoomUsers(room),
    });
  }
});
```

Opuszczanie pokoju przez gracza

```js
socket.on("lobby-leave", () => {
  const user = getCurrentUser(socket.id);

  userLeave(socket.id);

  if (user) {
    io.to(user.room).emit("pass-room", {
      room: user.room,
      users: getRoomUsers(user.room),
    });
  }
});
```

Wyrzucanie gracza z pokoju

```js
socket.on("kick", ({ player }) => {
  userLeave(player.id);
  io.to(player.id).emit("kicked", { room: player.room });

  io.to(player.room).emit("pass-room", {
    room: player.room,
    users: getRoomUsers(player.room),
  });
});
```

Koniec rozgrywki, przekazanie odpowiednich danych `pleyer.username` oraz `score`.

```js
socket.on("end-game", ({ score }) => {
  const player = getCurrentUser(socket.id);

  io.to(player.room).emit("write-to-end-list", {
    player: player.username,
    score: score,
  });
});
```

Opuszczenie rozgrywki przez gracza

```js
socket.on("disconnect", () => {
    console.log("user disconnected");
    userLeave(socket.id);
    socket.emit("export-room");
  });
});
```
