# Chez Rosario: sezioni

Ordine nella pagina: **Cornice → Intro → Our Chefs → Footer**. La cornice (bordi, strisce, cupola, fascia footer) è in `decorations.md`.
Node id Figma indicati come `mobile / desktop`.

Nota: il frame desktop ha strisce di sfondo alte 3115px, residuo del frame mobile. L'altezza reale della pagina desktop è ≈1529px (pannello fino a 1378 + footer 151). Ignorare le strisce a tutta altezza: il pannello è crema pieno.

---

## 1. Intro (`3:1437` / `3:1743`)

Colonna centrata, `gap 35px`.

1. **Logo** (`3:1320` / `3:1744`): immagine unica per entrambe le versioni (contiene "EST. 2026", "Chez", "ROSARIO", "VYNER ST."). Mobile 326px di larghezza (aspect 312/100), desktop 712×228. Inizia a y=60 (mobile) / y=120 (desktop) dal bordo alto del frame, quindi si sovrappone alla fascia a strisce (vedi `decorations.md`, sezione 2).
2. **Paragrafo** (verde, centrato, Instrument Sans). Tre blocchi separati da una riga vuota (lh 20px). Larghezza testo 284px (mobile) / 916px (desktop). Dimensioni in `design-tokens.md`.
3. **"Hello & Buongiorno"** (Adobe Handwriting Ernie, rosso): testo ruotato **-9°** (mobile, 42px) / **-6°** (desktop, 72px). Il blocco che lo contiene è alto ≈115px (mobile) / ≈135px (desktop) e centra il testo: lasciare spazio sufficiente perché la rotazione non venga tagliata.

Copy (non modificare):
> Chez Rosario is built from many visits and tours across Italy with the experience of a chef born from Britain.
>
> Tasting from the pot of many families to truly understand the heart of Italian cooking. This is married with a deep rooted englishness of our head chef and the left field thinking of his team to generate a fusion restaurant truly new and truly original.
>
> We here welcome you with open arms here at Chez Rosario. Where Britalian food is perfected.

Export logo: dal Figma esporta il nodo "Logo" a 2× o 3× in PNG (oppure SVG se il designer ha il vettoriale) e salvalo come `src/assets/logo.png`. Il nodo include già il ritaglio corretto.

## 2. Our Chefs (`3:1439` / `3:1747` + titolo `3:1748`)

**Titolo**: "OUR CHEFS" che si adatta alla larghezza, vedi `decorations.md`, sezione 4.
Distanza titolo → card: 35px (mobile) / 45px (desktop).

**Griglia delle card** (larghezza card fissa 315px):
- < 768: 1 colonna, gap 35px, card centrate.
- 768 → 1399: 2 colonne (2×2), gap 23px, centrate.
- ≥ 1400: 4 colonne, gap 23px, centrate.
- Card della stessa riga con la stessa altezza (`items-stretch`). Nel design desktop le card Rosario e Michael sono alte 517px, le altre si adeguano.

**Struttura di una card** (bordo 2px rosso, larghezza 315px, colonna centrata):
1. Immagine 311×175 (`overflow: hidden`), con ritaglio (vedi sotto).
2. Banner a strisce alto 37px (`decorations.md`, sezione 5).
3. Dettagli: `py-[35px]`, `gap-[25px]`, testo centrato:
   - Blocco nome + ruolo, alto ≈70px: nome Marseille Bold 50px / lh 35px; ruolo Adobe Handwriting Ernie 25px / lh 35px (entrambi rossi).
   - Bio, Instrument Sans 14px verde, larghezza testo 285px, due paragrafi separati da una riga vuota.

| Chef | Ruolo | Node id card (mobile / desktop) | Node id immagine (mobile / desktop) |
|---|---|---|---|
| ROSARIO | Head Chef | `3:1378` / `3:1749` | `3:1338` / `3:1750` |
| HANNAH | Sous Chef | `3:1467` / `3:1776` | `3:1468` / `3:1777` |
| MICHAEL | Chef De Partie | `3:1494` / `3:1803` | `3:1495` / `3:1804` |
| GIACOMO | Saucier | `3:1521` / `3:1830` | `3:1522` / `3:1831` |

Attenzione: il livello Figma di Hannah si chiama **"Anna"**, ma il testo corretto è **HANNAH**.

Copy:

**ROSARIO, Head Chef**
> Renowned for his skills in making something out of nothing, magic out of the mundane, and the wonderful from the humdrum.
>
> Our Head Chef is someone who has no need for the rule book any more - a committed bon viveur and creative genius.

**HANNAH, Sous Chef**
> Our second-in-command brings years of experience of bringing together the best ingredients to create more than the sum of their parts.
>
> This has allowed this chef to carve out a name for herself as one of the best - and most organised - in the business

**MICHAEL, Chef De Partie**
> Our Station Chief for the evening has a wealth of experience in elevating the right things to make unforgettable experiences.
>
> An experimental chef with a focus on proteins and a love of Greek yoghurt, they’re sure to take our evening to higher heights

**GIACOMO, Saucier**
> A desire to treat cuisine like science, not art, has allowed this chef to carve a space in the cookbooks that makes for interesting reading.
>
> A demand for precision and a belief in the ‘correct’ way to do things brings a precise and measured impact to dishes

(Nel design c'è un doppio spazio in "impact to  dishes": usarne uno solo.)

**Foto**: stesse in mobile e desktop, già salvate in `src/assets/`. Il box è 311×175. Ritaglio nel Figma (immagine posizionata dentro il box):

| Chef | Ritaglio |
|---|---|
| Rosario | altezza 217,36%, larghezza 100%, `top: -26,78%`, `left: 0` |
| Hannah | `object-fit: cover`, nessun offset |
| Michael | altezza 177,71%, larghezza 100%, `top: -10,71%`, `left: 0` |
| Giacomo | altezza 170,7%, larghezza 114,15%, `top: -19,94%`, `left: -7,07%` |

- Se i file in `assets` sono già l'export 311×175 (consigliato: nodi "immagine" esportati a 2×, 622×350), usa solo `object-fit: cover` e non applicare questi offset.
- Se sono le foto originali, replica il ritaglio con `object-fit: cover` + `object-position`, o con le percentuali sopra.
- Usa `<Image />` con `widths={[311, 622]}` e `sizes="311px"`.
- Alt: "Rosario, Head Chef", "Hannah, Sous Chef", "Michael, Chef De Partie", "Giacomo, Saucier".

## 3. Footer (`3:1550` + `3:1551` / `3:1726` + `3:1857`, `3:1981`, `3:1982`)

Fascia rossa piena, alta 151px, testo crema Marseille Bold: `DELICIOUS BRITALIAN FOOD`.
- Mobile: 30px, tre righe centrate (`DELICIOUS` / `BRITALIAN` / `FOOD`).
- Desktop: 50px, tre parole su una riga con `justify-between`, a filo dei bordi laterali interni.
- Dettagli di posizione e verifica in `decorations.md`, sezione 3.

Tra l'ultima riga di card e la fascia footer c'è circa 35px di spazio (da verificare sul Figma).
