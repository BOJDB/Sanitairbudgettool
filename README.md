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

Alle bedragen zijn inclusief btw.

## Prijzen aanpassen

Open `index.html` in een teksteditor. Bovenin staat de lijst `SECTIES`. Elk
artikel heeft `p: [budget, comfort, luxe]`:

```js
{ id: "inloopdouche", naam: "Inloopdouche", p: [600, 950, 1500], keuze: "afscheiding" },
```

Pas de drie getallen aan, sla op en upload het bestand opnieuw. GitHub houdt
bij wat er per wijziging is veranderd, dus je kunt altijd terug naar een
eerdere prijslijst.

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
