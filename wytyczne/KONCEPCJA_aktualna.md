# Koncepcja aktualna — Dual Use Hackathon (poszukiwania + AR)

Zapis rozmowy decyzyjnej i preferowanego pitchu.  
`IDEA.md` w katalogu nadrzędnym jest **nieaktualny** — nie analizować.

Źródła: `istotne_zdania.md`, `wnioski_po_spotkaniu.md`, `Opis zadnia Dual Use Hackathon.pdf`, `prezka hackathon dronowy.pdf`, rozmowa agent–autor (wrzesień 2026).

Legenda: tekst w `<…>` = uzupełnienia / propozycje agenta do akceptacji lub edycji przez autora.

---

## 1. Decyzje zamknięte (pytania → odpowiedzi autora)

### Pytanie 1 — Który wariant produktu?

**Pytanie (agent):** Który jeden użytkownik / scenariusz na slajdzie 2 — wariant A (poszukiwania policja/GOPR), B (PSP/pierwsza linia jak stary IDEA), C (granica jako pitch główny)?

**Odpowiedź (autor):** **A — poszukiwania (policja / GOPR).**

Uzupełnienie autora:

- Pilot na okularach zyskuje też to, że **nie musi** korzystać z gogli FPV i zbierać obrazu analogowego — wystarczą okulary (np. XREAL) z wpiętym po USB odbiornikiem: ten sam podgląd obrazu.
- Po znalezieniu obiektu i włączeniu np. **półautonomii** (dron podąża za celem) operator może **zminimalizować** obraz na okularach i **uczestniczyć w poszukiwaniach**, nadal widząc podgląd z kamer drona.
- **Inni** użytkownicy z okularami (bez podglądu analogowego FPV) otrzymują:
  - zdjęcia terenu poglądowe (informacja o ukształtowaniu terenu — wg mentorów przydatna),
  - minimapę szybko zmieniającego się obiektu,
  - prosty znacznik celu na ekranie.
- Cel: nie patrzeć non-stop w tablet; to są informacje, które szybko się zmieniają.

Granica / inne służby: na razie **nie** jako główny pitch (opcjonalnie „dalszy rozwój”).

### Pytanie 2 — Preferowany pitch (szkielet autora)

**Pytanie (agent):** Domknij historię *potrzeba → dron → info → działanie* jednym scenariuszem.

**Odpowiedź (autor):** Szkielet poniżej — uzupełniony w `<…>` przez agenta.

---

## 2. Preferowany pitch (uzupełniony)

### Potrzeba

W trakcie poszukiwań przez policję / GOPR, WOT i inne służby terenowe, pojawia się potrzeba częstego monitorowania przemieszczającego się obiektu. Standardowe metody umożliwiają zbieranie informacji na podręczny tablet i po ciągłym zerkaniu na niego możemy analizować zmieniającą się sytuację. Jednak ta metoda ogranicza skupienie do jednej czynności: patrzenia w tablet

### Rozwiązanie

Dlatego nasze rozwiązanie polega na wykorzystaniu okularów AR przy akcjach poszukiwawczych. Dzięki nim użytkownik mógłby jednocześnie widzieć wszystko przed sobą, a na okularach wyświetlałyby się przydatne, aktualne informacje z dronów poszukiwawczych. Niwelowałoby to potrzebę ciągłego sprawdzania tabletu z istotnymi, zwłaszcza nagłymi informacjami.

To mogłyby być m.in.:

- aktualne obrazy ukształtowania terenu wokół poszukiwanego obiektu,
- minimapa ze znacznikami ich przemieszczania,
- znacznik obiektu bezpośrednio na okularach.

<Dla **operatora** dodatkowo: podgląd FPV z drona (odbiornik USB → okulary), z możliwością minimalizacji po włączeniu półautonomicznego śledzenia — wtedy wraca do akcji pieszej. Dla **pozostałych** w grupie: bez FPV — stills + CoT/znacznik + minimapa.>

### Jak by to działało

System działałby zarówno w środowiskach z GPS, jak i bez GPS.

**Z GPS:** dron zna swoją pozycję, robi detekcję obiektu i wysyła współrzędne oraz zdjęcia poglądowe za pomocą protokołu cywilno-/wojskowego ATAK wszystkim użytkownikom systemu. Każdy może je odebrać — osoby z okularami oraz z samym tabletem.

**Bez GPS:** sama pozycja drona nie ułoży pinezki w polu widzenia ani na minimapie. Stereowizja w okularach i na dronie buduje lokalną mapę i wiąże pozycje użytkownika, drona oraz celu.

### Przykładowy scenariusz

Dwóch policjantów rozpoczyna poszukiwania; obaj mają okulary, a jeden jest operatorem drona z wpiętym do okularów odbiornikiem FPV po USB. Operator widzi otoczenie i obraz z kamer drona. A gdy ktoś zostanie znaleziony, określane jest położenie i wysyłane są zdjęcia poglądowe wszystkim. Jeśli dron jest w stanie podążać za celem, operator może aktywnie brać udział w poszukiwaniach i się przemieszczać, mając nadal podgląd z drona w czasie rzeczywistym, ale zminimalizowany. Drugi policjant bez FPV idzie po znaczniku i zdjęciach terenu, bez ciągłego zerkania w tablet.

### Koszt

- Okulary (m.in. podgląd / HUD w GPS): ok. **1500–2000 zł**.
- Ze stereowizją (lepsze GPS-denied): ok. **3000–4500 zł**
  <w notatkach ze spotkania padało też 4500–5000 zł — ujednolicić przed prezentacją>.

### Co dalej (domknięcie pitchu — propozycja)

<**Wartość dla użytkownika:** szybsza reakcja na ruch celu, mniej head-down, operator nie jest „wyłączony” z akcji po znalezieniu obiektu; grupa dzieli ten sam obraz sytuacji przez ATAK.

**Rola drona (nie konstrukcja):** latający sensor + źródło pozycji/kadrów; półautonomiczne śledzenie = *założenie / istniejąca zdolność platformy*, nie przedmiot projektu. Wkład zespołu: proces od danych misji → przefiltrowana info w okularach → działanie.

**Innowacyjność vs mapa/stream/tablet:** nie kolejny live-stream do oglądania, lecz przestrzenny znacznik + stills terenu + filtr „tu i teraz” w polu widzenia; vs ciężkie suite’y typu Anduril — lżejszy stos (okulary + telefon/compute + ATAK), świadomie bez pełnego COP w oku.

**Dual-use (defensywne):** poszukiwania osób zaginionych, wsparcie służb cywilnych i bezpieczeństwa publicznego; bez uzbrojenia / ofensywy / inwigilacji bez podstawy prawnej.

**Ograniczenia i ryzyka:** canopy/las może utrudnić follow (wtedy ręczne prowadzenie / inna procedura — poza naszym sednem); clutter AR; latencja i świeżość pinezki; zaufanie do detekcji; GPS-denied droższy; przepustowość ATAK → stills zamiast ciągłego video dla grupy; prawo i retencja wizerunku.

**Mini-demo na hackathon:** makieta POV okularów (znacznik + minimapa + still) + schemat przepływu ATAK + scenariusz „2 policjantów” przed/po; bez obiecywania działającego follow w lesie.

**Dalszy rozwój:** stereo/GPS-denied, więcej użytkowników w grupie, opcjonalnie transfer dual-use (np. ochrona granicy) dopiero po domknięciu case’u poszukiwań.>

---

## 3. Mapowanie na kryteria oceny (prezka)

| Kryterium | Jak ten pitch odpowiada |
| --- | --- |
| Użyteczność operacyjna | Realny ból: tablet head-down + operator wyłączony z akcji przy poszukiwaniach |
| Rola technologii dronowych | Dane: pozycja, detekcja, kadry terenu, (opcjonalnie) follow jako założenie platformy |
| Innowacyjność | Nakładka decyzyjna w AR + stills dla grupy, nie sam stream/mapa |
| Realność | ATAK + okulary konsumenckie + USB FPV; koszty podane; stereo = faza 2 |
| Prezentacja | Jedna historia: 2 policjantów, potrzeba → info → działanie |

---

## 4. Otwarte kwestie (jeszcze do przemyślenia)

- Jednoznaczna nazwa klienta na slajdzie 2: **policja** czy **GOPR** (albo „służby poszukiwawcze, case: policja”).
- Ujednolicenie widełek cen stereo (3000–4500 vs 4500–5000).
- Czy półautonoma follow jest na slajdzie „rozwiązanie”, czy tylko „założenie platformy / ryzyko lasu”.
- Treść mini-demo (statyczna makieta vs krótki film POV).
- Jedno zdanie różnicy vs Anduril na Q&A.
- Polityka prywatności / retencja zdjęć osób (slajd ryzyka).

---

## 5. Historia plików

| Plik | Status |
| --- | --- |
| `../IDEA.md` | Nieaktualny — nie analizować |
| `KONCEPCJA_aktualna.md` (ten plik) | Aktualny zapis decyzji i pitchu |
| `wnioski_po_spotkaniu.md` | Brudnopis mentorów |
| `istotne_zdania.md` | Cytaty z opisu zadania |
