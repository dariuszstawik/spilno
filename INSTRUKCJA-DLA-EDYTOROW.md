# Jak edytować stronę „Znajdź swoje miejsce"

Cześć! Ten dokument pokazuje, jak edytować treść strony — dodawać i zmieniać miejsca przyjazne, poprawiać tytuły, modyfikować kroki ścieżki. Nie potrzebujesz znać kodu ani HTML.

## Co dostałeś

- **Adres panelu**: `twoja-strona.netlify.app/admin` *(dokładny adres dostaniesz osobno)*
- **Link aktywacyjny** w mailu od Netlify
- **Twoje konto** zostanie utworzone, gdy klikniesz w link i ustawisz hasło

## Pierwszy raz — aktywacja konta

1. Otwórz maila od Netlify z tematem „You've been invited to..."
2. Kliknij przycisk **Accept the invite**
3. W formularzu, który się otworzy, wpisz hasło, które wybierzesz (zapisz je sobie!)
4. Po kliknięciu **Sign Up** zostaniesz przekierowany na panel CMS

Od teraz logujesz się tym hasłem przez stronę `…/admin`.

## Co widzisz w panelu

Po zalogowaniu po lewej stronie masz trzy sekcje:

- 🏠 **Strona główna** — tytuły, podtytuły, nagłówek sekcji „Przyjazne miejsca"
- 📋 **Kroki ścieżki** — osiem kroków instrukcji „jak trafić do klubu"
- 📍 **Przyjazne miejsca** — lista klubów / miejsc spotkań

Klikasz w sekcję, widzisz listę wpisów (np. „Krok 1 — Wybierz klub", „Krok 2 — Poproś o pomoc"…), klikasz wpis — otwiera się formularz do edycji.

## Edycja istniejącego wpisu

Powiedzmy, że chcesz zmienić numer telefonu w klubie KAFOS:

1. W lewym menu kliknij **Przyjazne miejsca**
2. Z listy wybierz **☕ Klub Seniorów KAFOS**
3. W formularzu znajdź sekcję **Telefony** — kliknij w numer i wpisz nowy
4. Na górze okna kliknij **Save** — zmiana zapisała się jako szkic
5. Następnie kliknij **Publish** → **Publish now**
6. Po około 30-60 sekundach nowy numer pojawi się na stronie publicznej

> **Ważne**: **Save** to tylko zapis szkicu — nie pojawia się na stronie. Dopiero **Publish** wprowadza zmianę online. Jeśli zostawisz coś tylko jako Save, Twoja zmiana nie będzie widoczna.

## Dwa języki — polski i ukraiński

Każde pole tekstowe w formularzu pojawia się w dwóch wersjach: **PL** (po lewej) i **UK** (po prawej). Trzeba wypełnić obie:

```
Tytuł kroku
┌─────────────────────────┐  ┌─────────────────────────┐
│ PL                      │  │ UK                      │
│ Wybierz klub            │  │ Вибери клуб             │
└─────────────────────────┘  └─────────────────────────┘
```

Jeśli zostawisz pole UK puste — na stronie w wersji ukraińskiej pojawi się pustka. Dlatego zawsze wypełniaj obie wersje.

> **Wskazówka**: Jeśli nie znasz ukraińskiego, zapytaj kogoś z zespołu o tłumaczenie. Nie używaj automatycznego tłumacza dla tekstów wrażliwych — strona dotyczy seniorów uchodźców i błąd w tłumaczeniu może być mylący.

## Dodawanie nowego miejsca przyjaznego

To najczęstsza operacja. Krok po kroku:

1. **Przyjazne miejsca** → na górze listy kliknij **New place** (lub „+ Add Miejsce")
2. Wypełnij pola:
   - **Emoji w nagłówku karty** — pojedynczy znak emoji (np. 🏠, ☕, 🌳, 🌟). W telefonie i większości komputerów otwierasz panel emoji skrótem Win+. (Windows) lub Cmd+Ctrl+Spacja (Mac).
   - **Nazwa miejsca** — w obu językach
   - **Adres** — pełny, z dzielnicą w nawiasie. Przykład: `Katowice, ul. Mariacka 12 (Śródmieście)`
   - **Telefony** — kliknij **+ Add Numer** żeby dodać każdy numer osobno
   - **E-maile** — analogicznie. Można pominąć jeśli klub nie ma maila.
   - **Godziny** — np. `9:00 - 17:00 (pon-pt)`
   - **Odpłatność** — krótki opis na karcie, np. `zajęcia bezpłatne` lub `zajęcia częściowo odpłatne`
   - **Linki** — strony WWW i Facebook. Każdy link to:
     - **Typ**: wybierasz z listy „Strona WWW" albo „Facebook"
     - **Adres URL**: musi zaczynać się od `https://`
     - **Etykieta**: tekst, który zobaczy użytkownik (np. nazwa strony bez `https://www.`)
3. **Szczegóły** (rozwijane na karcie po kliknięciu „Zobacz więcej"):
   - **Informacje o grupie** — lista pytań w stylu „Klub jest otwarty na przyjęcie seniorów z Ukrainy: tak". Każde to osobny punkt — kliknij **+ Add Punkt** żeby dodać kolejne.
   - **Charakter spotkań** — opis typu zajęć (towarzyskie, ruchowe, edukacyjne…)
   - **Udział w zajęciach** — np. „Bezpłatny" lub „Częściowo płatny"
   - **Częstotliwość** — np. „Raz w tygodniu", „Kilka razy w miesiącu"
   - **Dostępność** — informacja o dostępności dla osób z ograniczoną mobilnością
   - **Zapisy** — czy wymagane wcześniejsze zapisy
4. Na górze: **Save**, potem **Publish**

Po publikacji nowe miejsce pojawi się jako ostatnie na liście miejsc na stronie.

## Edycja kroku ścieżki

Kroki to bardziej skomplikowane wpisy, bo mają **edytor tekstu** dla pola „Rozwinięcie" (treść po kliknięciu „Zobacz więcej").

Gdy klikniesz w treść rozwinięcia, dostaniesz pasek narzędzi z:

- **B** — pogrubienie zaznaczonego tekstu
- *I* — kursywa
- **•** — lista punktowana
- **1.** — lista numerowana
- 🔗 — wstawienie linku

To wszystko. Inne formatowania nie są dostępne — żebyś nie zepsuł przypadkowo wyglądu strony.

> **Pro tip**: Gdy wpiszesz w pasku adresu pełny URL (np. `https://przyklad.pl`), zaznaczysz go, a potem klikniesz 🔗 — możesz wpisać tekst, który będzie widoczny zamiast samego adresu.

## Zmiana kolejności miejsc

Lista miejsc na stronie ma stałą kolejność. Aby ją zmienić, trzeba edytować listę miejsc w pliku konfiguracyjnym — to robota dla osoby technicznej, daj znać administratorowi (osobie, która zaprosiła Cię do panelu).

## Czego NIE da się zmienić w panelu

Świadomie kilka rzeczy zostało zaszytych w kodzie strony:

- Wygląd (kolory, czcionki, układ)
- Loga partnerów na dole strony
- Stopka (informacje o licencji, projekcie, finansowaniu)
- Liczba kroków (jest 8, nie da się dodać 9. ani usunąć któregoś)

Jeśli któraś z tych rzeczy musi się zmienić, daj znać administratorowi.

## Co jeśli coś zepsujesz?

Spokojnie. Każda zmiana, którą publikujesz, zostaje zapisana w historii. Można ją cofnąć — administrator jednym kliknięciem przywróci poprzednią wersję. To dlatego korzystamy z tego rozwiązania zamiast np. pliku Word, gdzie pomyłka jest „na zawsze".

Jeśli widzisz, że coś nie wygląda po Twojej edycji — nie panikuj, zrób zrzut ekranu i napisz do administratora.

## Najczęstsze pytania

**Czy muszę publikować od razu po edycji?** Nie. **Save** zapisuje szkic, do którego możesz wrócić później. **Publish** wprowadza zmianę online. Możesz robić wiele Save, a potem jednym Publish wszystko opublikować.

**Po publikacji zmiana nie jest widoczna na stronie.** Spróbuj odświeżyć stronę z czyszczeniem cache (Ctrl+Shift+R na Windows, Cmd+Shift+R na Mac). Czasem przeglądarka pamięta starą wersję.

**Mogę edytować z telefonu?** Tak. Sveltia działa na komórce, ale na większym ekranie jest wygodniej. Niektóre pola (np. listy z drag-and-drop) mogą być trudniejsze do obsługi.

**Czy moje hasło widzą inni?** Nie. Hasło ustaliłeś tylko Ty, jest zaszyfrowane na serwerze Netlify. Nie widzi go nawet administrator.

**Zapomniałem hasła.** Na ekranie logowania kliknij „Forgot password?". Dostaniesz mail z linkiem do ustawienia nowego.

**Mogę dodać zdjęcie do miejsca?** Aktualnie nie — pola zdjęć nie ma w formularzu. To celowe (proste rozwiązanie, mniej kłopotów). Jeśli to istotnie potrzebne, daj znać administratorowi.

---

Powodzenia! Jak coś nie działa, napisz do osoby, która Cię zaprosiła do panelu.
