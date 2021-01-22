# Administrowanie systemami sieciowymi

## Sprawozdanie z laboratorium

Data | Tytuł zajęć | Uczestnicy
:-: | :-: | :-:
13.01.2021 11:15 | Instalowanie i konfigurowanie serwerów WWW i FTP | Bartosz Rodziewicz (226105)

### Opis środowiska
Zajęcia laboratoryjne z części nt. systemu Linux zostały wykonane na maszynie wirtualnej postawionej z wykorzystaniem VirtualBox. Zainstalowana w maszynie dystrybucja to Manjaro 20.2 ze środowiskiem (DE) KDE Plasma. Do zajęć użyta została czysta instalacja systemu po doinstalowaniu najnowszych aktualizacji pakietów. W wielu miejscach używany jest alias `ll`, który jest aliasem na `ls -alF`.

### Przebieg laboratorium
#### Sprawdzić czy serwer WWW (Apache 2) jest zainstalowany (jeśli nie, zainstalować go) i czy jest uruchomiony (jeśli nie, należy go uruchomić). Przy pomocy przeglądarki WWW połączyć się z nim i przetestować czy wyświetli się strona startowa.

Aby sprawdzić czy dany pakiet jest zainstalowany w dystrybucji Manjaro należy użyć komendy `pacman` z flagami `-Qs` lub `-Qi`, gdzie pierwsza szuka podanej nazwy w nazwach oraz opisach paczek, natomiast druga sprawdza czy paczka o dokładnie takiej nazwie jest zainstalowana.

Sprawdzenie stanu usługi można sprawdzić komendą `systemctl status <nazwa>`, a włączenie usługi komendą `systemctl start <nazwa>`.

Nazwa usługi serwera WWW Apache w Manjaro to `httpd`.

![instalacja i uruchomienie www](screenshots/01.png =500x0)

Na powyższym zrzucie widać sprawdzenie, że pakiet `apache` jest zainstalowany oraz włączenie usługi `httpd`.

![domyślna strona Apache Manjaro](screenshots/02.png =500x0)

Serwer Apache w Manjaro nie posiada domyślnej strony WWW wyświetlanej po uruchomieniu serwera z domyślnymi ustawieniami. Zamiast tego po połączeniu się ze stroną http://localhost:80/ wyświetla zawartość domyślnego katalogu znajdującego się pod `/srv/httpd`.

Dla pewności działania serwera WWW poniżej widać stworzenie przykładowego dokumentu `html` z przykładowym tekstem oraz efekt w przeglądarce.

![stworzenie testowego index.html](screenshots/03.png =500x0)

![wyświetlenie testowego index.html](screenshots/04.png =500x0)

#### Sprawdzić czy serwer FTP (Vsftpd) jest zainstalowany (jeśli nie, zainstalować go) i czy jest uruchomiony (jeśli nie, należy go uruchomić).

Serwer `vsftpd` jest domyślnie niezainstalowany w dystrybucji Manjaro. Pakiet jak i usługa nazywają się tak samo. Na poniższych zrzutach ekranu widać instalację oraz włączenie serwera.

![instalacja i uruchomienie ftp](screenshots/05.png =500x0)

![uruchomiony ftp](screenshots/06.png =500x0)

Poniżej widać próbę połączenia z serwerem na domyślnych ustawieniach.

![błąd połączenia ftp](screenshots/07.png =500x0)

#### Skonfigurować serwer WWW, aby spełniał następujące wymagania:
* po wpisaniu w przeglądarce adresu: http://nazwa_serwera/ ma się otworzyć plik "index.html", zlokalizowany w katalogu "/www" serwera, w pliku tym należy umieścić swoje dane: imię i nazwisko oraz numer indeksu.
* jedynie pracownicy firmy będą mogli (po podaniu hasła) uzyskać dostęp i wyświetlić zawartość katalogu "private", dostępnego pod adresem: http://nazwa_serwera/private/ i umieszczonego w katalogu "/www/private". Należy w tym celu utworzyć grupę pracownicy i dodać do niej użytkownika <Imię Nazwisko> (wpisać swoje dane). Grupie pracownicy należy nadać prawo przeglądania ww. katalogu.

##### Stworzenie wymaganych katalogów oraz plików

Do realizacji tego zadania konieczne jest stworzenie wymaganych z treści folderów - `/www` oraz `/www/private` oraz pliku `/www/index.html` z odpowiednią treścią. Dodatkowo stworzony został plik `/www/private/index.html`, aby możliwe było przetestowanie dostępu zabezpieczonego. Na zrzucie poniżej widać użyte komendy, by to zrealizować.

![tworzenie folderów i plików](screenshots/08.png =500x0)

##### Konfiguracja otwartego dostępu serwera Apache

Domyślne ustawienia serwera realizują politykę opisaną w pierwszy punkcie zadania, jednak udostępniają inny katalog. Najprostszym podejściem będzie więc zmiana by domyślne zasady dotyczyły katalogu `/www`, a nie `/srv/http`.

Aby to zrobić należy znaleźć linijkę ustawiającą `DocumentRoot` i zmienić jej wartość na `/www` oraz znaleźć wycinek definiujący ustawienia dla folderu (`<Directory "/srv/http">`) i zmienić jego wartość na `/www`. Na poniższych zrzutach widać oryginalne wartości oraz zmienione wartości.

![oryginalne ustawienia głównego folderu](screenshots/09.png =340x0)
![zmienione ustawienia głównego folderu](screenshots/10.png =340x0)

<div class="page-break"></div>

Po restarcie usługi `httpd` przeglądarka wyświetla odpowiedni dokument pod adresem http://localhost, co widać na poniższym zrzucie.

![index](screenshots/11.png =500x0)

![niezabezpieczony private](screenshots/12.png =500x0)

Na zrzucie powyżej widać, że katalog `/www/private` jest również dostępny bez żadnych zabezpieczeń pod adresem http://localhost/private.

##### Konfiguracja zabezpieczonego dostępu

Konfigurację zabezpieczonego dostępu należy zacząć od stworzenia grupy i użytkownika w serwerze Apache.

Użytkowników tworzy się komendą `htpasswd`, która tutaj tworzy plik przechowujący dane o użytkownikach i zapisauje dane o użytkowniku `bartosz_rodziewicz`.

Stworzenie grupy polega na wpisaniu do pliku zawartości: `<nazwa grupy>: <uzytkownik1> <uzytkownik2> (...) <uzytkownikN>`.

Następnym, aby dodatkowo podnieść bezpieczeństwo zalecane jest zabranie użytkownikom dostępu do czytaniu stworzonych plików. Tutaj kluczowy jest fakt, że nie można go zabrać każdemu i zostawić tylko rootowi, ponieważ serwer Apache sam nie działa z uprawnieniami roota, tylko użytkownika `http` w wersji dla Manjaro. Rozwiązaniem na to, jest pozostawienie roota jako ownera i danie mu praw do zapisu i odczytu (6), podczas oraz ustawienie grupy plików na `http` i zostawienie jej tylko dostępu do czytania (4), inni użytkownicy nie powinni mieć żadnych uprawnień (0).

Wykonanie powyżej opisanych czynności widoczne jest na zrzucie poniżej.

![dodanie użytkownika oraz grupy](screenshots/13.png =500x0)

Następnym konieczne jest ustawienie w ustawieniach serwera Apache informacji, że dostęp do folderu `/www/private` ma być zabezpieczony hasłem. Aby to zrobić do pliku konfiguracyjnego należy dopisać poniższe linijki.

![ustawienia folderu private](screenshots/14.png =500x0)

Powyższe ustawienia po kolei znaczą:
* włączenie zabezpieczenia dostępu
* treść wyświetlanego komunikatu z monitem o hasło
* ścieżka do pliku z użytkownikami
* ścieżka do pliku z grupami
* ustawienie, że dostęp mają tylko użytkownicy z grupy `pracownicy`

##### Po wykonaniu zadania należy przetestować, czy serwer działa zgodnie z wytycznymi.

Po zapisaniu tych ustawień oraz restarcie serwera dostęp do strony głównej wciąż jest bez hasła, jednak katalog pod adresem http://localhost/private wymaga podania hasła, oraz po podaniu poprawnego hasła strona się ładuje. Widać to na poniższych zrzutach.

![strona główna](screenshots/15.png =500x0)

![monit o hasło](screenshots/16.png =500x0)

![strona zabezpiecozna](screenshots/17.png =500x0)

Informacja od Firefoxa o tym, czy użytkownik chce zapisać hasło, jest dowodem, że druga strona wymagała logowania.

<div class="page-break"></div>

#### Skonfigurować serwera FTP tak, aby spełniał następujące wymagania:
* w katalogu `/ftp` będą pliki dostępne do odczytu dla wszystkich użytkowników anonimowo po wpisaniu adresu: ftp://nazwa_servera/,
* użytkownicy posiadający konta na serwerze mają, po zalogowaniu do serwera FTP, uzyskiwać dostęp do swojego katalogu domowego i mają mieć możliwość pobierania z niego plików, jak też umieszczania tam nowych (download/upload).

##### Konfiguracja serwera `vsftpd`

Aby skonfigurować serwer `vsftpd`, konieczne jest najpierw utworzenie katalogu `/ftp`, który ma być katalogiem dostępnym dla anonimowego użytkownika.

Następnym krokiem jest zmiana następujących ustawień w pliku `/etc/vsftpd.conf`:
* `anonymous_enable` - pozwala na dostęp każdemu (bez podawania loginu i hasła); domyślnie `NO`, należy zmienić na `YES`
* `local_enable` - pozwala użytkownikom posiadającym lokalne konta użytkownika na serwerze na logowanie; domyślnie `NO`, należy zmienić na `YES`
* `write_enable` - główny włącznik możliwości zapisywania plików na serwerze, bez innych parametrów pozwala tylko lokalnie zalogowanym kontom zapisywać pliki tam gdzie mają do tego uprawnienia; domyślnie `NO`, należy zmienić na `YES`
* `anon_root` - katalog, który staje się `/` dla użytkowników niezalogowanych; domyślnie `/srv/ftp`, należy dopisać linijkę z wartością `/ftp`

Treść zadania nie mówi wprost czy użytkownicy lokalni mają uzyskiwać dostęp tylko do swoich katalogów domowych, czy ogólnie do całego serwera (na tych samych uprawnieniach co gdyby logowali się lokalnie). Powyższe wypisane ustawienia dają dostęp użytkownikowi do całego serwera na tych samych prawach co lokalnie.

Aby ograniczyć dostęp tylko do katalogu użytkownika konieczna jest zmiana jeszcze dwóch wartości:
* `chroot_local_user` - `/` połączenia ftp staje się katalog domowy użytkownika i użytkownik ma dostęp tylko do niego; nie zalecane ze względów bezpieczeństwa, gdy użytkownik ma możliwość zapisu do katalogu który staje się `/`; domyślnie `NO`, należy zmienić na `YES`
* `allow_writeable_chroot` - aby powyższa opcja działała w połączeniu z katalogiem domowym użytkownika (do którego user ma prawa zapisu), konieczna jest aktywacja tej opcji; tak samo niezalecane ze względów bezpieczeństwa; domyślnie `NO`, należy dopisać linijkę z wartością `YES`

Z uwagi na moją wątpliwość co do treści zadania, oraz fakt, że dwa ostatnie ustawienia są niezalecane, kolejne zrzuty prezentują serwer bez aktywacji tych funkcji.


##### Po wykonaniu zadania należy przetestować, czy serwer działa zgodnie z wytycznymi. W sprawozdaniu należy zamieścić zrzut z ekranu pokazujący umieszczenie na serwerze sprawozdań z poprzednich laboratoriów.

![logowanie jako anon](screenshots/26.png =580x0)
_Poprawne zalogowanie jako anonimowy użytkownik i wyświetlenie listy sprawozdań z poprzednich zajęć._

![pobieranie anon](screenshots/23.png =580x0)
_Pobranie pliku z serwera jako anonimowy użytkownik._

![wysyłanie anon](screenshots/24.png =580x0)
_Próba wysłania pliku na serwer jako anonimowy użytkownik._

![logowanie jako user](screenshots/20.png =580x0)
_Poprawne logowanie na serwer jako użytkownik lokalny._

![poprawne transfery w obie strony jako user](screenshots/21.png =580x0)
_Pobranie oraz wysłanie pliku jako użytkownik lokalny._

![logowanie jako anon z hosta](screenshots/25.png =580x0)
_Logowanie się jako anon z innego komputera._

Ostatni z powyższych zrzut został zamieszczony tylko, aby pokazać, że jest możliwe podłączenie z innej maszyny. Gdyby pomysł o połączeniu z komputera hosta powstał wcześniej wszystkie zrzuty byłyby w ten sposób zrobione.

![umieszczenie sprawek](screenshots/27.png =580x0)

Już po wykonaniu wcześniejszych zrzutów pomyślałem, że "zrzut z ekranu pokazujący umieszczenie na serwerze sprawozdań z poprzednich laboratoriów" może dotyczyć zrzutu przedstawiającego transfer sprawozdań za pomocą ftp (a nie ich obecność w folderze `/ftp`), więc dla pewności zamieszczam ostatni zrzut.
