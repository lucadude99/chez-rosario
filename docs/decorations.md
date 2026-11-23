# Chez Rosario: decorazioni a codice

Tutto quello che è geometrico e a due colori si fa in **CSS**, non con PNG. Un PNG ha larghezza fissa: su uno schermo più largo si sfoca, si deforma o si ripete male. Il CSS segue qualsiasi larghezza, resta nitido e pesa 0 KB.

Vale per: strisce dell'header, bordi laterali, fascia del footer, cupola, banner delle card. L'unica immagine "decorativa" che resta è il logo.

## 1. La griglia di strisce (concetto chiave)

La fascia in alto è una sequenza di strisce **tutte della stessa larghezza** che attraversa l'intera pagina, bordi inclusi. Contando dal Figma:

| | Mobile | Desktop |
|---|---|---|
| Strisce totali `N` | **25** (rossa + 23 interne + rossa) | **47** (rossa + 45 interne + rossa) |
| Larghezza striscia `s` al frame di design | 15px (375 / 25) | 30,64px (1440 / 47) |
| Bordo laterale rosso | 15px = `s` | 31px = `s` |
| Prima striscia interna | crema | crema |
| Striscia centrale | rossa | crema |

Il bordo laterale rosso è quindi semplicemente la prima e l'ultima striscia: **larghezza bordo = larghezza striscia = larghezza pagina / N**.

Scelta: il **numero** di strisce è fisso per breakpoint e la **larghezza** si adatta. In questo modo la composizione resta identica al design a qualsiasi larghezza (inizia e finisce con una striscia intera, è simmetrica). Con strisce a larghezza fissa avresti strisce tagliate ai bordi.

```css
/* global.css */
.page  { container-type: inline-size; }

.frame {
  --n: 25;                                   /* strisce totali, mobile */
  --s: calc(100cqw / var(--n));              /* larghezza di una striscia */
  border-inline: var(--s) solid var(--color-brand-red);
  background: var(--color-brand-cream);
}
@media (min-width: 768px) { .frame { --n: 47; } }
```
- `.page` è il container (full width, wrapper esterno). `.frame` è il figlio: `cqw` si risolve sulla larghezza di `.page`, senza il problema della scrollbar che avrebbe `vw`.
- Non usare `cqw` sullo stesso elemento che ha `container-type`: per questo ci sono due livelli.

## 2. Fascia a strisce + cupola

Struttura:
```astro
<div class="page">
  <div class="frame">
    <div class="stripes" aria-hidden="true"></div>   <!-- fascia a strisce -->
    <div class="panel">                              <!-- pannello crema, contiene la cupola e il contenuto -->
      <span class="dome" aria-hidden="true"></span>
      ... contenuto ...
    </div>
    <footer class="footer-band">...</footer>
  </div>
</div>
```

```css
.stripes {
  height: var(--stripes-h);
  background-image: linear-gradient(to right,
    var(--color-brand-cream) 50%, var(--color-brand-red) 50%);   /* prima crema */
  background-size: calc(var(--s) * 2) 100%;
  background-repeat: repeat-x;
}
.panel { position: relative; background: var(--color-brand-cream); }
.dome {
  position: absolute; bottom: 100%; left: 50%; translate: -50% 0;
  width: var(--dome-w); height: var(--dome-h);
  background: var(--color-brand-cream);
  border-radius: 50% 50% 0 0 / 100% 100% 0 0;     /* semi-ellisse */
}
.frame { --stripes-h: 76px; --dome-h: 46px; --dome-w: /* TODO: misurare su nodo 3:1322 */ 0px; }
@media (min-width: 768px) { .frame { --stripes-h: 150px; --dome-h: 76px; --dome-w: 526px; } }
```

Come funziona: le strisce sono una fascia alta `--stripes-h`. Il pannello crema parte sotto di essa e ha una "cupola" (semi-ellisse) che sale sopra il bordo superiore, coprendo la parte centrale delle strisce. Per questo nel Figma le strisce centrali sembrano più corte.

Misure dal Figma:
- Desktop: strisce alte 150px, cupola larga ≈526px e alta ≈76px (da y=150 a y≈74), centrata. Nodo del pannello: `3:1739`.
- Mobile: strisce alte ≈76px, cima della cupola a y≈30, quindi altezza cupola ≈46px. **Larghezza da misurare** sul nodo `3:1322`. Se la forma non è una semi-ellisse perfetta (nel Figma c'è un leggero "raccordo" alla base), regola `border-radius`; se non basta, usa l'SVG del nodo solo per la cupola.

Il contenuto (logo) parte *sopra* il bordo del pannello: il logo inizia a y=120 (desktop) / y=60 (mobile) dal bordo alto del frame, quindi con margine negativo di 30px (desktop) e 16px (mobile) rispetto all'inizio del pannello. La parte superiore del logo è trasparente e si sovrappone alle strisce.

## 3. Bordi laterali e footer
- Bordi: `border-inline` del `.frame` (vedi sopra). Si estendono per tutta l'altezza.
- Footer: fascia rossa piena, alta 151px, larghezza piena. Il testo (crema, Marseille Bold) è `DELICIOUS BRITALIAN FOOD`:
  - Mobile: 30px, lh 27px, tre righe centrate. Il testo parte 35px sotto il bordo alto della fascia.
  - Desktop: 50px, lh 27px, tre parole su una riga con `justify-between`, la prima a filo del bordo sinistro interno e l'ultima del destro. Nel design il centro del testo è a 52px dal bordo alto della fascia (non centrato: controllare a occhio).

## 4. Titoli che si adattano alla larghezza ("OUR CHEFS")

Regola del design: il testo deve **toccare i bordi rossi laterali** a qualsiasi larghezza. Essendo rosso su rosso, il contatto si legge come un'unica forma.
- Mobile: la frase "OUR CHEFS" una volta.
- Desktop (≥ 768): "OUR CHEFS • OUR CHEFS • OUR CHEFS • OUR CHEFS", 4 volte, intervallate da un punto elenco, senza spazio finale.

Soluzione solo CSS (niente JS): la `font-size` è la larghezza interna divisa per la larghezza del testo misurata in `em`.

```css
.fit-title {
  display: block; white-space: nowrap; text-align: center; line-height: 1;
  font-size: calc((100cqw - 2 * var(--s) + 4px) / var(--r));   /* +4px: sconfina 2px per lato sotto il bordo rosso */
  margin-inline: -2px;
}
.frame { --r: 4.93; }                                          /* mobile: "OUR CHEFS" */
@media (min-width: 768px) { .frame { --r: 21.87; } }          /* desktop: la frase ×4 */
```
`--r` = larghezza del testo in `em`. I valori sopra sono stime ricavate dal design (345px / 70px e 1378px / 63px). **Vanno tarati** con i font Adobe caricati:
1. Metti il testo in un elemento `white-space: nowrap` con `font-size: 100px`.
2. Leggi la larghezza in px con `getBoundingClientRect().width` (a font caricati: `document.fonts.ready`).
3. `--r` = larghezza / 100.

Markup (due varianti, una visibile per breakpoint; l'`h2` ha il testo accessibile):
```astro
<h2 class="fit-title font-display text-brand-red" aria-label="Our Chefs">
  <span aria-hidden="true" class="md:hidden">OUR CHEFS</span>
  <span aria-hidden="true" class="hidden md:inline">OUR CHEFS • OUR CHEFS • OUR CHEFS • OUR CHEFS</span>
</h2>
```
Alternativa se la taratura dà problemi (es. il font Adobe non è caricato al primo render): piccolo script che misura il testo e imposta `font-size` al resize. Preferire la soluzione CSS.

## 5. Banner a strisce nelle card
Identico in mobile e desktop (card larga 315px in entrambi): una fascia alta **37px** con strisce larghe **14,905px**, rossa e crema, che inizia e finisce con una striscia **rossa** (21 strisce = 313px, 1px per lato oltre la larghezza interna, quindi si fonde col bordo rosso della card).

```css
.card-banner {
  height: 37px;
  width: calc(100% + 2px); margin-inline: -1px;
  background-image: linear-gradient(to right,
    var(--color-brand-red) 50%, var(--color-brand-cream) 50%);
  background-size: 29.81px 100%;      /* 2 strisce */
  background-repeat: repeat-x;
}
```
Le card hanno larghezza fissa 315px, quindi qui non serve alcun adattamento.

## 6. Controllo (obbligatorio prima di chiudere la cornice)
Verifica a 375, 430, 768, 1024, 1440, 1920 px:
- [ ] Le strisce sono simmetriche, iniziano e finiscono con una striscia intera.
- [ ] Il bordo rosso ha la stessa larghezza di una striscia.
- [ ] La cupola è centrata e copre la parte centrale delle strisce.
- [ ] "OUR CHEFS" tocca i due bordi, senza essere tagliato e senza lasciare spazio bianco.
- [ ] Il banner delle card inizia e finisce rosso, a filo del bordo della card.
- [ ] Nessuno scroll orizzontale.
