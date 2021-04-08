# Lokalne sieci komputerowe
## Sprawozdanie z laboratorium

Data | Tytuł zajęć | Uczestnicy
:-: | :-: | :-:
24.03.2021 9:15 | Wi-Fi | Bartosz Rodziewicz (226105)

### Zapoznanie się z funkcjami zintegrowanych routerów bezprzewodowych
#### Wyszukasz w Internecie trzy różne routery bezprzewodowe dowolnego standardu i stworzysz listę ważnych funkcji tego routera, zapisując je w przykładowej tabeli

| Marka/Model | Cena | Obsługujący IPv6 | Ochrona komunikacji bezprzewodowej | Pasmo | Inne funkcje |
| --- | --- | --- | --- | --- | --- |
| TP-Link TL-WR940N | 89.00 | tak | 64/128-bit WEP, WPA Enterprise, WPA2 Enterprise, WPA-PSK, WPA2-PSK | 2.4GHz | 3T3R MIMO, WPS, automatyczne wybieranie kanałów Wi-Fi |
| ASUS RT-N66U | 449.00 | tak | 64/128-bit WEP, WPA Enterprise, WPA2 Enterprise, WPA-PSK, WPA2-PSK | 2.4GHz / 5GHz | 3T3R MIMO, WPS, automatyczne wybieranie kanałów Wi-Fi, 2.4GHz / 5GHz DualBand, Beamforming, 2 porty USB (udostępnianie zasobów dyskowych, pobieranie plików na zasoby dyskowe, wsparcie modemów sieci komórkowej), osobna sieć dla gości, wsparcie IPTV, DualWAN |
| Securifi Almond | 329.00 | nie | 64/128-bit WEP, WPA-PSK, WPA2-PSK | 2.4GHz | 2T2R MIMO, WPS, automatyczne wybieranie kanałów Wi-Fi, wbudowany ekran dotykowy, obsługa przez Amazon Alexa |

#### Wyszukasz w Internecie po jednym routerze bezprzewodowym dla wymienionych powyżej standardów i stworzysz listę ważnych funkcji tego routera w tabeli

| Marka/Model | Standard | Cena | Obsługujący IPv6 | Ochrona komunikacji bezprzewodowej | Pasmo | Inne funkcje |
| --- | --- | --- | --- | --- | --- | --- |
| ASUS RT-N66U | 802.11n | 449.00 | tak | 64/128-bit WEP, WPA Enterprise, WPA2 Enterprise, WPA-PSK, WPA2-PSK | 2.4GHz / 5GHz | 3T3R MIMO, WPS, automatyczne wybieranie kanałów Wi-Fi, 2.4GHz / 5GHz DualBand, Beamforming, 2 porty USB (udostępnianie zasobów dyskowych, pobieranie plików na zasoby dyskowe, wsparcie modemów sieci komórkowej), osobna sieć dla gości, wsparcie IPTV, DualWAN |
| ASUS ROG GT-AC5300 | 802.11ac | 1449.00 | tak | 64/128-bit WEP, WPA Enterprise, WPA2 Enterprise, WPA-PSK, WPA2-PSK | 2.4GHz / 5GHz | MU-MIMO, WPS, automatyczne wybieranie kanałów Wi-Fi, 2.4GHz / 2x5GHz TriBand, Beamforming, 2 porty USB (udostępnianie zasobów dyskowych, pobieranie plików na zasoby dyskowe, wsparcie modemów sieci komórkowej), osobna sieć dla gości, priorytetyzacja ruchu gier, 8 portów Gbit, Link aggregation 802.3ad  |
| ASUS RT-AX56U | 802.11ax | 549.00 | tak | 64/128-bit WEP, WPA Enterprise, WPA2 Enterprise, WPA-PSK, WPA2-PSK | 2.4GHz / 5GHz | MU-MIMO, WPS, automatyczne wybieranie kanałów Wi-Fi, 2.4GHz / 5GHz DualBand, Beamforming, 2 porty USB (udostępnianie zasobów dyskowych, pobieranie plików na zasoby dyskowe, wsparcie modemów sieci komórkowej), osobna sieć dla gości |

#### Który router bezprzewodowy wybrałbyś dla sieci w swoim domu? Wyjaśnij swój wybór.

Ciężko powiedzieć który, do żadnego z nich nie jestem w pełni przekonany. Router, który byłby idealny dla mnie to router, który posiada:
* przynajmniej 6 portów 1Gbit Eth, ponieważ trzon mojej sieci nadal stanowią połączenia kablowe,
* wysoką wydajność, ponieważ posiadam przyłącze światłowodowe 1000/100Mbit i często wykorzystuje sieć w pełni (duża ilość urządzeń, setki osobnych sesji, częste duże transfery),
* wsparcie najnowszego standardu WiFi (802.11ax, MU-MIMO, Beamforming), aby mieć jak najlepsze osiągi mimo połączenia bezprzewodowego wielu urządzeń,
* przyjemny interfejs WEB z wieloma funkcjami i opcjami konfiguracji,
* Dual Band wraz z Band Steering, aby wykorzystywać możliwości pasma 5GHz wciąż oferując pasmo 2.4GHz dla urządzeń które 5GHz nie wspierają
* osobna sieć dla gości niezapewniająca dostępu do zasobów LAN

Najbliższym tym wymaganiom jest ASUS RT-AX56U.

### Zapoznanie się z funkcjami punktów dostępu
####  Stwórz specyfikacje techniczną dotyczącą dwóch punktów AP, zapisując je w tabeli

| Model | Zabezpieczenia | Pasmo | Inne funkcje/Komentarz |
| --- | --- | --- | --- |
| Ubiquiti UAP AC PRO | 64/128-bit WEP, WPA, WPA2 | 2.4GHz / 5GHz | MU-MIMO, Band Steering, automatyczne wybieranie kanałów Wi-Fi |
| Edimax CAX1800 | 64/128-bit WEP, WPA, WPA2, WPA3 | 2.4GHz / 5GHz | MU-MIMO, Beamforming |

#### Wskazać różnice dla ruterów bezprzewodowych i punktów AP

AP i router pełnią bardzo odmienne rolę, a dokładniej, bycie AP to tylko jedna z wielu roli typowego domowego routera. Sam AP to tylko i wyłącznie hub sieciowy, który umożliwia przyłączenie do istniejącej już sieci klientów bezprzewodowych. Router poza tym zajmuje się routingiem, przydzielaniem adresów (serwer DHCP), obsługą połączenia WAN (NAT), serwery multimediów, zasobów, czy drukarek, itd. Router jest trzon, który tworzy sieć, AP to tylko punkt dostępowy rozszerzający istniejącą sieć o sieć bezprzewodową. Z uwagi na to, że większość routerów, oferuje funkcjonalność AP w sobie, najczęstszym zastosowaniem AP aktualnie jest Range Extender, który zwiększa pokrycie sieci Wi-Fi.

#### Jakie funkcje routerów bezprzewodowych lub punktów AP mają istotne znaczenie dla twojej sieci? Dlaczego?
* duża ilość portów eth, ponieważ trzon mojej sieci nadal stanowią połączenia kablowe,
* wysoka wydajność, ponieważ posiadam przyłącze światłowodowe 1000/100Mbit i często wykorzystuje sieć w pełni (duża ilość urządzeń, setki osobnych sesji, częste duże transfery),
* wsparcie najnowszego standardu WiFi (802.11ax, MU-MIMO, Beamforming), aby mieć jak najlepsze osiągi mimo połączenia bezprzewodowego wielu urządzeń,
* przyjemny interfejs WEB z wieloma funkcjami i opcjami konfiguracji,
* Dual Band wraz z Band Steering, aby wykorzystywać możliwości pasma 5GHz wciąż oferując pasmo 2.4GHz dla urządzeń które 5GHz nie wspierają
* osobna sieć dla gości niezapewniająca dostępu do zasobów LAN

### Dodatkowe pytania:
#### Jakie są skutki wyłączenie opcji broadcast SSID?
Sieć najczęściej przestaje być widoczna dla klientów, a do połączenia wymagane jest podanie poprawnej nazwy sieci.

#### Które z zabezpieczeń stosowanych we współczesnych sieciach Wi-Fi jest najbezpieczniejsze?
Szyfrowanie, ponieważ nie dość, że dostęp do sieci wymaga hasła, to również każdy pakiet komunikacji bezprzewodowej jest szyfrowany. Z dostępnych metod szyfrowania najbezpieczniejsze jest WPA2, które oferuje szyfrowanie AES. WPA3 jest w trakcie rozwoju.

#### Które z zabezpieczeń stosowanych w sieciach Wi-Fi jest wystarczające dla zdefiniowanego zastosowania?
Najlepszym zabezpieczeniem dostępnym w sieciach bezprzewodowych jest WPA2. Wykorzystuje on szyfrowanie AES i oferuje wersje dla użytkowników prywatnych, jak i biznesowych.

#### Wytłumaczyć dlaczego obserwowane rzeczywiste prędkości transmisji różnią się od danych podanych w standardzie Wi-Fi?
Prędkości zdefiniowane w standardzie to prędkości szczytowe, które są niemożliwe do osiągnięcia w realnych warunkach. To prędkości, które urządzenia sieciowe powinny obsługiwać, ale które nigdy się nie wydarzą z powodu zakłóceń, czy wielu urządzeń podłączonych do jednej sieci.

#### Czy zwiększanie liczby stacji w sieci bezprzewodowej ma wpływ na szybkość transmisji?
Ilość AP jednej sieci działającej na podobnym terenie ma wpływ na szybkość połączenia, ponieważ sieci nachodzą na siebie i wzajemnie się zakłócają. Zwiększenie ilości klientów również powoduje spadek wydajności sieci z powodu zakłóceń oraz obciążeń urządzenia dostępowego.

#### Ile oddzielnych podsieci określonego standardu (odpowiedzieć dla dwu standardów), może działać na tym samym terenie?
Standard g działający na paśmie 2.4GHz, gdzie sieci pracowały na 20MHz kanałach pozwalał na pracę 3 sieci bez wzajemnych interferencji. Kolejne standardy wprowadzały obsługę pasm 40, 80, a nawet 160MHz, które zajmują stopniowo więcej pasma. Oczywiście sieci mogą na siebie nachodzić, jednak będzie to powodowało spadek jakości połączenia bezprzewodowego.
