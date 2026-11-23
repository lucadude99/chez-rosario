# Chez Rosario: design tokens

Valori letti dai frame Figma (mobile 375 px, desktop 1440 px). In caso di dubbio rileggi il nodo con l'MCP.

## Colori
| Token | Valore | Uso |
|---|---|---|
| `brand-red` | `#ED2024` | bordi, strisce, titoli, nomi, bordi delle card, fascia footer |
| `brand-cream` | `#FFF6E7` | pannello centrale, strisce chiare, testo del footer |
| `brand-green` | `#006937` | testi di paragrafo |
| bianco | `#FFFFFF` | sfondo fuori dal pannello (visibile solo sopra la cupola) |

## Font
| Uso | Font | Fonte |
|---|---|---|
| Paragrafi | Instrument Sans Regular (con `"wdth" 100`) | Fontsource |
| Titoli, nomi, footer | Marseille Bold | Adobe Fonts (Web Project) |
| Ruoli, "Hello & Buongiorno" | Adobe Handwriting Ernie | Adobe Fonts (Web Project) |

## Scala tipografica
| Elemento | Font | Mobile (< 768) | Desktop (≥ 768, design a 1440) |
|---|---|---|---|
| Paragrafo intro | Instrument Sans, verde, centrato | 14px / lh 20px, larghezza testo 284px | 16px / lh 20px, larghezza testo 916px |
| "Hello & Buongiorno" | Adobe Handwriting Ernie, rosso | 42px / lh 42px, ls -0.42px, rotazione **-9°** | 72px / lh 42px, ls -0.72px, rotazione **-6°** |
| "OUR CHEFS" | Marseille Bold, rosso | ~70px, 1 volta (si adatta alla larghezza) | ~63px, 4 volte con "•" (si adatta alla larghezza) |
| Nome chef | Marseille Bold, rosso | 50px / lh 35px | uguale |
| Ruolo chef | Adobe Handwriting Ernie, rosso | 25px / lh 35px | uguale |
| Bio chef | Instrument Sans, verde, centrato | 14px / lh normal, larghezza testo 285px | uguale |
| Footer | Marseille Bold, crema | 30px / lh 27px, 3 righe centrate | 50px / lh 27px, 3 parole su una riga |

Le dimensioni di "OUR CHEFS" non sono fisse: sono quelle del design alla larghezza del frame. Il testo deve riempire la larghezza (vedi `decorations.md`).

## Misure ricorrenti
- Card chef: larghezza **315px**, bordo **2px** rosso, immagine 311×175, banner a strisce alto 37px, area testo `py-[35px]` con `gap-[25px]`.
- Distanze mobile: blocco Intro → blocco Our Chefs 45px; dentro Intro 35px; dentro Our Chefs 35px tra titolo e card e tra le card.
- Distanze desktop: Intro → titolo → card 45px; dentro Intro 35px; tra le card 23px.
- Fascia footer: alta 151px in entrambe le versioni.

## Breakpoint
- `md` (768px): passaggio da versione mobile a desktop (numero di strisce, titolo "OUR CHEFS", testi, footer su una riga).
- `min-[1400px]`: le card passano da 2×2 a 4 su una riga. Servono almeno 4×315 + 3×23 + bordi ≈ 1390px, quindi sotto i 1400px restano 2 colonne.
- Sotto i 768px: 1 colonna di card.

## Starter `src/styles/global.css` (Tailwind v4)
```css
@import "tailwindcss";

@theme {
  --color-brand-red: #ed2024;
  --color-brand-cream: #fff6e7;
  --color-brand-green: #006937;

  --font-sans: "Instrument Sans", ui-sans-serif, system-ui, sans-serif;
  --font-display: marseille, sans-serif;                       /* Adobe Fonts, solo peso 700 */
  --font-script: adobe-handwriting-ernie, sans-serif;          /* Adobe Fonts, solo peso 400 */
}
```
Usi: `bg-brand-red`, `text-brand-green`, `font-display font-bold`, `font-script font-normal`.
Marseille esiste nel Web Project solo in Bold (700) e Adobe Handwriting Ernie solo in Regular (400): usa sempre quei pesi, altrimenti il browser sintetizza un grassetto finto.
Le classi delle decorazioni (`.page`, `.frame`, `.stripes` ecc.) stanno in `decorations.md`.
