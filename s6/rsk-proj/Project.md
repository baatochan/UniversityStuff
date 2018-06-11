# Rozległe sieci komputerowe
## Projekt

Uczestnicy | Prowadzący | Termin zajęć
-----------|------------|-------------
Iwo Bujkiewicz (226203)<br />Bartosz Rodziewicz (226105) | Prof. dr hab. inż. Andrzej Kasprzak | Poniedziałek 13:15

### Założenia projektowe

W zakres prac projektowych wchodziło zaprojektowanie sieci rozległej pomiędzy centralą i innymi oddziałami firmy funkcjonującej na terenie województw dolnośląskiego i opolskiego.

Projekt zakłada następujące lokalizacje oddziałów firmy:

* Opole (centrala)
* Wrocław
* Kędzierzyn-Koźle
* Prudnik
* Świdnica
* Wałbrzych

Wszystkie oddziały firmy czynne są codziennie w godzinach 09:00-18:00. W tym czasie każdego dnia między każdymi dwoma oddziałami przesyłane jest 10 MB danych, z każdego oddziału do centrali 51.5 MB, a z centrali do każdego oddziału 20 MB. Poza tymi godzinami, każdego dnia między każdymi dwoma oddziałami przesyłane jest 10.8 MB danych, a z każdego oddziału do centrali 55 MB. Klienci firmy każdego dnia generują łącznie 3 GB ruchu sieciowego przychodzącego i wychodzącego z centrali.

Do transmisji danych pomiędzy oddziałami oraz na zewnątrz firmy wykorzystywane są linie transmisyjne Orange.

### Ogólny opis koncepcji rozwiązania

Model struktury teleinformatycznej firmy jest hierarchiczny (podzielony na centralę - będącą jednocześnie oddziałem - i pozostałe oddziały). Uwzględniając występującą w sieci komunikację pomiędzy poszczególnymi oddziałami, a także ich położenie geograficzne, za najlepszy wybór uznano konstrukcję sieci w topologii pierścienia.

Sieć budowana jest z użyciem połączeń MetroEthernet firmy Orange, zgodnie z wymaganiami klienta.

Celem podniesienia niezawodności sieci zastosowane są:
* redundancja sprzętu - zapasowe routery w oddziałach, replikujące konfigurację aktywnie używanych routerów;
* odpowiedni dobór topologii sieci - zapewniający, w przypadku awarii w jednym z oddziałów, połączenie między wszystkimi pozostałymi;
* możliwość rozbudowy sieci o kolejne połączenia;
* dobór urządzeń sieciowych produkowanych przez firmy z wieloletnią renomą.

Jedną z cech prawidłowo zaprojektowanej sieci jest uwzględnienie potencjalnej przyszłej rozbudowy. Z tego powodu wykorzystane w projekcie routery posiadają dodatkowe, wolne porty, a jako tymczasowe rozwiązanie w przypadku szerzej zakrojonej rozbudowy można zastosować aktywne użycie routerów zapasowych, zakupionych na wypadek awarii (nie jest to jednak rozwiązanie wskazane, sugeruje się zakup nowych routerów).

Każdy oddział ma zapewnione bezpośrednie przyłącze do sieci Internet.

### Dobór struktury sieci
#### Topologia sieci

![Map](img/project_map.png)

Wykorzystywane są połączenia MetroEthernet typu LINK, za pomocą których komunikują się ze sobą następujące pary oddziałów firmy:

* Opole - Kędzierzyn-Koźle (42 km)
* Kędzierzyn-Koźle - Prudnik (46 km)
* Prudnik - Wałbrzych (105 km)
* Wałbrzych - Świdnica (15 km)
* Świdnica - Wrocław (49 km)
* Wrocław - Opole (79 km)

Redundancja połączeń między każdymi dwoma oddziałami jest ustanowiona dzięki połączeniu w topologii pierścienia.

#### Analiza niezawodnościowa

Niezawodne działanie sieci jest bardzo istotne dla sprawnego funkcjonowania firmy.

Na niezawodność sieci wpływa wiele czynników, takich, jak:
* niezawodność urządzeń sieciowych,
* topologia sieci,
* niezawodność łącz telekomunikacyjnych zewnętrznego dostawcy,
* możliwość transmisji danych poprzez sieć Internet.

Pierwszy z wymienionych czynników niezawodności, czyli awaryjność sprzętu, jest minimalizowany przez zakup nadmiarowych routerów do wszystkich oddziałów. Dzięki takiemu rozwiązaniu, nawet w przypadku awarii urządzenia sieciowego, istnieje możliwość natychmiastowego przywrócenia sprawności węzła.

Drugim sposobem na zminimalizowanie prawdopodobieństwa awarii sprzętowej jest zakup urządzeń firmy o uznanej marce i dużym doświadczeniu w dostarczaniu tego typu rozwiązań. W ramach projektu wybrano urządzenia firmy Juniper Networks, które nie tylko spełniają wymagania projektowanej sieci pod względem funkcjonalności, ale także cieszą się znakomitą renomą na rynku IT.

Konstrukcja sieci w technologii pierścienia zapewnia niską podatność sieci na awarię w pojedynczym oddziale, bądź na jednym odcinku sieci, ze względu na obecność dwóch tras pomiędzy każdymi dwoma węzłami. Jeszcze wyższą niezawodność może potencjalnie zapewnić możliwość rozbudowy sieci o dodatkowe połączenia. Pierwsze sugerowane takie połączenie to bezpośrednie łącze Opole - Wałbrzych. Nie zostało ono jednak uwzględnione w podstawowej wersji projektu.

Usługa MetroEthernet firmy Orange zawiera SLA, co oznacza formalną gwarancję wysokiej jakości usług operatora - wysokiej dostępności usługi, krótkiego czasu usunięcia awarii oraz ograniczenia przerw w działaniu usługi.

Ostatnim filarem niezawodności sieci jest podłączenie każdego z oddziałów do sieci Internet. Pozwala to na utrzymanie funkcjonowania komunikacji pomiędzy odległymi lokalizacjami firmy - za pomocą szyfrowanych tuneli - nawet w wypadku awarii wielu z wymienionych wyżej elementów.

#### Reguła doboru tras

Ze względu na nieskomplikowaną konstrukcję sieci, zdecydowano o wykorzystaniu statycznych reguł doboru tras.

Porty routerów w poszczególnych węzłach zostały przypisane następująco:

Węzeł początkowy | Węzeł docelowy | Numer portu w węźle początkowym
---|---|---
Opole | Kędzierzyn-Koźle | 0/1/0
Opole | Wrocław | 0/1/1
Opole | ISP | 0/1/2
Wrocław | Opole | 0/1/0
Wrocław | Świdnica | 0/1/1
Wrocław | ISP | 0/1/2
Świdnica | Wrocław | 0/1/0
Świdnica | Wałbrzych | 0/1/1
Świdnica | ISP | 0/1/2
Wałbrzych | Świdnica | 0/1/0
Wałbrzych | Prudnik | 0/1/1
Wałbrzych | ISP | 0/1/2
Prudnik | Wałbrzych | 0/1/0
Prudnik | Kędzierzyn-Koźle | 0/1/1
Prudnik | ISP | 0/1/2
Kędzierzyn-Koźle | Prudnik | 0/1/0
Kędzierzyn-Koźle | Opole | 0/1/1
Kędzierzyn-Koźle | ISP | 0/1/2

Wpis "ISP" oznacza połączenie do sieci Internet. Każdy oddział posiada światłowodowe połączenie internetowe dostarczane przez Orange. Centrala ma zapewnioną prędkość pobierania i wysyłania danych na poziomie odpowiednio 300 Mb/s i 30 Mb/s, a każdy z pozostałych oddziałów na poziomie 100 Mb/s i 10 Mb/s.

W każdym z węzłów tworzona jest statyczna tablica routingu, w której, przez odpowiednie ustawienie statycznego kosztu, ustala się trasy podstawowe i alternatywne. Szeroki zakres metryki tras pozwala na łatwą ewentualną rozbudowę sieci o kolejne węzły,1 bez konieczności całkowitej redefinicji tablic routingu. Tablice tworzone są w taki sposób, aby trasy o mniejszej liczbie przeskoków między węzłami były wybierane w pierwszej kolejności.

#### Wyznaczanie średniego opóźnienia pakietu

Średnie opóźnienie pakietu obliczono zgodnie z metodą zdefiniowaną w [1].

Obliczanie opóźnienia rozpoczęło się od zdefiniowania parametrów opisujących połączenie, takich jak:

* przepustowość użytego kanału,
* rozmiar przesyłanych pakietów,
* ilość danych przesyłanych pomiędzy węzłami.

Większość par oddziałów łączy się ze sobą za pośrednictwem innych oddziałów. Należało obliczyć, jaka ilość danych przepływa poprzez poszczególne węzły.

Ilość danych wysyłanych pomiędzy dwoma oddziałami to 10 MB w obie strony, z centrali do oddziału 20 MB, a z oddziału do centrali 51.5 MB.

Dla każdego kanału transmisyjnego ilość codziennie przesyłanych danych definiuje wzór:

`P = X * (51.5 MB + 20 MB) + Y * 10 MB`, gdzie
* `P` to ilość danych,
* `X` to ilość oddziałów łączących się po tym odcinku z centralą,
* `Y` to ilość par oddziałów łączących się ze sobą po tym odcinku.

Mając ten wzór oraz dane dotyczące topologii sieci i tablic routingu można wyznaczyć `X` i `Y` dla każdego odcinka, a następnie wyznaczyć ilość danych. Na jej podstawie szacowana jest przepływność kanału, przy założeniu, że takie dane są przesyłane w sposób zbliżony do ciągłego w godzinach pracy firmy (9 godzin dziennie). Pakietów wysyłanych poza godzinami pracy nie uwzględniono w obliczeniach, ponieważ tworzą one niższe wartości przepływowości kanałów.

Połączenie | `X` | `Y` | Przesyłane dane [MB] | Przepływowość [kb/s]
---|---|---|---|---
Opole - Wrocław | 3 | 5 | 264.5 | 66.88
Wrocław - Świdnica | 2 | 4 | 183.0 | 46.27
Świdnica - Wałbrzych | 1 | 5 | 121.5 | 30.72
Wałbrzych - Prudnik | 0 | 4 | 40.0 | 10.11
Prudnik - Kędzierzyn-Koźle | 1 | 5 | 121.5 | 30.72
Kędzierzyn-Koźle - Opole | 2 | 4 | 183.0 | 46.27

Wyliczona przepływowość kanałów pokazuje, że teoretycznie dopuszczalny byłby wybór łącz przepustowości 128 kb/s i 64 kb/s. Jednakże, z uwagi na komfort użytkowania, jak i nieustanny rozwój firm i technologii, zaleca się wybór kanałów o przepustowości przynajmniej 10 Mb/s.

<div class="page-break"></div>

Średnie opóźnienie pakietu obliczono ze wzoru:

![Wzór](img/project_equation1.png =420x)

Parametr `γ` obliczono, sumując przepływności kanałów i dzieląc je przez rozmiar pakietu. Za średni rozmiar pakietu przyjęto 1518 B, podążając za zaleceniami firmy Orange. Po wykonaniu obliczeń parametr `γ` wynosi 155.81 pakietów na sekundę.

Pozostałe parametry są znane, więc korzystając z arkusza kalkulacyjnego można obliczyć `T`, które wynosi 0.1 ms, co jest nieporównywalnie krótszym czasem, niż wymagane przez klienta maksymalne 700 ms. Dodatkowe opóźnienie wprowadzą urządzenia sieciowe; jest ono szacowane na kilka dodatkowych milisekund.

Uwzględniając tylko opóźnienie w przesyle pakietów, można było bez przeszkód wybrać kanały o niższej przepustowości, co można wziąć pod uwagę, gdyby nastąpiła konieczność redukcji kosztów.

### Adresacja w sieci
##### Opole - Kędzierzyn-Koźle

Adres CIDR IPv4 | Przeznaczenie
---|---
176.16.0.0/30 | Sieć
176.16.0.1/30 | Opole: 0/1/0
176.16.0.2/30 | Kędzierzyn-Koźle: 0/1/1
176.16.0.3/30 | Broadcast

##### Kędzierzyn-Koźle - Prudnik

Adres CIDR IPv4 | Przeznaczenie
---|---
176.16.0.4/30 | Sieć
176.16.0.5/30 | Kędzierzyn-Koźle: 0/1/0
176.16.0.6/30 | Prudnik: 0/1/1
176.16.0.7/30 | Broadcast

<div class="page-break"></div>

##### Prudnik - Wałbrzych

Adres CIDR IPv4 | Przeznaczenie
---|---
176.16.0.8/30 | Sieć
176.16.0.9/30 | Prudnik: 0/1/0
176.16.0.10/30 | Wałbrzych: 0/1/1
176.16.0.11/30 | Broadcast

##### Wałbrzych - Świdnica

Adres CIDR IPv4 | Przeznaczenie
---|---
176.16.0.12/30 | Sieć
176.16.0.13/30 | Wałbrzych: 0/1/0
176.16.0.14/30 | Świdnica: 0/1/1
176.16.0.15/30 | Broadcast

##### Świdnica - Wrocław

Adres CIDR IPv4 | Przeznaczenie
---|---
176.16.0.16/30 | Sieć
176.16.0.17/30 | Świdnica: 0/1/0
176.16.0.18/30 | Wrocław: 0/1/1
176.16.0.19/30 | Broadcast

##### Wrocław - Opole

Adres CIDR IPv4 | Przeznaczenie
---|---
176.16.0.20/30 | Sieć
176.16.0.21/30 | Wrocław: 0/1/0
176.16.0.22/30 | Opole: 0/1/1
176.16.0.23/30 | Broadcast

<div class="page-break"></div>

### Wykaz urządzeń

Oddział | Rodzaj | Urządzenie | Ilość
---|---|---|---
Opole | Router | Juniper ACX1100-AC | 2
Wrocław | Router | Juniper ACX1100-AC | 2
Świdnica | Router | Juniper ACX1100-AC | 2
Wałbrzych | Router | Juniper ACX1100-AC | 2
Prudnik | Router | Juniper ACX1100-AC | 2
Kędzierzyn-Koźle | Router | Juniper ACX1100-AC | 2

### Literatura

1. Kasprzak, A., 1999. _Rozległe sieci komputerowe z komutacją pakietów_ (Oficyna Wydawnicza Politechniki Wrocławskiej, 1999)

1. Juniper Networks, 2018. _ACX Series Universal Metro Routers_ (https://www.juniper.net/assets/us/en/local/pdf/datasheets/1000397-en.pdf)

1. Orange Polska, 2017. _Regulamin usługi Miejski Ethernet_ (http://www.orange.pl/ocp-http/PL/Binary2/1993810/4083323399.pdf)
