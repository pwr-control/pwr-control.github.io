# pwr-control.com — sito statico

Rifacimento del sito, settembre 2026. HTML e CSS puri, nessun framework, nessun build step:
si apre e si modifica in Dreamweaver e si pubblica su GitHub Pages così com'è.

## Struttura

```
index.html                 Home
projects.html              Elenco progetti (5 sezioni con ancore: #dcdc #inverters #grid #control #teaching)
notes.html                 Note tecniche (PDF ospitati su GitHub)
about.html                 Bio, competenze, pubblicazioni, contatti
404.html                   Pagina "non trovata" (GitHub Pages la usa da sola)
projects/<slug>.html       Una pagina per progetto (14)
Templates/main.dwt         Template Dreamweaver: testata, menu e piè di pagina di tutte le pagine
css/style.css              Unico foglio di stile (colori e font nelle variabili in :root)
img/logo.svg               Logo (spirale) — da images/pwr-control_logo.svg del repo pwr-control
img/favicon.png, apple-touch-icon.png
img/preview/*.jpg          Anteprime 1000 px (le stesse del README GitHub)
img/figures/*.jpg          Figure dei progetti, ridotte a 1800 px per il web
img/figures/*.svg          Schemi segnaposto disegnati a mano per i progetti senza figura
                           (grid_forming, pmsm_sensorless, adaptive_control, string_actuated)
CNAME                      "pwr-control.com" — dominio custom per GitHub Pages
.nojekyll                  Dice a GitHub Pages di non passare i file per Jekyll
robots.txt, sitemap.xml
```

I PDF delle note **non** sono copiati nel sito (sono ~50 MB): i link puntano ai file nel repo
`pwr-control/pwr-control` su GitHub (`.../blob/main/docs/...` apre il viewer, `?raw=true` scarica).
Se preferisci ospitarli qui, copia la cartella `docs/` del repo nella radice del sito e sostituisci
`https://github.com/pwr-control/pwr-control/blob/main/docs/` con `docs/` nei link.

## Dreamweaver

1. **Site > New Site**: nome `pwr-control`, *Local Site Folder* = questa cartella. La cartella
   `Templates/` deve stare nella radice del sito (è già così).
2. Tutte le pagine sono istanze di `Templates/main.dwt`. Le regioni modificabili sono tre:
   `doctitle` (titolo e meta description), `head` (CSS o script extra della singola pagina) e
   `main` (tutto il contenuto). Testata, menu e piè di pagina sono bloccati: si modificano nel
   template e Dreamweaver propaga a tutte le pagine (**Modify > Templates > Update Pages**).
3. Il menu evidenzia da solo la sezione corrente (piccolo script in fondo al template).
4. **Nuovo progetto**: duplica una pagina in `projects/` (es. `dab.html`), cambia titolo, testo,
   tabella "At a glance" e link; metti la figura in `img/figures/`; aggiungi una card nella sezione
   giusta di `projects.html` (copia un blocco `<a class="card">…</a>`) e, se vuoi, una riga in
   `sitemap.xml`. I link "← precedente / successivo →" in fondo alla pagina sono a mano.
5. **Nuova nota**: una riga nella tabella di `notes.html`.
6. Colori, font e larghezza massima si cambiano in `css/style.css`, blocco `:root`.
   I font (IBM Plex Sans / Mono) vengono da Google Fonts; se non si caricano il sito usa i
   font di sistema.

Le pagine funzionano anche senza template (i commenti `InstanceBegin…` sono inerti): se non vuoi
usare i template di Dreamweaver, ignora la cartella `Templates/`.

## Pubblicazione su GitHub Pages

1. Crea il repository `pwr-control/pwr-control.github.io` (pubblico) e carica il contenuto di
   questa cartella nella radice (branch `main`). Da Dreamweaver si può usare l'integrazione git
   (**Site > Manage Sites > Associate a Git repository**) oppure GitHub Desktop / riga di comando:

   ```bash
   cd pwr-control-site
   git init -b main
   git add .
   git commit -m "New site"
   git remote add origin https://github.com/pwr-control/pwr-control.github.io.git
   git push -u origin main
   ```

2. Su GitHub: **Settings > Pages**, *Source: Deploy from a branch*, branch `main`, cartella `/ (root)`.
3. Sempre in **Settings > Pages > Custom domain** scrivi `pwr-control.com` (il file `CNAME` è già
   nel repo) e, appena il certificato è pronto, spunta **Enforce HTTPS**.
4. DNS del dominio (dove hai registrato pwr-control.com):
   - record `A` per `@` (apex) verso i quattro indirizzi di GitHub Pages:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - record `CNAME` per `www` verso `pwr-control.github.io`
   - **rimuovi** i record che oggi puntano ad Adobe Portfolio, e in Adobe Portfolio scollega il
     dominio, altrimenti i due servizi si contendono il nome.
   La propagazione richiede da pochi minuti a qualche ora; GitHub mostra lo stato del dominio
   nella pagina Settings > Pages.
5. I vecchi indirizzi del sito Adobe Portfolio (`/work`, `/dab`, `/ups-6kva`, …) non esistono più:
   chi li apre vede `404.html` con i link alle nuove pagine. Se vuoi dei redirect veri, crea per
   ogni vecchio indirizzo una cartella con un `index.html` che contiene
   `<meta http-equiv="refresh" content="0; url=/projects/dab.html">`.

## Cosa manca / da completare a mano

- **About > Publications**: aggiungi titoli, coautori e link degli articoli PCIM Europe e ISIEA
  (c'è un commento HTML nel punto giusto).
- **UPS 6 kVA**: la descrizione è generica (sul vecchio sito c'era solo una riga); se hai
  specifiche o waveform in più, la pagina `projects/ups-6kva.html` è da arricchire.
- Le quattro figure SVG segnaposto vanno sostituite con figure vere quando le hai.
- Nessun cookie, nessun tracciamento, nessun banner: non serve l'informativa cookie che aveva
  Adobe Portfolio. Se un giorno aggiungi analytics, valuta di nuovo.
