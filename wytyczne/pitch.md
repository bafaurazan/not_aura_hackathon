## [NOT] AURA

Dzień dobry wszystkim, jestem Rafał. Mój zespół thenotaura skupiał się na stworzeniu systemu wspierającego decyzje w akcjach poszukiwawczych z wykorzystaniem okularów AR i danych zbieranych z dronów.

## Jaki jest problem?
W trakcie poszukiwań przez policję / GOPR, WOT i inne służby terenowe, pojawia się potrzeba częstego monitorowania przemieszczającego się obiektu. Standardowe metody umożliwiają zbieranie informacji na podręczny tablet i po ciągłym zerkaniu na niego możemy analizować zmieniającą się sytuację. Jednak ta metoda ogranicza skupienie do jednej czynności: patrzenia w tablet

## Rozwiązanie
Dlatego nasze rozwiązanie polega na wykorzystaniu okularów AR przy akcjach poszukiwawczych. Dzięki nim użytkownik mógłby jednocześnie widzieć wszystko przed sobą, a na okularach wyświetlałyby się przydatne, aktualne informacje z dronów poszukiwawczych. Niwelowałoby to potrzebę ciągłego sprawdzania tabletu z istotnymi, zwłaszcza nagłymi informacjami.

To mogłyby być m.in.:

- aktualne obrazy ukształtowania terenu wokół poszukiwanego obiektu,
- minimapa ze znacznikami ich przemieszczania,
- znacznik obiektu bezpośrednio na okularach.

## Jak by to działało

System działałby zarówno w środowiskach z GPS, jak i bez GPS.

**Z GPS:** dron zna swoją pozycję, robi detekcję obiektu i wysyła współrzędne oraz zdjęcia poglądowe za pomocą protokołu cywilno-/wojskowego ATAK wszystkim użytkownikom systemu. Każdy może je odebrać — osoby z okularami oraz z samym tabletem.

**Bez GPS:** sama pozycja drona nie ułoży pinezki w polu widzenia ani na minimapie. Ale stereowizja w okularach i na dronie powiązałaby pozycje użytkownika, drona oraz celu.

## Przykładowy scenariusz

Dwóch policjantów rozpoczyna poszukiwania; obaj mają okulary, a jeden jest operatorem drona z wpiętym do okularów odbiornikiem FPV po USB. Operator widzi otoczenie i obraz z kamer drona. A gdy ktoś zostanie znaleziony, określane jest położenie i wysyłane są zdjęcia poglądowe wszystkim. Jeśli dron jest w stanie podążać za celem, operator może aktywnie brać udział w poszukiwaniach i się przemieszczać, mając nadal podgląd z drona w czasie rzeczywistym, ale zminimalizowany. Drugi policjant bez FPV idzie po znaczniku i zdjęciach terenu, bez ciągłego zerkania w tablet.

## Koszt

- Okulary umożliwiające podgląd i HUD z GPS: ok. **1500–2000 zł**.
- Ze stereowizją w środowiskach bez gps): ok. **3000–4500 zł**

## podsumowując

nasz system umożliwia szybką reakcje na ruch celu. użytkownik nie musi tracić skupienia spoglądając na tablet

dron tu pełni role latającego źródła pozycji. najwięcej zyskuje w połączeniu z systemami autonomicznych rojów dronów, bo umożliwiłby podgląd poruszania się wielu obiektów.

## to demonstracja jak wygląda projekt

POV drugiego policjanta (bez FPV): znacznik + minimapa + zdjęcie z drona.

![HUD POV](hud-pov-policjant-demo.jpg)

## to nasz zespół
<tu zdjęcie zespołu>