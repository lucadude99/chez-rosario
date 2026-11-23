# Chez Rosario: brief di progetto

Sito vetrina **a pagina singola**, statico, responsive (mobile + desktop). Nessun backend, nessun CMS.
Il sito è in inglese (`<html lang="en">`), titolo: "Chez Rosario".

## Stack
- **Astro** (output statico) + **Tailwind CSS v4** con il plugin Vite `@tailwindcss/vite`.
- Nessun `tailwind.config.js`: i token stanno in `@theme` dentro `src/styles/global.css` (vedi `design-tokens.md`).
- Nessun framework UI (niente React): la pagina non ha interattività.
- Immagini in `src/assets/`, con `<Image />` da `astro:assets`. Mai in `public/` (lì non vengono ottimizzate). In `public/` vanno solo favicon e immagine per l'anteprima social.
- Font:
  - **Instrument Sans Regular**: self-host con `@fontsource/instrument-sans` (import del peso 400).
  - **Marseille Bold** e **Adobe Handwriting Ernie**: Adobe Fonts, tramite Web Project (codice di embed nel `<head>`). Non esistono file da scaricare. Famiglie CSS dal Web Project: `marseille` (peso 700, normal) e `adobe-handwriting-ernie` (peso 400, normal). Nel `<head>` della pagina:
    ```html
    <link rel="preconnect" href="https://use.typekit.net" crossorigin>
    <link rel="stylesheet" href="https://use.typekit.net/qdn0bcd.css">
    ```

## Design (Figma)
File `bC702FKPyeTgYLOYA6LNeU`.

| Versione | Frame | Larghezza | Node id | Link |
|---|---|---|---|---|
| Mobile | Page | 375 | `1:2` | https://www.figma.com/design/bC702FKPyeTgYLOYA6LNeU/Chez-Rosario-%E2%80%93-Mobile?node-id=1-2&m=dev |
| Desktop | Page | 1440 | `3:1710` | https://www.figma.com/design/bC702FKPyeTgYLOYA6LNeU/Chez-Rosario-%E2%80%93-Mobile?node-id=3-1710&m=dev |

Palette: rosso `#ED2024`, crema `#FFF6E7`, verde `#006937`, sfondo pagina bianco.

## Come lavorare (in quest'ordine)
1. **Setup**: token e font in `global.css`, embed Adobe nel `<head>`, layout base della pagina.
2. **Cornice** (bordi laterali rossi, fascia a strisce con cupola, fascia rossa del footer): segui `decorations.md`. Verifica a 375, 768, 1440, 1920 px prima di andare avanti.
3. **Sezioni**, una alla volta, nell'ordine di `sections.md`: Intro, Our Chefs (titolo + 4 card), Footer.
   Per ciascuna: leggi il nodo Figma con l'MCP (mobile e desktop), guarda lo screenshot, implementa, confronta.
4. **Rifinitura**: meta description, favicon, og-image, controllo performance (Lighthouse).

## Regole
- Il codice che restituisce l'MCP di Figma è un riferimento visivo con posizionamento assoluto: traducilo in flex/grid. Non copiarlo.
- Strisce, cupola e banner delle card sono **CSS**, non immagini (motivi in `decorations.md`).
- Nessun URL temporaneo di Figma nel codice finale.
- Un solo breakpoint di layout: `md` (768 px) per il passaggio mobile → desktop, più `min-[1400px]` per le 4 card su una riga. Dettagli in `design-tokens.md`.
- Mobile first: gli stili base sono quelli mobile, i `md:` aggiungono il desktop.
- Il testo del design è in maiuscolo per i nomi e i titoli: usa il testo già maiuscolo, come nel design.
- Alt delle foto: "Rosario, Head Chef" ecc. Il logo ha `alt="Chez Rosario"`. Le decorazioni sono `aria-hidden`.

## TODO / dati mancanti
- [x] Embed Adobe e nomi delle famiglie: definiti nella sezione Font. Se il Web Project ha una lista di domini consentiti, aggiungere il dominio del sito (anche `localhost` per lo sviluppo).
- [ ] Export del logo da Figma (vedi `sections.md`, Intro).
- [ ] Larghezza della cupola nella versione mobile: misurarla sul nodo `3:1322` (desktop già misurata, nodo `3:1739`).
- [ ] Taratura delle costanti `--r` dei titoli che si adattano alla larghezza (vedi `decorations.md`), con i font Adobe già caricati.
- [ ] Meta description, favicon, immagine og.
