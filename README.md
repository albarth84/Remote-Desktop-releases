<p align="center">
  <img src="assets/icon.png" width="96" alt="Kronos Remote Support">
</p>

<h1 align="center">Kronos Remote Support</h1>

<p align="center">
  Assistenza remota multipiattaforma: vedi e controlli un altro computer con ID e password.<br>
  macOS · Windows · Linux
</p>

---

## Download

Scarica l'ultima versione dalla pagina **[Releases](../../releases/latest)**:

| Sistema | File |
|---|---|
| macOS Apple Silicon (M1/M2/M3…) | `Kronos.Remote.Support_<versione>_aarch64.dmg` |
| macOS Intel | `Kronos.Remote.Support_<versione>_x64.dmg` |
| Windows | `Kronos.Remote.Support_<versione>_x64-setup.exe` (oppure `.msi`) |
| Linux | `.AppImage` (si aggiorna da sola), `.deb`, `.rpm` |

Le app non sono ancora firmate con un certificato Apple/Microsoft, quindi al primo avvio il sistema avvisa.
Si apre comunque **senza usare il Terminale**:

- **macOS** — apri l'app: compare *"Apple non può verificare che «Kronos Remote Support» sia privo di malware"*.
  Premi **Fine** (non "Sposta nel Cestino"), poi apri *Impostazioni di Sistema → Privacy e sicurezza*, scorri fino
  in fondo e premi **Apri comunque** accanto al nome dell'app; conferma con la password del Mac e **Apri**.
  Va fatto una sola volta; gli aggiornamenti dall'app non lo richiedono più.
  (Solo se l'app risultasse *"danneggiata"*, da Terminale: `xattr -dr com.apple.quarantine "/Applications/Kronos Remote Support.app"`.)
- **Windows** — nella schermata SmartScreen: *Ulteriori informazioni* → *Esegui comunque*.
- **Antivirus aziendali** (es. WithSecure) possono bloccare l'app perché non è firmata digitalmente e, come ogni
  software di assistenza remota, cattura lo schermo e simula mouse e tastiera. Serve un'esclusione da parte
  dell'amministratore dell'antivirus.

Una volta installata, l'app si aggiorna dal pulsante **Aggiornamenti** in alto (pacchetti firmati e verificati).

### Kronos Quick Support (senza installazione)

Per farsi assistere al volo: si scarica, si avvia, mostra **ID e password**, ogni connessione va **confermata**.
Serve solo a condividere il proprio schermo (non a controllare altri computer); niente accesso non presidiato,
niente avvio automatico. Chiusa la finestra la condivisione termina e non resta nulla di salvato
(su Windows resta solo la cache del motore web nella cartella del profilo).

| Sistema | File |
|---|---|
| Windows | `KronosQuickSupport_<versione>_windows_x64.exe` (serve WebView2, già presente in Windows 10/11 aggiornati) |
| macOS Apple Silicon | `KronosQuickSupport_<versione>_macos_aarch64.zip` |
| macOS Intel | `KronosQuickSupport_<versione>_macos_x64.zip` |
| Linux | `KronosQuickSupport_<versione>_linux_amd64.AppImage` (rendilo eseguibile: `chmod +x`) |

Su macOS: estrai lo zip e apri l'app; al primo avvio vale la procedura **Apri comunque** descritta sopra. Servono
i permessi Registrazione schermo e Accessibilità.

## Come funziona

Ogni installazione riceve un **ID di 9 cifre** e mostra una **password** temporanea di 8 caratteri.
Chi vuole collegarsi inserisce ID e password del partner; il partner vede una **richiesta di conferma**
e decide se consentire. Dopo la conferma si vede lo schermo del partner e, se attivo, si controllano mouse e tastiera.

- Il collegamento tra i due computer è **diretto e cifrato** (WebRTC). Quando la rete non permette il collegamento
  diretto, il traffico passa da un **relay** (TURN), restando cifrato da un capo all'altro.
- La barra in alto indica sempre il tipo di connessione: **Diretta (rete locale)**, **Diretta (Internet)** o **Relay TURN**.
- La **password non lascia mai il computer**: viene verificata con il protocollo SPAKE2, legato ai certificati della
  connessione. Il server mette solo in contatto i due computer: non vede schermo, input né password.
- Dopo 5 password errate in 10 minuti il computer rifiuta nuovi tentativi per un po'.

## Uso

1. Avvia **Kronos Remote Support** su entrambi i computer.
2. Sul computer da assistere leggi **ID** e **password** (riquadro *Consenti il controllo*).
3. Sull'altro computer inseriscili in *Controlla un computer remoto* e premi **Connetti**.
4. Sul computer remoto compare la richiesta: **Consenti** o **Rifiuta** (rifiuto automatico dopo 30 secondi).
5. Si apre lo schermo del partner:
   - menu **Schermo** per scegliere il monitor, se il partner ne ha più di uno;
   - **Controllo attivo/spento** per inviare o no mouse e tastiera (i tasti seguono il layout del computer remoto);
   - **Schermo intero** e **Disconnetti**.

Chi condivide il proprio schermo vede un banner rosso con il pulsante **Termina**.
Chiudendo la finestra l'app resta attiva nell'icona della barra di sistema; per uscire: icona → *Esci*.

## Accesso non presidiato (i tuoi dispositivi)

Per controllare un tuo computer **senza conferma**:
1. Sul computer da controllare: *Consenti il controllo* → **Imposta password personale**
   (almeno 8 caratteri) e, se vuoi, **Avvia all'accesso**.
2. Dall'altro computer inserisci ID e password personale, spunta **Password personale (senza conferma)** e
   facoltativamente **Salva come**: il dispositivo comparirà in **I miei dispositivi** e si apre con un clic.

La password personale non viene mai salvata né trasmessa: l'app conserva solo un valore derivato, valido per quel solo
dispositivo. Il computer controllato mostra comunque il banner "schermo condiviso" con **Termina**.

## Permessi necessari sul computer controllato

- **macOS**: *Registrazione schermo* (per farsi vedere) e *Accessibilità* (per farsi controllare), in
  Impostazioni di Sistema → Privacy e sicurezza. L'app li chiede alla prima connessione.
- **Windows**: nessuno. Le finestre avviate come amministratore e le richieste UAC non sono controllabili.
- **Linux**: sessione **Xorg** (dalla schermata di login, es. "Ubuntu su Xorg"); Wayland non è ancora supportato.

---

Questo repository contiene solo i pacchetti pubblicati e i workflow che li costruiscono; il codice sorgente è privato.
