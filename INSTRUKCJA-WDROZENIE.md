# Wdrożenie CMS — instrukcja dla administratora

Ten dokument prowadzi Cię przez konfigurację panelu CMS dla strony „Znajdź swoje miejsce". Po przejściu wszystkich kroków:

- Twoi współpracownicy będą mogli edytować stronę przez panel pod adresem `twoja-strona.netlify.app/admin`
- Każda zmiana zapisuje się jako commit do repozytorium GitHub
- Strona przebudowuje się automatycznie i jest aktualna w 30-60 sekund

Cały proces zajmuje **15-25 minut**.

## Zanim zaczniesz — co musisz mieć

- [ ] Konto na GitHubie z dostępem do repozytorium z plikami strony
- [ ] Konto na Netlify, gdzie strona jest już hostowana
- [ ] Adresy e-mail współpracowników, których chcesz zaprosić do edycji

## Kontekst — co tu się dzieje

Sveltia CMS to lekki panel, który działa w przeglądarce — nie ma własnego serwera. Logowanie współpracowników i zapisywanie zmian odbywa się przez dwie usługi Netlify:

- **Netlify Identity** — system kont (e-mail + hasło) dla edytorów. Współpracownicy nie potrzebują kont GitHub.
- **Git Gateway** — pośrednik, który w imieniu zalogowanego użytkownika zapisuje zmiany do repozytorium na GitHubie.

> **Ważna uwaga**: Netlify oznaczyło Git Gateway jako technologię w trybie utrzymaniowym — naprawiają tylko błędy bezpieczeństwa, nie funkcjonalne. Działa stabilnie i nadal jest najprostszą drogą dla małych zespołów, ale gdyby kiedyś została wycofana, alternatywą jest logowanie przez GitHub OAuth (każdy współpracownik z kontem GitHub jako collaborator). Sekcja na końcu dokumentu opisuje, jak ewentualnie przemigrować.

## Krok 1 — Wrzuć pliki do repozytorium GitHub

Skopiuj zawartość paczki `sveltia-preview/` do swojego repozytorium. Struktura, którą dostałeś:

```
twoje-repo/
├── index.html              ← strona (zmieniona, czyta dane z plików)
├── admin/
│   ├── index.html          ← panel CMS (ładuje Sveltię)
│   └── config.yml          ← konfiguracja CMS (jakie pola, kolekcje)
└── content/
    ├── site/
    │   ├── header.yml
    │   └── places_section.yml
    ├── steps/
    │   ├── step-1.md
    │   ├── step-2.md
    │   └── ... (8 plików)
    └── places/
        ├── spilno.yml
        ├── kafos.yml
        └── ... (4 pliki)
```

Wrzuć przez GitHub Desktop, panel webowy, albo `git push` — jak Ci wygodnie. **Zachowaj pliki logo (logo.png, logo-pcg.png itp.) z aktualnej wersji** — one zostają w głównym folderze, niezmienione.

Po wgraniu wejdź na swoją stronę — wszystko powinno wyglądać identycznie jak wcześniej. Jeśli coś nie działa, w sekcji „Rozwiązywanie problemów" na końcu jest checklist.

## Krok 2 — Włącz Netlify Identity

1. Wejdź do panelu Netlify → wybierz swoją stronę
2. Z lewego menu: **Project configuration** → **Identity**
3. Kliknij **Enable Identity**
4. Po włączeniu zobaczysz nowe ustawienia. Przejdź do **Settings & usage** (na samym dole strony Identity)
5. W sekcji **Registration preferences** wybierz: **Invite only**
   - Dlaczego: zapobiega temu, żeby ktokolwiek z internetu mógł utworzyć konto edytora. Tylko osoby przez Ciebie zaproszone uzyskają dostęp.

## Krok 3 — Włącz Git Gateway

W tej samej sekcji Identity:

1. Przewiń do **Services**
2. Znajdź **Git Gateway** i kliknij **Enable Git Gateway**
3. Netlify automatycznie wygeneruje token dostępu do Twojego repo. Nie musisz nic kopiować ani zapisywać.

Tu mogą się pojawić różne pytania o uprawnienia, jeśli jeszcze nie autoryzowałeś Netlify do dostępu do GitHuba. Postępuj zgodnie z instrukcjami — Netlify przeprowadzi Cię przez to.

## Krok 4 — Zaproś współpracowników

W panelu Identity:

1. Kliknij **Invite users**
2. Wpisz adresy e-mail osób, które mają edytować treść (przecinki między adresami)
3. Kliknij **Send**

Każda osoba dostanie maila z linkiem aktywacyjnym. Po kliknięciu ustawi sobie hasło i będzie mogła się zalogować pod adresem `twoja-strona.netlify.app/admin`.

> **Wskazówka**: Sam też się zaproś! Twoje konto GitHub jest osobne od konta edytora — żebyś mógł testować panel jak współpracownik, potrzebujesz osobnego konta Identity.

## Krok 5 — Test

1. Wejdź na `twoja-strona.netlify.app/admin`
2. Powinieneś zobaczyć ekran logowania Sveltii. Kliknij **Login**.
3. Po zalogowaniu po lewej masz trzy sekcje: **Strona główna**, **Kroki ścieżki**, **Przyjazne miejsca**
4. Spróbuj wejść w jakiś krok, zmienić tytuł, kliknąć **Save**, potem **Publish**
5. Wróć na stronę główną (otwórz w nowej karcie) — po 30-60 sekundach zmiana powinna być widoczna

Jeśli to działa — **gratulacje, masz CMS!** Możesz wysłać współpracownikom link i krótką instrukcję (osobny dokument: `instrukcja-dla-edytorow.md`).

## Rozwiązywanie problemów

### „Your Git Gateway backend is not returning valid settings"

Najczęstsza przyczyna: Git Gateway nie został włączony albo token wygasł. Wróć do Krok 3 i kliknij **Enable Git Gateway** jeszcze raz (jeśli przycisk nadal jest dostępny) lub **Generate access token**.

### „This site requires JavaScript to function"

Pusty ekran w `/admin` z taką informacją oznacza, że skrypt Sveltii nie zdążył się załadować. Odśwież stronę. Jeśli problem się powtarza, sprawdź konsolę przeglądarki (F12) — najczęściej to chwilowy problem z CDN.

### Współpracownik dostał maila z zaproszeniem, ale link nie działa

Linki Netlify Identity wygasają po 7 dniach. W panelu Identity → Users znajdź jego adres, kliknij **Resend invitation**.

### Strona się nie aktualizuje po zapisie

Sprawdź w Netlify zakładkę **Deploys** — czy nowy deploy się rozpoczął. Jeśli nie, oznacza, że commit nie został zapisany. Najczęściej powód to brakujące uprawnienia Git Gateway — patrz pierwszy punkt.

### Edytor pokazuje pole jako puste, ale w pliku jest treść

Zwykle to problem z formatem pliku — Sveltia ścisle przestrzega struktury z `config.yml`. Jeśli ręcznie edytowałeś jakiś plik treści w GitHubie i pomyliłeś składnię, panel może go odrzucić. Wróć do edytora w GitHub, wyrównaj wcięcia, ewentualnie skopiuj strukturę z innego, działającego pliku.

## Migracja na GitHub OAuth (gdyby Git Gateway przestał działać)

W razie gdyby Netlify w pewnym momencie wycofało Git Gateway albo Twoja konfiguracja przestała działać, masz prostą drogę awaryjną:

1. Każdy współpracownik zakłada konto na GitHubie
2. Dodajesz ich jako collaborators do repo (Settings → Collaborators → Add people)
3. W pliku `admin/config.yml` zmieniasz pierwsze linie:
   ```yaml
   backend:
     name: github
     repo: nazwa-uzytkownika/nazwa-repo
     branch: main
   ```
4. Tworzysz GitHub OAuth App pod adresem `github.com/settings/applications/new` (instrukcja w dokumentacji Sveltii: https://sveltiacms.app/en/docs/backends/github)

To wymaga więcej pracy od współpracowników (każdy musi mieć konto GitHub i być dodany do repo), ale nie zależy od Netlify.

## Co dalej

Codzienna praca to już domena Twoich współpracowników — wysłałeś im link, mają instrukcję, edytują samodzielnie. Twoja rola admina to:

- **Dodawanie nowych edytorów** — Netlify panel → Identity → Invite users
- **Reagowanie na ich pytania** — najczęściej wystarcza odesłanie do `instrukcja-dla-edytorow.md`
- **Aktualizacje wyglądu strony** — kolorystyka, układ, dodawanie nowych sekcji to dalej kod, więc wracasz do niego (idealnie w nowym czacie z Claude'em z plikiem strony i opisem zmian)

Powodzenia.
