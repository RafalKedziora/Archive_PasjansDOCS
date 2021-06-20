## Baza danych MySQL

Baza danych aplikacji jest oparta o MySQL. To jedna baza składająca się z kilku tabel:

`cardsets`

```
id int(11) AI PK
name varchar(32)
```

`gameoccurrences`

```
id int(11) AI PK
player_id int(11)
game_id int(11)
points int(11)
completion_time int(11)
moves text
starting_distribution text
is_win tinyint(1)
```

Foreign Keys

```
Related Tables:
Target players (player_id → id)
On Update RESTRICT
On Delete RESTRICT
Target games (game_id → id)
On Update RESTRICT
On Delete RESTRICT
```

`games`

```
id int(11) AI PK
date_started datetime
date_ended datetime
```

`icons`

```
id int(11) AI PK
src varchar(255)
```

`inventory`

```
id bigint(20) UN AI PK
name varchar(50)
quantity int(11)
```

`players`

```
id int(11) AI PK
icon_id int(11)
username varchar(32)
email varchar(32)
password varchar(64)
active tinyint(1)
country varchar(40)
registration_date varchar(35)
last_login datetime
```

Foreign Keys

```
Related Tables:
Target icons (icon_id → id)
On Update RESTRICT
On Delete RESTRICT
```

`settings`

```
id int(11) AI PK
user_id int(11)
cardset_id int(11)
volume int(11)
effect int(11)
card_animation tinyint(1)
```

Foreign Keys

```
Related Tables:
Target cardsets (cardset_id → id)
On Update RESTRICT
On Delete RESTRICT
Target players (user_id → id)
On Update RESTRICT
On Delete RESTRICT
Target players (user_id → id)
On Update RESTRICT
On Delete RESTRICT
```

`statstable`

```
ID int(11) AI PK
Nazwa varchar(255)
Avatar varchar(300)
Ranking int(11)
Wygrane int(11)
Remisy int(11)
Przegrane int(11)
```
