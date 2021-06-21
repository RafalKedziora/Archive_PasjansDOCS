!> Klikając w tytuły użytkownik zostaje przeniesiony do dokumentacji poszczególnych technologii.

# [JestJS](https://jestjs.io/docs/getting-started)

`Jest` to uniwersalna platforma testowa, z możliwością dostosowania do dowolnej biblioteki lub frameworka `JavaScript`.
Testy pisane w `Jest` są zrównoleglone, uruchamiając je we własnych procesach w celu maksymalizacji wydajności.
Od `expect` do `toBe` - Jest ma cały zestaw narzędzi w jednym miejscu, które są dobrze udokumentowane. Był to ważny
czynnik w wyborze głównego narzędzia, ze wzgledu na brak dużego doświadczenia w testowaniu.

`Jest` używa niestandardowego resolvera dla importów w testach, co ułatwia mockowanie dowolnego obiektu poza zakresem
testu. Mogliśmy używać mockowanych importów z interfejsem API Mock Functions do szpiegowania wywołań funkcji z czytelną
składnią testową.

# [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)

`React Testing Library` rozwija się na bazie `DOM Testing Library`, dodając interfejsy API do pracy z
komponentami `React`.

Chcieliśmy pisać możliwe do utrzymania testy dla swoich komponentów React, aby testy unikały uwzględniania
szczegółów implementacji komponentów i raczej skupiały się na tym, aby testy dawały pewność, do której są przeznaczone.
W ramach tego baza testów była możliwa do utrzymania na dłuższą metę, aby refaktoryzacje naszych komponentów (zmiany w
implementacji, ale nie w funkcjonalności) nie zakłócały pisanych testów i nie spowalniały naszego całego zespołu.