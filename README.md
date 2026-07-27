# Sanitairtool — Jouw Droombadkamer

Tool om snel het sanitair voor een badkamer samen te stellen en er direct een
pdf-offerte van te maken. Alles zit in één bestand: `index.html`. Er is geen
internetverbinding nodig en er wordt niets geïnstalleerd.

## Live zetten met GitHub Pages

1. Zet `index.html` in de repository.
2. Ga naar **Settings → Pages**.
3. Kies bij *Build and deployment* de bron **Deploy from a branch**,
   branch `main` en map `/ (root)`.
4. Na een paar minuten staat de tool op
   `https://<gebruikersnaam>.github.io/<repo-naam>/`.

Let op: bij een gratis account moet de repository openbaar zijn. Iedereen die
de link kent, kan dan ook de prijzen in het bestand bekijken.

## Hoe de tool werkt

1. **Ruimte en niveau** — type ruimte (A t/m E) en het niveau Budget, Comfort
   of Luxe. Het type bepaalt welke onderdelen daarna verschijnen.
2. **Per onderdeel** — douche, bad, toilet, wastafelmeubel, fontein, radiator
   en extra opties. Alleen de onderdelen die bij het gekozen type horen.
3. **Overzicht** — totaalbedrag, de drie niveaus naast elkaar en de knop
   *Download pdf*.

Via **Prijzen aanpassen** in stap 1 kom je in het beheerscherm. Dat is
afgeschermd met een wachtwoord.

Alle bedragen zijn inclusief btw.

## Prijzen aanpassen

Dit kan op twee manieren.

### In de tool zelf (het makkelijkst)

1. Open de tool en klik in stap 1 onderaan op **Prijzen aanpassen**.
   Vul het wachtwoord in (`jdb`).
2. Alle artikelen staan er met drie velden: Budget, Comfort en Luxe.
   Wijzigingen werken meteen.
3. Klik op **Bestand downloaden**. Je krijgt een nieuw `index.html` met de
   nieuwe prijzen erin.
4. Upload dat bestand op GitHub over het bestaande heen. Op de repository:
   klik op `index.html`, dan op het potloodje of op **Upload files**, en
   bevestig met **Commit changes**.

Zolang je de laatste stap niet doet, gelden de nieuwe prijzen alleen op jouw
eigen scherm. Pas na het uploaden ziet iedereen ze.

### Rechtstreeks in de code

Bovenin `index.html` staat de lijst `SECTIES`. Elk artikel heeft
`p: [budget, comfort, luxe]`:

```js
{ id: "inloopdouche", naam: "Inloopdouche", p: [600, 950, 1500], keuze: "afscheiding" },
```

GitHub houdt per wijziging bij wat er veranderd is, dus je kunt altijd terug
naar een eerdere prijslijst.

### Betekenis van de velden

| Veld | Wat het doet |
|---|---|
| `p` | prijs per niveau: `[budget, comfort, luxe]` |
| `keuze` | artikelen met dezelfde waarde sluiten elkaar uit (radioknoppen) |
| `groep` | kopje waaronder het artikel in het scherm valt |
| `alleenBij` | pas te kiezen als één van die artikelen aan staat |
| `nodig` | tekst die verschijnt zolang dat nog niet zo is |
| `nietBij` | vervalt zodra dat artikel gekozen is |
| `x2` | telt dubbel bij een dubbele wastafel |
| `types` | bij welke typen ruimte het onderdeel hoort |

## Wachtwoord

Het beheerscherm zit achter een wachtwoord. Het staat niet als tekst in het
bestand, maar als controlegetal in `SLEUTEL`. Wil je het wijzigen, reken dan
de nieuwe waarde uit met dezelfde formule als in `sleutelVan()` en zet die in
`SLEUTEL`.

Let op: dit houdt meekijkers tegen, maar het is geen echte beveiliging. Alles
draait in de browser, dus wie de broncode bekijkt kan de prijzen sowieso
inzien en het slot omzeilen. Moeten de prijzen echt geheim blijven, zet de
tool dan achter een login op de eigen website.

## Bedrijfsgegevens en logo

Ook bovenin `index.html`:

- `BEDRIJF` — naam, adres, telefoon, e-mail en website, zoals ze onder de
  offerte en in de pdf verschijnen.
- `LOGO` — het logo als data-URL, ingebakken zodat het altijd meekomt.
  Vervang je het, pas dan ook `LOGO_VERHOUDING` aan (breedte gedeeld door
  hoogte van de afbeelding).

## Techniek

Losse HTML met CSS en JavaScript, zonder bibliotheken of build-stap. De pdf
wordt door de tool zelf opgebouwd. Werkt in elke moderne browser, ook op
telefoon en tablet.
