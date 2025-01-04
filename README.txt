Ciefp IPTV Link Checker 1.1

Evo kratkog objašnjenja za izmene koje su vezane za tmdb_key i subdl_key, kao i za opciju skeniranja M3U linkova sa mode: no-cors:

1. Ignorisanje stavki sa tmdb_key i subdl_key:

Problemi sa undefined vrednostima: 
Pojavljivale su se vrednosti Host: undefined, Username: undefined, Password: undefined, jer su se neke stavke u JSON-u 
odnosile na objekat koji je imao ključeve kao što su tmdb_key ili subdl_key, ali nisu sadržavale potrebne informacije za tip (MAG ili M3U).

Rešenje: U funkciji koja procesira linkove (processLinks), dodali smo uslov koji preskoči stavke koje sadrže tmdb_key ili subdl_key.

Efekat: Kada se nađu stavke sa tmdb_key ili subdl_key, one se preskaču, a dalje skeniranje se nastavlja sa preostalim linkovima, 
sprečavajući prikazivanje undefined vrednosti.


2. Skeniranje M3U linkova sa mode: no-cors:

Zašto mode: no-cors?: 
Kada se skeniraju M3U linkovi, koristi se metoda HEAD, koja samo proverava zaglavlja (headers) resursa, 
bez preuzimanja celokupnog sadržaja. Međutim, neki serveri mogu blokirati zahtev izvan njihovog domena zbog CORS (Cross-Origin Resource Sharing) politika.

Rešenje sa no-cors: 
Da bi se omogućila provera ovih linkova bez blokiranja od strane servera, dodali smo opciju mode: 'no-cors' u fetch zahtev za M3U linkove. 
To omogućava da se obavi provera linka iako CORS pravila mogu blokirati pristup podacima.

Efekat: 
Ova opcija omogućava proveru M3U linkova bez potrebe za preuzimanjem celokupnog sadržaja sa servera, 
dok istovremeno omogućava da se detektuje da li je link dostupan ili nije.

Zaključak:
Ignorisanje ključeva (tmdb_key i subdl_key) omogućava da se izbegne prikazivanje nepotpunih ili nevažnih podataka, 
što sprečava pojavu grešaka u tabelama sa undefined vrednostima.

Korišćenje mode: no-cors za M3U linkove omogućava da se proveravaju M3U linkovi čak i ako serveri blokiraju direktne zahteve, 
što pomaže u obavljanju provere dostupnosti bez preuzimanja sadržaja.
Ove izmene poboljšavaju tačnost i funkcionalnost aplikacije, omogućujući bolje i brže skeniranje linkova.

..::ciefpsettings::..


Ciefp IPTV Link Checker 1.1

Here is a short explanation of the changes related to tmdb_key and subdl_key, as well as the option to scan M3U links with mode: no-cors:

1. Ignoring items with tmdb_key and subdl_key:

Problems with undefined values:
The values Host: undefined, Username: undefined, Password: undefined appeared, because some items in the JSON
referred to an object that had keys such as tmdb_key or subdl_key, but did not contain the necessary information for the type (MAG or M3U).

Solution: In the function that processes links (processLinks), we added a condition that skips items containing tmdb_key or subdl_key.

Effect: When items with tmdb_key or subdl_key are found, they are skipped, and further scanning continues with the remaining links,
preventing the display of undefined values.

2. Scanning M3U links with mode: no-cors:

Why mode: no-cors?:
When scanning M3U links, the HEAD method is used, which only checks the resource headers,
without downloading the entire content. However, some servers may block requests from outside their domain due to CORS (Cross-Origin Resource Sharing) policies.

Solution with no-cors:
To enable checking these links without being blocked by the server, we added the mode: 'no-cors' option to the fetch request for M3U links.
This allows the link to be checked even though CORS rules may block access to the data.

Effect:
This option allows checking M3U links without having to download the entire content from the server,
while at the same time allowing it to detect whether the link is available or not.

Conclusion:
Ignoring keys (tmdb_key and subdl_key) allows to avoid displaying incomplete or irrelevant data,
which prevents errors in tables with undefined values.

Using mode: no-cors for M3U links allows to check M3U links even if servers block direct requests,
which helps to perform availability checks without downloading content.

These changes improve the accuracy and functionality of the application, allowing better and faster link scanning.

..::ciefpsettings::..