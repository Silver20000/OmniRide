# Changelog - OmniRide 🏍️📊

Tutte le modifiche e le evoluzioni del firmware, delle app e dell'hardware di OmniRide (fino alla 3.6 chiamato RideLink).

---

## [4.7.1] - 2026-10-25
### Display (auto)
- **Stili del cruscotto**: Classico (contagiri ad arco), Racing (10 LED di cambiata, marcia gigante, giri in cifre) e Digitale (velocità grande, barra dei giri a segmenti, marcia nel riquadro). Si sceglie tenendo premuto il cruscotto per 1 secondo, oppure dall'app (*🏁 Stile del cruscotto*); la centralina auto lo tiene per tutti i display.
- **Auto ibride**: quando l'auto si muove in elettrico (motore spento) al posto della marcia compare "EV" in verde.
- Nuovo valore per i riquadri: **batteria ibrida %** (se l'auto la fornisce).

---

## [4.7.0] - 2026-10-25
### App
- **Parametri OBD (scansione)**: nuova pagina nel menu Auto con tutti i parametri OBD2 che l'auto fornisce, ognuno con il nome e il valore in tempo reale. Spunta quelli che vuoi vedere: compaiono nella pagina principale, sotto i valori soliti. "Scansiona di nuovo" richiede all'auto l'elenco aggiornato.

### Auto
- **Marcia dall'auto**: se l'auto la fornisce (parametro OBD "marcia inserita"), la marcia arriva direttamente dall'auto; altrimenti resta quella imparata da giri e velocità.
- **Collegamento all'adattatore più stabile**: tollera fino a 6 secondi di disturbo prima di considerarlo perso.
- Se l'adattatore salvato non c'è, un altro dispositivo che non si collega viene ignorato dopo 3 tentativi.

---

## [4.6.9] - 2026-10-24
### Auto
- **La centralina auto legge l'auto con gli adattatori vLinker (IOS-Vlink)**: l'adattatore riceveva i comandi ma le sue risposte non arrivavano mai (iscrizione alle notifiche senza conferma).
- **Adattatore ritrovato anche per nome**: molti adattatori cambiano indirizzo Bluetooth quando li stacchi e riattacchi. Se quello salvato non si sente per un minuto, la centralina prende qualsiasi adattatore OBD2.
- **Protocollo dell'auto**: se l'auto non risponde la centralina prova a turno i protocolli più comuni; quello che funziona viene ricordato e usato da allora in poi.
- **Giri più rapidi**: l'adattatore risponde appena ha la prima risposta, i giri vengono letti 2 volte su 3, tempi di attesa adattivi.
- Dopo 3 preparazioni dell'adattatore senza risposta la centralina si ricollega da capo; sulla porta seriale si vedono comandi e risposte.

### Display
- **Contagiri fluido**: lancetta e numero dei giri scorrono a ogni fotogramma verso l'ultimo valore letto; lo shift light usa il valore reale, senza ritardo.

---

## [4.6.8] - 2026-10-24
### Auto
- **Aggiornamenti più veloci dalla centralina auto** (per lei e per i display): pacchetti grandi come sulla centralina moto (517 byte), collegamento rapido con il telefono durante l'aggiornamento, adattatore OBD2 in pausa finché l'aggiornamento non finisce (i tentativi di collegamento bloccavano la radio per secondi) e meno pacchetti ai display nel frattempo.

---

## [4.6.7] - 2026-10-24
### Auto
- **Più portata verso l'adattatore OBD2**: il Bluetooth della centralina auto trasmette alla massima potenza (+9 dBm), così l'adattatore sente meglio la richiesta di collegamento.
- **Nomi nell'elenco "Scegli l'adattatore a mano"**: la ricerca usa tutta la radio per quei secondi e raccoglie i nomi dei dispositivi (es. "IOS-Vlink"). I dispositivi che non trasmettono un nome restano con il solo codice.
- Diagnostica sulla porta seriale della centralina: `l` elenca i dispositivi Bluetooth sentiti, `u<indirizzo>` sceglie l'adattatore.

Nota: gli adattatori Bluetooth LE accettano un solo collegamento alla volta. Se un'app OBD sul telefono è collegata all'adattatore, la centralina non può collegarsi: chiudila.

---

## [4.6.6] - 2026-10-24
### Auto
- **Corretto: il telefono si scollegava e ricollegava dalla centralina auto.** Mentre la centralina prova a collegarsi all'adattatore OBD2 la radio resta occupata qualche secondo: ora il collegamento con il telefono tollera fino a 8 secondi di silenzio.
- Dopo un tentativo fallito con l'adattatore la centralina aspetta di più prima di riprovare (da 1 fino a 20 secondi), lasciando respirare telefono e display.
- Un dispositivo trovato in automatico che non si collega per 3 volte viene ignorato per 5 minuti (spesso non è un adattatore OBD2). Per sceglierne uno preciso: *Impostazioni auto > Altro > Scegli l'adattatore a mano*.

### App
- Prima del collegamento l'app dice **"Collega la centralina"** (non sa ancora se è una moto o un'auto).

---

## [4.6.5] - 2026-10-24
### Auto
- **La centralina auto si aggiorna dall'app**, come quella della moto: collegati all'auto e vai in *Altro > Aggiornamento firmware*, compare "Centralina auto" insieme ai display. Ogni centralina accetta solo il proprio firmware.
- Le centraline auto già programmate prima della 4.6.5 vanno riprogrammate una volta via cavo (nuova divisione della memoria per gli aggiornamenti); poi basta l'app. Le centraline nuove si programmano sempre via cavo la prima volta.

---

## [4.6.4] - 2026-10-24
### Display
- **Schermata di attesa**: finché non sentono una centralina (moto o auto) tutti i display mostrano "IN ATTESA di collegamento", con le sole impostazioni del display.
- **Collegati alla centralina auto**: compaiono subito le pagine e i menu auto, con "--" al posto dei valori; una riga piccola dice cosa sta facendo la centralina con l'adattatore OBD2.
- **Benvenuto** senza nome della moto: solo "Benvenuto su OmniRide" e la versione.
- Pagine da mostrare scelte dall'app (vedi sotto).
- Corretto: in attesa c'erano due pagine uguali.

### Auto
- **Corretto: i display non sentivano la centralina auto.** A 15 dBm l'antenna della scheda ESP32-C3 li accecava: ora trasmette a 8,5 dBm, più che sufficienti in auto.
- La centralina prova l'adattatore per al massimo 4 secondi alla volta, così i display non la perdono.

### App
- **Scegli l'adattatore a mano**: in *Impostazioni auto > Altro* la centralina elenca i dispositivi Bluetooth che sente (★ quelli che sembrano adattatori OBD2) e tu scegli il tuo.
- **Valori nell'app**: l'elenco di tutti i valori che l'auto fornisce, con una spunta per scegliere quali vedere nella pagina principale.
- **Schermate del display**: in moto e in auto scegli quali pagine mostrano i display; la centralina tiene la scelta e la passa a tutti i display.

---

## [4.6.3] - 2026-10-24
### Auto
- **Aggiornamento dei display dall'app anche in auto.** La centralina OBD ora elenca i display collegati e li aggiorna, come fa la centralina moto. I display con la 4.6.3 si fanno vedere dalla centralina auto; quelli con una versione precedente vanno aggiornati una volta da cavo.
- La centralina auto non si può aggiornare dall'app (ha un firmware diverso da quello della moto): si aggiorna da cavo.

### App
- **Schermata iniziale più pulita**: finché non ti colleghi a una centralina vedi solo la scheda di connessione; voci e dati compaiono quando sei collegato.

---

## [4.6.2] - 2026-10-24
### App
- **Modalità auto completa**: quando l'app si collega alla centralina auto (`CAPS:car=1`), tutta l'interfaccia passa in versione auto.
  - La barra inferiore mostra la scheda "Auto" con icona dedicata, "Viaggi" al posto di "Giri", e la scheda SOS caduta viene nascosta.
  - Funzionalità disponibili in auto: computer di viaggio (km, media e consumo dall'OBD), "Dove ho parcheggiato" con percorso per ritrovarla, registrazione viaggio con mappa colorata per velocità (senza piega), aggiornamento firmware via Bluetooth, lettura/cancellazione errori (DTC) e scansione centraline (UDS).
  - Funzionalità moto rimosse in auto: angolo di piega, forze G, allarme caduta SOS, sensori TPMS, calibrazione del montaggio, 0-100 da IMU e inoltro notifiche/navigatore ai display.
  - Alla disconnessione o collegandosi alla moto, l'app torna automaticamente alla modalità moto.

### Auto (OBD Hub)
- **Corretto: crash e riavvio all'avvio dell'hub OBD**: inizializzazione della memoria NVS come prima operazione e stack Bluetooth LE NimBLE pronto con server GATT per l'app prima dell'avvio della scansione dell'adattatore OBD2.

---

## [4.6.1] - 2026-10-24
### App
- **Corretto: l'app si collegava sempre alla moto.** Se vede più centraline (moto e auto) ora chiede a quale collegarsi; se ne vede una sola si collega da sola.
- **Scansione centraline (auto)**: in *Impostazioni auto > Altro* legge gli errori di motore, cambio, ABS/ESP, airbag, quadro strumenti, gateway, servosterzo e clima, non solo quelli del motore. Tocca una centralina con errori per cancellarli.

### Auto
- Nuovi valori: **temperatura dell'olio** e **livello del carburante** (se l'auto li fornisce), sui display e nell'app.

---

## [4.6.0] - 2026-10-24
### Auto (nuovo)
- **OmniRide anche in auto**: una centralina OBD (ESP32-C3 o S3) si collega a un adattatore OBD2 Bluetooth LE e manda i dati ai display. Stesso firmware per tutti i display: con la centralina della moto mostrano le pagine moto, con quella OBD le pagine auto.
- **Cruscotto auto sui display**: contagiri con shift light, marcia (imparata da sola guidando), giri, velocità e una pagina con 6 riquadri a scelta (acqua, aria aspirata, acceleratore, carico motore, turbo, batteria, consumo).
- Si mostrano solo i valori che la tua auto fornisce davvero.

### App
- **Scheda Auto**: valori in tempo reale e impostazioni (shift light, riquadri dei display), salvate nella centralina OBD.
- **Errori del motore**: leggi gli errori memorizzati e quelli in attesa, cancellali (spegne la spia motore), leggi il numero di telaio.
- **All'apertura** l'app chiede a quale centralina collegarsi se ne vede più di una (moto e auto); se ce n'è una sola si collega da sola.

---

## [4.5.1] - 2026-10-11
### Centralina
- **Corretto: display che si scollegano o non si collegano.** Su molte schede ESP32-C3 SuperMini l'antenna lavora male alla potenza massima: misurato a 20 dBm, i display non ricevevano nessun pacchetto; da 15 dBm in giù li ricevono tutti. La radio verso i display ora trasmette a 15 dBm (11 dBm a batteria).
- Diagnostica sulla porta seriale: pacchetti inviati e ricevuti ogni 10 secondi, pause del ciclo principale, comando `w` per provare le potenze di trasmissione.

### Display
- **Piega in tempo reale**: tolta l'inerzia con cui il display "inseguiva" l'angolo; i dati arrivano sempre 50 volte al secondo, anche a batteria.
- **Barra della piega e archi con i bordi sfumati** e numero grande della piega sfumato, con l'"1" nella forma originale.
- Sensore del gas scollegato: niente più 100% finto, la barra sparisce.
- **Display più fluido**: segmenti e numeri sfumati più leggeri da disegnare, invio allo schermo più veloce (anche in modalità notte): da 18 a 28 fotogrammi al secondo sul rettangolare.
- **Corretto: piega in ritardo e sbagliata dopo il montaggio automatico.** Il montaggio veniva "imparato" anche maneggiando la centralina a moto ferma; ora impara solo durante la guida vera (GPS oltre 15 km/h). Se la piega non torna, in *Calibrazione* tocca "Riconosci di nuovo il montaggio".

---

## [4.5.0] - 2026-10-11
### Centralina
- **A batteria, senza fili alla moto**: con una batteria al litio ricaricata via USB-C la centralina funziona da sola. A batteria va in risparmio energetico (processore a 80 MHz, Bluetooth e radio dei display a potenza ridotta, radio in ascolto a intervalli), con la USB-C collegata va a piena potenza. Livello della batteria nell'app e sui display, avviso al 20% e al 10%.
- Tolto il supporto ai moduli 4G e GPS.
- Sensore del gas (TPS) solo sui prototipi: spento di serie, si attiva da *Altro > Modalità sviluppatore* (con password). Senza TPS la barra del gas non compare sui display. Spostato su GPIO 2: GPIO 7 sull'ESP32-C3 non legge tensioni.

### Display
- Icona della batteria della centralina nella barra in alto e avviso di batteria scarica.

---

## [4.4.0] - 2026-10-11
### Gomme
- **Sensori pressione gomme (TPMS Bluetooth)**: tappi sulle valvole letti dalla centralina, senza fili. Il display alterna la pressione alla riga della manutenzione e avvisa con un popup se una gomma scende sotto la pressione impostata (0,3 bar) o si sgonfia in fretta (foratura). Abbinamento e pressioni da mantenere in *Altro > Moto e display*; nella pagina Moto compare la scheda delle gomme solo se ci sono sensori abbinati.

### Display
- **Numeri e scritte più morbidi**: i caratteri grandi in grassetto (velocità, piega, tempi, titoli) ora hanno i bordi sfumati (antialiasing) invece dei gradini. Stesse dimensioni e posizioni di prima.

### App
- **Pagella del giro**: nella mappa del giro, punteggio di guida fluida, curve a destra e sinistra, le tre pieghe più forti, frenate in piega, gas chiuso di colpo in curva e un consiglio.
- **Novità della versione** nella pagina Aggiornamenti: dopo *Controlla* l'app mostra cosa c'è di nuovo nell'ultima versione.

---

## [4.3.0] - 2026-10-11
### Centralina
- **Montaggio automatico: la centralina si installa in qualsiasi verso** (in piedi, sdraiata, girata, sotto la sella, nel codone o nel cupolino), basta che sia fissata rigida. Impara da sola come è montata mentre guidi: la verticale dalla media delle forze, l'avanti dal giroscopio in curva (una moto inclinata in curva ruota sempre con una parte verso la sua destra). Dopo qualche minuto di guida con un po' di curve piega, accelerazioni, bussola e 0-100 sono giusti senza toccare impostazioni.
- Provato su uscite simulate con montaggi casuali: direzione entro circa 5 gradi.
- Contiene anche tutte le correzioni dalla 4.2.1 alla 4.2.7 (aggiornamenti più veloci e affidabili, stato del collegamento alla riapertura dell'app).

### App
- Calibrazione: stato del montaggio automatico e pulsante "Riconosci di nuovo il montaggio" (se sposti la centralina). Gli assi manuali valgono solo finché il montaggio non è riconosciuto.

---

## [4.2.7] - 2026-10-11
### App
- **Aggiornamento dei display di nuovo veloce**: la 4.2.6 lo aveva reso lentissimo togliendo anche il Bluetooth veloce. Ora il Bluetooth veloce è di nuovo attivo; resta solo la conferma per ogni pezzo, che lascia la radio libera per il display.

---

## [4.2.6] - 2026-10-11
### App e centralina
- **Aggiornamento dei display corretto**: si interrompeva dopo circa un minuto con "trasmissione al display interrotta". La centralina usa la stessa radio per il telefono e per i display, e l'invio veloce dal telefono la teneva occupata. Per i display l'app ora invia normalmente (il limite è comunque il collegamento col display); la centralina riprova più a lungo e, se fallisce, il messaggio dice il motivo. La centralina continua ad aggiornarsi in modo veloce. Aggiorna prima la centralina, poi i display.

---

## [4.2.5] - 2026-10-11
### Centralina
- **Aggiornamento dei display più affidabile**: si interrompeva spesso con un errore quando il display era lento a rispondere (stava scrivendo in memoria). Ora la centralina riconosce le risposte in ritardo, aspetta un po' di più e, se qualcosa va storto, sblocca subito il display (prima il tentativo successivo diceva "display non trovato"). Aggiorna prima la centralina, poi i display.

---

## [4.2.4] - 2026-10-11
### App
- **Corretto**: chiudendo e riaprendo l'app, la moto risultava "non collegata" anche se il collegamento in background era attivo (i dati arrivavano lo stesso). Ora la schermata mostra subito lo stato reale.

---

## [4.2.3] - 2026-10-11
### App e centralina
- **Aggiornamenti firmware più veloci**: l'app invia il firmware di seguito senza aspettare una conferma per ogni pezzo (una verifica ogni 8 kB) e la centralina sospende la telemetria durante il trasferimento. Alla fine l'app mostra quanti secondi ci ha messo. L'invio continuo vale dal secondo aggiornamento: la centralina deve già avere la 4.2.3.

---

## [4.2.1] - 2026-10-11
### App
- **Aggiornamenti di centralina e display più veloci**: durante il trasferimento l'app usa il Bluetooth alla massima velocità (intervallo corto e 2M), poi torna al collegamento a basso consumo.

---

## [4.2.0] - 2026-10-04
### iPhone
- **Notifiche dell'iPhone sui display, senza app**: la centralina usa il servizio Apple ANCS. Si abbina una volta da *Impostazioni → Bluetooth → OmniRide* (poi *Consenti* le notifiche) e da lì arrivano chiamate con il nome, chiamate perse, WhatsApp, SMS/iMessage, Telegram, Signal e le indicazioni di Google Maps (svolta, distanza, via).
- L'app Android e la web app funzionano come prima: un telefono Android non vede differenze.

### Display
- **Impostazioni più semplici**: all'apertura solo due pulsanti, MOTO e DISPLAY; ognuno apre il suo menu, con la barra "<" per tornare indietro.
- **Orientamento**: scegli di quanto ruotare lo schermo (90, 180 o 270 gradi) invece di cambiarlo a ogni tocco.
- Display rettangolare in orizzontale: "NAVIGAZIONE NON ATTIVA" ora è centrata sotto l'icona (prima finiva sul bordo destro).
- Tolta la scritta "LIVE" con gli Hz in alto: resta solo l'avviso quando manca il segnale.

### App
- **Mappa del giro**: toccando un punto del percorso il popup mostra ora, velocità, piega, G e gas di quel punto (prima era vuoto).
- **Pagina Moto più semplice**: in alto collegamento e cruscotto dal vivo, poi tre voci (Viaggio e manutenzione, Dove ho parcheggiato, 0-100); i controlli compaiono solo se c'è qualcosa da sistemare. Il nome della moto è in Altro > Moto e display.
- **Pagina Altro a menu**: sei voci chiare (Moto e display, Calibrazione, Notifiche, Registrazione, Aggiornamenti, Aiuto); ognuna mostra solo le sue impostazioni, con "Torna al menu" o il tasto indietro.

### 0-100 km/h
- **Partenza riconosciuta sempre**: funziona anche con il sensore montato al contrario (la direzione si impara dalla prima prova riuscita), con partenze dolci di frizione e se dondoli la moto prima di partire.
- Il tempo parte quando la moto comincia davvero a muoversi; si attiva più in fretta e non si disarma per i piccoli errori del GPS da fermo.
- Provato su partenze simulate (pendenze, vibrazioni, dondolii, frizione dolce, sensore al contrario, GPS impreciso, senza telefono): errore entro circa 0,2 s.

### Modulo 4G e GPS (facoltativi)
- **SMS di soccorso inviato dalla moto** con un modulo 4G A7670E e una SIM: parte anche con iPhone o con il telefono spento o rotto. Posizione dal GPS del modulo, altrimenti l'ultima del telefono. Se annulli dopo l'invio parte il "falso allarme".
- Con l'app Android collegata il telefono resta di riserva: niente SMS doppi, interviene solo se la moto non riesce a inviare (niente rete o SIM).
- **Contatti SOS salvati nella centralina**: l'app li invia da sola a ogni collegamento; nella web app c'è la nuova scheda *SMS dalla moto* (utile con iPhone). SMS di prova dalla moto: web app, oppure tieni premuto *SMS di prova* nell'app.
- **Modulo GPS** (ATGM336H, NEO-6M/M8N): velocità sui display e 0-100 anche senza telefono.
- I moduli si collegano a GPIO 6 e 10 e vengono riconosciuti da soli; lo stato (rete, segnale, satelliti) è nella web app e nella diagnostica dell'app.

---

## [4.1.2] - 2026-10-04
### Display
- Pagina 0-100: l'avviso "solo in pista o area chiusa" e gli altri messaggi non escono più dai bordi. Il testo si adatta da solo: carattere grande, medio o su due righe.

---

## [4.1.1] - 2026-10-04
### Centralina
- **0-100 km/h corretto**: il cronometro non partiva o si annullava da solo. Usava l'accelerazione "compensata" dal filtro dell'assetto, che in una partenza dritta scambia l'accelerazione per un beccheggio e la azzera in un decimo di secondo. Ora misura l'accelerazione grezza meno quella da fermo (pendenza e montaggio), corregge l'alzata della moto con il giroscopio e usa il tempo reale tra i campioni.
- Riconoscimento "fermo" e partenza robusti alle vibrazioni del motore; il cronometro parte dal primo istante della spinta; se la moto viene solo dondolata torna in attesa invece di annullare.
- Provato su partenze simulate (salita, discesa, vibrazioni, alzata, cambi marcia, senza telefono): errore entro circa 0,1 s.

---

## [4.1.0] - 2026-10-03
### App
- **Aggiornamenti automatici dell'app**: all'apertura OmniRide controlla se c'è una versione nuova, la scarica e la installa con un tocco (poi propone di aggiornare centralina e display).
- **Configurazione guidata** al primo avvio: permessi spiegati uno per uno, collegamento, nome della moto, contatto SOS, zero piega (si può rifare da Altro).
- **Cruscotto dal vivo** nella scheda Moto: arco della piega con i picchi, cerchio delle forze G con la scia, barra del gas.
- **Scheda del giro da condividere**: immagine con tracciato colorato per piega e i numeri principali, pronta per WhatsApp e Instagram.
- **Inglese** (segue la lingua del telefono) e testi rifiniti con gli accenti; **km o miglia** a scelta.
- **Invia diagnostica**: un file per l'assistenza, con numeri di telefono e posizioni oscurati.
- APK più leggero (2 MB invece di 7), Android 15.

### Display e centralina
- Con le miglia scelte nell'app, le pagine Viaggio e Navigatore mostrano mph e mi.

### Web app
- **Stessa struttura e stesso aspetto dell'app**: schede Moto, SOS, Giri, Altro con la barra in basso e lo stato del collegamento in alto.
- Corretto: alcune impostazioni comparivano sotto tutte le pagine.

---

## [4.0.1] - 2026-10-01
### Novita'
- **App scaricabile**: l'APK di OmniRide si trova nelle release di questa pagina (`omniride.apk`), insieme ai firmware.
- **Web app**: la pagina Impostazioni non compare piu' sotto tutte le altre pagine.
- L'app installata da qui si aggiorna con le versioni successive senza doverla disinstallare.

---

## [4.0.0] - 2026-10-01
### Nuovo nome: OmniRide
- Progetto, app, web app, display ("Benvenuto su OmniRide"), nome Bluetooth della centralina ("OmniRide <modello>"), documentazione e repository GitHub rinominati **OmniRide**.
- L'app Android ha un nuovo identificativo (`com.omniride.app`): va installata come app nuova (disinstalla la vecchia RideLink). Contatti SOS, giri e impostazioni dell'app vanno reinseriti.
- Le impostazioni salvate in centralina e display (calibrazioni, orientamento, abbinamenti, luminosita') e i dati della web app restano: non serve rifare niente.
- App e web app trovano anche le centraline che si chiamano ancora "RideLink", per poterle aggiornare.

---

## [3.6.0] - 2026-10-01
### Consumi
- **Standby della centralina piu' leggero**: ogni controllo del movimento e' un riavvio completo (~0,2 s a ~20 mA), quindi ora diventano piu' radi man mano che la moto resta ferma: ogni 3 s nei primi 20 minuti, poi 10 s, 30 s dopo due ore, 60 s dopo un giorno. Il consumo medio in standby scende di 3-10 volte.
- **Risveglio dal sensore (GY-87)**: collegando il pin INTA del GY-87 al GPIO 5, l'accelerometro resta in ascolto a basso consumo e sveglia la centralina solo quando la moto si muove (standby di pochi microampere; il timer resta come sicurezza ogni 2 minuti). Il collegamento viene riconosciuto da solo.
- **App**: il GPS del telefono si spegne dopo 3 minuti senza moto collegata (parcheggio, standby) e si riaccende al ricollegamento. Resta acceso se stai registrando un giro a mano o durante un allarme caduta.

---

## [3.5.0] - 2026-10-01
### Piu' moto vicine
- **Abbinamento display-centralina**: ogni display ascolta solo la sua centralina (riconosciuta dall'indirizzo radio) e le manda i comandi direttamente, quindi piu' moto RideLink possono stare vicine senza mescolare i dati. Un display mai abbinato si abbina da solo alla prima centralina che sente; per cambiarla: Impostazioni > DISPLAY > Abbina centralina (sceglie quella in modalita' abbinamento dall'app, altrimenti quella col segnale piu' forte).
- Gli aggiornamenti firmware arrivano solo ai display abbinati a quella centralina.
- La centralina si annuncia in Bluetooth come "RideLink <modello>" (es. "RideLink FZ8").

### App e web app
- L'app memorizza la sua moto e si collega solo a quella; se al primo collegamento ce ne sono piu' vicine chiede quale. Pulsanti "Cambia moto" e "Abbina un display" (scheda Altro).
- Web app: "Abbina un display"; la moto si sceglie nella finestra Bluetooth del browser.
- **Installa l'app 3.5 prima di aggiornare la centralina**: le versioni precedenti cercano il nome esatto "RideLink".

---

## [3.4.2] - 2026-10-01
### Display tondo
- Corretto il touch: gli assi X e Y venivano scambiati, per cui i tocchi finivano nel punto sbagliato (riflessi in diagonale).

---

## [3.4.1] - 2026-10-01
### Display rettangolare
- Corretto il touch: anche l'asse orizzontale era invertito (in verticale destra/sinistra specchiate, in orizzontale sopra/sotto invertiti).

---

## [3.4.0] - 2026-10-01
### Display
- **Pagina Viaggio**: velocita' dal GPS del telefono (senza Google Maps), km del viaggio, tempo in sella, media, autonomia e promemoria di manutenzione (catena, tagliando). Doppio tocco su "Viaggio", "Autonomia" o sulla riga della manutenzione per azzerare / segnare il pieno / segnare il lavoro fatto.
- **Pagina 0-100 km/h**: tocca ARMA, fermati e parti; la centralina misura con l'accelerometro a 100 Hz e tiene il record. Il display rettangolare suona quando e' pronto e a fine prova.
- **Impostazioni a schede** MOTO / DISPLAY: luminosita' (100/75/50/25%) e modalita' notte (automatica dal tramonto all'alba, sempre, mai). In orizzontale le righe sono a tutta larghezza e i testi non escono piu' dai pulsanti.
- **Calibrazione del touch**: tieni premuto lo schermo 3 secondi e tocca i tre mirini; il display impara come e' montato il pannello touch (per ogni orientamento).
- Display tondo: retroilluminazione regolabile (PWM). Display rettangolare: luminosita' regolata via software.

### App e web app
- Schede Viaggio (con intervalli di manutenzione), **Dove ho parcheggiato** (salvato quando ti allontani dalla moto o va in standby, con "Portami alla moto" a piedi) e 0-100.
- Luminosita' e modalita' notte dei display; pulsanti per le nuove pagine.

---

## [3.3.0] - 2026-10-01
### Display rettangolare
- Corretto il touch: l'asse verticale era invertito, per cui nella pagina Impostazioni toccando "Orientamento" si selezionava "Zero piega".

### Centralina
- Supporto al modulo sensori **GY-87** (MPU6050 + HMC5883L o QMC5883L + BMP180) oltre al GY-89: la centralina riconosce da sola quale e' collegato, con le stesse scale (+/-4 g, +/-500 dps). Col GY-87 bastano SDA e SCL.
- Lo standby (spegnimento sensori e controllo movimento al risveglio) funziona con entrambi i moduli.

---

## [3.2.0] - 2026-10-01
### Display
- **Pagina Impostazioni** sui display (quinta pagina): zero piega, avvia/ferma registrazione, auto-calibrazione, azzera record. Ogni azione chiede un secondo tocco entro 3 s, cosi' non parte per sbaglio.
- **Display rettangolare ruotabile** (0/90/180/270°) dalla sua pagina Impostazioni, dall'app o dalla web app; tutte le pagine hanno un layout orizzontale dedicato e il touch segue la rotazione. L'orientamento resta salvato.
- Schermata di benvenuto di 4 s con barra di caricamento.

### App e web app
- Pulsanti per la pagina Impostazioni e per l'orientamento del display rettangolare.

---

## [3.1.0] - 2026-10-01
### Aggiornamento firmware via Bluetooth
- App e web app scaricano l'ultima versione pubblicata e la installano via Bluetooth: la centralina aggiorna se stessa e passa i firmware ai display via ESP-NOW (pacchetti confermati uno a uno, controllo MD5, la versione precedente resta se qualcosa va storto).
- I display si annunciano alla centralina con tipo e versione; l'app mostra cosa e' installato e cosa e' da aggiornare.
- Nuova azione GitHub: a ogni tag `vX.Y.Z` compila i tre firmware e li pubblica sul ramo `firmware` e come release.
- Rimosso l'aggiornamento via Wi-Fi dal PC (`*_ota`, `secrets.h`): non serve piu'.
- Versione mostrata nella schermata di benvenuto dei display.

---

## [3.0.0] - 2026-10-01
### Nuovo nome: RideLink
- Progetto, app, web app, firmware e nome Bluetooth rinominati **RideLink**; la centralina si annuncia come `RideLink`.
- Le impostazioni gia' salvate (calibrazioni della centralina, sessioni della web app) vengono migrate automaticamente al primo avvio.
- L'app Android ha un nuovo identificativo (`com.ridelink.app`): va reinstallata.

### Sicurezza
- **Rilevamento caduta + SOS**: conto alla rovescia di 30 s sui display (sfondo rosso, cicalino) e sul telefono; annullabile dal display, dal pulsante della centralina o dalla notifica; SMS con posizione GPS fino a 5 contatti, SMS "falso allarme" se annullato dopo l'invio. Prova da fermo con "Prova rilevamento reale".

### Navigazione
- Supporto a **Google Maps** (Waze non espone le indicazioni): parser delle frasi italiane, distanza sconosciuta gestita, ripetizione dell'indicazione per non perderla.
- **Immagine della manovra** presa dalla notifica di Maps e mostrata sui display: indica la vera direzione delle uscite in rotonda.
- Bip a 200 m e 50 m dalla svolta sul display rettangolare.

### Display
- Motore grafico comune (`include/CockpitCommon.h`) con fotogramma intero in RAM (diviso in fasce se la memoria e' frammentata).
- Display rettangolare riscritto (4 pagine, angoli arrotondati rispettati); piega con smorzamento "da TV".
- Schermata di benvenuto "Benvenuto su RideLink" con il modello della moto scelto nell'app.

### Centralina
- **Standby** dopo 5 minuti da ferma, risveglio dal movimento; nuove partizioni `partitions_ota.csv` (due spazi per il firmware).

### App e web app
- App Android rifatta (schede Moto, SOS, Giri, Altro), registrazione giri con mappa delle pieghe ed export GPX/CSV, calibrazioni e scelta pagina dei display.
- Web app allineata: stesse pagine dei display, stessi colori della mappa, nome della moto, prove SOS e aggiornamento firmware.

---

## [2.3.0] - 2026-09-30
### 🖥️ Secondo Display Rettangolare 1.69" (Spotpear ST7789 240x280 + Touch CST816)
- **Nuovo ambiente PlatformIO**: `[env:cockpit_st7789_169]`.
- **Mappatura Pin Hardware Spotpear**:
  - `TFT_SCLK`: GPIO 5
  - `TFT_MOSI`: GPIO 6
  - `TFT_CS`: GPIO 3
  - `TFT_DC`: GPIO 2
  - `TFT_RST`: GPIO 8 / GPIO 10
  - `TOUCH_SCL`: GPIO 7
  - `TOUCH_SDA`: GPIO 11
  - `TOUCH_INT`: GPIO 9
- **Motore di Rendering Differenziale Zero-Flicker (60 FPS)**:
  - Eliminato lo sfarfallio ridisegnando gli elementi statici (sfondi card, cerchi, etichette) una sola volta.
  - Cancellazione mirata della lancetta di piega e aggiornamento numerico con colore di sfondo nativo.
- **Supporto Multi-Display Simultaneo**:
  - Il protocollo broadcast ESP-NOW consente a **entrambi i cruscotti** (il rotondo 1.28" GC9A01 e il rettangolare 1.69" ST7789) di operare in parallelo ricevendo gli stessi dati in tempo reale a 50Hz.
- **Risoluzione Bug Android Companion App**:
  - Risolto errore di resource linking su temi night (`values-night/themes.xml`).
  - Corretto callback BLE `onScanFailed` e rimossi filtri restrittivi sul nome device.
  - Aggiunti permessi `POST_NOTIFICATIONS` e documentata procedura sblocco *Restricted Settings* su Android 13/14/15.

---

## [2.2.0] - 2026-09-30
### 🎨 Revisione Grafica High-Tech & Notifiche Smart HUD
- **Display Rotondo 1.28" (Sunton ESP32-2424S012 / GC9A01)**:
  - **Schermata 0 (MotoGP Sport Lean Cluster)**:
    - Sostituito l'indicatore wireframe con un **nastro a 27 segmenti LED radiali** (stile superbike) con colorazione progressiva dinamica (Ciano -> Verde Neon -> Arancio -> Rosso Fiamma).
    - Marker di picco massimo SX e DX memorizzati e tracciati direttamente sull'arco radiale.
    - **Capsula centrale in titanio scuro** con indicatore di direzione dinamico (`◀ SX`, `DX ▶`, `▲ DRITTO`) e cifre piega giganti ad alto contrasto.
    - Due card laterali per i valori di picco (`MAX L` e `MAX R`).
    - **Barra Gas TPS a 10 segmenti LED** progressivi con valore percentuale `xx%`.
  - **Schermata 1 (G-G Friction Radar Scope)**:
    - Grafica da radar aeronautico con anelli concentrici di aderenza (0.5G, **1.0G Blu Racing**, 1.4G limite).
    - Mirino G-force a doppio anello con **tracciamento vettoriale dinamico** dall'origine degli assi.
    - 4 badge cardinali sagomati a pillola: `▲ FRENATA` (Rosso), `▼ ACCEL` (Verde), `◀ SX` (Ciano), `DX ▶` (Ambra).
    - Due capsule in alto con lettura in tempo reale di `G-TOT` e `MAX G`.
  - **Schermata 2 (Race Telemetry Cockpit)**:
    - Sostituita la lista testuale con un vero cruscotto racing da superbike.
    - Badge testata `RACE TELEMETRY` in blu.
    - Confronto visivo pieghe con due card verticali affiancate e barre di livello grafiche.
    - Confronto visivo forze G con barre progressive orizzontali per staccata (rosso) e accelerazione (verde).
    - Capsula inferiore con quota altimetrica e indicatore di trasmissione live 50Hz.
  - **Schermata 3 (Turn-by-Turn Navigation HUD - Beeline Moto II Style)**:
    - **Anello circolare di countdown svolta**: arco radiale esterno a 360° che si consuma progressivamente man mano che la distanza si riduce da 500m a 0m.
    - Tachimetro GPS sagomato a capsula (`VEL xx KM/H`).
    - Frecce vettoriali con intagli e doppi chevron (svolta secca, tornanti, rotonda numerata con corsia, bandiera di arrivo).
    - Hero box della distanza ad altissima leggibilità (`SVOLTA!`, `xxx m`, `x.x km`).
    - Capsula sagomata per il nome della via.
  - **Sistema Popup Notifiche Chiamate & WhatsApp**:
    - Sovrimpressione card animata su qualsiasi schermata attiva:
      - 📞 **Chiamate in arrivo**: badge rosso con icona cornetta, nome chiamante e sottotitolo.
      - 💬 **WhatsApp**: badge verde smeraldo con icona fumetto, nome mittente e anteprima messaggio.
      - ⚠️ **Autovelox**: badge ambra per segnalazioni Waze.
    - **Tap-to-Dismiss**: tocco istantaneo sul touch per chiudere la notifica in marcia e ripristinare il cruscotto.
    - Auto-chiusura temporizzata (6-8s).
    - Simulazione dimostrativa da banco ogni 25s per test immediati.

### 📱 Android Companion App (`android_companion/`)
- Nuova app Android nativa completa, pronta per Android Studio:
  - `RideLinkNotificationListener` (`NotificationListenerService`): cattura in tempo reale le notifiche di Waze, chiamate dialer e WhatsApp.
  - Parser intelligente per le indicazioni di Waze e Google Maps (distanza in metri, tipologia di svolta, rotonde e nome via).
  - `RideLinkBleService`: connessione automatica in background alla centralina su BLE.
  - `MainActivity`: interfaccia dark con stato connessione, pulsante abilitazione permessi notifiche e pulsanti di test rapido.

### 🌐 Web App Telemetria PWA (`web_ble_app/index.html`)
- Aggiunta card interattiva **"Smart HUD: Notifiche & Navigazione Display"** per testare chiamate, WhatsApp e svolte Waze con un clic dal browser.

### ⚡ Centralina Master (`src/main.cpp`)
- Implementato inoltro comandi BLE ➔ ESP-NOW a 50Hz per `NAV:`, `CALL:`, `CALL_END`, `WA:`, `ALERT:`.

---

## [2.1.0] - 2026-09-30
### 🚀 Integrazione Display Rotondo 1.28" (GC9A01 + Touch CST816D)
- **Nuovo ambiente PlatformIO**: `[env:cockpit_round_gc9a01]`.
- Configurazione Hardware SPI a **40 MHz con DMA** su pin standard Sunton (SCLK=6, MOSI=7, DC=2, CS=10, BL=3).
- Risolto bottleneck del costruttore software bit-banging Adafruit, passando da 2 FPS a 60 FPS stabili.
- Driver I2C per touch capacitivo CST816D (SDA=4, SCL=5, INT=0, RST=1).
- Motore di gesture con swipe naturale orizzontale/verticale e tocco bi-zona (destra = avanti, sinistra = indietro) con filtro debounce di 350ms.
- Ricevitore ESP-NOW edge-triggered per consentire il cambio schermata sia da touch locale che da remoto senza conflitti.

---

## [2.0.0] - 2026-09-28
### 📡 Architettura Dual-Node Wireless & Auto-Calibrazione
- Separazione architetturale in 2 nodi:
  - **Master Node (Sottosella)**: ESP32-C3 + GY-89 (IMU 10-DOF) + TPS + Datalogger Flash.
  - **Cockpit Display Node (Manubrio)**: Ricevitore wireless ultra-veloce via ESP-NOW (<2.5ms).
- **Auto-Calibratore Dinamico 3 Minuti**: algoritmo in marcia per identificare lo zero di rollio e pitch eliminando gli errori di montaggio.
- **Server BLE Dual-Mode**: compatibile sia con RaceChrono DIY (frequenza 20Hz) che con Web BLE Browser PWA.
- **Datalogger Flash LittleFS**: salvataggio automatico di sessione a 10Hz in formato CSV.

---

## [1.0.0] - 2026-09-20
### 🏁 Rilascio Iniziale Prototipo
- Filtro cinematico selettivo anti-deriva per moto (gate cinematico durante la percorrenza in curva).
- Supporto sensori GY-89 (LSM303D accelerometro/bussola + L3GD20 giroscopio + BMP180 barometro).
- Display SPI 1.6" monocromatico transflettivo SSD1283A.
