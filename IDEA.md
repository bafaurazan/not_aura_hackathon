> **NIEAKTUALNY — NIE ANALIZOWAĆ.**  
> Ten plik jest historyczny / zastąpiony. Aktualny kierunek koncepcji, pytania
> decyzyjne i preferowany pitch: `wytyczne/KONCEPCJA_aktualna.md`.  
> Nie używaj poniższej treści do oceny, prezentacji ani dalszego rozwijania
> projektu bez świadomej decyzji o przywróceniu starego wariantu.

# IDEA — ResQ-Sight / AR Crisis HUD

Koncepcja projektu na Dual Use Hackathon: systemowe wykorzystanie technologii
dronowych dual-use w zarządzaniu kryzysowym.

Źródła wytycznych: `wytyczne/Opis zadnia Dual Use Hackathon.pdf`,
`wytyczne/Baza danych publicznych.pdf`, `wytyczne/prezka hackathon dronowy.pdf`.
Oparcie merytoryczne: research inżynierski w `notaura_ws/docs/notaura_thesis/documents/company/`.

---

## 1. Jednym zdaniem

Dron (lub rój) pozyskuje i lokalizuje zagrożenia w terenie; system przetwarza te
dane w czasie rzeczywistym i rzutuje je jako nakładkę AR (HUD) w okularach
ratownika lub funkcjonariusza — tak, by wiedział **gdzie iść, czego unikać i co
zrobić dalej**, bez spoglądania w tablet przy brzuchu.

---

## 2. Problem operacyjny

W akcji kryzysowej (pożar, zawalenie, powódź, poszukiwania, obiekt bez GPS)
decyzje muszą zapadać pod presją czasu, przy ograniczonej widoczności i
rozproszonych źródłach informacji.

Obecne rozwiązania są niewystarczające, bo:

1. **Surowy stream z drona** trafia do operatora przy ekranie, a nie do osoby
   działającej w terenie. Informacja ginie w łańcuchu radio → werbalny opis →
   interpretacja w głowie ratownika.
2. **Tablet z ATAK / mapą** przy brzuchu wymusza postawę *head-down*: ręce
   zajęte, wzrok oderwany od otoczenia, utrata świadomości sytuacyjnej w
   krytycznej chwili.
3. **Kolega ma rację częściowo:** pełny strumień ATAK (logistyka, statusy
   jednostek, warstwy planistyczne, historia zdarzeń) **nie musi** być ciągle
   w polu widzenia. To są dane *na żądanie* albo dla sztabu. Ale istnieje
   klasa danych **tu-i-teraz**, których brak w HUD bezpośrednio zwiększa ryzyko
   — właśnie te chcemy wyświetlać.

Kluczowe pytanie wyzwania: *jak z danych z drona zrobić użyteczną informację
dla właściwej osoby, by szybciej i lepiej zareagowała?*

---

## 3. Użytkownik

- **Pierwsza linia:** ratownik PSP/OSP, funkcjonariusz, żołnierz WOT / patrol
  ochrony infrastruktury — osoba wchodząca w strefę zero.
- **Wtórnie:** KDR / sztab (tablet, COP) — pełniejszy obraz; okulary pierwszej
  linii dostają tylko warstwę krytyczną.

---

## 4. Rola technologii dronowych

Dron **nie jest celem projektu** (nie projektujemy konstrukcji). Jest
**latającym sensorem i źródłem danych**:

| Co robi dron | Co z tego wynika dla systemu |
| --- | --- |
| Kamera RGB / termowizja | Detekcja ludzi, ognia, pojazdów, źródeł ciepła |
| Pozycja własna (GNSS lub lokalny układ GPS-denied) | Georeferencja detekcji w przestrzeni 3D |
| Relacja przestrzenna dron ↔ operator (VIO / outside-in / tf) | Rzutowanie zagrożeń w układ oczu noszącego okulary |
| Ciągłość misji (rój / rotacja) | Brak „czarnych dziur” w napływie świeżych danych |

Dodatkowo (opcjonalne rozszerzenia UX, nie sedno architektury):

- miniatura podglądu z kamery drona (PiP) w rogu HUD — na komendę głosową,
- komendy głosowe hands-free (Whisper / RAI): *„pokaż poszkodowanych”*,
  *„podgląd z drona”*, *„ukryj warstwy”*.

---

## 5. Rozwiązanie systemowe — od danych do decyzji

```text
Potrzeba operacyjna
    → misja drona (sensor w powietrzu / w obiekcie)
    → pozyskanie danych (obraz + pozycja + detekcje)
    → przetworzenie (AI: kto/co; georeferencja: gdzie)
    → fuzja pomocnicza z danymi publicznymi (NMT, BDOT10k, IMGW — gdy pomaga)
    → filtr „tu i teraz” (tylko warstwa krytyczna dla pierwszej linii)
    → HUD w okularach AR / ATAK CoT jako nośnik
    → decyzja i działanie w terenie
```

**Innowacja względem „zwykłego streamu / mapy”:**  
informacja nie jest raportem do oglądania — jest **przestrzenną nakładką w
świecie rzeczywistym** („wallhack” taktyczny: znacznik 3D za dymem / ścianą /
regałem, wektor dojścia, alert odległości).

W GPS-denied: patrząc okularami na drona (lub mając wspólną mapę lokalną
outside-in), system nadal zna relację operator ↔ dron ↔ obiekt → lokalizacja
detekcji pozostaje poprawna w układzie oczu użytkownika.

---

## 6. Jakie dane są krytyczne „tu i teraz” (na HUD ciągle / prawie ciągle)

Kolega miał rację: **nie wlewamy całego ATAK-a do okularów**.  
Do HUD wpuszczamy tylko dane, które zmieniają **natychmiastowe zachowanie**
pierwszej linii. Reszta zostaje na tablecie / w sztabie.

### Warstwa A — zawsze w polu (lub jednym gestem / głosem)

| Dane | Skąd | Po co „tu i teraz” |
| --- | --- | --- |
| **Pozycja i typ zagrożenia / celu** (człowiek, ogień, wyciek, pojazd) | Detekcja AI z kamery/IR drona + georeferencja | Wiesz *co* i *gdzie* jest — nawet za przeszkodą / w dymie |
| **Odległość i kierunek względny** do znacznika | Transformacja 3D (dron → mapa → oczy) | Decyzja ruchu bez liczenia w głowie |
| **Alert strefy niebezpiecznej** (promień, temperatura, zalanie) | Detekcja + progi + ewentualnie NMT/IMGW | Unikanie wejścia w strefę śmierci |
| **Wektor bezpiecznego podejścia / ucieczki** | Fuzja detekcji + BDOT10k / lokalna mapa | Gdzie iść *teraz*, nie „ogólnie na mapie” |
| **Status „świeżości” danych** (wiek detekcji w sekundach) | Timestamp z misji drona | Stare pinezki kłamią — musi być widać, że dane są aktualne |

### Warstwa B — na żądanie (głos / przycisk), nie ciągły clutter

| Dane | Skąd | Kiedy |
| --- | --- | --- |
| PiP / podgląd obrazu z konkretnego drona | Stream kamery | „Chcę zobaczyć to, co widzi sensor” |
| Identyfikator jednostki / krótkie ID CoT | ATAK | Koordynacja z kolegą |
| Mini-mapa top-down | Mapa + pozycje | Orientacja globalna na 2–3 s |
| Pełna warstwa BDOT / adresy / logistyka | Geoportal / ATAK | Planowanie, nie sprint w dymie |

### Warstwa C — nie na HUD pierwszej linii (tablet / sztab)

- pełna historia zdarzeń, raporty, statusy baterii całej floty, kolejki zadań,
  dokumenty, długie listy kontaktów, warstwy planistyczne długoterminowe.

**Zasada filtracji:**  
*Jeśli informacja nie zmienia ruchu, unikania zagrożenia albo priorytetu
ratowania w najbliższych 30–60 sekundach — nie zasługuje na stałe miejsce w
HUD.*

---

## 7. Fuzja z danymi publicznymi (gdy wzmacnia decyzję)

Zgodnie z `Baza danych publicznych.pdf` — dane pomocnicze, nie zastępujące
drona:

- **NMT / LiDAR (GUGiK):** gdzie woda / dym / fala pójdzie dalej; ukryte spadki
  terenu.
- **BDOT10k:** które drogi/korytarze są odcięte vs dostępne.
- **IMGW:** trend przyboru wody, radar opadów — kontekst dla alertów.
- **CEMS / Sentinel:** szerszy obraz klęski dla sztabu (raczej COP niż HUD).

Na HUD pierwszej linii z tej fuzji trafia tylko **wynik** (np. „droga X zalana —
objazd Y”), nie surowa warstwa GIS.

---

## 8. Dual-use (bezpieczne, defensywne ramy)

- Zastosowanie: ratownictwo, ochrona ludności, świadomość sytuacyjna,
  ochrona infrastruktury, wsparcie służb.
- Poza zakresem: uzbrojenie, targeting ofensywny, jamming, hijacking, obchodzenie
  zabezpieczeń, nieuzasadniona inwigilacja.
- Privacy by Design: przetwarzanie lokalne / edge; w HUD tylko to, co potrzebne
  do akcji; bez ciągłego streamu biometrii do chmury.

---

## 9. Co pokazać na hackathonie (mini-demonstracja)

1. Schemat przepływu: dron → detekcja → georeferencja → filtr „tu i teraz” → HUD.
2. Makieta POV okularów: znaczniki 3D + dystans + opcjonalny PiP + komenda głosowa.
3. Jedna scena case study (np. zadymiony obiekt / powódź): przed (tablet + radio)
   vs po (HUD z danymi z drona).
4. Krótka lista ryzyk: clutter AR, latencja, zaufanie do AI, synchronizacja
   GPS-denied, zmęczenie wzroku.

---

## 10. Kryteria oceny — jak ta idea je pokrywa

| Kryterium (prezka) | Odpowiedź projektu |
| --- | --- |
| Użyteczność operacyjna | Hands-free świadomość sytuacyjna pierwszej linii |
| Rola technologii dronowych | Dron = sensor + pozycja detekcji; nie konstrukcja |
| Innowacyjność | Nie kolejny stream — przestrzenna nakładka decyzyjna |
| Realność | Buduje się na ATAK/CoT + AR + research HRI/outside-in |
| Prezentacja | Jasny użytkownik, łańcuch danych→decyzja, demo POV |

---

## 11. Nazwa robocza

**ResQ-Sight** (alternatywnie: *Crisis HUD*, *ATAK-AR First Line*).

Hasło: *Dron widzi. System rozumie. Ty działasz — bez odrywania wzroku od terenu.*
