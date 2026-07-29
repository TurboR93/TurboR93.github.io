# Curriculum Vitae — Riccardo Brunello

Sito statico che raccoglie curriculum, progetti e contatti, pubblicato con
GitHub Pages su **https://turbor93.github.io**.

L'identità visiva riprende quella di [hAutomatico](https://hautomatico.com):
stessa palette (giallo `#FDF07A`, rosso `#D03F29`, fondo notte `#1A1A1A`),
stesso carattere PT Sans, stesse forme — pillole, divisori ondulati, card che
si sollevano.

---

## Cosa c'è dentro

| Pagina | File | A cosa serve |
|---|---|---|
| Home | `index.html` | Presentazione, ambiti di lavoro, invito al contatto |
| Curriculum | `cv.html` | Il CV vero e proprio, in HTML |
| Progetti | `progetti.html` | Portfolio con schede di dettaglio |
| Contatti | `contatti.html` | Modulo di contatto |
| Conferma | `grazie.html` | Pagina di atterraggio dopo l'invio |
| Privacy | `privacy.html` | Informativa sul trattamento dei dati |
| Errore | `404.html` | Pagina non trovata |

---

## Come è fatto

**Nessun JavaScript.** Nemmeno una riga: gli effetti sono tutti in CSS, il menu
mobile è un elemento `<details>` nativo e il modulo di contatto è un normale
invio `POST`. Il sito funziona a script disattivati.

- **Sass** — 12 file sorgente organizzati in `abstracts`, `base`, `layout`,
  `components`, `pages`; compilati in un unico foglio di stile.
- **Bootstrap 5** — importato dai sorgenti Sass, non dalla CDN, così i suoi
  breakpoint vengono riscritti su quelli di hAutomatico (640/768/1024/1280/1536)
  prima della compilazione. Vengono inclusi solo i moduli usati davvero:
  normalizzazione, griglia, contenitori e classi di utilità.
- **CSS Grid e Flexbox** — Grid per l'impaginazione del curriculum e delle
  griglie di card, Flexbox per barre, gruppi di bottoni e liste di etichette.
- **Animazioni legate allo scorrimento** — `animation-timeline: view()` e
  `scroll()` per comparse, parallassi e barra di avanzamento della lettura.
  Vivono dentro un blocco `@supports`: dove non sono riconosciute, la pagina
  appare semplicemente completa e ferma.
- **`prefers-reduced-motion`** — chi ha attivato la riduzione del movimento nel
  sistema operativo vede il sito immobile.
- **Foglio di stampa** — da `cv.html` il comando di stampa produce un CV su
  fondo bianco, senza menu né decorazioni, con gli indirizzi dei collegamenti
  resi espliciti.

---

## Sviluppo in locale

```bash
npm install          # installa sass e bootstrap
npm run css          # compila una volta, in forma leggibile
npm run css:watch    # ricompila a ogni salvataggio
npm run build        # compila minificato, per la pubblicazione
npm run serve        # apre un server locale su http://localhost:4173
```

Il CSS compilato (`assets/css/main.css`) **è versionato di proposito**: GitHub
Pages serve file statici e non compila Sass, quindi il foglio di stile deve
essere già pronto nella repository.

---

## Attivazione del modulo di contatto

Il modulo si appoggia a [FormSubmit](https://formsubmit.co), lo stesso servizio
usato dal sito hAutomatico. Non richiede registrazione né chiavi API, ma va
attivato una volta sola.

1. Apri `contatti.html` e sostituisci temporaneamente `CHIAVE_FORMSUBMIT`
   nell'attributo `action` con l'indirizzo email di destinazione.
2. Pubblica il sito e invia un messaggio di prova dal modulo.
3. Arriva una email da FormSubmit con un pulsante di conferma: premilo.
   Nella stessa email trovi una **stringa personale** (il tuo alias).
4. Torna in `contatti.html` e metti quella stringa al posto dell'indirizzo:

   ```html
   <form action="https://formsubmit.co/xxxxxxxxxxxxxxxx" method="POST">
   ```

Il quarto passaggio non è un dettaglio: usare l'alias al posto dell'indirizzo
evita che la casella di posta resti scritta in chiaro nel sorgente della pagina,
dove i raccoglitori automatici la troverebbero in poche ore.

Protezioni già attive nel modulo: campo esca invisibile ai visitatori
(`_honey`), reindirizzamento alla pagina di conferma (`_next`), validazione
HTML5 su tutti i campi obbligatori.

---

## Pubblicazione

Ogni `push` sul ramo `main` fa partire il workflow in
`.github/workflows/deploy.yml`, che compila il Sass e pubblica su GitHub Pages.

Perché funzioni, in **Settings → Pages** la voce *Source* dev'essere impostata
su **GitHub Actions**.

---

## Cosa manca

- [x] Fotografia ritratto — in `assets/img/me/`, due misure servite con `srcset`
- [x] Esperienze lavorative e formazione complete in `cv.html`
- [ ] Livello di inglese: indicato come "Professionale", da confermare
- [ ] Attivazione di FormSubmit (procedura qui sopra): finché manca, il modulo non recapita
- [ ] Schermate del progetto mooVe (ora ha una copertina tipografica)

I punti sono segnalati anche nei file, con commenti che iniziano per `⚠️`.

---

## Crediti

Palette, tipografia e stilemi derivati da [hautomatico.com](https://hautomatico.com).
Icone ridisegnate su misura, in SVG dentro il markup.
