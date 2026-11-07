Epik 1: Wyszukiwanie i filtrowanie ofert noclegowych

Główny obszar odpowiedzialny za interakcję użytkownika z kryteriami wyszukiwania oraz prezentację dostępnych pokoi z podziałem na dopasowania.
Historyjka 1.1: Wyszukiwanie dostępnych pokoi

    Tytuł: Wyszukiwanie pobytu na podstawie miasta, dat i liczby osób

    Format: Jako klient, chcę wyszukać dostępne pokoje podając miasto, daty pobytu, liczbę osób oraz liczbę pokoi, aby znaleźć ofertę dopasowaną do moich planów podróży.

    Priorytet: Wysoki (High)

    Szacowanie: 5 SP

    Kryteria Akceptacji:

        Użytkownik nie może wybrać daty zameldowania (check-in) wcześniejszej niż dzisiejsza, a data wymeldowania (check-out) musi być ustawiona na co najmniej następny dzień.

        Pole liczby pokoi posiada walidację uniemożliwiającą wpisanie wartości mniejszej niż 1 (błąd lub automatyczna korekta przy próbie wpisania 0 lub wartości ujemnych).

        Po kliknięciu „Szukaj pokoi” system odpytuje lokalny serwer (/rooms) i wyświetla listę pokoi spełniających kryteria lub komunikat o braku ofert.

    Zadania techniczne / Podzadania:

        Implementacja logiki kalendarza w JS (dynamiczne ustawianie właściwości min dla daty wyjazdu).

        Stworzenie asynchronicznej funkcji fetch filtrującej dane pokoi po mieście, pojemności i dostępności (availableRooms).

        Osoba odpowiedzialna: Frontend Developer.

Historyjka 1.2: Prezentacja wyników z podziałem na kategorie pokoi

    Tytuł: Wyświetlanie wyników z podziałem na dokładne dopasowania i większe pokoje

    Format: Jako klient, chcę widzieć wyniki wyszukiwania podzielone na dokładne dopasowanie oraz dostępne większe pokoje, aby łatwiej wybrać optymalną ofertę.

    Priorytet: Średni (Medium)

    Szacowanie: 3 SP

    Kryteria Akceptacji:

        Wyniki wyszukiwania są podzielone na dwie wyraźne sekcje: „Dokładnie dopasowane pokoje” oraz „Dostępne większe pokoje”.

        Każda karta pokoju zawiera nazwę hotelu, nazwę pokoju, maksymalną liczbę osób, liczbę wolnych pokoi oraz cenę za noc.

        Kliknięcie przycisku „Wybierz” przy wybranej karcie ukrywa sekcję wyników i płynnie przenosi użytkownika do formularza danych gościa.

Epik 2: Zarządzanie procesem rezerwacji i formularzem gościa

Obszar obejmujący wprowadzanie danych osobowych, dynamiczne wyliczanie kosztów, walidację poprawności oraz ostateczne potwierdzenie i zapis rezerwacji.
Historyjka 2.1: Podgląd wybranego obiektu i ceny w kroku danych gościa

    Tytuł: Dynamiczne wyliczanie i prezentacja całkowitego kosztu pobytu

    Format: Jako klient, chcę widzieć podsumowanie wybranego pokoju oraz automatycznie wyliczoną sumę do zapłaty za wszystkie noce w formularzu danych gościa, aby kontrolować koszty przed podsumowaniem.

    Priorytet: Wysoki (High)

    Szacowanie: 3 SP

    Kryteria Akceptacji:

        Po przejściu do kroku 3 w nagłówku formularza wyświetla się nazwa wybranego hotelu, pokoju oraz cena za dobę.

        System automatycznie oblicza liczbę nocy na podstawie wybranych dat oraz mnoży ją przez cenę i liczbę pokoi.

        Kwota całkowita jest dynamicznie prezentowana w sekcji danych gościa w PLN.

Historyjka 2.2: Walidacja danych osobowych i kontaktowych gościa

    Tytuł: Walidacja poprawności pól formularza danych gościa

    Format: Jako klient, chcę, aby formularz weryfikował poprawność wpisywanych przeze mnie danych osobowych i kontaktowych, aby uniknąć błędów w rezerwacji.

    Priorytet: Wysoki (High)

    Szacowanie: 5 SP

    Kryteria Akceptacji:

        Pola imienia, drugiego imienia i nazwiska posiadają reguły walidacji (szablony pattern) akceptujące wyłącznie litery alfabetu polskiego (w tym znaki diakrytyczne).

        Pole numeru telefonu wymaga wprowadzenia dokładnie 9 cyfr, a pole e-mail wymaga poprawkowego formatu adresu pocztowego.

        Próba kliknięcia przycisku „Przejdź do podsumowania” przy błędnych lub pustych danych uruchamia wbudowaną walidację przeglądarki (.checkValidity()) i blokuje przejście dalej.

    Zadania techniczne / Podzadania:

        Konfiguracja atrybutów pattern, required oraz maxlength w polach HTML.

        Obsługa zdarzenia kliknięcia z walidacją .checkValidity() w pliku skryptu JS.

        Osoba odpowiedzialna: Frontend Developer / QA.

Historyjka 2.3: Podsumowanie rezerwacji i ostateczne potwierdzenie wysłania

    Tytuł: Ekran podsumowania i zatwierdzenie rezerwacji (POST do API)

    Format: Jako klient, chcę zobaczyć pełne podsumowanie rezerwacji i zatwierdzić jej wysłanie, aby mieć pewność, że rezerwacja została poprawnie zapisana w systemie.

    Priorytet: Wysoki (High)

    Szacowanie: 3 SP

    Kryteria Akceptacji:

        Ekran podsumowania prezentuje kompletny zestaw informacji: miejsce, miasto, pokój, liczbę pokoi i gości, termin, liczbę nocy, dane kontaktowe oraz ostateczną cenę całkowitą bez zbędnych ikonek.

        Użytkownik ma możliwość powrotu do edycji danych przyciskiem „Wróć / Edytuj” lub ostatecznego zatwierdzenia przyciskiem „Tak, jestem pewien i wysyłam”.

        Po potwierdzeniu dane są wysyłane metodą POST do endpointu http://localhost:3000/reservations, po czym wyświetla się komunikat o sukcesie z ID rezerwacji i następuje odświeżenie strony.
