# Sprawozdanie z praktyki studenckiej w formie pracy zawodowej
## Politechnika Wrocławska

Imię i nazwisko studenta| Nr indeksu	| Okres odbywania praktyki
:----------------------:|:-------------:|:-------------------------:
Bartosz Rodziewicz		| 226105		| 01.07.2019 - 30.09.2019

### Wstęp

Praktykę studencką odbywałem w formie zatrudnienia na podstawie umowy zlecenia w firmie _Nokia Solutions & Networks_ na stanowisku _5G R&D Engineer Working Student_. Praktyka rozpoczęła się w dniu 1 lipca 2019, a zakończyła dnia 30 września 2019 (trzy pełne miesiące).

Zadania realizowane w trakcie odbywania się praktyki:
1. szkolenie BHP;
1. szkolenie z zachowania poufności danych firmowych;
1. zapoznanie się ze strukturą i organizacją pracy w firmie;
1. przygotowanie swojego stanowiska pracy i komputera zgodnie z wytycznymi;
1. zapoznania się z metodologią pracy oraz technikami tworzenia oprogramowania stosowanymi przez firmę;
1. dołączenie do zespołu roboczego i rozwój umiejętności pracy w zespole;
1. uczestnictwo w regularnych spotkaniach zespołu, w celu omówienia postępów w realizacji pracy oraz przydzielenia nowych zadań;
1. praca programistyczna w ramach projektu realizowanego przez firmę, z użyciem wyspecjalizowanych narzędzi do rozwoju oprogramowania;
1. omawianie efektów pracy w formie dyskusji podczas spotkań zespołu z przełożonym;
1. udział w wewnątrz firmowych szkoleniach, aby lepiej zrozumieć projekt.

### Wprowadzenie organizacyjne

Szkolenie BHP i szkolenie z zachowania poufności danych firmowych odbyło się pierwszego dnia pracy. Drugiego dnia odbyło się wprowadzenie do organizacji pracy w firmie, gdzie mój bezpośredni przełożony (line manager) przedstawił mi hierarchię osób w firmie, zasady współpracy pomiędzy członkami zespołów i między zespołami, a także przedstawił mnie zespołowi roboczemu, do którego później dołączyłem.

W ciągu następnych kilku dni przygotowałem swoje stanowisko pracy, poprzez instalacje systemu operacyjnego i wymaganego oprogramowania oraz uzyskanie dostępu do niezbędnych narzędzi. Nastąpiło też wtedy wdrożenie w metodologie pracy w firmie. Przedstawiono mi proces rozwoju produktu i metody kontroli jakości z wykorzystaniem narzędzi do inspekcji kodu, ciągłej integracji oraz kontroli wersji. Przedstawiono także tok śledzenia zadań do realizacji i postępów prac poszczególnych zespołów z wykorzystaniem tablic kanban. Poznałem również wykorzystywane w firmie narzędzia do skutecznej komunikacji pomiędzy zespołami, jak również pomiędzy osobnymi placówkami firmy.

### Zadania

Przypisany zostałem do zespołu odpowiadającego za rozwój nadajnika sieci komórkowej w technologii 5G, dokładniej za komponent odpowiadający za warstwę użytkownika (uplane), czyli przesyłanie pakietów z danymi pomiędzy końcowym użytkownikiem (UE - user equipment), a siecią szkieletową (core network) operatora. Projekt, do którego zostałem przypisany, praktycznie w całości jest napisany w języku C++14.

Z uwagi na podpisaną umowę poufności (NDA) nie mogę przedstawić szczegółów moich zadań. Większość z nich polegała na ulepszeniu jakości kodu (refactor), usunięciu nieużywanych elementów kodu (dead code) i wprowadzeniu lepszych rozwiązań do istniejących funkcjonalności (improvements).

### Tok pracy i jej monitorowanie

Większość zespołów w firmie pracuje w strukturze scrumowej, do takiego też zespołu zostałem przypisany.

<div class="page-break"></div>

Zadania dla poszczególnych członków teamu są przydzielane podczas codwutygodniowych spotkań z przełożonym (product owner), w trakcie, których omawiane są efekty pracy w poprzednim sprincie, jak i rozdzielane taski na kolejny. Dodatkowo codziennie na kilkunastominutowych spotkaniach z liderem zespołu (tzw. daily) omawiane są postępy w realizacji zadań.

Z uwagi na krótki staż w pracy nie uczestniczyłem aktywnie w spotkaniach, na których przygotowywane były zadania do wykonania. Obecność na niektórych z nich pozwoliła mi jednak zobaczyć, jak duży wpływ na końcowe rozwiązanie ma poszczególny zespół developerski, który nad zadaniem będzie pracować.

W przypadku problemów ze zrozumieniem bądź realizacja zadania zgłasza się to w trakcie daily i osoby z zespołu wzajemnie te zadania wyjaśniają. Po wykonaniu zadania (zmian w kodzie, implementacji nowych funkcjonalności) paczkę zmian należy wysłać do narzędzia inspekcji kodu, gdzie najpierw narzędzie ciągłej integracji wykonuje testy, a następnie koledzy z teamu wykonują inspekcje kodu. Po pozytywnej ocenie zmiana zostaje zintegrowana w repozytorium narzędzia kontroli wersji.

Poza kolejnością (niezależnie od scrumowych sprintów) rozdzielane są zadania związane ze zgłoszeniami nieprawidłowego działania oprogramowania od testerów. Tutaj również z uwagi na krótki staż nie rozwiązywałem samemu takich zgłoszeń, jednak miałem możliwość zobaczenia całego procesu, gdy robili to inni uczestnicy mojego zespołu, z czego korzystałem i co przyda mi się w dalszej mojej pracy w firmie.

### Efekty udziału w praktyce

Poprzez trzymiesięczną pracę w firmie udało mi się poszerzyć moje umiejętności programistyczne, a także dowiedzieć się jak wygląda profesjonalne projektowanie oprogramowania i jak zarządzane są duże projekty informatyczne.

Dzięki wewnątrz firmowym szkoleniom lepiej poznałem historię telefonii komórkowej i działanie nadajników w technologii 5G oraz LTE.

Praca w zespole deweloperskim pozwoliła mi na lepsze zapoznanie się z narzędziami używanymi do profesjonalnego rozwoju oprogramowania, takimi jak narzędzia kontroli wersji, ciągłej integracji, inspekcji kodu, czy listy zadań w formie tablic kanban. Pokazała mi też jak znane mi narzędzia używa się inaczej w przypadku profesjonalnego zastosowania.

Podczas realizacji moich zadań, udało mi się poszerzyć moje doświadczenie w programowaniu obiektowym. Najważniejsza wiedza, jaką zdobyłem, to większa świadomość, czego nie wiem w tym temacie i jakiego doświadczenia mi brakuje. Zobaczyłem również jakie praktyki w programowaniu należy stosować, a jakich unikać. Z pewnością zaprocentuje to w mojej przyszłości jako inżynier.

Praktyka nauczyła mnie również nieco więcej o pracy w zespole, przez systematyzację współpracy między członkami teamu oraz regularnych spotkań. Uświadomiła mi, jak ważna jest komunikacja na temat celów, zadań i postępów.
