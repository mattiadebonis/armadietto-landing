# Cosa Armadietto fa al posto tuo

La mappa degli automatismi dell'app (codice su `staging`, 13/11/2026), ordinata per il
pensiero che toglie. È la materia prima per ripensare la landing: il prodotto che
vendiamo è lo sgravio cognitivo e il controllo della situazione, non le funzioni.

## 1. Sapere cosa hai in casa

| Prima lo facevi tu | Ora lo fa Armadietto | Dove nel codice |
|---|---|---|
| Copiare nome, dosaggio, quante compresse ci sono | Inquadri la scatola: la riconosce dal catalogo dei farmaci AIFA (12.501 farmaci, 158.264 confezioni) e ne legge nome, principio attivo, forma, dosaggio e unità per confezione | Fase 69, `ScanRecognizedFace`, `ResolveScan` |
| Leggere e segnarti la scadenza | La legge dalla scatola; ti chiede solo quello che non ha letto | Fase 49, `AddStepRules` |
| Tenere in testa quale scatola stai usando | Le scatole di riserva in fila: quando una finisce passa da sola alla successiva | Fase 35, `ReserveRules` |
| Cercare il bugiardino | Foglio illustrativo e scheda tecnica AIFA a un tocco | Fase 63 |

## 2. Contare

| Prima | Ora |
|---|---|
| Contare le pastiglie rimaste | La scorta scende da sola con le dosi previste («≈ 83 compresse»); la ricontiamo solo se vuoi |
| Calcolare quando finisce | Il giorno esatto, anche con più schemi, terapie a scalare, più dosaggi, più persone sulla stessa scatola |

## 3. Ricordarti quando muoverti

| Prima | Ora |
|---|---|
| Accorgerti che sta finendo | Ti avvisa N giorni prima (1–30, scegli tu), anche contando solo i giorni lavorativi e saltando i festivi |
| Ricordare le scadenze | Avviso prima che scada |
| Capire cosa fare e in che ordine | «Da sistemare»: un posto solo, per urgenza, col verbo pronto — Compra · Chiedi ricetta · Butta |
| Chiederti se serve la ricetta | Lo sa dal catalogo, e cambia il verbo da sé |
| — | Quando non c'è niente da fare lo dice: «Tutto sotto controllo · Bastano tutti per almeno 14 giorni · Ti avviso tra 5 giorni per…» |

## 4. La ricetta

| Prima | Ora |
|---|---|
| Scrivere al medico l'elenco, le dosi, quando finiscono | «Scrivi al medico»: il messaggio è già scritto (farmaci, quando finiscono, quante al giorno, la tua firma), il medico preso dai Contatti, lo mandi con un tocco |
| Ricordare quante confezioni copre la ricetta che hai in mano | «Ho una ricetta»: ogni scatola nuova ne scala una — «Hai la ricetta · 2 confezioni fino al 7 dicembre» |

## 5. La farmacia

| Prima | Ora |
|---|---|
| Fare la lista | «In farmacia»: la lista è pronta, anche sulla schermata di blocco (Live Activity) da spuntare al banco |
| Cercare una farmacia | La più vicina, col percorso |
| Aggiornare le scorte dopo | «Comprata» a un tocco: la scorta riparte e il conto pure |

## 6. Prenderle

| Prima | Ora |
|---|---|
| Ricordare l'ora | Promemoria all'ora giusta: silenzioso, notifica o sveglia; due terapie alla stessa ora fanno una notifica sola |
| Spostare tutti gli orari se cambia la giornata | I «momenti» (Mattina 8:00…): sposti il momento, tutte le terapie agganciate lo seguono |

## 7. Le altre persone

| Prima | Ora |
|---|---|
| Tenere a mente le terapie di figli o genitori | Ogni terapia ha la sua persona, col suo colore; filtri per persona; vedi le loro scorte accanto alle tue |

## 8. Fuori dall'app

Widget, Siri, Spotlight, il controllo che apre lo scanner, e le cose da fare che escono
da sole in Promemoria, Todoist o TickTick.

## 9. Niente da perdere

Ogni eliminazione si annulla; backup ogni giorno su iCloud Drive (opzionale); funziona
offline; i dati restano sul telefono e in iCloud.

## Attenzione alle promesse

- Il catalogo AIFA nell'app è del 20 luglio 2026 e oggi non si aggiorna (workflow
  `aifa-catalog` senza `CATALOG_CSV_URL`, `CatalogUpdater` spento): non scrivere
  «aggiornato».
- Live Activity, widget e sync con Todoist/TickTick esistono nel codice: verificare cosa
  entra nella prima beta prima di metterli in pagina.

## Proposta: la landing come «un mese in cui non ci pensi»

Il filo: dopo due gesti, il lavoro passa a lui. Mostrarlo nel tempo rende tangibile lo
sgravio meglio di un elenco di funzioni.

1. **Hero** — la promessa. «Le medicine di casa, senza pensarci.» Sotto: «Armadietto
   conta, calcola e ti avvisa. Tu vedi solo cosa fare, quando serve.» Visivo: la lista con
   «Da sistemare».
2. **Le cose che smetti di fare** — sei righe «prima / ora», le più pesanti: contare le
   pastiglie · ricordare le scadenze · accorgerti che serve la ricetta · scrivere al medico ·
   fare la lista per la farmacia · tenere a mente le terapie degli altri.
3. **Due gesti** — scansioni la scatola, dici come la prendi (i componenti animati).
4. **Poi lavora lui: un mese** — una linea del tempo coi componenti:
   giorno 1 scansione · ogni mattina il promemoria · giorno 21 «finisce tra 7 giorni» e il
   messaggio al medico già scritto · giorno 23 «Hai la ricetta» · in farmacia la lista sulla
   schermata di blocco · «Comprata» e il conto riparte.
5. **Un posto solo da guardare** — «Da sistemare» coi tre verbi, e lo stato
   «Tutto sotto controllo»: il controllo che si vende.
6. **Anche per chi assisti** — le persone, i colori, le scorte accanto.
7. **Fiducia** — catalogo AIFA (senza promettere aggiornamenti), dati sul telefono.
8. **Domande e iscrizione.**

## Proposte per l'app: far vedere lo sgravio anche dentro

Oggi l'app fa molto lavoro invisibile e lo racconta poco. Le proposte rendono visibili il
controllo («è tutto a posto, fino a quando») e il lavoro fatto per te («ci penso io, ecco
il prossimo passo»). Ognuna dice cosa c'è oggi su `staging`.

1. **La testata dice lo stato, non il conteggio.** Oggi: «Medicinali 11». Proposta: sotto
   il titolo una riga sola — «Tutto sotto controllo fino al 21 novembre» oppure «2 cose da
   sistemare · la prima entro venerdì». È la prima cosa che si legge aprendo l'app: il
   controllo a colpo d'occhio, senza scorrere fino a «Da sistemare».
2. **Dalla notifica scorte al medico in un tocco.** Oggi l'avviso di un farmaco con ricetta
   dice «Serve la ricetta: chiedila al medico» ma le azioni sono «Comprato», «Domani»,
   «Una/Due confezioni». Proposta: per i farmaci con ricetta l'azione «Scrivi al medico»,
   che apre il messaggio già scritto. Il flusso più prezioso dell'app oggi è a tre passi
   dalla notifica che lo motiva.
3. **La ricetta che non arriva, ricordata da lui.** Oggi dopo due giorni lavorativi senza
   confezione la riga lo segnala (`SistemareRules.isStale`), ma solo se apri l'app.
   Proposta: una notifica — «La ricetta della Levotiroxina non è ancora arrivata. Richiami
   il medico?» con «Scrivi al medico». Chiude il cerchio: non devi ricordarti di
   ricordartelo.
4. **Ogni gesto dice il passo successivo.** Oggi «Comprata» mostra il toast con «Annulla».
   Proposta: il toast dice anche cosa farà lui — «Fatto. Ti riavviso il 12 gennaio.» Lo
   stesso dopo «Chiedi ricetta» («Ti ricordo giovedì se non arriva») e dopo «Butta». È il
   momento in cui l'utente sente di aver passato la mano.
5. **Il lavoro fatto per te, una riga a settimana.** Proposta: nel vuoto di «Da sistemare»
   (o in fondo alla lista) una riga grigia — «Questa settimana ho scalato 23 compresse e
   preparato 1 avviso». Rende visibile il lavoro invisibile, senza rumore.
6. **Un riepilogo facoltativo la domenica sera.** Proposta, spenta di default: «Settimana
   tranquilla: niente da fare» oppure «Questa settimana: 1 ricetta da chiedere, 1 scatola
   da comprare». Chi gestisce più persone pianifica una volta, non sette.

Da evitare: aggiungere schermate o grafici. Lo sgravio si vende togliendo, non mostrando
di più: ogni proposta qui è una frase in un posto che esiste già.
