# Administrowanie systemami sieciowymi

## Sprawozdanie z laboratorium

Data | Tytuł zajęć | Uczestnicy
:-: | :-: | :-:
16.12.2020 11:15 | Zarządzanie użytkownikami i grupami; Wykorzystanie udziałów dyskowych | Bartosz Rodziewicz (226105)

### Opis środowiska
Zajęcia laboratoryjne z części nt. systemu Linux zostały wykonane na maszynie wirtualnej postawionej z wykorzystaniem VirtualBox. Zainstalowana w maszynie dystrybucja to Manjaro 20.2 ze środowiskiem (DE) KDE Plasma. Do zajęć użyta została czysta instalacja systemu po doinstalowaniu najnowszych aktualizacji pakietów. W wielu miejscach używany jest alias `ll`, który jest aliasem `ls -alF`.

### Przebieg laboratorium
#### Jeśli w systemie nie jest zainstalowany pakiet `sudo`, należy go zainstalować.

W systemie jest zainstalowany pakiet `sudo`.

![sudo](screenshots/01.png =500x0)

#### Należy założyć konta dla pracowników działu „Produkcja” przestrzegając listy reguł stosowanych w organizacji.
* Konta użytkowników są tworzone zgodnie z konwencją: nazwisko bez polskich znaków + pierwsza litera imienia pracownika (w razie konfliktu, do nazwy użytkownika dodać liczbę porządkową, np.: kowalskij1, kowalskij2, ...). Np.: konto użytkownika Jan Kowalski, nosi nazwę „kowalskij”. Dla każdego pracownika, należy zdefiniować (w formie komentarza, w momencie tworzenia konta) jego pełne dane: imię i nazwisko (już z polskimi znakami).
* Konta użytkowników należących do działów są tworzone w podkatalogach katalogu „/home” o nazwach takich jak nazwa działu, np.: „/home/marketing”.
* Grupa domyślna dla osób z danego działu to grupa o takiej nazwie, jak nazwa działu.
* Osoby z różnych działów nie mają możliwości wzajemnego przeglądania swoich plików.
* Bezpośrednio po założeniu konta, hasła wszystkich użytkowników są takie same, jak nazwa ich konta.
* Hasła muszą być zmienione przy pierwszym zalogowaniu.
* Użytkownicy muszą zmieniać swoje hasła przynajmniej raz na dwa miesiące (60 dni). Na pięć dni przed upływem terminu ważności hasła, użytkownicy powinni być ostrzegani o konieczności jego zmiany.
* Jeden dzień po upływie terminu ważności hasła, konto, którego użytkownik nie dokonał zmiany hasła, zostanie zablokowane.

Do wykonania tego zadania konieczne było przygotowanie niektórych domyślnych wartości w systemie by były zgodne z podanymi powyżej wymogami.

![przygotowanie regul](screenshots/02.png =500x0)

Tymi aspektami były kolejno:
* stworzenie folderu dla grupy, której konta mają być utworzone (`/home/produkcja`)
* stworzenie grupy
* zmiana grupy folderu `/home/produkcja` na nowo stworzoną grupę
* zmiana uprawnień tak by tylko właściciel (`root`) miał możliwość edycji tego pliku, a grupa przeglądanie

Konieczna była również zmiana domyślnych parametrów w pliku `/etc/login.defs`:
* `UMASK` - odpowiada za domyślne uprawnienia nowo tworzonego katalogu użytkownika (077 to uprawnienia 700, 027 to uprawnienia 750)
* `PASS_MAX_DAYS` - po ilu dniach hasło wygasa
* `PASS_WARN_AGE` - ile dni przed wygaśnięciem hasła użytkownik jest informowany

![login.defs defaults](screenshots/03.png =500x0)
![login.defs zmienione](screenshots/04.png =500x0)

Oraz zmiana wartości `INACTIVE` z -1 na 1 (wartość ta symbolizuje ilość dni od wygaśnięcia hasła po których użytkownik jest blokowany).

![useradd zmienione](screenshots/05.png =500x0)

##### Należy założyć konta dla następujących pracowników działu „Produkcja”: <Imię Nazwisko>\*, Jan Kowalski\*\*, Tomasz Nowak\*\*\*
* \* wpisać swoje dane
* \*\* UID to pierwsze 3 cyfry numeru indeksu +1000
* \*\*\* UID to ostatnie 3 cyfry numeru indeksu +1000

![dodanie użytkownika](screenshots/06.png =500x0)

Utworzenie użytkownika wymaga wykonania następujących działań:
* wykonania komendy `useradd` z następującymi flagami:
	* `-b` - flaga wskazuje katalog w którym zostanie stworzony katalog domowy
	* `-m` - flaga powoduje, że katalog domowy zostanie stworzony
	* `-g` - flaga definiuje główną grupę użytkownika
	* `-p` - błędnie użyta flaga do ustawienia hasła, nie powinna zostać użyta
	* `-c` - flaga ustawia komentarz do użytkownika (w wielu DE traktowany jako nazwa wyświetlana)
* później przypadkowo widzimy, że użytkownicy spoza grupy `produkcja` nie mają dostępu do katalogu `/home/produkcja`
* następny krok pokazuje, że katalog użytkownika została stworzony z poprawnymi uprawnieniami
* komenda `chage` pokazuje szczegółowe dane o haśle użytkownika, które w całości zgadzają się z regułami firmy, z wyjątkiem konieczności zmiany hasła co jest osiągnięte następną komendą
* **w tym miejscu konieczne jest wywołanie `passwd` dla tworzonego użytkownika by ustawić mu hasło (błędne użycie `useradd -p` zostało zauważone po wykonaniu zrzutów i pozwoliłem sobie nie powtarzać całości do nowego zrzutu)**
* komenda `passwd` z flagą `--expire` powoduje, że użytkownik musi zmienić swoje hasło przy następnym logowaniu

![pozostali użytkownicy](screenshots/07.png =500x0)

Komendy wymagane do dodania pozostałych użytkowników wyglądają tak samo, różniąc się tylko dodatkową flagą `-u` pozwalającą podać konkretne UID tworzonego użytkownika. **Tutaj tak samo brakuje wywołania `passwd` by ustawić hasła przed wygaszeniem ich.**

##### Po wykonaniu zadania należy sprawdzić, czy wszystko działa zgodnie z zamierzeniami.

Większość zaprezentowałem w trakcie tworzenia tych użytkowników jednak przejdę w tym miejscu jeszcze raz przez punkty reguł:
* nazwy użytkownika oraz komentarz - ustawiane są w trakcie wykonania komendy `useradd`

![utworzeni użytkownicy](screenshots/08.png =500x0)

* lokalizacja katalogu domowego - ustawiane są w trakcie wykonania komendy `useradd`
* grupa - ustawiane są w trakcie wykonania komendy `useradd`
* uprawnienia - ustawione ręcznie i parametrem `UMASK`
* hasła - ustawiane ręcznie komendą `passwd` (zrzuty ekranu z poprzednich zadań mają błędne użycie `useradd -p`)
* pierwsze logowanie wymaga zmiany hasła - ustawione komendą `passwd`

![pierwsze logowanie](screenshots/09.png =500x0)

<div class="page-break"></div>

#### Należy zapewnić, by każdy użytkownik przed zalogowaniem zobaczył na swoim ekranie następujący komunikat (z załączonego pliku „komunikat.txt”)

Treść komunikatu musi być ustawiona w pliku `/etc/motd`.

![motd](screenshots/10.png =500x0)

#### Należy oddelegować część zadań administracyjnych użytkownikowi <Imię Nazwisko>, kierownikowi działu “Produkcja”. Należy umożliwić mu zmienianie haseł pozostałych użytkowników z jego działu (i tylko z tego działu!). Po wykonaniu zadania należy przetestować jego poprawność.

Do wykonania tego zadnia sugeruje użycie małego skryptu będącego nakładką na `passwd`.

Skrypt wygląda następująco:
```sh
#!/bin/bash

group="produkcja"
user="$1"

if [ "$EUID" -ne 0 ]
  then echo "Please run as root"
  exit
fi

if id "$user" | grep -qF "(${group})"; then
    passwd "$user"
else
    echo "User '${user}' is not in group '${group}'."
fi
```

Skrypt ma bardzo proste działanie, ma zahardcodowaną nazwę grupy do zmiany (stąd brak uniwersalności), nazwę użytkownika do zmiany bierze jako argument 1 (jak `passwd`). Następnie sprawdza czy jest uruchomiony jako root, jeśli nie to prosi o uruchomienie jako root. Gdy jest uruchomiony jako root wykorzystuje komendę `id` do sprawdzenia czy user podany w argumencie należy do zahardcodowanej grupy, jeśli tak to wywołuje `passwd` na nim, jeśli nie to pokazuje stosowny komunikat.

Skrypt mógłby zostać ulepszony o automatyczne rozpoznawanie grupy bazując na użytkowniku, który go uruchamia lub sprawdzenie czy argument z nazwą użytkownika do zmiany hasła został podany (aktualnie komenda `id` rzuca błąd, że user '' nie istnieje).

Zapisany został w systemie jako `/usr/local/bin/change-passwd-of-produkcja`.

Aby mógł korzystać z niego użytkownik <Imię Nazwisko>, czyli rodziewiczb, konieczne było dodanie następującej linijki do `/etc/sudoers`:
```
rodziewiczb ALL=PASSWD: /usr/local/bin/change-passwd-of-produkcja
```
Taki wpis pozwala użytkownikowi `rodziewiczb` na uruchamianie jako root komendy `/usr/local/bin/change-passwd-of-produkcja` po ówczesnym uwierzytelnieniu hasłem.

![special passwd](screenshots/11.png =500x0)

Prezentacja działania skryptu. Widzimy, że użytkownik `rodziewiczb` nie może uruchomić innych komend z sudo. Widzimy błędy przy próbie uruchomienia bez argumentu, z argumentem z innej grupy lub bez sudo. Widać też poprawne działanie skryptu.

#### Każdy użytkownik lokalnie zalogowany do serwera ma mieć prawo jego wyłączania i restartowania (polecenia poweroff i reboot) bez konieczności każdorazowego podawania swojego hasła. Przetestować, czy działa.

Domyślna konfiguracja dystrybucji Manjaro pozwala na reboot i shutdown, gdy inni użytkownicy nie są zalogowani.

Aby możliwe było wykonanie rebootu i shutdownu, gdy inni SĄ zalogowani konieczne jest dopisanie do pliku `/etc/sudoers` linijki:
```
ALL ALL=NOPASSWD: /usr/bin/systemctl poweroff,/usr/bin/systemctl reboot
```
oraz wywoływanie przez użytkowników komendy `systemctl poweroff/reboot` z użyciem `sudo`.

Działanie zostało przetestowane, jednak zrobienie zrzutów było niemożliwe z oczywistych powodów.

#### Należy ustalić następujące zasady udziałów dyskowych dla użytkowników utworzonych w zadaniu 1:
* użytkownik może zapisać na dysku co najwyżej 500 MB danych
* przez okres do dwóch dni można zajmować do 650 MB

Do ustawiania quoty dyskowej poziomu kernela w dystrybucji Manjaro należy doinstalować pakiet `quota-tools`.

Później konieczna jest aktywacja wsparcia quoty (dla użytkowników) dla odpowiedniego systemu plików w pliku `/etc/fstab`, w tym wypadku dla systemu plików zamontowanego jako `/`.

![fstab quota](screenshots/12.png =500x0)

Następnie konieczna jest inicjalizacja indeksów oraz aktywacja quoty.

W tym miejscu pojawia się komunikat o przestarzałym, bardziej ograniczonym trybie quoty - istnieje nowsza metoda, jednak to zadanie nie wspomina, którą metodę należy zastosować, więc wybrana została klasyczna, w rzeczywistym zastosowaniu warto jednak użyć tej nowszej, o której informacje można znaleźć np. na Arch Wiki.

![inicjalizacja i aktywacja](screenshots/13.png =500x0)

Następnym krokiem jest ustawienie quoty dla konkretnego użytkownika - do tego służy komenda `edquota <user>`. Otwiera ona plik w którym należy podać rozmiar quoty w blokach (1 blok to 1KB).

![ustawienie dla usera](screenshots/17.png =500x0)

Następnie należy skonfigurować długość grace period - `edquota -t`.

![ustawienie grace period](screenshots/16.png =500x0)

Soft quota to ilość miejsca jaką może zajmować user. Po przekroczeniu jej rozpoczyna się grace period, w trakcie którego user ma czas na pozbycie się nadmiaru plików. Hard quota to ilość jakiej miejsca jakiej użytkownik nie może przekroczyć (system nie pozwoli zapisać ponad nią, nawet w trakcie grace period). Gdy grace period się skończy użytkownik nie może nic zapisać dopóki nie wróci poniżej soft quota.

![ustawianie grace period](screenshots/14.png =500x0)

Komenda `qouta -u <user>` pokazuje aktualne ustawienie quoty dla usera.

Następnie należy skonfigurować to samo dla innych użytkowników - można do tego użyć komendy `edquota -p <set_user> <unset_user>` (kopiuje ustawienia set_usera do unset_usera).

![kopiowanie do innych](screenshots/20.png =500x0)

W całym zadaniu skupiam się wyłącznie na quotach per user, istnieją jeszcze quoty dla grup, jednak to zadanie nic o nich nie wspomina.

<div class="page-break"></div>

#### Po wykonaniu zadania należy sprawdzić, czy wprowadzone zasady są skuteczne. (testy wykonać dla użytkownika <Imię Nazwisko>)

![testy quoty](screenshots/21.png =500x0)

Powyżej widzimy testy quoty. Po przekroczeniu 500M rozpoczyna się grace period, jednak user dalej może zapisywać. Po uderzeniu w 650M `dd` przerywa swoją pracę ze stosowną informacją. Usunięcie plików poniżej 650M, jednak wciąż znajdując się powyżej 500M nie wpływa na odliczanie grace periodu. _Do testów skasowana została zawartość `/etc/motd` aby nie przeszkadzała w zrzutach ekranu._

#### Należy opracować własną strategię wykonywania backupu obejmującej pliki z katalogów domowych użytkowników (nie ograniczonej do nich). Rozważyć wykorzystanie kopii przyrostowych. Należy wykorzystać narzędzia takie jak `cron`, `tar`, itp. oraz napisać odpowiedni skrypt. Przetestować odzyskiwanie danych z backupu.

Rozwiązanie tego zadania jest bardzo podstawowe i można by je znacząco ulepszyć oraz rozbudować. Powinno jednak spełniać wszystkie wymagania z treści zadania.

Rozwiązanie realizuje backup przyrostowy miesięczny. Co miesiąc następuje usunięcie backupu z przed dwóch miesięcy, zabezpieczenie aktualnego backupu oraz stworzenie nowego przyrostowego. Już w tym miejscu widać wiele możliwości ulepszeń jak chociażby przechowywanie pełnych comiesięcznych paczek.

Skrypt comiesięczny wygląda następująco:
```sh
#!/bin/bash

backup_loc="/backup"
older_backup_loc="/backup-older"

rm -rf "$older_backup_loc"
mv "$backup_loc" "$older_backup_loc"

cd /home/

for group in *; do
        if [ "$group" == "baatochan" ]; then
                continue
        fi
        if [ -d "$group" ]; then
                for user in "$group"/*; do
                        mkdir -p "$backup_loc"/"$user"/
                        tar -cg "$backup_loc"/"$user"/data.snar -f "$backup_loc"/"$user"/data.tar "$user"
                done
        fi
done
```

Skrypt wykonuje wspomniane usunięcie 2 miesięcznego backupu oraz zabezpieczenie miesięcznego, po czym iteruje po grupach znajdujących się w `/home` i dla każdego usera grupy tworzy osobny backup data.tar (w jego podfolderze w folderze na backup) narzędziem `tar`. Komenda `tar` jest bardzo podstawowa i ją można by również ulepszyć (jak chociażby zwiększyć poziom kompresji). Realizuje ona jednak inicjalizację backupu przyrostowego.

Skrypt comiesięczny wygląda następująco:
```sh
#!/bin/bash

backup_loc="/backup"

cd /home/

for group in *; do
        if [ "$group" == "baatochan" ]; then
                continue
        fi
        if [ -d "$group" ]; then
                for user in "$group"/*; do
                        tar -cg "$backup_loc"/"$user"/data.snar -f "$backup_loc"/"$user"/"$(date +%s)".tar "$user"
                done
        fi
done
```

Wykonuje on zwykłą iterację po wszystkich użytkownikach i tworzy przyrostowe archiwum (o nazwie będącej aktualnych czasem zapisanym w formie sekund od epocha).

![crontab settings](screenshots/22.png =500x0)

Skrypty uruchamiane są za pomocą crontaba, odpowiednio miesięczny 1 dnia miesiąca o 1:00, a dzienny codziennie o 5:00.

![aktywacja backupu](screenshots/23.png =500x0)

Skrypty przetestowane zostaną za pomocą ręcznego uruchamiania i zaprezentowane na jednym użytkowniku. Na powyższym zrzucie widać efekt odpalenia skryptu miesięcznego oraz to jakie pliki wytworzył w porównaniu do istniejących plików w `/home`. Widoczna qouta dwóch użytkowników pokazuje, że backupy są poprawne, ponieważ zajmują podobną ilość miejsca (jednak kompresja jest słaba o czym wcześniej wspomniałem).

![zawartosc podstawowego archiwum](screenshots/24.png =500x0)

Na powyższym zrzucie widać część zawartości archiwum dla użytkownika wyświetlonego po prawej.

![dzienny bez zmian](screenshots/25.png =500x0)

Na kolejnym zrzucie widać backup dzienny wykonany 3 razy gdy nie nastąpiły żadne zmiany w katalogu użytkownika. W utworzonych nowych archiwach znajdują się tylko puste katalogi.

![dzienny z dodaniem pliku](screenshots/26.png =500x0)

Tutaj zaprezentowane jest dodanie jednego pliku o wielkości 5K.

![dzienny 2 zmiany](screenshots/27.png =500x0)

Tutaj widać, że zmiana pliku jest odwzorowywana w nowych archiwum, jednak zapisywany jest tylko ostatni stan na moment uruchomienia skryptu (sprawa oczywista).

![dzienny 2 nowe pliki](screenshots/28.png =500x0)

Zrzut pokazujący dodanie 2 nowych plików.

![dzienny usuniecie 2 plikow i dodanie 1](screenshots/29.png =500x0)

Zrzut pokazujący usunięcie 2 plików i dodanie 1. W archiwum nie widać informacji o usunięciu, jednak przy odzyskiwaniu (później będzie to widać) informacje o usunięciu plików też się zapisują.

![odzywskiwanie danych](screenshots/30.png =500x0)

Na powyższym screenie pokazane jest ręczne odzyskiwanie danych. Po prawej stronie najpierw są informacje ile plików user zajmuje (te tworzone `dd` się nie liczą, bo tworzył je `root` w katalogu usera). Później widać zawartość katalogu użytkownika i następuje jego usunięcie. Wtedy po lewej widać układ plików backupu oraz ręczne przywracanie danych po kolei. Komenda `tar` również jest tutaj bardzo podstawowa. Całość oczywiście można by zamknąć w ładny skrypt będący prostą pętlą `for`, jednak jest godzina 3:25, gdy to piszę i mam nadzieję, że jego brak nie zaniży mi oceny za to zadanie. Po ręcznym przeleceniu wszystkich katalogów widać po prawej, że pliki uległy przywróceniu oraz że user zajmuje tyle samo miejsca ile zajmował (pliki zostały przywrócone wraz z info o właścicielach i uprawnieniach). Warto zauważyć, że skasowane pliki `test1` i `test2` nie istnieją (zostały przywrócone którymś archiwum po czym ponownie skasowane, pozwala to na przywrócenie backupu z wybranego dnia, np do osobnego folderu). Po usunięciu katalogu użytkownika zapomniałem wykonać komendy `quota`, jednak jej wartość wtedy musiała być (bliska) 0.
