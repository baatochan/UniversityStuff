# Wirtualizacja systemów i sieci komputerowych

## Sprawozdanie z laboratorium

Data | Tytuł zajęć | Uczestnicy
:-: | :-: | :-:
29.10.2018 09:15 | Praca z maszyną wirtualną - Vagrant | Norbert Małecki (218280)<br>Bartosz Rodziewicz (226105)

### Przebieg laboratorium
Pracę rozpoczęliśmy od postawieniu dwóch maszyn wirtualnych poprzez uruchomienie komendy `vargant up` w katalogu `~/VirtualBox VMs/vag/`.

Domyślna konfiguracja sieciowa maszyn stworzonych przez Vagranta prezentuje się następująco:

![Domyślna konfiguracja](screenshots/Screenshot_from_2018-10-29_11-43-54.png =500x0)

Zadanie mówi, aby maszyny były dostępne z poziomu komputera hosta, ale nie były widoczne w sieci laboratoryjnej, więc skonfigurowaliśmy je w trybie `host-only`.

![Konfiguracja host-only](screenshots/Screenshot_from_2018-10-29_11-48-31.png =400x0)
![Konfiguracja host-only 2](screenshots/Screenshot_from_2018-10-29_11-48-49.png =400x0)

Instrukcja mówi, że powinniśmy ustawić nazwę sieci na własną jednak nie udało nam się tego zrobić. Dlatego na screenshocie zamieściliśmy nasz indeks.

W maszynach dostępne są dwa interfejsy - wirtualne połączenie Ethernet i Loopback:
![Interfejsy](screenshots/Screenshot_from_2018-10-29_11-49-49.png)

Z uwagi na naszą konfigurację sieci `host-only` (bez DHCP) adres nie został automatycznie pobrany i musieliśmy ustawić go ręcznie.

Adresy zostały ustawione następująco.
* Host - `10.42.0.1`
* Serwer WWW - `10.42.0.3`
* Baza danych - `10.42.0.4`
Maska podsieci to `255.255.255.0`, a brama domyślna nie jest ustawiona.

Do konfiguracji maszyn wirtualnych użyliśmy narzędzia `nmtui`, zgodnie z dołączoną instrukcją użycia w instrukcji do laboratorium.
![Ustawienie adresów](screenshots/Screenshot_from_2018-10-29_11-52-38.png)
![Restart interfejsów](screenshots/Screenshot_from_2018-10-29_11-53-09.png)

Po tej konfiguracji ping z hosta szedł do obu maszyn wirtualnych, było połączenie z serwerem WWW, jednak serwer nie łączył się z bazą danych.
![Pingi do maszynek](screenshots/Screenshot_from_2018-10-29_11-56-39.png)

<div class="page-break">

Po chwili zastanowienia się uświadomiliśmy sobie, że kod php na serwerze nie jest w stanie automatycznie znaleźć adresu naszej bazy danych. Znaleźliśmy plik `index.php`, który znajdował się na serwerze WWW w folderze `/var/www/html/`.
![index.php](screenshots/Screenshot_from_2018-10-29_12-01-00.png)

Za pomocą Vima (nie było to łatwe) zmieniliśmy argument funkcji `mysqli_connect` z `db` na właściwy adres maszyny z bazą danych.
![Edytowany index.php](screenshots/Screenshot_from_2018-10-29_12-01-32.png)

<div class="page-break">

Po odświeżeniu strony na serwerze WWW (oczywiście z poziomu hosta) uzyskaliśmy komunikat potwierdzający połączenie z bazą danych.
![Poprawne połączenie z bazą danych](screenshots/Screenshot_from_2018-10-29_12-01-44.png)

### Realizacja projektu
Wykorzystaliśmy gotowy obraz pobrany z [https://app.vagrantup.com/ubuntu/boxes/trusty64](https://app.vagrantup.com/ubuntu/boxes/trusty64).
![Vagrant up](screenshots/vagrant_up.png)

<div class="page-break">

Następnie zmieniliśmy domyślny plik `Vagrantfile` tak aby możliwe było użycie odpowiednich komend potrzebnych do dostosowania maszyny. W tym celu utworzyliśmy skrypt `bootstrap.sh`, który był uruchamiany poprzez dodanie do pliku `Vagranfile` komendy `config.vm.provision :shell, path: "bootstrap.sh"`. Możliwe jest podanie komend bezpośrednio w pliku `Vagrantfile`, ale lepiej jednak jest oddzielić pliki od siebie.

![Vagrantfile](screenshots/vagrantfile.png =500x0)

Skrypt zawierał komendy służące do zainstalowania PHP, systemu kontroli wersji Git oraz serwera Apache.
![Bootstrap.sh](screenshots/bootstrap.png =500x0)

Po utworzeniu maszyny wirtualnej i zalogowaniu się sprawdziliśmy czy system jest prawidłowo skonfigurowany.
![Sprawdzenie wersji](screenshots/check_installed.png =500x0)
