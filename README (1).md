# Sanitairtool — Jouw Droombadkamer

Tool waarmee de verkoper aan tafel snel een sanitair-indicatie samenstelt, met
een pdf voor de klant en een bestellijst voor de backoffice.

Alles zit in één bestand: `index.html`. Code, logo, prijzen, productnamen en
alle foto's zitten daarin ingebakken. Er wordt niets geïnstalleerd, er is geen
database en na het laden werkt de tool ook zonder internet.

## Live zetten met GitHub Pages

1. Zet `index.html` in de repository.
2. Ga naar **Settings → Pages**.
3. Kies bij *Build and deployment* de bron **Deploy from a branch**,
   branch `main`, map `/ (root)` en klik op **Save**.
4. Na een minuut staat de link bovenaan diezelfde pagina, in de vorm
   `https://<gebruikersnaam>.github.io/<repo-naam>/`.

Bijwerken: klik op `index.html` en gebruik **Upload files** om hem te
overschrijven. Elke upload is een commit, dus je kunt altijd terug naar een
vorige versie.

Let op: bij een gratis account moet de repository openbaar zijn. Iedereen met
de link kan dan ook de prijzen in de broncode bekijken. Wil je dat niet, dan
kan Cloudflare Pages gratis publiceren vanuit een privé-repository.

## Hoe de tool werkt

1. **Type ruimte** — vijf mogelijkheden:

   | Type | Ruimte |
   |------|--------|
   | A | Badkamer zonder toilet en zonder bad |
   | B | Badkamer met toilet, zonder bad |
   | C | Badkamer met bad, zonder toilet |
   | D | Badkamer met bad en toilet |
   | E | Alleen een toilet met fontein |

   Bij A tot D staat daaronder een vinkje **Er komt ook een apart toilet bij**.
   Dat voegt een extra stap toe met een eigen toilet, fontein en spiegel, los
   van de badkamer. Bij type E is het vinkje niet zichtbaar.

2. **Niveau** — Budget, Comfort of Luxe voor de hele ruimte.

3. **Per onderdeel** — douche, bad, toilet, wastafelmeubel, toilet en fontein,
   radiator en extra opties. Alleen wat bij het gekozen type hoort. Per
   onderdeel zie je het product met foto en de prijs. Klik op een foto om hem
   groot te zien.

4. **Overzicht** — het totaal, een notitieveld, en twee knoppen:
   **Download pdf** voor de klant en **Download bestellijst** voor de
   backoffice.

Op het startscherm staat ook **Hoe werkt het?** met de uitleg voor verkopers,
en **Prijzen aanpassen** voor het beheerscherm.

De tool onthoudt de laatste offerte op het apparaat, ook na het sluiten van de
pagina. **Opnieuw beginnen** wist hem, met een bevestiging vooraf.

Alle bedragen zijn inclusief btw. Het totaal wordt naar boven afgerond op
tientallen; dat staat als `AFRONDING` bovenin het script.

## Werken met niveaus

De knoppen bovenaan zetten de hele ruimte op Budget, Comfort of Luxe. Achter
elk gekozen onderdeel staan daarnaast kleine knopjes **B**, **C** en **L**.
Daarmee zet je één onderdeel op een ander niveau, bijvoorbeeld een luxe douche
bij een verder eenvoudige badkamer. Zo'n afwijking krijgt een geel label op het
overzicht en op de pdf.

Klik je daarna weer op een van de grote niveauknoppen, dan gaat alles terug
naar dat ene niveau en vervallen de afwijkingen.

Is er voor Comfort of Luxe geen prijs, product of foto ingevuld, dan gebruikt
de tool automatisch die van Budget. **Budget is dus altijd de basis en mag
nooit leeg zijn.**

## Aantallen

Bij een aantal artikelen staan min- en plusknopjes: inbouwspots,
handdoekhaak, handdoekrek, inbouwnis, kolomkast, toiletrolhouder en beide
radiatoren. Het aantal komt mee in de pdf en de bestellijst.

De wastafelkraan verdubbelt automatisch bij een dubbele wastafel.

## Prijzen aanpassen

### In de tool zelf

1. Klik in stap 1 op **Prijzen aanpassen** en vul het wachtwoord in (`jdb`).
2. Per artikel staan drie bedragen (Budget, Comfort, Luxe), daaronder drie
   velden voor de productnaam, daaronder drie fotovakken en daaronder drie
   knoppen voor de onderdelen. Wijzigingen werken meteen.
3. Klik op **Bestand downloaden**. Je krijgt een nieuw `index.html` met alles
   erin, en met de datum van vandaag als datum van de prijslijst.
4. Upload dat bestand op GitHub over het bestaande heen.

Verlaat je het beheerscherm met niet-opgeslagen wijzigingen, dan waarschuwt de
tool. Zolang je niet downloadt, gelden de wijzigingen alleen op jouw scherm.

### Foto's

Klik op **+ foto** en kies een bestand. De tool verkleint hem naar 480 pixels
en slaat hem op als jpeg. Het kruisje verwijdert hem weer. Onderaan staat
hoeveel ruimte alle foto's samen innemen.

### Rechtstreeks in de code

Bovenin het script staat `var SECTIES` met alle artikelen. Per artikel:

| Veld | Betekenis |
|------|-----------|
| `id` | vaste naam, nooit wijzigen |
| `naam` | wat de verkoper ziet |
| `p` | prijs per niveau: `[budget, comfort, luxe]` |
| `v` | productnaam per niveau. Meerdere producten scheiden met een puntkomma |
| `f` | foto per niveau, als data-url |
| `keuze` | radiogroep: hiervan kan er één tegelijk aan staan |
| `groep` | subkopje in het scherm |
| `types` | bij welke ruimtetypes dit artikel hoort |
| `alleenBij` | alleen zichtbaar als een van deze artikelen aan staat |
| `nietBij` | vervalt bij dit artikel |
| `x2` | dubbel bij een dubbele wastafel |
| `tel` | krijgt min- en plusknopjes |

## Onderdelen

De prijs van een artikel kan worden opgebouwd uit de losse onderdelen die
besteld worden. In het beheerscherm staat per artikel een rij **onderdelen**
met een knop per niveau. Daar vul je omschrijving, aantal en prijs per stuk in.

Staan er onderdelen bij een niveau, dan is de som daarvan de prijs en wordt het
handmatige bedrag niet meer gebruikt. Onderdelen verschijnen nergens als keuze
in de verkooptool; ze bepalen alleen het bedrag en komen als losse regels in de
bestellijst.

Bovenaan het beheerscherm staat een schakelaar of de onderdeelprijzen exclusief
btw zijn. Staat die aan, dan telt de tool er 21% bij op (`ONDERDEEL_FACTOR`).

## De pdf

Kop met logo, klantnaam, adviseur en datum. Daarna per blok de artikelen met
een foto, de productnaam en het bedrag, en een zwarte totaalbalk. Onderaan de
notitie en de melding dat het om een vrijblijvende indicatie gaat, geldig tot
twee weken na vandaag, met een volledige offerte die nog volgt.

De pdf wordt door de tool zelf opgebouwd, zonder externe bibliotheek.

## De bestellijst

Een xlsx voor de backoffice, met het vaste sjabloon van alle kopjes — ook de
lege, zodat in één oogopslag te zien is wat er niet besteld is. Verdeeld in
Badkamer, Toiletruimte en Tegels, met een subtotaal per kopje en per blok.

Alle regels rekenen door: aantal maal prijs, en de totalen tellen op. Vult de
backoffice zelf regels in, bijvoorbeeld tegels, dan loopt dat mee tot in het
eindtotaal.

Op rij 9 staat **Budget**: het bedrag dat de klant op de pdf ziet, als vast
getal. Rij 10 is de som van de lijst zelf. Zo zie je meteen of de backoffice
nog op het bedrag van de klant uitkomt.

## Wachtwoord

Het wachtwoord van het beheerscherm is `jdb`, hoofdlettergevoelig. Het staat
niet leesbaar in het bestand, maar als controlegetal in `SLEUTEL`. Een ander
wachtwoord instellen kan met de functie `sleutelVan()`.

Dit is geen echte beveiliging: de broncode van een webpagina is altijd
inzienbaar. Het houdt alleen bezoekers tegen die niet in de code kijken.

## Bedrijfsgegevens en logo

Bovenin het script staat `var BEDRIJF` met naam, adres, telefoon, e-mail en
website. Die gegevens komen op de pdf en onderaan de tool.

Het logo staat als `var LOGO` in het bestand, als data-url. Vervangen kan door
die regel te vervangen door een nieuwe data-url, en `LOGO_VERHOUDING` aan te
passen naar breedte gedeeld door hoogte.

## Techniek

Één html-bestand met alles erin: geen frameworks, geen externe bestanden, geen
internetverbinding nodig na het laden. De pdf en de xlsx worden in de browser
zelf opgebouwd. De laatste offerte wordt bewaard in de browser van het
apparaat; er gaat niets naar buiten.

Het bestand is ongeveer 1,6 MB, vooral door de foto's.
