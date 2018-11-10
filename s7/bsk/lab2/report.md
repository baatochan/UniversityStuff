# Bezpieczeństwo sieci komputerowych

## Sprawozdanie z laboratorium

Data | Tytuł zajęć | Uczestnicy
:-: | :-: | :-:
26.10.2018 09:15 | Kryptografia | Igor Bejnarowicz (218573)<br>Bartosz Rodziewicz (226105)

### Przebieg laboratorium

#### 2. Generacja 3 par kluczy
Oboje wygenerowaliśmy trzy pary kluczy:

![3 pary ja](screenshots/ScreenClip_[12].png =500x0)
![3 pary igor](screenshots/Capture.png)

<div class="page-break">

#### 3. Klucze publiczne
Wyeksportowaliśmy klucze do plików tekstowych. Odciski kluczy są następujące:

| Osoba | Odcisk |
| :-: | :-: |
| Igor | 4BE1CA5D520DD702D9CB30283F5BE433401C1FDC |
| Bartosz | 9E4DBBA1772805EA45A6F77719FF00DCEB26EB88 |

![publiczny ja](screenshots/ScreenClip_[13].png =500x0)
![publiczny igor](screenshots/Capture2.png =500x0)

#### 4. Serwer kluczy
Oboje wysłaliśmy nasze klucze na serwer kluczy `pgp.mit.edu`.

![potwierdzenie wysylki](screenshots/ScreenClip_[14].png)

#### 5. Wzajemne podpisanie kluczy
Poprzez serwer kluczy wymieniliśmy się naszymi kluczami i wzajemnie je sobie podpisaliśmy.

![podpisany klucz ja](screenshots/ScreenClip_[15].png =500x0)
![podpisany klucz igor](screenshots/Capture3.png =500x0)

#### 6. Podpisanie małego pliku
Utworzyliśmy plik o nazwie `smallfile.txt` o treści:
```
Bejnarowicz, Rodziewicz
09.11; 22:54
```

<div class="page-break">

Został on podpisany z poziomu konsoli:

![podpisany plik konsola](screenshots/ScreenClip_[16].png)

i sprawdzona jego poprawność z poziomu Kleopatry:

![podpisany plik konsola sprawdzenie](screenshots/ScreenClip_[17].png)

<div class="page-break">

#### 7. Podpisanie pliku binarnego

![podpisany plik binarny](screenshots/ScreenClip_[18].png)

#### 8. Zaszyfrowanie pliku z Kleopatry, odszyfrowanie z konsoli
Użyta komenda:
```
gpg --decrypt-files task.pdf.gpg
```

![zaszyfrowany plik](screenshots/ScreenClip_[20].png)

<div class="page-break">

#### 9. Zaszyfrowanie pliku z konsoli, odszyfrowanie z Kleopatry
Użyta komenda:
```
gpg --recipient bartek2 --output _3_gnupg_2012.pdf.gpg --encrypt _3_gnupg_2012.pdf
```

![zaszyfrowany plik](screenshots/ScreenClip_[21].png)

#### 11. Ukryte zadanie
Poprawnym zadaniem było zadanie nr 5.

![ukryte zadanie](screenshots/ScreenClip_[22].png =500x0)

Jego treść to:
```
Zapisać do pliku tekstowego imiona członków grupy.
Plik zaszyfrować za pomocą gpg algorytmem AES192 (tylko symetrycznym) z kluczem 'LABORKA'.
Obliczyć sumę kontrolną SHA-1 pliku (Kleopatra).
Komendy gpg, treść pliku przed i po zaszyfrowaniu oraz sumę kontrolną umieścić w sprawozdaniu.
```

Stworzony został plik o nazwie `imiona.txt`, z treścią `Igor Bartosz`.

Plik został zaszyfrowany komendą:
```
gpg --recipient "Marcin Markowski" --cipher-algo aes192 --encrypt imiona.txt
```

Nie zrozumieliśmy co znaczy, że mamy użyć kluczu `LABORKA`.

Po zaszyfrowaniu treść pliku to:
```
…¿|˜ô|« —µ)HQ&œ/sþ
´ä@*Û­ÊÖÛDBE>õpŠ‘x1»çëoêu\F?H.¨RþZ
ü¤ù×@s€%¾´Ø¥éjT¬.cAòØÞ´ÒöÒå¦ïs"^û¢Ü	Î]G…¨GâæVÁ~ñžàEöàìÞ`)èôŠ¾ è¨“½¶}Þ·<Í{´Žòx|ÎdµDbÝÓÎû¢)+²Âðˆ“Q
`Ð3	Öá&…£ 1µAÞ”B]	©¶S¶{¨§ÈRÆ)+È;,Î9íG¨JVürµ#˜Ð…3‚ `óÚ!“\W^«²£ßeØì«^IZõå|¿Ë1â@â›ÒQÀ^ÛdÐw=¦!Ÿ˜e\Ã¼Kh„âea/šp6®+«:U,ËjT\(,0£"§ óó{HA–DU²}Á¼6d¯p\\o„U›G<0ã
```

Suma kontrolna SHA-1: `55f24a0a2ae41f1d68085396f3eb3070`.

#### 12. Zaszyfrowane maile
Przesłaliśmy sobie wzajemnie maile. Aby zachowana była zgodność kluczy potrzebna była zmiana domyślnego klucza w Thunderbirdzie. Przed odszyfrowaniem mail wygląda następująco:

![zaszyfrowany mail](screenshots/ScreenClip_[24].png)

Po odszyfrowaniu wyświetla się wiadomość, że mail jest zaufany:

![odszyfrowany mail](screenshots/ScreenClip_[25].png)
![dane szyfrowania](screenshots/ScreenClip_[26].png =500x0)

#### 13. Porównanie szyfrowania
Domyślnym algorytmem szyfrowania jest `AES-128` (w `gpg` od wersji 2.1).
Poniżej znajduje się porównanie plików zaszyfrowanych `AES-192`, `3DES` i `TWOFISH`.
![porownanie szyfrowania komendy](screenshots/ScreenClip_[28].png)
![porownanie szyfrowania](screenshots/ScreenClip_[27].png)
![porownanie szyfrowania rozmiar](screenshots/ScreenClip_[29].png)
