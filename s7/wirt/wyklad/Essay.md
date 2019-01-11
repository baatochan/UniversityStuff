# Wirtualizacja sieci i systemów komputerowych

## Modele wirtualizacji - cechy i zastosowania

#### Bartosz Rodziewicz (226105)

### Wirtualizacja ogółem

Wirtualizacja to zbiorcze określenie technik i technologii umożliwiających uruchamianie oprogramowania w różnych wirtualnych kontekstach architekturalnych, sprzętowych i systemowych na tym samym urządzeniu pod kontrolą tego samego systemu operacyjnego, a także korzystanie z zasobów obliczeniowych, pamięciowych, sieciowych i blokowych oraz systemów plików tak, jakby były one zbudowane i skonfigurowanie w inny sposób, niż faktycznie. W tym opracowaniu skupiono się na wirtualizacji oprogramowania oraz platform sprzętowych.

**Do głównych celów i korzyści wirtualizacji należą:**

* wykorzystanie zalet pracy z wieloma komputerami bez inwestycji w dodatkowy sprzęt;
* zwiększenie bezpieczeństwa przez izolację środowisk uruchomieniowych różnego oprogramowania lub różnych instancji tego samego oprogramowania;
* efektywne dzielenie fizycznych zasobów sprzętowych pomiędzy wielu użytkowników;
* uruchamianie oprogramowania przeznaczonego na różne platformy na jednym urządzeniu;

### Pełna wirtualizacja

Pełna wirtualizacja zapewnia emulację funkcjonowania kompletnej platformy sprzętowej, zwanej maszyną wirtualną, na której można uruchomić dowolny kompatybilny system operacyjny i inne oprogramowanie. Uruchamiane oprogramowanie nie musi być przystosowane do pracy w maszynie wirtualnej, ani mieć 'świadomości' pracy w takowej. Instrukcje wykonywane na wirtualizowanym procesorze oraz adresy pamięci tłumaczone są przez _hypervisor_ na instrukcje i adresy właściwe dla fizycznego komputera zarządzającego maszyną wirtualną.

* Wszystkie elementy typowego komputera lub innego programowalnego urządzenia elektronicznego są wirtualizowane: procesor(y), pamięć operacyjna, magistrale, urządzenia peryferyjne, przechowywanie danych, łączność sieciowa, itp., wraz z pełnym systemem operacyjnym lub programem startowym.
* Dla oprogramowania uruchamianego w maszynie wirtualnej, rożnice względem uruchamiania na fizycznym urządzeniu są znikome i nie wymagają specjalnego przygotowania oprogramowania do pracy pod kontrolą _hypervisora_.

### Parawirtualizacja

W przypadku parawirtualizacji niektóre funkcje maszyny wirtualnej są oddelegowane do bezpośredniej realizacji przez _hypervisor_ w kontekście fizycznego komputera. Służy to zwiększeniu wydajności maszyny wirtualnej przez ograniczenie czasu spędzanego przez nią na wykonywaniu zadań, które zdecydowanie trudniej wykonać w wirtualnym kontekście.

* Zasadniczo wirtualizowane są wszystkie elementy typowego komputera, jednak część z nich nie jest dostarczana w formie całkowitej emulacji funkcjonalności fizycznych odpowiedników, lecz w formie programowej abstrakcji, umożliwiającej _hypervisorowi_ bezpośrednie i optymalne wykonanie tych samych zadań, zamiast tłumaczenia poszczególnych kroków ich wykonywania pomiędzy maszyną wirtualną a fizycznym sprzętem.
* System operacyjny musi wspierać środowisko parawirtualizowane, w którym jest uruchamiany, wykorzystując udostępnianą przez _hypervisor_ abstrakcję programową, zamiast niskopoziomowych instrukcji sprzętowych. Z tego względu zwykły, nieprzygotowany do tego system operacyjny nie może zostać uruchomiony w parawirtualizacji.

#### Zastosowania

* Podział dużych zasobów obliczeniowych pomiędzy wiele zadań, systemów operacyjnych i użytkowników
* Izolacja środowisk oprogramowania w celu zapewnienia większej niezawodności oraz bezpieczeństwa (jeśli w jednej maszynie wirtualnej wystąpi krytyczny problem, a _hypervisor_ jest dobrze skonstruowany, to pozostałe maszyny wirtualne oraz fizyczny komputer pozostaną nienaruszone)
* Uruchamianie oprogramowania przeznaczonego na różne platformy
* Testowanie oprogramowania w wielu środowiskach sprzętowo-systemowych
* Emulacja infrastruktury sieciowej bez inwestycji w fizyczne urządzenia sieciowe

### Konteneryzacja

Konteneryzacja, inaczej wirtualizacja na poziomie systemu operacyjnego, to technika, w której pojedynczy kernel systemu operacyjnego obsługuje wiele odizolowanych instancji przestrzeni użytkownika. Każda z tych instancji ma do dyspozycji ten sam współdzielony kernel, ale oddzielne systemy plików oraz zestawy dostępnych urządzeń, wątków procesora itp. W ten sposób, programy uruchamiane w każdym z tak przygotowanych 'kontenerów' pracują pod kontrolą tego samego systemu operacyjnego, ale z ograniczonym dostępem do różnych, izolowanych zasobów.

* Niski koszt wydajnościowy
* Oprogramowanie pracujące w kontenerze nie wymaga specjalnego przygotowania do tego celu; z jego punktu widzenia środowiskiem uruchomieniowym jest typowy, pełnoprawny komputer i system operacyjny.
* Nie jest konieczna emulacja kompletnej platformy sprzętowej.

<div class="page-break"></div>

### Wirtualizacja aplikacji

W ramach wirtualizacji aplikacji, w wirtualnym środowisku umieszczany jest tylko jedna aplikacja użytkownika, której dostęp do zasobów systemu jest emulowany i/lub izolowany od pozostałych programów działających na danym komputerze. Jest to podejście podobne do konteneryzacji, jednak zamiast tworzenia wielu instancji przestrzeni użytkownika, dostęp pojedynczej aplikacji do zasobów systemu jest w różnym stopniu emulowany przez warstwę pośredniczącą, często będącą tzw. piaskownicą (_sandbox_), uniemożliwiającą wpływ aplikacji na stan oprogramowania, danych i sprzętu poza nią.

* Wirtualizacja aplikacji wykorzystuje jeden współdzielony kernel systemu operacyjnego, lecz aplikacje uruchamiane w ten sposób mogą postrzegać go jako zupełnie inny, niż faktycznie. Przykładowo, program Wine umożliwia uruchamianie aplikacji stworzonych dla systemów rodziny Microsoft Windows na systemach rodziny Linux, poprzez emulację funkcjonowania interfejsów i bibliotek udostępnianych przez systemy Windows.

#### Zastosowania

* Oddzielenie oprogramowania od fizycznych zasobów komputera w celu zwiększenia bezpieczeństwa i niezawodności
* Testowanie oprogramowania z użyciem różnych konfiguracji oraz kontekstów systemowych
* Uruchamianie aplikacji z użyciem różnych zestawów programów, bibliotek i konfiguracji w celu uzyskania wymaganego środowiska uruchomieniowego bez modyfikacji bazowej instalacji ystemu i oprogramowania
* Uruchamianie wielu instancji jednej aplikacji z użyciem jednej konfiguracji w celu zapewnienia redundancji i większej przepustowości danych
* Uruchamianie aplikacji przeznaczonych na inne systemy operacyjne

### Wirtualizacja przestrzeni roboczej

Wirtualizacja przestrzeni roboczej umożliwia umiesczenie w wirtualnym środowisku uruchomieniowym zestawu aplikacji, które tworzą kompletne środowisko pracy na poziomie użytkownika, i które mogą ze sobą współpracować w ramach zwirtualizowanej przestrzeni.

* Na zwirtualizowaną przestrzeń roboczą składają się wszelkie aplikacje, dane i ustawienia użytkownika, oraz niektóre podsystemy systemu operacyjnego niewymagające uprawnień administratorskich, pozwalające stworzyć kompletne środowisko pracy dla użytkownika.
* Oprogramowanie przestrzeni roboczej uruchamiane jest na komputerze użytkownika i ma szybki dostęp do lokalnych zasobów sprzętowych.

### Wirtualizacja środowiska graficznego

Wirtualizacja środowiska graficznego odpowiada za uruchomienie kompletnego środowiska graficznego ("pulpitu") do użycia na komputerze użytkownika. Zwirtualizowane środowisko może pracować w maszynie wirtualnej lub na zupełnie innym komputerze w sieci. Umożliwia to dostęp do tego samego środowiska pracy z wielu komputerów, na przykład wielu stacji roboczych w firmie, lub komputerów należących do użytkownika w wielu miejscach na świecie.

* Zwiększa wygodę pracy poprzez odseparowanie fizycznego urządzenia od używanego za jego pomocą środowiska pracy, co pozwala częściowo wyeliminować przywiązanie użytkownika do jednego urządzenia oraz konieczność ciągłej synchronizacji danych.
* Umożliwia podniesienie bezpieczeństwa, gdyż na urządzeniu końcowym nie są przechowywane żadne wrażliwe dane, zatem jego utrata nie wiąże się bezpośrednio z utratą ani niepowołanym dostępem do danych.
* Potencjalnie wymaga dużej przepustowości łącz sieciowych, która nie zawsze jest dostępna.

#### Zastosowania

* Ułatwienie dystrybucji kompletnego środowiska pracy dla użytkownika
* Udostępnienie użytkownikowi dużych zasobów obliczeniowych i pamięciowych za pośrednictwem urządzenia lub wielu urządzeń o niewielkich zasobach (tzw. _thin client_)
* Centralizacja środowiska pracy w celu zwiększenia jego elastyczności względem wykorzystania różnych urządzeń końcowych w różnych miejscach
* Ułatwienie kontroli dostępu do wrażliwych danych oraz minimalizacja szansy ich kradzieży bądź utraty

### Bibliografia

[ dostęp 23. grudnia 2018 ]
1. _Virtualization_ (Wikipedia) (https://en.wikipedia.org/wiki/Virtualization)
1. _Wirtualizacja_ (Wikipedia) (https://pl.wikipedia.org/wiki/Wirtualizacja)
1. _Hardware virtualization_ (Wikipedia) (https://en.wikipedia.org/wiki/Hardware_virtualization)
1. _Application virtualization_ (Wikipedia) (https://en.wikipedia.org/wiki/Application_virtualization)
1. _Workspace virtualization_ (Wikipedia) (https://en.wikipedia.org/wiki/Workspace_virtualization)
1. _Desktop virtualization_ (Wikipedia) (https://en.wikipedia.org/wiki/Desktop_virtualization)
1. _Operating-system-level virtualization_ (Wikipedia) (https://en.wikipedia.org/wiki/Operating-system-level_virtualization)
1. _Paravirtualization_ (Wikipedia) (https://en.wikipedia.org/wiki/Paravirtualization)
1. _Full virtualization_ (Wikipedia) (https://en.wikipedia.org/wiki/Full_virtualization)
1. _Docker (software)_ (Wikipedia) (https://en.wikipedia.org/wiki/Docker_(software))
