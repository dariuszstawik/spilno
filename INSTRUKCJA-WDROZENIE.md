# Wdrożenie CMS — instrukcja dla administratora

Ten dokument prowadzi Cię przez konfigurację panelu CMS dla strony „Znajdź swoje miejsce". Po przejściu wszystkich kroków:

- Twoi współpracownicy będą mogli edytować stronę przez panel pod adresem `twoja-strona.netlify.app/admin`
- Logowanie odbywa się przez konto GitHub (każdy edytor potrzebuje konta GitHub i dostępu do repo)
- Każda zmiana zapisuje się jako commit do repozytorium GitHub
- Strona przebudowuje się automatycznie i jest aktualna w 30-60 sekund

Cały proces zajmuje **20-30 minut**.

## Zanim zaczniesz — co musisz mieć

- [ ] Konto na GitHubie z dostępem do repozytorium z plikami strony
- [ ] Konto na Netlify, gdzie strona jest już hostowana
- [ ] Adresy GitHub współpracowników, których chcesz zaprosić do edycji (każdy musi już mieć konto GitHub — jeśli jeszcze nie ma, niech się zarejestruje na github.com)

## Kontekst — dlaczego tak

Sveltia CMS to lekki panel działający w przeglądarce — nie ma własnego serwera. Logowanie i zapis zmian odbywa się przez:

- **GitHub OAuth** — każdy edytor loguje się swoim kontem GitHub
- **Netlify jako pośrednik OAuth** — Netlify obsługuje wymianę tokenów między Sveltią a GitHubem, dzięki czemu nie musisz stawiać własnego serwera autoryzacyjnego

To podejście jest oficjalnie wspierane przez Sveltię. Wcześniejsza alternatywa (Netlify Identity + Git Gateway) została wycofana zarówno przez Sveltię jak i Netlify w 2025-2026.

## Krok 1 — Wrzuć pliki do repozytorium GitHub

Skopiuj zawartość paczki `sveltia-preview/` do swojego repozytorium. Struktura:

```
twoje-repo/
├── index.html              ← strona (czyta dane z plików)
├── admin/
│   ├── index.html          ← panel CMS (ładuje Sveltię)
│   └── config.yml          ← konfiguracja CMS
└── content/
    ├── site/               (nagłówek + tytuł sekcji miejsc)
    ├── steps/              (8 kroków ścieżki)
    └── places/             (4 miejsca przyjazne)
```

> **WAŻNE — zanim wgrasz `admin/config.yml`**: otwórz go i podmień wartość `repo:` na rzeczywistą nazwę Twojego repozytorium.
>
> ```yaml
> backend:
>   name: github
>   repo: TWOJ-UZYTKOWNIK/TWOJE-REPO   # ← zmień na np. mostkatowice/mapa-wsparcia
>   branch: main
> ```
>
> Format: `użytkownik/nazwa-repozytorium`. Jeśli repo jest w organizacji (np. mostkatowice), podaj nazwę organizacji zamiast użytkownika.

**Zachowaj pliki logo (logo.png, logo-pcg.png itp.) z aktualnej wersji** — one zostają w głównym folderze, niezmienione.

Po wgraniu wejdź na swoją stronę publiczną — wszystko powinno wyglądać identycznie jak wcześniej (panel `/admin` jeszcze nie zadziała, ale strona główna tak).

## Krok 2 — Zarejestruj GitHub OAuth Application

To jest serce konfiguracji. Robisz to raz, na samym początku.

1. Wejdź na GitHub i kliknij swoją ikonkę → **Settings** → **Developer settings** → **OAuth Apps**
   (skrót: <https://github.com/settings/developers>)
2. Kliknij **Register a new application**
3. Wypełnij formularz:
   - **Application name**: dowolna nazwa, którą rozpoznasz, np. `Mapa Wsparcia CMS`
   - **Homepage URL**: adres Twojej strony, np. `https://mapawsparcia.netlify.app`
   - **Authorization callback URL**: dokładnie `https://api.netlify.com/auth/done`
     (to ważne — Netlify będzie obsługiwał wymianę tokenów)
   - Pole **Application description** możesz zostawić puste
4. Kliknij **Register application**
5. Na stronie aplikacji:
   - **Skopiuj Client ID** — będzie potrzebny za chwilę
   - Kliknij **Generate a new client secret** → **Skopiuj Client Secret** od razu, bo zniknie po zamknięciu strony

**Trzymaj te dwie wartości pod ręką** — w następnym kroku wkleisz je do Netlify.

## Krok 3 — Połącz GitHub OAuth z Netlify

1. Wejdź do panelu Netlify → wybierz swoją stronę
2. Z menu po lewej: **Project configuration** → **Access & security** → **OAuth**
3. W sekcji **Authentication Providers** kliknij **Install Provider**
4. Wybierz **GitHub**
5. Wklej **Client ID** i **Client Secret** z poprzedniego kroku
6. Kliknij **Install**

To wszystko. Netlify będzie teraz obsługiwał logowanie współpracowników do panelu CMS.

## Krok 4 — Dodaj współpracowników jako collaborators do repo

Każdy edytor musi mieć **uprawnienia zapisu** do repozytorium na GitHubie, żeby Sveltia mogła w jego imieniu wprowadzać zmiany.

1. Na GitHubie wejdź do repozytorium ze stroną
2. **Settings** → **Collaborators**
3. Kliknij **Add people**
4. Wpisz nazwę użytkownika GitHub współpracownika i kliknij **Add**

GitHub wyśle mu zaproszenie mailem. Współpracownik klika link → akceptuje → ma dostęp do repo.

## Krok 5 — Test

1. Wejdź na `twoja-strona.netlify.app/admin`
2. Powinieneś zobaczyć logo Sveltii i przycisk **Sign in with GitHub**
3. Kliknij — wyskoczy okno autoryzacji GitHub
4. Zatwierdź dostęp aplikacji do repo
5. Po zalogowaniu po lewej masz trzy sekcje: **Strona główna**, **Kroki ścieżki**, **Przyjazne miejsca**
6. Spróbuj wejść w jakieś miejsce, zmienić godziny otwarcia, kliknąć **Save** → **Publish**
7. Wróć na stronę główną (otwórz w nowej karcie) — po 30-60 sekundach zmiana powinna być widoczna

Jeśli to działa — **gratulacje, masz CMS!**

## Rozwiązywanie problemów

### „There is an error in the CMS configuration"

- Sprawdź `admin/config.yml` — czy `repo:` zawiera poprawną wartość `użytkownik/repozytorium` (a nie placeholder `TWOJ-UZYTKOWNIK/TWOJE-REPO`)
- Sprawdź czy plik `config.yml` jest faktycznie pod adresem `twoja-strona.netlify.app/admin/config.yml` (otwórz tę URL bezpośrednio — powinien się pobrać tekst YAML)

### „This site requires JavaScript to function" lub pusty ekran

Skrypt Sveltii nie zdążył się załadować. Odśwież stronę. Jeśli problem się powtarza, sprawdź konsolę przeglądarki (F12) — najczęściej to chwilowy problem z CDN.

### Po kliknięciu „Sign in with GitHub" wyskakuje błąd autoryzacji

- Sprawdź, że **Authorization callback URL** w GitHub OAuth App to dokładnie `https://api.netlify.com/auth/done` — częsta literówka to `https://app.netlify.com/...`
- Sprawdź, że Client ID i Client Secret w Netlify zgadzają się z tymi w GitHubie
- Jeśli zmieniałeś Secret w GitHubie po wklejeniu do Netlify — zaktualizuj go też w Netlify

### Logowanie działa, ale nie widzę kolekcji albo Sveltia mówi że plik nie istnieje

- Sprawdź, że folder `content/` ze wszystkimi plikami treści jest faktycznie w Twoim repo na GitHubie (nie tylko lokalnie)
- Sprawdź `branch:` w `admin/config.yml` — domyślnie `main`, ale jeśli Twoje repo używa `master`, zmień

### Współpracownik widzi „You don't have access to this repository"

Jego konto GitHub nie zostało jeszcze dodane jako collaborator albo nie zaakceptował zaproszenia mailem. Wróć do Kroku 4.

### Strona się nie aktualizuje po zapisie zmian w panelu

Sprawdź w Netlify zakładkę **Deploys** — czy nowy deploy się rozpoczął. Jeśli nie, oznacza, że commit nie został zapisany przez Sveltię. Sprawdź historię commitów w GitHubie — czy zmiana faktycznie się tam pojawiła. Jeśli nie pojawiła się, problem jest po stronie Sveltii — sprawdź konsolę przeglądarki w trakcie zapisu.

## Co dalej

Codzienna praca to już domena Twoich współpracowników — dasz im link do panelu, dasz instrukcję (`INSTRUKCJA-DLA-EDYTOROW.md`) i edytują samodzielnie. Twoja rola admina to:

- **Dodawanie nowych edytorów** — Settings → Collaborators na GitHubie
- **Reagowanie na ich pytania** — najczęściej wystarcza odesłanie do `INSTRUKCJA-DLA-EDYTOROW.md`
- **Aktualizacje wyglądu strony** — kolory, układ, dodawanie nowych sekcji to dalej kod, więc wracasz do niego

## Zabezpieczenie tokenów GitHub OAuth

**Client Secret** wygenerowany w Kroku 2 to tajny ciąg, który daje pełną kontrolę nad logowaniem do Twojego CMS-a. Nigdy go nie commituj do repo, nie wklejaj do dokumentów ani publicznych miejsc — siedzi już bezpiecznie w panelu Netlify, więcej nigdzie nie powinien być potrzebny. Jeśli kiedyś go zgubisz albo ktoś zobaczy — w GitHub OAuth App po prostu wygeneruj nowy i zaktualizuj w Netlify.

Powodzenia.
