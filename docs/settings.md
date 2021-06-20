# Settings.js

W pliku tym znajdują się wszystkie właściwości związane z ustawieniami. Funkcja przyjmuje parametr `ID` który jest indywidualnym id każdego użytkownika.

Funkcja `Settings` daje możliwość:
- zmiany motywów kart,
- ustawienia poziomu głośności muzyki,
- ustawienia poziomu głośności efektów.

Ustawienia można ustawiać zarówno z poziomu gościa, jak i zalogowanego użytkownika. Ustawienia dla gości zapamiętywane są tylko na czas trwania sesji. Dla zalogowanych użytkowników ustawienia są zapamiętywane.

Motywy kart możliwe do wybrania:
```js
  const motives = ["cyberpunk", "default"];
```

Motywy kart można zmieniać za pomocą przycisków, pokazują się one takze na podglądzie. Wybrany motyw trzeba zatwierdzić przyciskiem "Wybierz".

Ustawienie poziomu głośności muzyki oraz efektów odbywa się za pomocą dwóch osobnych sliderów. Obok sliderów pokazana jest wartość głośności jako procent maksymalnej głośności.