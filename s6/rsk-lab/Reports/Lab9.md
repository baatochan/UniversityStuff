# Rozległe sieci komputerowe

## Sprawozdanie z laboratorium

Data				| Tytuł zajęć												| Uczestnicy
--------------------|-----------------------------------------------------------|---------------------------
07.05.2018 07:30	| Konfiguracja i weryfikacja standardowych i rozszerzonych list kontroli dostępu ACL				| Iwo Bujkiewicz (226203)<br />Bartosz Rodziewicz (226105)<br />Dominik Szymon Cecotka

### Odpowiedzi na pytania

1. Standardowe listy ACL to bardzo potężne narzędzie. W jakim celu używa się rozszerzonych list ACL?  
	Podstawowe listy ACL pozwalają na blokowanie pakietów tylko na podstawie źródłowego adresu IP. Czasem potrzeba bardziej dokładnych metod kontroli i wtedy przydają się listy rozszerzone.
1. Typowo listy nazywane wymagają więcej linii niż listy numerowane. Dlaczego więc często stosuje się listy nazywane?  
	Administrator przeglądający konfigurację routera używając listy nazywanej widzi później do czego się ona odnosi (zakładając, że została poprawnie nazwana) zamiast nic nie znaczącej liczby.
1. Dlaczego uważnie trzeba planować i testować listy kontroli dostępu?  
	Listy kontroli dostępu to jedna z najważniejszych metod zabezpieczenia sieci i warto aby były one poprawnie skonfigurowane.
1. Które z typów list kontroli dostępu są lepsze: standardowe czy rozszerzone?  
	Nie ma jednoznacznej odpowiedzi na to pytanie. Standardowe listy są prostsze w konfiguracji i zarządzaniu, jednak nie oferują takich możliwości jak listy rozszerzone. Osoba wybierająca, których list użyć musi sprawdzić co oferują jedne i drugie i zdecydować, czy dodatkowa funkcjonalność jest jej potrzebna.
1. Dlaczego pakiety hello i aktualizacje routingu OSPF nie są blokowane przez domniemany wpis kontroli dostępu deny any (ACE) lub listy ACL zastosowane na routerach R1 i R3?  
	Listy te są zastosowane do ruchu wychodzącego.
