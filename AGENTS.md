## Chez Rosario

Sito vetrina a pagina singola (Astro + Tailwind v4, statico, nessun backend).

**Prima di scrivere codice leggi, in quest'ordine:**
1. `docs/brief.md`: contesto, stack, workflow, regole
2. `docs/design-tokens.md`: colori, font, scala tipografica, breakpoint
3. `docs/decorations.md`: strisce, cupola, bordi, titoli che si adattano alla larghezza (la parte più delicata)
4. `docs/sections.md`: sezione per sezione, con copy, misure e node id Figma

**Regole fisse**
- Le decorazioni (strisce, cupola, banner delle card) sono CSS, mai PNG.
- Non usare il codice generato da Figma così com'è (posizionamento assoluto): traducilo in flex/grid.
- Niente URL temporanei di Figma nel codice: gli asset stanno in `src/assets/`.
- Lavora una sezione alla volta e confronta con lo screenshot Figma a 375, 768 e 1440 px prima di passare alla successiva.
- Se un numero in Figma e un numero nei docs sono in conflitto, vale Figma. Per il comportamento fluido (cosa succede tra 375 e 1440) valgono i docs.

## Development

When starting the dev server, use background mode:

```
astro dev --background
```

Manage the background server with `astro dev stop`, `astro dev status`, and `astro dev logs`.

## Documentation

Full documentation: https://docs.astro.build

Consult these guides before working on related tasks:

- [Adding pages, dynamic routes, or middleware](https://docs.astro.build/en/guides/routing/)
- [Working with Astro components](https://docs.astro.build/en/basics/astro-components/)
- [Using React, Vue, Svelte, or other framework components](https://docs.astro.build/en/guides/framework-components/)
- [Adding or managing content](https://docs.astro.build/en/guides/content-collections/)
- [Adding styles or using Tailwind](https://docs.astro.build/en/guides/styling/)
- [Supporting multiple languages](https://docs.astro.build/en/guides/internationalization/)
