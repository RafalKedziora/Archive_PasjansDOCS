## users.js

`users.js` dzieli się na `USERS` i `ROOMS`. Przechowuje elementy potrzebne do obsługi zdarzeń w pokoju.

USERS:

- `userJoin` w momencie dołączania użytkownika do pokoju.
- `getCurrentUser` szuka użytkownika za pomocą `id`.
- `userLeave` obsługa opuszczania pokoju przez użytkownika. Usuwa użytkownika, na jego indeksie.
- `getAllUsers` zwraca wszystkich użytkowników.

ROOMS:

- `getRoomUsers` zwraca wszystkich użytkowników danego pokoju.
- `setUsersInGame` u graczy w pokoju ustawia właściwość `.ingame` na true, aby wiadomo było, że są w grze.
- `setUsersOutOfGame` u graczy w pokoju ustawia właściwość `.ingame` na fakse, aby wiadomo było, że nie są w grze.
- `modifyRoom` u każdego gracza modyfikuje wyświetlaną nazwę pokoju.
