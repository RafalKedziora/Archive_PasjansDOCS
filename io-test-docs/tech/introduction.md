# Cel testowania
Testowanie aplikacji internetowych to praktyka oprogramowania, która zapewnia jakość poprzez testowanie,
czy funkcjonalność danej aplikacji internetowej działa zgodnie z przeznaczeniem lub zgodnie z wymaganiami.
Testowanie umożliwia znajdowanie błędów w dowolnym momencie, przed wydaniem lub na co dzień.

>Testowanie jest bardzo ważną częścią tworzenia oprogramowania. 

Dzieje się tak, ponieważ za każdym razem, 
gdy nastąpi zmiana w kodzie, bez względu na to jak mała jest zmiana, błędy mogą pojawić się w innym miejscu systemu. 
Co więcej, koszt naprawy tych błędów również rośnie z czasem, więc posiadanie skutecznych testów internetowych 
zapewni Ci czas i pieniądze na rozwój Twojej aplikacji.

# Jak testujemy aplikację?

Stworzenie najwyższej klasy aplikacji internetowej wymaga wielu testów, które wykonywane ręcznie mogą być żmudne 
i czasochłonne. Automatyzacja testów przenosi te rutynowe i powtarzalne zadania testowe z ludzi na maszyny. Testy 
porównują rzeczywiste wyniki z przewidywanymi. Takie podejście może pomóc w znalezieniu błędów w określonych operacjach 
i prostych przypadkach (np. logowanie, tworzenie nowego konta, resetowanie hasła).

>Oprócz testów automatycznych nie odeszliśmy jednakże od testów manualnych

# Testy manualne

Testowanie manualne (ręczne) to proces testowania oprogramowania, w którym przypadki testowe są wykonywane ręcznie bez użycia 
zautomatyzowanego narzędzia. Wszystkie przypadki testowe wykonywane przez testera ręcznie zgodnie z perspektywą 
użytkownika końcowego. Zapewnia, że aplikacja działa, jak wspomniano w dokumencie wymagań, czy nie. Przypadki testowe
są planowane i wdrażane w celu ukończenia prawie 100 procent aplikacji. Raporty przypadków testowych są również 
"generowane" ręcznie.

# Testy jednostkowe

Tworzona przez nas gra jest testowana poprzez wykonywanie testów weryfikujących poprawność działania pojedynczych 
elementów (jednostek) programu – np. `metod` i `obiektów`. Testowany fragment programu poddawany jest testowi, 
który wykonuje go i porównuje wynik (np. zwrócone wartości, stan obiektu, zgłoszone wyjątki) z oczekiwanymi wynikami – 
tak pozytywnymi, jak i negatywnymi (niepowodzenie działania kodu w określonych sytuacjach również może 
podlegać testowaniu).

# Testy funkcjonalne

Służą nam do weryfikacji funkcjonalności aplikacji, czy funkcja działa zgodnie ze specyfikacją wymagań.
W testach funkcjonalnych każda `funkcja` testowana jest przez podanie wartości, określenie wyjścia i weryfikację rzeczywistego 
wyjścia z wartością oczekiwaną. Są prezentowane w celu potwierdzenia, że funkcjonalność aplikacji lub systemu 
zachowuje się zgodnie z oczekiwaniami. Odbywa się to w celu weryfikacji funkcjonalności aplikacji.

# Testy e2e

Testowanie typu `end-to-end` to technika, która testuje całe oprogramowanie od początku do końca, aby upewnić się, 
że przepływ aplikacji zachowuje się zgodnie z oczekiwaniami. Definiuje zależności systemowe produktu i zapewnia, 
że wszystkie zintegrowane elementy współpracują ze sobą zgodnie z oczekiwaniami.

Głównym celem testowania `end-to-end` (E2E) jest testowanie na podstawie doświadczenia użytkownika końcowego poprzez 
symulację rzeczywistego scenariusza użytkownika i walidację testowanego systemu i 
jego komponentów pod kątem integracji i integralności danych.