# Rozległe sieci komputerowe
## Sprawozdanie z laboratorium

| Data             | Tytuł zajęć | Uczestnicy                                                                           |
| :--------------: | :---------: | :----------------------------------------------------------------------------------: |
| 04.06.2018 07:30 | NAT i PAT   | Iwo Bujkiewicz (226203)<br />Bartosz Rodziewicz (226105)<br />Dominik Szymon Cecotka |

### Odpowiedzi na pytania - instrukcja 12.1

1. **Dlaczego NAT jest używany w sieci?**

	Na świecie jest nie wystarczająca liczba publicznych adresów IP i technologia NAT pozwala uczynić tylko niektóre urządzenia dostępne z zewnątrz utrzymując inne lokalne urządzenia dostępne tylko wewnątrz sieci lokalnej.

1. **Jakie są ograniczenia NAT?**

	NAT wymaga do działania adres IP lub numer portu w nagłówku TCP lub IP pakietów do translacji.

	Przykładowe protokoły, których nie można wykorzystać z technologią NAT:
	* `SNMP`,
	* `LDAP`,
	* `Kerberos v5`.

### Odpowiedzi na pytania - instrukcja 12.2

1. **Jakie korzyści zapewnia statyczny NAT?**

	Statyczny NAT pozwala użytkownikom z zewnątrz sieci LAN na dostęp do komputerów lub serwerów znajdujących się w lokalnej sieci.

1. **Jakie problemy pojawią się, jeśli 10 hostów z tej sieci będzie próbowało jednoczesnej komunikacji z Internetem?**

	W puli adresów NAT nie ma wystarczającej liczby adresów, by zapewnić dostęp dla 10 jednoczesnych sesji.

### Odpowiedzi na pytania - instrukcja 13

1. **Jakie korzyści zapewnia translacja portów PAT?**

	PAT zmniejsza ilość publicznych adresów IP potrzebną, by dostarczyć dostęp do Internetu. PAT zapewnia również zwiększone bezpieczeństwo, poprzez ukrycie prywatnych adresów IP z zewnątrz.
