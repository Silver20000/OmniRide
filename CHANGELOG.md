# Changelog - OmniRide 🏍️📊

Tutte le modifiche e le evoluzioni del firmware, delle app e dell'hardware di OmniRide (fino alla 3.6 chiamato RideLink).

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
