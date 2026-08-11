# Bilancio

> Nota: il nome definitivo dell'app è ancora da decidere — quando lo scegli, basta sostituire "Bilancio" con il nome scelto in questo file e nel tag `<title>` di `bilancio.html`.

Un'app di gestione delle finanze e della casa, pensata per essere usata in coppia. È un unico file HTML autosufficiente (nessun server, nessuna build, nessuna dipendenza da installare) che si sincronizza tra due telefoni tramite un Gist GitHub privato.

## Sezioni

- **Home** — saldo del mese, andamento entrate/uscite, stato dei budget per categoria, ripartizione delle spese per importanza.
- **Movimenti** — registro completo di entrate e uscite, con filtri combinabili per tipo, categoria, importanza e periodo (anno/mese o intervallo di date libero).
- **Agenda** — due sotto-sezioni:
  - *Spese pianificate*: spese fisse ricorrenti (es. affitto, abbonamenti) e pianificazioni una tantum (es. assicurazione a febbraio), con promemoria automatico quando arriva la data.
  - *Scadenze documenti*: patente, carta d'identità, bollo, assicurazione, con avviso configurabile per ogni documento.
- **Dispensa** — lista della spesa organizzata per reparto, con livello di urgenza (Finito / In esaurimento).
- **Impostazioni** — categorie personalizzabili, budget mensili, sincronizzazione GitHub, esportazione dati.

Ogni spesa ha anche un livello di importanza (Essenziale / Normale / Superfluo) usato nei filtri e nel riepilogo della Home.

## Come usarla

Non serve installare nulla. Basta aprire `bilancio.html` in un browser mobile — su iOS e Android si può anche "Aggiungere alla schermata Home" per farla comportare come un'app (icona propria, si apre a schermo intero).

Tutti i dati vengono salvati in locale sul dispositivo (`localStorage`). Senza sincronizzazione configurata, l'app funziona comunque normalmente: resta semplicemente "isolata" su quel telefono.

## Pubblicarla su GitHub Pages (opzionale)

Se preferisci avere un link invece di aprire il file da locale:

1. Crea un repository GitHub e carica `bilancio.html`.
2. Vai su **Settings → Pages**, scegli il branch (es. `main`) e la cartella root.
3. Dopo qualche minuto l'app sarà raggiungibile su `https://<tuo-utente>.github.io/<repo>/bilancio.html`.

## Configurare la sincronizzazione tra due telefoni

I Gist privati di GitHub possono essere scritti via API solo dall'account proprietario: non esiste una "scrittura condivisa" tra due account diversi. La soluzione più semplice è che entrambi usiate **lo stesso token** e **lo stesso Gist**.

**Passo 1 — Crea un token GitHub**
1. Su GitHub: **Settings → Developer settings → Personal access tokens → Tokens (classic) → Generate new token**.
2. Assegna solo il permesso **`gist`** (nessun altro scope è necessario).
3. Copia il token generato (inizia con `ghp_...`) — GitHub lo mostra una sola volta.

**Passo 2 — Crea il Gist condiviso**
1. Apri l'app, vai su **Impostazioni → Sincronizzazione**.
2. Incolla il token nel campo apposito.
3. Premi **"Crea nuovo Gist"**. L'app genererà un ID Gist e lo salverà in automatico.

**Passo 3 — Collega il secondo telefono**
1. Sull'altro telefono, apri l'app e vai su **Impostazioni → Sincronizzazione**.
2. Incolla lo **stesso token** e lo **stesso ID Gist** (visibile nelle Impostazioni del primo telefono, oppure nell'URL del Gist su gist.github.com).
3. Premi **"Sincronizza ora"**.

Da questo momento entrambi i telefoni leggono e scrivono sullo stesso Gist. La sincronizzazione parte automaticamente all'apertura dell'app e ogni volta che torna in primo piano (ad esempio quando sblocchi il telefono e la ritrovi già aperta); resta comunque disponibile il pulsante "Sincronizza ora" per forzarla manualmente.

In caso di modifiche fatte sui due telefoni offline nello stesso momento, l'app fa il merge automaticamente tenendo la versione più recente di ogni singola voce (in base alla data di ultima modifica), quindi non si perdono dati.

## Sicurezza e privacy

- Il token non è mai scritto nel codice dell'app: resta solo nel `localStorage` del dispositivo su cui lo inserisci.
- Il token ha permesso solo su `gist`: non dà accesso a repository, email o altre parti dell'account GitHub.
- Il Gist è privato (non pubblico): è visibile solo a chi ha il link diretto o l'accesso all'account che lo ha creato, ma tenendo presente che chiunque abbia token e ID può leggerlo/scriverlo — condividili solo con la persona con cui vuoi condividere i dati.

## Backup dei dati

Da **Impostazioni → Dati** è possibile:
- esportare i movimenti in **CSV**;
- esportare/importare un **backup JSON completo** (categorie, budget, movimenti, pianificazioni, scadenze, dispensa), utile per spostare i dati su un altro dispositivo o come copia di sicurezza indipendente dal Gist.

## Struttura del progetto

```
bilancio.html   → l'intera app: markup, stile e logica in un solo file
README.md       → questo file
```

Non ci sono altre dipendenze, pacchetti o passaggi di build: modificare l'app significa semplicemente modificare `bilancio.html`.
