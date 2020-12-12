# Administrowanie systemami sieciowymi

## Sprawozdanie z laboratorium

Data | Tytuł zajęć | Uczestnicy
:-: | :-: | :-:
02.12.2020 11:15 | Włączanie i wyłączanie systemu Linux; Podstawowe usługi systemu Linux; Zarządzanie programami i usługami | Bartosz Rodziewicz (226105)

### Opis środowiska
Zajęcia laboratoryjne z części nt. systemu Linux zostały wykonane na maszynie wirtualnej postawionej z wykorzystaniem VirtualBox. Zainstalowana w maszynie dystrybucja to Manjaro 20.2 ze środowiskiem (DE) KDE Plasma. Do zajęć użyta została czysta instalacja systemu po doinstalowaniu najnowszych aktualizacji pakietów.

### Przebieg laboratorium
#### Zapoznać się z narzędziami zarządzania pakietami dostępnymi w wybranej dystrybucji. Zainstalować w systemie menedżer plików Midnight Commander (`mc`). Jeśli program ten jest już zainstalowany, wybrać inny program do zainstalowania.
##### Zapoznać się z narzędziami zarządzania pakietami dostępnymi w wybranej dystrybucji.
W dystrybucji Manjaro dostępne są dwa narzędzia do zarządzania pakietami - `pacman` i `pamac`.

Pierwszy z nich jest starszym narzędziem wywodzącym się z dystrybucji Arch (z której Manjaro samo się wywodzi). `pacman` jest narzędziem CLI, czyli programem który można używać tylko z terminala (istnieją do niego różne GUI, jak np. `octopi`, jednak sam `pacman` takiego nie udostępnia). `pacman` w Manjaro umożliwia instalacje pakietów z oficjalnych repozytoriów systemu.

`pamac` to nowe narzędzie do zarządzania pakietów stworzone na potrzeby Manjaro. Posiada bardziej przyjazny interfejs CLI ("łatwiejsze" komendy) oraz samemu udostępnia GUI. GUI `pamac` poza podstawowaymi operacjami, jak instalowanie i usuwanie pakietów posiada również możliwość przeglądania pakietów z repo wraz z możliwością czytania opisów i przeglądania zrzutów ekranu. Pozwala to uznać ją za aplikację typu sklep, gdzie poza samą instalacją można odkrywać nowe oprogramowanie w przyjemnym, nowoczesnym interfejsie. Brak takiego miejsca był częstym zarzutem dlaczego ta dystrybucja nie nadaje się dla początkujących użytkowników Linuxa. `pamac` poza instalacją oprogramowania z oficjalnych repo systemu umożliwia również instalację z AURa (wcześniej do obsługi AUR na Manjaro konieczne było doinstalowanie pakietu lub ręczna obsługa), a także trwają prace nad obsługą Snapa i Flatpacka.

W dystrybucji Manjaro istnieją dwa główne źródła pakietów:
* oficjalne repozytoria
* AUR - Arch User Repository

Oficjalne repo systemowe to repozytoria z najpopularniejszymi i systemowymi gotowymi pakietami. Repozytoria te bazują na repozytoriach dystrybucji Arch, jednak posiadają bardziej przetestowane pod kątem stabilności i niezawodności oprogramowanie Arch i Manjaro są dystrybucjami typu rolling release, czyli zawsze posiadają najnowszą wersje danego pakietu w repo. Manjaro w swoich repo dłużej testuje oprogramowanie, więc aktualizacje ukazują się z lekkim opóźnieniem do Archa, zapewniając lepszą stabilność.

AUR to zbiór pakietów zarządzany przez społeczność Archa (jak i pochodnych). Sam AUR przechowuje tylko skrypty do przygotowania i instalacji pakietu. Same źródła (lub binarka) programu najczęściej pobierana jest z oficjalnego źródła wydawcy. W AURze można znaleźć praktycznie wszystkie pakiety jakie wyszły na Linuxa czyniąc instalacje oprogramowania z poza oficjalnych repo bardzo łatwą. Nie jest to jednak rozwiązanie idealne. Przy korzystaniu z AURa trzeba zachować czujność i zrozumieć skrypty instalacyjne, ponieważ zdarzały się przypadki niebezpiecznych komend w tych skryptach. Skrypty te wykorzystywane są przez `makepkg`, który służy do przygotowywania pakietów do Archa. Użycie AURa możliwe jest ręcznie (samodzielne pobranie skryptów i potrzebnych binarek/źródeł oraz wykonanie `makepkg`) lub za pomocą róźnych helperów AUR, jak wspomniany przeze mnie, od niedawna natywny dla Manjaro, `pamac`.

<div class="page-break"></div>

##### Zainstalować w systemie menedżer plików Midnight Commander (`mc`). Jeśli program ten jest już zainstalowany, wybrać inny program do zainstalowania.

Zainstalowanie pakietu `mc` możliwe jest za pomocą komendy `pamac install mc`. Później `pamac` pyta się o instalację opcjonalnych dependencji, hasło użytkownika (user musi być na liście sudoers) oraz prosi o potwierdzenie "transakcji".

![Instalacja mc](screenshots/01.png =400x0)

Na zrzucie powyżej widzimy instalacje pakietu `mc` z wszystkimi opcjonalnymi dependencjami.

#### Korzystając z dpkg lub APT sprawdzić, czy w systemie jest zainstalowany program httpd (serwer WWW Apache) oraz określić jakie pliki wchodzą w jego skład. Określić, na jakich poziomach pracy ten program (usługa) jest uruchomiony.

Aby sprawdzić, czy dana paczka jest zainstalowana można użyć komendy `pamac search <nazwa_paczki>`. Poniżej widzimy, że pakiet `apache` jest dostępny w systemie. _Note: W dystrybucji Manjaro nazwa pakietu serweru http apache to `apache`, a nie `httpd`._

![Czy zainstalowano apache](screenshots/02.png =500x0)

<div class="page-break"></div>

Listę plików danej paczki można sprawdzić za pomocą komendy `pamac list --files <nazwa_paczki>`. Lista plików serwera Apache jest bardzo długa, więc pokazuje tylko jej początek. Listę plików można sprawdzić również dla niezainstalowanej paczki.

![Lista plików apache](screenshots/03.png =400x0)

Pakiet apache do działania wykorzystuje własną control grupę, na poziomie systemowym (roota).

![Usługa apache](screenshots/04.png =500x0)

#### Zapoznać się z konfiguracją menu startowego systemu Linux (`grub`). Zmienić domyślnie ładowany system na uruchamianie testu pamięci. Po przetestowaniu zmian przywrócić poprzedni stan.

Konfiguracja GRUBa wykonywana jest z poziomu pliku `/etc/default/grub`. Opis odpowiednich opcji dostępny jest w [dokumentacji GRUBa](https://www.gnu.org/software/grub/manual/grub/html_node/Simple-configuration.html#Simple-configuration). Do zmiany domyślnie bootowanego wpisu w grub konieczna będzie również znajomość kolejności wpisów. Możliwe jest to poprzez np. analizę pliku `/boot/grub/grub.cfg`. W moim przypadku system operacyjny jest na pozycji 0, natomiast `memtest` na pozycji 2.

![Domyślny config GRUBa](screenshots/05.png =400x0)

Wyżej widać domyślny plik konfiguracyjny GRUB w tej dystrybucji. Domyślnym ustawieniem jest ukryty GRUB przy starcie oraz zapamiętywanie ostatnio bootowanej pozycji (domyślnie bootowana pozycja to ostatnio wybrana).

Aby zmienić na domyślne bootowanie `memtest` konieczne będzie usunięcie (zakomentowanie znakiem `#`) opcji `GRUB_SAVEDEFAULT`, a dopisanie opcji `GRUB_DEFAULT="2"` (2 to pozycja `memtest`).

Dodatkowo zmieniona zostaje pozycja `GRUB_TIMEOUT_STYLE=hidden`, na `countdown`, aby GRUB zawsze był widoczny podczas bootowania. Ułatwi to powrót do pozycji 0, przy używaniu systemu w maszynie wirtualnej.

![Zmieniony config GRUBa](screenshots/06.png =500x0)

Aby zmiana konfiguracji została zapisana, poza zmianą ustawień w tych plikach konieczne jest jeszcze uruchomienie komendy `grub-mkconfig -o /boot/grub/grub.cfg` z uprawnieniami roota.

![grub-mkconfig](screenshots/07.png =500x0)

<div class="page-break"></div>

Po reboocie komputera i przejściu licznika automatycznie uruchamia się `memtest`.

![memtest](screenshots/08.png =500x0)

Po wyłączeniu `memtest`a i wybootowaniu systemu, aby przywrócić konfigurację należy cofnąć zmiany w pliku `/etc/default/grub` oraz ponownie uruchomić `grub-mkconfig`.

#### Wykorzystując polecenie at wywołać zadanie, którego czas uruchomienia zostanie odłożony o 10 minut od chwili wydania polecenia `at`.

Dystrybucja Manjaro nie posiada domyślnie zainstalowanego pakietu `at`, więc konieczne było jego doinstalowanie.

Zaplanowanie zadania na 10 minut w przyszłość wykonuje się komendą `at now +10 minutes`, po czym podaje komendy, które mają się wykonać. Zaplanowane komendy to:
```
echo "Bartosz Rodziewicz, 226105" >> info.txt
date >> info.txt
w >> info.txt
```
Zakończenie planowania następuje po podaniu EOF, czyli po wciśnięciu `Ctrl+D`.

![Planowanie zadania](screenshots/09.png =500x0)

Poniżej widać że zadanie się wykonało (dwa pierwsze wpisy były pisane z ręki by sprawdzić czy komendy działają).

![Zawartość pliku info.txt](screenshots/12.png =350x0)

#### Wykorzystując polecenie `atq` sprawdzić jakie zadania oczekują na wykonanie. Wcześniej zaplanować kilka zadań (dowolnych).

![Zaplanowane zadania](screenshots/10.png =500x0)

#### Wykorzystując polecenie `atrm` , usunąć jedno z utworzonych wcześniej zadań.

![Usunięcie zadania](screenshots/11.png =500x0)

#### Sprawdzić jakie zadania są aktualnie przeznaczone do wykonywania z wykorzystaniem `crontab`.

![Lista zadań crontab](screenshots/13.png =500x0)

#### Utworzyć nowy plik z zadaniami dla polecenia crontab, o nazwie "`nowy_plik_crontab`". W pliku tym ma się znaleźć linia z zadaniem, które będzie się uruchamiać 15 minut po każdej pełnej godzinie i zapisywać listę uruchomionych procesów do pliku: `procesy_<godzina>_<data>.log` w katalogu domowym. Następnie należy wywołać polecenie crontab wykorzystując utworzony plik (`nowy_plik_crontab`).

Do wykonania zadania plik `new_file_crontab` ma następującą zawartość:
```
15 * * * * /usr/bin/ps -aux > /home/baatochan/processes_`date +\%H-\%M-\%S`_`date +\%Y-\%m-\%d`.log 2>&1
```
gdzie:

* `15 * * * * *` - informacja, że polecenie ma zostać wykonane 15 min po każdej pełnej godzinie,
* `/usr/bin/ps -aux` - komenda listująca procesy,
* \> /home/baatochan/processes_\`date +\\%H-\\%M-\\%S\`_\`date +\\%Y-\\%m-\\%d\`.log - przekierowanie wyjścia do pliku `processes_data_godzina.log` zapisanego w katalogu domowym; komendy `date` muszą być zawarte w \`, ponieważ są to komendy w komendzie, a dodatkowo dla zadania cron wszystkie `%` muszą być wyescapowane,
* `2>&1` - przekierowanie również wyjscia błędów do pliku (tam gdzie standardowe wyjście).

Uruchomienie zadania polega na wykonaniu komendy `crontab new_file_crontab`.

![crontab](screenshots/14.png =500x0)

Na zrzucie powyżej widać zawartość pliku, aktywacje zadania oraz efekt zadania.  _Działanie komendy zostało sprawdzone na zadaniu cron uruchamianym co minutę (`* * * * *`) oraz na wykonaniach ręcznych._

#### Usunąć wszystkie zadania, które aktualnie są przeznaczone do wykonania.

![Usunięcie crontab](screenshots/15.png =500x0)

#### Sprawdzić czy usługa ssh jest aktywna. Jeśli nie, zainstaluj/uruchom w systemie usługę ssh.

![Aktywacja usługi ssh](screenshots/16.png =500x0)

#### Wykonaj kopię pliku konfiguracyjnego usługi ssh.
Plik konfiguracyjny serwera ssh to `/etc/ssh/sshd_config`. Poniżej widać wykonanie kopii domyślnych ustawień serwera ssh. Do dostępu do katalogu i plików ustawień ssh konieczne są uprawnienia roota.

![Backup ustawień ssh](screenshots/17.png =500x0)

#### Wprowadź zmiany w konfiguracji usługi ssh
##### Ustaw następujące polecenia powitalne "<Imię> <Nazwisko> - laboratorium 2.1 - <termin zajęć>"
Ustawienie wiadomości powitalnej dzieli się na kilka kroków. Najpierw konieczne jest stworzenie pliku zawierającego odpowiednią treść. Poniżej widać stworzenie pliku `/etc/ssh/welcome.msg`.

![Plik z wiadomością](screenshots/18.png =500x0)

Następnie w konfiguracji ssh należy znaleźć i odkomentować ustawienie `Banner` oraz podać ścieżkę do pliku z wiadomością. Do edycji configu wymagane są uprawnienia roota.

![Odpowiednie ustawienia banneru](screenshots/19.png =350x0)

##### Zmień domyślny port, na którym pracuje usługa ssh (jaki?) na inny (spoza puli well-known ports)

Serwer ssh domyślnie pracuje na porcie 22. Zmiana tego portu wymaga odkomentowania `Port` w ustawieniach serwera i zmianie wartości na oczekiwany port.

![Odpowiednie ustawienia portu](screenshots/20.png =500x0)

Kolejnym krokiem jest restart usługi ssh komendą `systemctl restart sshd`.

#### Po restarcie usługi ssh połączyć się z serwerem lokalnie
Do połączenia poza adresem (`localhost`) należy podać parametr `-p`.

![Połączenie localhost](screenshots/21.png =500x0)

#### Spróbować połączyć się z innej maszyny (np. z poziomu systemu Windows - klient Putty) w celu zweryfikowania dokonanych
zmian.
Do połączenia z hosta konieczna była zmiana ustawień maszyny wirtualnej, aby karta sieciowa była w trybie bridged. Adres IP maszyny wirtualnej można po tym odczytać komendą `ifconfig -a`. Połączenie z hosta zostało wykonane z Windowsa z użyciem powershella, ponieważ nie posiadam klienta putty.

![Połączenie host-vm](screenshots/22.png =500x0)

#### Przywrócić oryginalny plik konfiguracyjny usługi ssh

![Przywrócenie ustawień ssh](screenshots/23.png =500x0)
