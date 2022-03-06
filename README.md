
HBOR data 1992-2018
==============

Scroll [below](#the-original-hbor-database) for an English version! 
___

# Izvorna baza podataka

Ustupljena baza podataka od 1992. do 2018. se sastoji od **31972** opservacija, koje obuhvaćaju
preko **109.27** milijardi kuna.\
Jedna opservacija = jedan dodijeljen kredit.

Ustupljena baza se sastoji od 3 stupca.\
To su: Program kreditiranja, Korisnik kredita, Odobreno KN.

Koristeći se ovom bazom, trenutačno meni jedini mogući proxy pomoću kojeg se može doći do OIBa
jest upravo naziv korisnika kredita.

# Spajanje OIB-a

Pomoću izvornih naziva korisnika kredita, i raznih prilagodba istih se dolazi do podudarajućih naziva s nazivima u raznim drugim bazama podataka. Primarno je korištena baza EOJN-a, dostupna na [linku](https://eojn.nn.hr/SPIN/application/ipn/Oglasnik/PreuzimanjeObavijesti.aspx), agregirana 14-11-2021.

Ovakav proces rezultira krivo spojenim OIB-ima i konačna baza ne sadrži sve uparene opservacije. To nastaje zbog:

- poduzeća s jednakim nazivima - u tom slučaju se uzima OIB jednog nasumično sparenog poduzeća,
- poduzeća bez podudarajućeg naziva - rezultat nestandardiziranih naziva, krivih unosa i slično, u tom slučaju nema dostupnog OIB-a,
- poduzeća koja uopće nisu prisutna u sparivanim bazama - također ostaju bez dostupnog OIB-a,
- i drugih sličnih problema.
   
Ukupno preostaje **1929** opservacija koje nemaju dostupan OIB. No, također od **30043** spojenih opservacija, **633** opservacija je spojeno s potencijalno krivim OIB-om.

# Konačna baza podataka

Zbog spomenutih problema kod spajanja OIB-a kreira se i dodatna dummy varijabla koja označava potencijalno krive OIB-e.\
Ona ima vrijednost 1, ukoliko se radi o slučaju gdje je postojalo više poduzeća pod istim nazivom. U tom je slučaju uzet *nasumični* OIB od svih spojenih. Inače ta dummy varijabla ima vrijednost 0.\
Naravno, moguće je da su i drugi OIB-i potencijalno krivo spojeni zbog manjka podataka za točnu identifikaciju, no s isključivo ovom bazom je teško locirati greške u spajanju, jer je jedino dostupan naziv poduzeća.\
Konačno, izvučena je i godina iz naziva programa kreditiranja, iako nije u potpunosti jasno njeno značenje.

# Varijable konačne baze podataka:

    - Program kreditiranja - naziv programa u sklopu kojeg je kredit i dodijeljen
    - Korisnik kredita - naziv korisnika kredita
    - Odobreno KN - iznos dodijeljen kreditom u HRK
    - Godina - izdvojena godina iz naziva programa ukoliko je isti sadrži, inače NA
    - OIB - spojeni odgovarajući OIB korisniku kredita
    - sus - dummy varijabla, 1 ukoliko se radi o nasumično izvučenim OIB-om od njih više sparenih, inače 0

___

 In English.
___

# The original HBOR database

The given database for the period of 1992-2018 encompasses **31972** observations with over **109.27** billion HRK.\
One observation corresponds to one given loan.

The database contains only 3 variables, and their names are left in Croatian:

    - Program kreditiranja - name of the frame/programme of a given loan
    - Korisnik kredita - name of the loan recipient
    - Odobreno KN - value of the loan

Using the name of the loan recipient we can obtain a proxy from which we can extract the recipients unique tax PIN/ID, known as OIB in Croatia.

# Joining the OIB

We construct the proxy so it can match multiple different databases which contain the name of a firm & its' wanted OIB. Primarily, we use, and match with the database aggregated 14-11-2021 from the Croatian Official Gazette's online registry of public procurements [i.e. EOJN](https://eojn.nn.hr/SPIN/application/ipn/Oglasnik/PreuzimanjeObavijesti.aspx). 

This process results with many errors:

- firms have same names, so we do not know which firm is exactly the recipient, and a random OIB out of all matches is kept as a *true* one (we create a dummy to mark these),
- firms appear under different names, so their OIB cannot be matched, and is left as NA,
- firms do not exist in both databases, hence no match is even possible, left as NA,
- and so on.

In the end, we are left with **1929** observations which are not matched with an OIB (are left as NAs). Also, out of **30043** matched observations, **633** are randomly assigned out of multiple matches.

# Final database

Because of the mentioned firms with same names, we create an additional dummy variable which marks potentially mismatched OIB's.\
It takes a value of 1, if that is the case, and 0 otherwise.

Of course, the dummy when 0 does not mean that the OIB is matched with 100% certainty. This type of joining OIB's, using only the given name of a subject, is highly prone to errors, which are difficult to locate on an aggregate level, and should be closely inspected by checking each & every observation. However, this is proven to be really time consuming, and certainly is not of large use for a database with only these few variables.

# Variables in the final database

    - Program kreditiranja - name of the frame/programme of a given loan
    - Korisnik kredita - name of the loan recipient
    - Odobreno KN - value of the loan
    - Godina - year, extracted from the name of the programme of a given loan, if one is present in it
    - OIB - matched recipient's OIB
    - sus - dummy variable, 1 if the OIB is randomly pulled from multiple matched OIB's, 0 otherwise 
