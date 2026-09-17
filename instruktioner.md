# Övning: gör Ekern responsiv

Du får en färdig sida som ser bra ut på dator: `index.html` och `style.css`. Den är byggd **desktop-first**. Din uppgift är att få den att fungera ner till 360 pixlars bredd, en del i taget.

## Så jobbar du

Öppna sidan med Live Server och slå på enhetsläget i devtools. Ställ in bredden i sifferfältet, inte genom att välja en telefonmodell.

Varje steg har tre delar:

- **Nu:** vad som är fel och vid vilken bredd du ser det
- **Mål:** hur det ska se ut när du är klar
- **Klart när:** hur du kontrollerar

Skriv alla media queries **längst ner** i `style.css`. Eftersom sidan är desktop-first använder du `max-width`, och ordningen blir **största bredden först**:

```css
@media (max-width: 960px) { ... }
@media (max-width: 800px) { ... }
@media (max-width: 600px) { ... }
```

Har du redan en media query med samma bredd lägger du nya regler i den. Skapa inte en till.

Ändra aldrig textstorlekar i dina media queries.

---

## Steg 1: viewport-taggen

**Nu:** Välj en telefon i enhetsläget. Hela datorsidan visas i miniatyr och texten går inte att läsa.

**Mål:** Sidan ritas i telefonens egen bredd.

**Klart när:** Texten är normalstor i enhetsläget. Sidan ser fortfarande trasig ut, det är meningen.

*Tips: titta i `<head>`. Det är raden Emmet brukar ge dig.*

---

## Steg 2: sidan får inte vara bredare än fönstret

**Nu:** Ställ bredden på 1000. Det går att rulla sidan i sidled, för `.behallare` är alltid 1100 pixlar bred.

**Mål:** Behållaren är 1100 pixlar på stora skärmar, men aldrig bredare än fönstret.

**Klart när:** Vid 1000 finns ingen vågrät rullning i sidhuvudets bakgrund, hero och sidfot.

*Det här steget löses **utan** media query. Det räcker att ändra en egenskap i `.behallare`.*

---

## Steg 3: sidlayouten blir en spalt

**Nu:** Ställ bredden på 700. Sidomenyn tar en tredjedel av bredden och innehållet blir trångt.

**Mål:** Under 800 pixlar ligger sidomenyn **ovanför** innehållet, i full bredd.

**Klart när:** Vid 700 är `main` lika bred som sidomenyn.

*Brytpunkt: `max-width: 800px`. Egenskapen du ändrar finns i `.sida`.*

---

## Steg 4: sidomenyn blir en rad länkar

**Nu:** Efter steg 3 är sidomenyn en lång lista som man måste scrolla förbi.

**Mål:** Under 800 pixlar ligger länkarna **bredvid varandra** och radbryter när de inte får plats. Strecken mellan länkarna försvinner.

**Klart när:** Vid 700 tar menyn högst två rader. Vid 400 får den radbryta mer.

*Tips: listan `ul` kan bli en flexbehållare.*

---

## Steg 5: hero från rad till kolumn

**Nu:** Ställ bredden på 850. Bilden behåller sin bredd och texten kläms ihop bredvid.

**Mål:** Under 800 pixlar ligger texten **överst** och bilden **under**. Bilden fyller hela bredden och är 220 pixlar hög.

**Klart när:** Vid 700 och 400 syns ingen vågrät rullning i hero-delen.

*Tips: `.hero-inre` ska byta riktning. Bilden har en fast bredd som måste bort.*

---

## Steg 6: erbjudandet

**Nu:** Den gula rutan har text och knapp i rad. Minska bredden och se när knappen trycker ihop texten.

**Mål:** Knappen hamnar **under** texten, vänsterställd.

**Klart när:** Texten har hela rutans bredd.

*Brytpunkt: hitta den själv. Kan du använda en media query du redan har?*

---

## Steg 7: sidhuvudet

**Nu:** Minska bredden från 1100. Vid någon punkt får logo, meny och sökfält inte längre plats på en rad.

**Mål:** Logo och sökfält ligger kvar på första raden. Menyn flyttas till en **egen rad under**. Sidhuvudet blir så högt som innehållet kräver.

**Klart när:** Inga länkar ligger ovanpå varandra eller utanför kanten, oavsett bredd ner till 600.

*Brytpunkt: hitta den själv. Tips: `.sidhuvud-inre` har en fast höjd. Egenskapen `order` flyttar ett flexelement utan att röra HTML.*

---

## Steg 8: korten

**Nu:** Ställ bredden på 500. Tre kort i rad blir smala pelare.

**Mål:** Korten ligger **under varandra**, ett per rad.

**Klart när:** Vid 500 är varje kort lika brett som innehållet.

*Brytpunkt: hitta den själv. Fundera: blev korten trånga före eller efter steg 3? Varför?*

---

## Steg 9: meny och sök på smal telefon

**Nu:** Ställ bredden på 400. Menylänkarna går utanför kanten och sökfältet får inte plats bredvid logon.

**Mål:** Menylänkarna radbryter. Sökfältet hamnar på en **egen rad längst ner** i sidhuvudet och fyller hela bredden.

**Klart när:** Vid 360 syns alla länkar och hela sökfältet, utan vågrät rullning.

---

## Steg 10: sidfoten från rad till kolumn

**Nu:** Ställ bredden på 400. De tre spalterna i sidfoten är trånga.

**Mål:** Spalterna ligger **under varandra**.

**Klart när:** Vid 400 läses sidfoten uppifrån och ner.

---

## Slutkontroll

Dra långsamt från 1400 till 360. Skriv ner varje bredd där något fortfarande ser dumt ut.

Svara på:

1. Hur många media queries fick du? Kunde några slås ihop?
2. Vilket steg löste du utan media query? Varför gick det?
3. Varför måste `max-width: 600px` stå **efter** `max-width: 800px`?

---

## Extra A: hamburgarmeny

Under 600 pixlar ska menyn gömmas bakom en knapp. Lägg till knappen i sidhuvudet:

```html
<button class="menyknapp" aria-expanded="false">Meny</button>
```

Och JavaScript före `</body>`:

```html
<script>
  const knapp = document.querySelector('.menyknapp');
  knapp.addEventListener('click', () => {
    const oppen = document.querySelector('.huvudmeny').classList.toggle('oppen');
    knapp.setAttribute('aria-expanded', oppen);
  });
</script>
```

**Mål:** På dator syns inte knappen. Under 600 syns knappen, menyn är dold, och menyn visas som en kolumn när man klickar.

## Extra B: vänd på det

Ta sidfoten och skriv om den till **mobile-first**: grundstilen är kolumn, och en media query med `min-width` gör den till rad. Beteendet ska bli exakt detsamma. Vad hände med ordningen på dina media queries?
