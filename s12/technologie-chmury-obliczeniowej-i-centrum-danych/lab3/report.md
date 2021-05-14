# Technologie chmury obliczeniowej i centrum danych

## Sprawozdanie z laboratorium

Data | Tytuł zajęć | Uczestnicy
:-: | :-: | :-:
12.04.2021 11:15 | SAN Configuration | Bartosz Rodziewicz (226105)

### Configuring Openfiler iSCSI Target
#### Openfiler iSCI Target
##### Create iSCSI Network ACL
![ACL for local network](screenshots/01.png)  
_Dodanie ACL odpowiedniego do sieci lokalnej._

Powyższa lista ACL umożliwia podłączenie do serwera jedynie hostom z podsieci 192.168.1.0/24, czyli każdemu urządzeniu w mojej domowej sieci lokalnej.

##### Start iSCSI Service
![iSCSI service activated](screenshots/02.png)  
_Akrywowana usługa iSCSI._

##### Create iSCSI Target
![iSCSI target created](screenshots/03.png)  
_Utworzony target iSCSI._

![LUN mapping created](screenshots/04.png)  
_Utworzone mapowanie LUN._

![ACL bound to iSCSI target](screenshots/05.png)  
_ACL przypisane do odpowiedniego targetu._

##### Question 1: Click the CHAP Authentication tab. Why would enabling CHAP authentication for iSCSI be beneficial? Would CHAP protect against unauthorized users intercepting sensitive data? What else should you do in order to secure iSCSI?
Domyślnie protokół iSCSI nie wymaga żadnego uwierzytelniania i wystarcza znajomość adresu IP systemu gdzie działa target. Włączenie CHAP zapewnia podstawowe zabezpieczenie dostępu do systemu wymagając podania przez niego hasła. CHAP nie zabezpiecza jednak przed podsłuchem ruchu sieciowego, ponieważ jedyne co robi to wymaga autoryzacji użytkownika co jakiś czas, pozostawiając ruch sieciowy w żaden sposób nie szyfrowany. W przypadku, gdy musimy postawić zasób iSCSI w sieci, gdzie możemy martwić się o podsłuch transmisji możemy zabezpieczyć dodatkowo same połączenie z iSCSI np. poprzez wykorzystanie SSH.

### Configuring Linux iSCSI Initiator
#### iSCSI Software
##### Install & Start iSCSI Software
![iSCSI sw installed](screenshots/06.png)  
_Instalacja oprogramowania do iSCSI._

![iSCSI service started](screenshots/07.png)  
_Usługa iSCSI aktywowana pomyślnie._

##### Discover & Configure IQN
![iSCSI target discovered](screenshots/08.png)  
_Wykryty target iSCSI._

![iSCSI target connected](screenshots/09.png)  
_Poprawne połączenie z targetem iSCSI._

#### Configure Storage
##### Partition iSCSI Device
![iSCSI target partitioned](screenshots/10.png)  
_Zasób iSCSI podzielony na partycje._

##### Format iSCSI Device
![iSCSI target formatted](screenshots/11.png)  
_Zasób iSCSI sformatowany wykorzystując ext3._

##### Mount iSCSI Device
![iSCSI target mounted](screenshots/12.png)  
_Zasób iSCSI zamontowany jako `/mnt/iscsi`._

### iSCSI Software installation and configuration using Microsoft Windows OS
#### Install & Start iSCSI Software
Próba uruchomienia narzędzia iSCSI Initiator informuje, że usługa nie jest wystartowana - z poziomu tego komunikatu wystarczy kliknąć yes by ją uruchomić. Usługa może być również uruchomiona ręcznie z poziomu zarządzania usługami.

![iSCSI sw installed](screenshots/13.png)  
_Komunikat o nieaktywnej usłudze iSCSI._

#### Discover & Configure IQN
![iSCSI target connected](screenshots/14.png)  
_Poprawne połączenie z targetem iSCSI._

#### Partition iSCSI Device
Po podłączeniu do zasobu widać, że jest on widoczny w Disk Management. Widać tam, też że dysk jest już podzielony na partycję. Jako, że jest on sformatowany ext3 Windows nie potrafi tego wykryć.

![iSCSI target partitioned by Linux](screenshots/15.png)  
_Zasób iSCSI podzielony na partycje, jeszcze z poziomu Windowsa._

Aby podzielić na partycję z poziomu Windowsa konieczne jest usunięcie istniejącej partycji oraz uruchomienie kreatora tworzenia nowej partycji.

![Creating new partition](screenshots/16.png)  
_Kreator tworzenia partycji - wybór litery pod jaką partycja będzie zamontowana._

#### Format iSCSI Device
![Formatting new partition](screenshots/17.png)  
_Kreator tworzenia partycji - wybór systemu plików i szczegółów formatowania partycji_

#### Mount iSCSI Device
Kreator tworzenia partycji po skończeniu domyślnie montuje dysk do wybranej litery w trakcie tworzenia partycji. Wybór litery pokazany był powyżej._

![iSCSI target mounted](screenshots/18.png)  
_Zamontowany zasób iSCSI widoczny z poziomu My PC._

![iSCSI target content](screenshots/19.png)  
_Domyślna zawartość zasobu iSCSI po sformatowaniu jako NTFS._
