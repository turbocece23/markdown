<style type="text/css">
	h1 { color: #EF3E36; }
	h2
	{
		padding-top: 0.7%;
		padding-bottom: auto;
		width: 100%;
		text-align: center;
		color: white;
		background-color: #C01B2D;
	}
	h3
	{
		padding-top: 0.7%;
		padding-bottom: auto;
		text-align: center;
		width: 100%;
		background-color: #FF8811;
		color:white;
	}

	h4
	{
		color: #384682;
		background-color: #c2ceff;
		padding-top: 0.7%;
		padding-left: 0.7%;
	}
	h5
	{
		color: #3e5d36;
		padding-top: 0.7%;
		padding-left: 0.7%;
	}
	
	img
	{
		margin-left: auto;
		margin-right: auto;
		display: block;
	}

	.testocentro
	{
		text-align: center;
	}

	a:link { color: white; }
	a:visited { color: white; }
	ul a:link { color: black; }
	ul a:visited { color: black; }
	.hig/*hlight*/ { color:#1ba63d; }
</style>

# S I S T E M I

## <span id="indice">Indice</span>

- <a href="#U2">U2 - VLAN: Virtual Local Area Network</a>
	- <a href="#U2L1">**L1** *66* Le Virtual LAN (VLAN)</a>
- <a href="#U3">U3 - Tecniche crittografiche per la protezione dei dati</a>
	- <a href="#U3L1">**L1** *96* La crittografia simmetrica</a>
	- <a href="#U3L2">**L2** *108* La crittografia asimmetrica</a>
	- <a href="#U3L3">**L3** *120* Certificati e firma digitale</a>
- <a href="#U4">U4 - La sicurezza delle reti</a>
	- <a href="#U4L1">**L1** *166* La sicurezza nei sistemi informativi</a>
	- <a href="#U4L2">**L2** *183* La sicurezza delle connessioni con SSL/TLS</a>
	- <a href="#U4L3">**L3** *191* Firewall, Proxy, ACL e DMZ</a>

## <a href="#indice" id="U2">U2 - VLAN: Virtual Local Area Network</a>
### <a href="#indice" id="U2L1">L1 - Le Virtual LAN (VLAN)</a>

Reti LAN realizzate logicamente grazie allo standard **802.1Q**.

> Ciascuna VLAN si comporta come fosse una **rete locale separata dalle altre** dove i pacchetti broadcast sono confinati all'interno di essa. Possiamo affermare che la **comunicazione a livello 2** è confinata all'interno della VLAN e la connettività tra diverse VLAN può essere realizzata **solo a livello 3**, attraverso il *routing*.

Le VLAN consentono maggiore agilità di manutenzione e modifica delle infrastrutture di rete, riducendo il traffico perché isolano il traffico di broadcast.

Principali **vantaggi** delle VLAN:

- Economicità: serve solo uno switch di livello 3 per implementare le VLAN
- Scalabilità: le si VLAN possono estendere su diversi switch
- Ottimizzazione dell'uso delle infrastrutture: per isolare una subnet non è necessario aggiungere uno switch e/o un router, ma riassegnare alcune porte.
- Possibilità di estensione oltre i limiti fisici di un singolo switch

#### Realizziamo una VLAN

La realizzazione di VLAN può avvenire secondo due modalità:

- VLAN port based (untagged LAN o private VLAN)
- VLAN tagged

Le VLAN vengono distinte attraverso un numero identificativo chiamato **VID** (Virtual Identificator), compreso tra 1 e 4094 e un proprio blocco di indirizzi IP.

Una volta definita la VLAN ci sono due modi per associarvi gli host:

- Usando i numeri di porta dello switch: per esempio la prima metà delle porte a una VLAN, altra metà ad una VLAN diversa
- Usando gli indirizzi di rete degli host: associamo i singoli indirizzi degli host ad ogni VLAN, sistema più sicuro

#### Port based VLAN (untagged)

Questo metodo usa i numeri delle porte dello switch. Ciascuna porta prende il nome di **Access port**.

Le operazioni che devono svolgere gli switch sono:

- **Ingress**: un frame in ingresso **appartiene alla VLAN** a cui è assegnata la porta, lo lascia passare
- **Forwarding**: il frame può essere inoltrato solo verso porte appartenenti alla stessa VLAN a cui appartiene la porta di ingresso che è mappata in un forwarding database, distinto per ogni VLAN
- **Egress**: una volta determinata la porta attraverso cui deve essere trasmesso il frame, questo può essere trasmesso così com'è stato ricevuto, senza modifica

#### VLAN 802.1Q (tagged VLAN)

Permette di far condividere una VLAN a due o più switch mediante una **modifica del formato** del frame ethernet, vengono aggiunti **4 byte** (**TAG**) che trasportano le informazioni sulla VLAN e altre aggiuntive. Ciascuna **porta tagged** prende anche il nome di **porta di Trunk**.

I primi 2 byte chiamati **TAG Protocol Identifier** (**TPI**) contengono il tag **EtherType** e indica il nuovo formato del frame.

I successivi 2 byte sono chiamati **Tag Control Information** (**TCI** o **VLAN TAG**)

- user_priority
- CFI (indica il formato dei MAC nel frame)
- VID: 12 bit che indicano il numero della VLAN, la VLAN 0 e la 4095 sono riservate, quindi gli ID utilizzabili sono 4094

## <a href="#indice" id="U3">U3 - Tecniche crittografiche per la protezione dei dati</a>
### <a href="#indice" id="U3L1">L1 - La crittografia simmetrica</a>
Ci sono diversi aspetti collegati al problema della sicurezza nelle reti:

- **Segretezza**: le informazioni devono essere leggibili solo a chi ne ha i diritti
- **Autenticazione**: processo di riconoscimento delle credenziali dell'utente in modo di assicurarsi dell'identità di chi invia messaggi o esegue operazioni
- **Affidabilità dei documenti**: avere la garanzia e la certezza che un documento sia originale, il mittente è certo e non è stato letto e/o alterato da persone non autorizzate

#### Crittografia

Desiderio di mantenere messaggi tra due interlocutori nascosti agli occhi di terzi.

- **Codifica**: sostituisce parole con altre
- **Cifratura**: sostituisce lettere o caratteri

Quando la chiave di cifratura coincide con quella di de-cifratura lo schema crittografico si dice **simmetrico** e la chiave prende il nome di **chiave comune**.

Quando la chiave di cifratura è diversa da quella di de-cifratura lo schema crittografico si dice **asimmetrico** e le due chiavi si chiamano:

- **chiave pubblica**: usata per la cifratura, comune a tutti i mittenti e di pubblico dominio
- **chiave privata**: utilizzata per la de-cifratura, segreta e di conoscenza solo del destinatario del messaggio

#### Crittoanalisi

Studio dei metodi per ottenere il significato di informazioni cifrate: tipicamente si tratta delle operazioni effettuate alla ricerca della chiave segreta.

Il **principio di Kerckhoffs** stabilisce che è la chiave l'elemento fondamentale per la sicurezza di un sistema informatico. La sicurezza di un crittosistema deve dipendere solo dalla segretezza della chiave e non dalla segretezza dell'algoritmo usato.

#### Cifrari e chiavi

La crittografia permette di:

- **identificare** un utente all'accesso alla rete o al singolo PC
- **autenticare** un messaggio, cioè accertarsi dell'identità dell'autore e dell'integrità del messaggio ricevuto
- **firmare digitalmente** un messaggio, cioè accertarsi dell'identità dell'autore e quindi la non ripudiabilità del messaggio stesso

#### <span class="hig">Il cifrario DES</span>

È un algoritmo simmetrico a chiave segreta di 64 bit, 8 sono di controllo, questa chiave prevede 16 trasformazioni successive applicate a ogni blocco del messaggio

Il **DES** rispetta il principio di **Kerckhoffs**, cioè l'algoritmo è noto e la chiave è segreta ed è stato realizzato applicando i principi di **Shannon**:

- **diffusione** dei caratteri consecutivi del messaggio in tutto il crittogramma
- **confusione** del messaggio con la chiave

Il *DES* viene anche usato per cifrare file personali su un disco locale ma:

> Nel 1998 la *Electronic Frontier Foundation* diffuse un comunicato stampa con il quale annunciò la **sconfitta del DES** grazie a un calcolatore da 250.000 piotte, che in meno di 60 ore era capace di forzare un messaggio cifrato con DES.

#### <span class="hig">3-DES</span>

Introdotto nel 1999, il **Triple DES**, con tre passi di cifratura DES consecutivi con tre chiavi diverse e per un totale di 168 bit. Maggior sicurezza rispetto al DES sta proprio nella lunghezza tripla della chiave.

#### <span class="hig">IDEA</span>

**International Data Encryption Algorithm** introdotto in sostituzione al DES. Attualmente non si conoscono tecniche in grado di forzare IDEA che, grazie alla chiave a 128 bit è immune da attacchi "brutali".

#### <span class="hig">AES</span>

Nel 1997 il **National Institute of Standards and Technology** organizzò un concorso per sostituire il DES, e definire un nuovo standard crittografico, l'**Advanced Encryption Algorithm**.

L'algoritmo fu valutato in base a:

- **sicurezza**: chiave a dimensioni minime di 128 bit
- **costo**: un algoritmo utilizzabile per un'ampia gamma di applicazioni
- **caratteristiche dell'algoritmo e dell'implementazione**: leggibilità, semplicità di codifica, flessibilità e versatilità per poter essere implementato in differenti piattaforme hardware e software


AES fu approvato da NSA per comunicazioni top-secret ed è tuttora il cifrario a chiave segreta più usato negli ambienti informatici.

#### Limiti degli algoritmi simmetrici

Gli algoritmi simmetrici descritti presentano alcuni limiti tra i quali il problema più evidente: le persone che devono comunicare devono essere in possesso della stessa chiave e, di fatto, questo limita la diffusione e il suo utilizzo, in quanto non sono molti i sistemi a disposizione per la distribuzione delle chiavi.

### <a href="#indice" id="U3L2">L2 - La crittografia asimmetrica</a>
Non è il metodo ideale per le comunicazioni su Internet principalmente perché il limite fondamentale è rappresentato dalla necessità di un canale sicuro e di un accordo preventivo per lo scambio delle chiavi. L'idea alla base delle **crittografie simmetriche** è quello di avere due chiavi diverse, una pubblica per la criptazione e una privata per la decriptazione.

Con la **crittografia asimmetrica**:

- si risolve il problema della **riservatezza**: criptando il messaggio con la chiave pubblica, solo il possessore della chiave privata è in grado di decriptarlo
- si risolve il problema dell'**autenticità del mittente**: a ogni chiave pubblica è associata l'identità certa del proprietario

Il principale svantaggio della *crittografia asimmetrica* è la complessità dei calcoli che rendono poco efficiente la loro implementazione sopratutto con l'aumentare della lunghezza della chiave.

Per mantenere relativamente leggeri gli algoritmi asimmetrici viene estratta una sequenza di numeri dal messaggio originale chiamata **fingerprint** utilizzata per le funzioni di hash *MD4* e **MD5**.

#### <span class="hig">RSA</span>

L'algoritmo RSA lavora sfruttando i numeri primi e come chiave utilizza un numero n ottenuto proprio dal prodotto di due numeri primi **p** e **q** cioè **n = p * q**

Usato per codificare un unico messaggio contenente una chiave segreta, tale chiave verrà poi utilizzata per scambiarsi messaggi tramite un algoritmo a chiave segreta (ad esempio **AES**)

#### Crittografia ibrida

Per gestire le chiavi pubbliche è necessario un sistema di **PKI** (**Public Key Infrastructure**) che si occupi della gestione e dello scambio delle chiavi.

<table>
	<thead>
		<tr>
			<th></th>
			<th>Crittografia simmetrica</th>
			<th>Crittografia asimmetrica</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th>Pro</th>
			<td class="testocentro">Molto veloce</td>
			<td class="testocentro">Non serve un canale sicuro per lo scambio delle chiavi</td>
		</tr>
		<tr>
			<th>Contro</th>
			<td class="testocentro">Problema dello scambio delle chiavi</td>
			<td class="testocentro">Molto lenta, a causa dei calcoli complessi da effettuare</td>
		</tr>
	</tbody>
</table>

In un **sistema a crittografia ibrida** utilizziamo la **chiave pubblica** soltanto per comunicare la **chiave segreta** che poi verrà usata per una normale comunicazione basata su crittografia simmetrica.

### <a href="#indice" id="U3L3">L3 - Certificati e firma digitale</a>

La **firma digitale** è l'equivalente informatico di una tradizionale firma apposta su carta.

Si basa su un sistema di crittografia a chiavi **asimmetriche** che consente:

- la sottoscrizione di un documento informatico
- la verifica, da parte dei destinatari, dell'identità del soggetto sottoscrittore
- la certezza che l'informazione contenuta nel documento non sia stata alterata

Durante l'apposizione della firma digitale,il file viene "incapsulato" in una **busta crittografica** e il risultato è un nuovo file, con estensione **.p7m**, la firma digitale in formato *p7m* consente di firmare qualunque tipo di file (rtf, doc, tiff, xls...)

#### Le frime digitali

Tra le motivazioni per cui è nata la firma digitale c'è la lentezza dei sistemi di crittografia a chiave pubblica, incluso RSA: per rendere più efficiente il meccanismo si utilizza una funzione **hash** attraverso la quale si calcola una stringa identificativa del messaggio detta *fingerprint* o *message digest*.

Le funzioni *Hash* più note sono:

- **MD5**: standard per Internet, più insicuro ma veloce
- **SHA**: standard governativo USA

#### MD5

**Message Digest 5** genera una stringa fissa di 128 bit, 32 caratteri chiamata *MD5 Checksum* o *MD5 Hash*.

### Gli algoritmi SHA

**Secure Hash Algorithm**, algoritmi sviluppati dalla NSA, nati come modifiche dell'MD4, ora è in uso lo SHA3.

#### I certificati digitali

Un certificato digitale è un documento informatico firmato digitalmente dal certificatore, i dati contenuti nel certificato sono:

- dati del proprietario
- dati del certificato
- dati della Certification Authority

Un **certificato digitale** può avere diversi formati:

- PGP (a pagamento)
- GPG (libero)
- certificati X.509

La differenza tra PGP/GPG e un X.509 è che è possibile creare il proprio certificato PGP/GPG in modo autonomo, mentre per X.509 è necessario rivolgersi a un ente certificatore.

#### Public Key Infrastructure

L'infrastruttura tecnica e organizzativa preposta alla creazione e distribuzione e revoca dei certificati di chiave pubblica è la **PKI** (**Public Key Infrastructure**). È organizzata come una foresta dove come radice e gestore del PKI vi è una **CA root**.

Ogni *CA root* può firmare i certificati di altri enti che possono essere sia utenti finali (foglie) che altre aziende certificatrici.

#### Richiedere un certificato digitale

<ol>
	<li>Generazione della coppia di chiavi asimmetriche da utilizzare per cifrare le comunicazioni</li>
	<li>Il richiedente comunica informazioni circa la propria identità alla Certification Authority</li>
	<li>La Registration Authority inizia la verifica dei dati ricevuti</li>
	<li>La Certification Authority genera il certificato e lo firma digitalmente</li>
	<li>Il certificato firmato viene inviato al richiedente</li>
</ol>

## <a href="#indice" id="U4">U4 - La sicurezza delle reti</a>
### <a href="#indice" id="U4L1">L1 - La sicurezza nei sistemi informativi</a>

#### La sicurezza dei dati

Le informazioni devono essere protette per garantire la "sicurezza informatica".

Le possibili situazioni che minacciano l'**integrità dei dati** sono di due tipologie:

- **minacce naturali**
- **minacce umane**

#### Minacce naturali
##### Can't stop 'em

Le minacce naturali sono dovute a calamità naturali imprevedibili quali:

- tempeste
- inondazioni
- fulmini
- incendi
- terremoti

Che sono praticamente impossibili da impedire e prevenire.

Per questa tipologia è necessario effettuare un'**analisi dei rischi** in quanto potrebbero causare solo periodi di inattività operativa. Tra queste minacce vengono considerati anche minacce dovuta a interventi umani, di fatto, imprevedibili:

- atti vandalici
- sommosse popolari
- guerre
- attacchi terroristici

#### Minacce umane

Soggetti che hanno interessi personali ad acquisire le informazioni di un'azienda o a limitare l'operatività di un organizzazione. Possono essere causate da personale interno (**attacco interno**, minacce più pericolose perché il personale conosce la struttura) o da soggetti estranei (**attacchi esterni**).

#### Sicurezza di un sistema informatico

Con le reti locali di PC e con l'avvento di Internet, le informazioni e l'elaborazione non sono più concentrate ma distribuite e la comunicazione avviene in "broadcast" generalmente su linee condivise

> La **sicurezza** di un sistema informativo significa impedire a potenziali soggetti attaccanti l'accesso o l'uso non autorizzato di informazioni e risorse

La sicurezza viene spesso indicata con l'acronimo **CIA**:

- Data **Confidentiality**: mantenere la segretezza dei dati
- Data **Integrity**: evitare che i dati vengano alterati
- System **Avalability**: garantire che il sistema continuerà ad operare

Questi obiettivi sono tra loro connessi e generano altri aspetti collegati all'analisi dei rischi della sicurezza:

- **Autenticazione**<br>Processo di riconoscimento delle credenziali dell'utente in modo da assicurarsi dell'identità di chi invia messaggi o esegue operazioni
- **Autorizzazione**<br>L'utente autenticato deve avere associato l'insieme delle autorizzazioni, cioè l'elenco che specifica quali sono le azioni permesse e negate
- **Riservatezza**<br>Le informazioni devono essere leggibili e comprensibili solo a chi ne ha i diritti
- **Disponibilità**<br>Un documento deve essere disponibile in qualunque momento a chi ne è autorizzato, è necessario quindi garantire la continuità del servizio per ciascun utente che deve poter accedere e utilizzare le risorse e i dati in ogni momento
- **Integrità**<br>La garanzia e la certezza che un documento sia originale e che il suo contenuto non sia stato letto e/o alterato e modificato da non autorizzati
- **Paternità**<br>Ogni documento deve essere associato a un utente

> Un documento elettronico ha valenza di prova in tribunale quando si può dimostrare l'autore del documento, cioè l'**identificazione** e l'**autenticazione** del **mittente** e l'**integrità** del documento

Le misure per ottenere la segretezza dei dati sono applicabili a diversi livelli della pila ISO/OSI:

- livello fisico (1): cercare di impedire che avvengano intercettazioni di dati
- livello data link (2): codifiche e cifrature dei dati trasmessi per renderli incomprensibili

#### Valutazione dei rischi

- Minacce alla sicurezza
	- Minacce Naturali
		- Inondazioni, incendi, terremoti, tempeste [...]
	- Minacce Umane
		- Intenzionali
			- Utenti esterni come cracker o hacker
			- Utenti interni come dipendenti scontenti
		- Involontarie
			- Dipendenti inesperti

#### Principali tipologie di minacce

Obiettivo + Metodo + Vulnerabilità = Attacco

#### Attacchi passivi

- Lettura del contenuto ad esempio mediante lo sniffing di pacchetti sulla LAN
- Analisi del sistema e del traffico di rete, senza analizzare i contenuti

#### Attacchi attivi

- Intercettazione
- Sostituzione di un host
- Produzione
- Phishing
- Intrusione

#### Sicurezza nei sistemi informativi distribuiti

> L'obiettivo base è quello di garantire al sistema il **principio minimo di sicurezza** che consiste nella *protezione dagli attacchi passivi* e nel *riconoscimento degli attacchi attivi*

Possiamo riassumere i tre "pilastri" della sicurezza in:

- **prevenzione** (avoidance): mediante protezione dei sistemi e delle comunicazioni
- **rilevazione** (detection): mediante il monitoraggio e il controllo degli accessi tramite autenticazione con password e certificati
- **investigazione** (investigation): con l'analisi dei dati, il controllo interno con il confronto e la collaborazione degli utenti

Tecniche minime per garantire questi tre pilastri:

- **Uso della crittografia**
- **Autenticazione degli utenti**<br>Sono collegate tre diverse problematiche
	- identificazione (chi sei?)
	- autenticazione (come ne sono sicuro?)
	- autorizzazione (cosa puoi fare?)
- **Firma elettronica**

### <a href="#indice" id="U4L2">L2 - La sicurezza delle connessioni con SSL/TLS</a>

Lo standard più diffuso per la protezione dei servizi offerti tramite Internet è il **Secure Socket Layer** (**SSL**) ed è un insieme di protocolli crittografici che aggiungono funzionalità di cifratura e autenticazione a protocolli preesistenti

Il protocollo SSL garantisce la sicurezza tramite tre funzionalità fondamentali:

- **privatezza del collegamento**: il collegamento viene criptato tramite crittografia a chiave simmetrica
- **autenticazione**: l'autenticazione dell'identità viene effettuata con la crittografia a chiave pubblica
- **affidabilità**: il livello di trasporto include un controllo sull'integrità del messaggio chiamato MAC (**Message Authetication Code**)

### <a href="#indice" id="U4L3">L3 - Firewall, Proxy, ACL e DMZ</a>

È necessario interpolare tra la LAN e il mondo esterno un meccanismo che consenta di controllare il traffico in transito: il **firewall**.

> Un **firewall** è un apparato hardware-software dedicato alla *difesa perimetrale* di una rete che agisce filtrando il traffico di pacchetti entranti e/o uscenti secondo delle regole.

#### Classificazione dei firewall

Prima differenziazione fatta sul tipo di protezione che il firewall deve fare:

- **Ingress firewall**: controlla i collegamenti *incoming*, gli accessi ai servizi che sono offerti all'esterno della LAN
- **Egress firewall**: controlla i collegamenti *outgoing*, cioè l'attività del personale interno nella LAN verso l'esterno


Seconda differenziazione fatta sul numero di host protetti contemporaneamente:

- **Personal firewall**: proteggono il singolo host consentendo (generalmente) tutto il traffico outbound e bloccando tutto quello inbound
- **Network firewall**: tra la LAN e Internet, controlla il traffico passante di una rete

Terza differenziazione fatta a seconda del livello di intervento

- **Filtri di pacchetto IP**: bloccano o abilitano selettivamente il traffico
- **Serventi proxy**: una sorta di intermediario che si occupa di intrattenere le connessioni per conto di qualcun altro nella rete interna

#### Personal Firewall

Può essere un programma installato sul proprio PC che lo protegge. Il traffico verso l'esterno è consentito di default mentre il traffico dall'esterno verso l'interno è vietato di default.

#### Network Firewall

A seconda del livello di rete nel quale si fanno i controlli i network firewall possono essere classificati in:

- **packet-filtering router**: network level gateway
- **circuit gateway**: gateway a livello di trasporto
- **proxy server**: gateway a livello di applicazione

#### Packet Filter Router

Analizza le informazioni contenute nell'header TCP/IP a livello di rete e di trasporto (packet inspetion) e individua:

- IP del mittente o del destinatario
- Indirizzo MAC sorgente o di destinazione
- Numero di porta verso cui è destinato il pacchetto
- Protocollo da utilizzare

Il firewall decide se il pacchetto può essere accettato o meno attraverso un algoritmo di scelta che si basa su una lista di regole (in ordine di priorità), le filosofie applicabili sono quindi due, diametralmente opposte:

- ciò che NON è specificatamente permesso, è proibito
- ciò che NON è specificatamente proibito, è permesso

Quindi in base a queste regole i pacchetti possono essere

- accept/allow: il pacchetto passa
- deny: il firewall scarta il pacchetto, viene inviato un messaggio di errore alla sorgente
- discard/reject: il firewall scarta il pacchetto senza inviare nessun messaggio (metodologia *black hole*, elimina i pacchetto senza che la sua presenza venga rilevata)

#### ACL Access Control List

Le regole vengono disposte nelle **ACL** (**Access Control List**) dove è possibile dettagliare i filtri da applicare a ogni pacchetto in funzione delle informazioni presenti negli header TCP/IP.

- **open security policy**: tutto è permesso di default, ciò che NON è specificatamente proibito, è permesso
- **closed security policy**: tutto è negato di default, ciò che NON è specificatamente permesso, è proibito

<table>
	<thead>
		<tr>
			<th>Vantaggi</th>
			<th>Svantaggi</th>
		</tr>
	</thead>
	<tbody class="testocentro">
		<tr>
			<td>
				trasparenza<br>
				velocità<br>
				immediatezza<br>
			</td>
			<td>
				loggin limitato<br>
				vulnerabile allo spoofing<br>
				basso livello<br>
				testing complesso
			</td>
		</tr>
	</tbody>
</table>

#### Stateful Inspection

I **firewall stateful inspection** effettuano il filtraggio non sul singolo pacchetto ma sulla connessione (da qui il nome stateful). Alla richiesta di connessione, se questa viene accettata e non bloccata dalle regole di filtraggio, vengono memorizzate le sue caratteristiche in una *tabella di stato* in modo che i successivi pacchetti non vengano più analizzati.

Lo stato della connessione in un firewall di questo tipo può essere:

- **handshaking**: connessione nella fase iniziale, si raccolgono le informazioni e si salvano nella tabella di stato
- **established**: connessione stabilita
- **closing**: connessione terminata, quindi la entry corrispondente viene cancellata dalla tabella di stato

#### Application Proxy

Il **proxy** è un programma che viene eseguito sul gateway che funge da intermediario a livello di applicazione, ad esempio tra il computer dell'utente e internet, nelle applicazioni client-server un *application proxy* comunica con il client simulando di essere il server, e viceversa, comunica con il server simulando di essere il client.

Un application proxy è in grado di ispezionare l'intera porzione dati del pacchetto ed è in grado di bloccare pacchetti FTP che contengono certi nomi dei file così da inibire la connessione con determinate pagine o siti Web.

<table>
	<thead>
		<tr>
			<th>Vantaggi</th>
			<th>Svantaggi</th>
		</tr>
	</thead>
	<tbody class="testocentro">
		<tr>
			<td>
				controllo completo<br>
				log dettagliati<br>
				nessuna connessione diretta<br>
				user-friendly
			</td>
			<td>
				poco trasparente<br>
				basse performance
			</td>
		</tr>
	</tbody>
</table>

#### DMZ

La **DeMilitarized Zone** è una sezione della rete che separa la rete interna dalla rete esterna, i server nella DMZ sono accessibili dalla rete pubblica e devono essere segregati in quanto se venissero compromessi, questo non deve produrre effetti collaterali nella rete più interna.

La principale difesa contro gli attacchi è una corretta *organizzazione topologica* della rete stessa.

> Per essere definita la DMZ necessita di un *IP statico* e permette di esporre al WWW un solo indirizzo IP, quindi un solo computer, al quale vengono inoltrate tutte le richieste di connessione.

### CLASSROOM normativa sulla privacy
- giurisprudenza informatica
- legge 547/93
- legge 675/96
- D.lgs 231/2001
- D.lgs 196/2003
- articolo 18 D.lgs 30/2005
- legge 48/2008

### p.242 reti wireless
- tipologie
- standard IEEE 802.11