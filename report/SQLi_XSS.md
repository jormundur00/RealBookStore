# SQL injection

## Napad

Dodavanjem komentara na stranicama pojedinačnih knjiga (http://localhost:8080/books/{id}) može da se izvrši SQLInjection napad.

![SQLi_XSS_1_v2](https://github.com/jormundur00/RealBookStore/assets/99336265/0d7c9627-e4d2-4d5b-b76c-3990730f7546)

Prethodni komentar naizgled samo dodaje komentar "Good book.".

![SQLi_XSS_2](https://github.com/jormundur00/RealBookStore/assets/99336265/ee1cc91a-3dde-4073-8770-65e0d1f18840)

Međutim, osim dodatog bezazlenog komentara, prethodni unos će u pozadini pokrenuti SQL kod kojim će se uneti novi korisnik u bazu podataka.
Odlaskom na stranicu Users (http://localhost:8080/persons) možemo videti da se sada u listi korisnika nalazi novi korisnik dodat SQLInjection napadom.

![SQLi_XSS_3](https://github.com/jormundur00/RealBookStore/assets/99336265/1603d3a2-9a3c-433a-9da7-690e32eb04b6)

## Odbrana

Implementiranjem dodavanja komentara koriščenjem klase PreparedStatement umesto klase Statement se maliciozni SQL kod ne izvršava, već samo ispisuje kao deo komentara.

![SQLi_XSS_Odbrana_1](https://github.com/jormundur00/RealBookStore/assets/99336265/3c116911-d317-4e50-8adc-2c8a6e867659)

# Cross-site scripting

## Napad

Stranica Users (http://localhost:8080/persons) nije zaštićena od cross-site scripting napada.
Korisnik dodat prethodnim SQLInjection napadom kao atribut email ima JavaScript skriptu koja se pokreće pri pretrazi korisnika i ispisuje vrednost kolačića sesije u konzoli.

![SQLi_XSS_4](https://github.com/jormundur00/RealBookStore/assets/99336265/22754445-0325-4eba-b3fe-c0ea56d5934c)

Kako kolačić sesije ima podešen HttpOnly fleg koji sprečava pregled kolačića korišćenjem metode document.cookie, u konzoli se ispisuje prazna niska.

## Odbrana

Korišćenjem atributa textContent umesto atributa innerHTML nad tekstualnim elementima korisnika, pretraživač ne izvršava skripte zadate kao vrednosti elemenata, već ih samo ispisuje.

![SQLi_XSS_Odbrana_2](https://github.com/jormundur00/RealBookStore/assets/99336265/4cc88c02-83df-4fa9-b8ea-98a5046b3461)
