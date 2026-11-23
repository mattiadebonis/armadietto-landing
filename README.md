# Landing con la lista d'attesa

Pagina statica, senza build: `index.html`, `privacy.html` e le due icone ricavate dall'icona dell'app
(`App/Resources/Assets.xcassets/AppIcon.appiconset/AppIcon.png` nel repo Armadietto) (`sips -z 180 180` e
`sips -z 512 512`). Non tocca l'app né il backend di sincronizzazione: le email della lista
d'attesa non passano da Supabase.

## La pagina

Costruita sui momenti in cui l'app fa vedere il suo valore, nell'ordine in cui arrivano:

1. **Primo schermo**: titolo, modulo e, accanto, un telefono fermo sulla schermata di
   blocco con la notifica «Ramipril 5 mg finisce il 7 febbraio». Sotto i 900 px solo la
   notifica, senza il telefono, subito dopo il modulo. Niente animazione: i passaggi sono
   in «Come funziona».
2. **Ti riconosci?**: tre situazioni (terapia, scorta, chi assisti); ognuna ha la sua
   risposta più giù.
3. **Come funziona**: un mese in cinque scene (l'inquadratura, la risposta «Finisce il…»,
   l'avviso, il messaggio al medico, «L'ho comprata»).
4. **Per chi assisti**, **Le medicine di scorta**, **I tuoi dati**, **La beta** (sparisce
   dopo il 15 dicembre), **Domande**, il modulo di nuovo.

I componenti dell'app sono disegnati in HTML coi colori di `Shared/Theme.swift`
(`ListaToken.action`, `actionSolid`, `actionFill`, le tinte delle persone), non sono
screenshot: un cambio di colore o di testo nell'app va riportato qui a mano.

### Lo scenario d'esempio

Tutti i numeri vengono da un solo caso, calcolato con le regole dell'app (`LeadCalendar`,
`StockForecast.coverageDays`, `NotificationCopy`, `SistemareRules.doctorMessage`), così
tornano tra una scena e l'altra:

- Ramipril 5 mg, 28 compresse, 1 alle 8:00, inquadrato lunedì 11 gennaio 2027:
  l'ultimo giorno coperto è domenica 7 febbraio («Finisce il 7 febbraio»).
- «Quanti giorni prima» a 7, lavorativi: il promemoria è giovedì 28 gennaio.
- Quel giorno alle 9:00 la notifica dice «Ramipril 5 mg finisce il 7 febbraio» ·
  «Scorte · ne restano 10», e il messaggio al medico «Ne restano per 10 giorni».
- Venerdì 29 gennaio la riga di «Da sistemare» dice «≈ 9 compresse», «9 giorni» in
  arancione, «L'ho comprata» · «L'ho prenotata» e «Ricetta chiesta ieri»; dopo «L'ho
  comprata» (28 in più) «37 compresse» e «37 giorni», senza «≈» perché la scorta è appena
  contata. Non lunedì 1 febbraio: a due giorni lavorativi dalla richiesta la ricetta è
  «vecchia» (`SistemareRules.isStale`) e il bottone pieno diventa «Chiedi di nuovo».

I mockup copiano l'app (Fase 82) misurata sul simulatore: il mirino della fotocamera con la
scatola e la scatola riconosciuta (si anima una volta quando arriva sullo schermo, come
«L'ho comprata», con «Rivedi»), il passo «Come lo prendi» del primo avvio con la risposta «Finisce il… · Promemoria il…», la notifica sulla schermata di
blocco, le righe di `SistemareRowView` (nome in grassetto solo con un bottone, bottoni a
capsula, il grigio col testo nero) e il foglio di `WriteToDoctorSheet`. Le misure stanno
in `--u` (punti dell'app per pixel della pagina: 0,85 nelle schede).

Nei componenti solo principi attivi, mai nomi di marca.

### Cosa non c'è

La domanda «Per quante persone tieni le medicine?» dopo l'iscrizione: un secondo invio allo
stesso modulo di Brevo col doppio opt-in rischia una seconda mail di conferma. Se serve, va
nella mail di benvenuto di Brevo (un modulo di aggiornamento del profilo) e nell'informativa.

## Raccolta delle iscrizioni

Il modulo manda i campi a un servizio di email con doppio opt-in, indicato in
`<meta name="waitlist-endpoint" content="">` in `index.html`. Vuoto, la pagina resta in
anteprima e non spedisce niente.

Servizio consigliato: Brevo (UE, piano gratuito, doppio opt-in, liste e invii).

1. Brevo › Contatti › Attributi: aggiungere `BETA` (booleano).
2. Brevo › Moduli › nuovo modulo d'iscrizione con doppio opt-in verso la lista
   «Lista d'attesa», con i campi `EMAIL`, `BETA` e la casella `OPT_IN`.
3. Dal codice d'incorporamento del modulo copiare l'URL dell'attributo `action`
   (`https://….sibforms.com/serve/…`) in `waitlist-endpoint`. La pagina aggiunge `isAjax=1` e legge la risposta JSON di Brevo, così un rifiuto non passa per un’iscrizione riuscita.
4. Compilare i segnaposto evidenziati in `privacy.html` (titolare, indirizzo, email,
   fornitore).

Campi spediti: `EMAIL`, `BETA`
(`1`), `OPT_IN` (`1`), `email_address_check` (trappola per i bot, sempre vuota), `locale`.
Nessun dato sanitario.

## Pubblicazione

GitHub Pages dal branch `main`, cartella radice (`.nojekyll` evita Jekyll):
https://mattiadebonis.github.io/armadietto-landing/

Dominio proprio (`armadietto.app` o simile): un file `CNAME` con il dominio nella radice,
poi nel DNS quattro record A verso 185.199.108.153, 185.199.109.153, 185.199.110.153,
185.199.111.153 e `www` CNAME verso `mattiadebonis.github.io`; in Settings › Pages
spuntare «Enforce HTTPS». Lo stesso dominio serve per il «Sito web di supporto» e
l'«URL della privacy policy» in App Store Connect.

Prima nel repo dell'app (`landing/`), spostata qui il 21/11/2026.

## La pagina

Costruita sui momenti in cui l'app fa vedere il suo valore, nell'ordine in cui arrivano:

1. **Primo schermo**: titolo, modulo e, accanto, un telefono fermo sulla schermata di
   blocco con la notifica «Ramipril 5 mg finisce il 7 febbraio». Sotto i 900 px solo la
   notifica, senza il telefono, subito dopo il modulo. Niente animazione: i passaggi sono
   in «Come funziona».
2. **Ti riconosci?**: tre situazioni (terapia, scorta, chi assisti); ognuna ha la sua
   risposta più giù.
3. **Come funziona**: un mese in cinque scene (l'inquadratura, la risposta «Finisce il…»,
   l'avviso, il messaggio al medico, «L'ho comprata»).
4. **Per chi assisti**, **Le medicine di scorta**, **I tuoi dati**, **La beta** (sparisce
   dopo il 15 dicembre), **Domande**, il modulo di nuovo.

I componenti dell'app sono disegnati in HTML coi colori di `Shared/Theme.swift`
(`ListaToken.action`, `actionSolid`, `actionFill`, le tinte delle persone), non sono
screenshot: un cambio di colore o di testo nell'app va riportato qui a mano.

### Lo scenario d'esempio

Tutti i numeri vengono da un solo caso, calcolato con le regole dell'app (`LeadCalendar`,
`StockForecast.coverageDays`, `NotificationCopy`, `SistemareRules.doctorMessage`), così
tornano tra una scena e l'altra:

- Ramipril 5 mg, 28 compresse, 1 alle 8:00, inquadrato lunedì 11 gennaio 2027:
  l'ultimo giorno coperto è domenica 7 febbraio («Finisce il 7 febbraio»).
- «Quanti giorni prima» a 7, lavorativi: il promemoria è giovedì 28 gennaio.
- Quel giorno alle 9:00 la notifica dice «Ramipril 5 mg finisce il 7 febbraio» ·
  «Scorte · ne restano 10», e il messaggio al medico «Ne restano per 10 giorni».
- Venerdì 29 gennaio la riga di «Da sistemare» dice «≈ 9 compresse», «9 giorni» in
  arancione, «L'ho comprata» · «L'ho prenotata» e «Ricetta chiesta ieri»; dopo «L'ho
  comprata» (28 in più) «37 compresse» e «37 giorni», senza «≈» perché la scorta è appena
  contata. Non lunedì 1 febbraio: a due giorni lavorativi dalla richiesta la ricetta è
  «vecchia» (`SistemareRules.isStale`) e il bottone pieno diventa «Chiedi di nuovo».

I mockup copiano l'app (Fase 82) misurata sul simulatore: il mirino della fotocamera con la
scatola e la scatola riconosciuta (si anima una volta quando arriva sullo schermo, come
«L'ho comprata», con «Rivedi»), il passo «Come lo prendi» del primo avvio con la risposta «Finisce il… · Promemoria il…», la notifica sulla schermata di
blocco, le righe di `SistemareRowView` (nome in grassetto solo con un bottone, bottoni a
capsula, il grigio col testo nero) e il foglio di `WriteToDoctorSheet`. Le misure stanno
in `--u` (punti dell'app per pixel della pagina: 0,85 nelle schede).

Nei componenti solo principi attivi, mai nomi di marca.

### Cosa non c'è

La domanda «Per quante persone tieni le medicine?» dopo l'iscrizione: un secondo invio allo
stesso modulo di Brevo col doppio opt-in rischia una seconda mail di conferma. Se serve, va
nella mail di benvenuto di Brevo (un modulo di aggiornamento del profilo) e nell'informativa.

## Raccolta delle iscrizioni

Il modulo manda i campi a un servizio di email con doppio opt-in, indicato in
`<meta name="waitlist-endpoint" content="">` in `index.html`. Vuoto, la pagina resta in
anteprima e non spedisce niente.

Servizio consigliato: Brevo (UE, piano gratuito, doppio opt-in, liste e invii).

1. Brevo › Contatti › Attributi: aggiungere `BETA` (booleano).
2. Brevo › Moduli › nuovo modulo d'iscrizione con doppio opt-in verso la lista
   «Lista d'attesa», con i campi `EMAIL`, `BETA` e la casella `OPT_IN`.
3. Dal codice d'incorporamento del modulo copiare l'URL dell'attributo `action`
   (`https://….sibforms.com/serve/…`) in `waitlist-endpoint`. La pagina aggiunge `isAjax=1` e legge la risposta JSON di Brevo, così un rifiuto non passa per un’iscrizione riuscita.
4. Compilare i segnaposto evidenziati in `privacy.html` (titolare, indirizzo, email,
   fornitore).

Campi spediti: `EMAIL`, `BETA`
(`1`), `OPT_IN` (`1`), `email_address_check` (trappola per i bot, sempre vuota), `locale`.
Nessun dato sanitario.

## Pubblicazione

Qualsiasi hosting statico con HTTPS. Il più semplice: Cloudflare Pages o Netlify con la
cartella `landing/` come radice e un dominio proprio (es. `armadietto.app`). Lo stesso
dominio serve poi per il «Sito web di supporto» e l'«URL della privacy policy» in App
Store Connect.
