# Cross-site request forgery

## Napad

Kako aplikacija nema zaštitu od CSRF napada, "3rd-party" stranice mogu maliciozno da utiču na njeno ponašanje.
Primer jedne takve stranice je stranica Prize (http://localhost:3000/).

![CSRF_1](https://github.com/jormundur00/RealBookStore/assets/99336265/de575f14-2e6f-4c18-ac9d-66aa5cbb5a9b)

Iako izgleda kao da je u pitanju nekakva nagrada, pritiskom na sliku nagrade se pokreće skripta koja menja sadržaj baze podataka naše aplikacije.

![CSRF_4](https://github.com/jormundur00/RealBookStore/assets/99336265/ee99f4fb-c6d4-4fba-b480-b655917f8b34)

U datom primeru, pokretanjem skripte se menjaju lični podaci korisnika sa id = 1, a promene možemo videti na stranici Users (http://localhost:8080/persons).

### Pre pokretanja skripte:
![CSRF_2](https://github.com/jormundur00/RealBookStore/assets/99336265/dbdaf9a2-7390-4e8b-af4e-f2a2f06551ec)
### Posle pokretanja skripte:
![CSRF_3](https://github.com/jormundur00/RealBookStore/assets/99336265/817b1a00-a3d8-4911-bc90-6f578cf3e224)

## Odbrana

Kreiranjem tokena na početku korisničke sesije i proverom vrednosti tokena pri svakom pozivu ažuriranja korisničkih informacija onemogućujemo promene od strane stranica koje nemaju istu vrednost tokena.