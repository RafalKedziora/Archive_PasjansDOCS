# Database

Folder odpowiadający za połączenia, kwerendy i skrypty w bazie danych.

# connection

Za stworzenie i weryfikacje połączenia odpowiada `mysql_query.js`.

W razie błędnego połączenia z bazą mysql konsola wypisuje błąd.

W przypadku użycia kwerend obsługa błędu wypisuje w konsoli informacje o błędnej kwerendzie.

# queries

`account_select.sql` - odpowiada za znalezienie konta po ID.

`account_update.sql` - aktualizacja danych konta.

`check_if_user_exist_by_email.sql` - sprawdzenie czy użytkownik istnieje korzystając z jego emaila.

`get_settings.sql` - pobranie ustawień gry dla gracza o odpowiednim user_id.

`get_stats_player.sql` - pobranie wszystkich statystyk gracza.

`get_stats.sql` - pobranie wszystkich statystyk (globalnych).

`insert_game_occur.sql` - wstawienie do bazy zdarzenia z gry.

`insert_game.sql` - wstawienie do tabeli `games`, wartości o rozpoczęciu i zakończeniu rozgrywki.

`login.sql` - wybranie danych dla użytkownika o danym emailu.

`player_exists.sql` - sprawdzenie czy użytkownik istnieje.

`register.sql` - dodanie danych z rejestracji do bazy danych.

`settings_insert.sql` - dodanie do tabeli `settings` wartości ustawień.

`update_settings` - zaktualizowanie danych dla danego konta.
