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
	h5 { color: #7C839D; }
	
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
- **Affidabilità dei documenti**: avere la garanzia e la certezza che un documento sia originale, il mittente è certo e non è stato letto e/o alterato da persone non autorzzate

#### Crittografia

Desiderio di mantenere messaggi tra due interlocutori nascosti agli occhi di terzi.

- **Codifica**: sostituisce parole con altre
- **Cifratura**: sostituisce lettere o caratteri

Quando la chiave di cifratura coincide con quella di decifratura lo schema crittografico si dice **simmetrico** e la chiave prende il nome di **chiave comune**.

Quando la chiave di cifratura è diversa da quella di decifratura lo schema crittografico si dice **asimmetrico** e le due chiavi si chiamano:

- **chiave pubblica**: usata per la cifratura, comune a tutti i mittenti e di pubblico dominio
- **chiave privata**: utilizzata per la decifratura, segreta e di conoscenza solo del destinatario del messaggio

#### Crittoanalisi

Studio dei metodi per ottenere il significato di informazioni cifrate: tipicamente si tratta delle operazioni effettuate alla ricerca della chiave segreta.

Il **principio di Kerckhoffs** stabilisce che è la chiave l'elemento fondamentale per la sicurezza di un sistema informatico. La sicurezza di un crittosistema deve dipendere solo dalla segretezza della nchiave e non dalla segretezza dell'algoritmo usato.

#### Cifrari e chiavi

La crittografia permette di:

- **identificare** un utente all'accesso alla rete o al singolo PC
- **autenticare** un messaggio, cioè accertarsi dell'identità dell'autore e dell'integrità del messaggio ricevuto
- **firmare digitalmente** un messaggio, cioè accertarsi dell'identità dell'autore e quindi la non ripudiabilità del messaggio stesso

#### <span class="hig">Il cifrario DES</span>

È un algoritmo simmetrico a chiave segreta di 64 bit, 8 sono di controllo, questa chiave prevede 16 trasformazioni successive applicate a ogni blocco del messaggio

Il **DES** rispetta il principio di **Kerckhoffs**, cioè l'algoritmo è noto e la chiave è segreta ed è statp realizzato applicando i principi di **Shannon**:

- **diffusione** dei caratteri consecutivi del messaggio in tutto il crittogramma
- **confusione** del messaggio con la chiave

Il *DES* viene anche usato per cifare file personali su un disco locale ma:

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
Non è il metodo ideale per le comunicazioni su Internet principalmente perché il limte fonamentale è rappresentato dalla necessità di un canale sicuro e di un accordo preventivo per lo scambio delle chiavi. L'idea alla base delle **crittografie simmetriche** è quello di avere due chiavi diverse, una pubblica per la criptazione e una privata per la decriptazione.

Con la **crittografia asimmetrica**:

- si risolve il problema della **riservatezza**: criptando il messaggio con la chiave pubblica, solo il possessore della chiave privata è in grado di decriptarlo
- si risolve il problema dell'**autenticità del mittente**: a ogni chiave pubblica è associata l'identità certa del proprietario

Il principale svantaggio della *crittografia asimmetrica* è la complessità dei calcoli che rendono poco efficiente la loro implementazione sopratutto con l'aumentare della lunghezza della chiave.

Per mantenere relativamente leggeri gli algoritmi asimmetrici viene estratta una sequenza di numeri dal messaggio originale chiamata **fingerprint** utilizzata per le funzioni di hash *MD4* e **MD5**.

#### <span class="hig">RSA</span>

L'algoritmo RSA lavora sfruttando i numeri primi e come chiave utilizza un numero n ottenutoproprio dal prodotto di due numeri primi **p** e **q** cioè **n = p * q**

Usato per codificare un unico messaggio contenente una chiave segreta, tale chiave verrà poi utilizzata per scambiarsi messaggi tramite un algoritmo a chiave segreta (ad esempio **AES**)

#### Crittografia ibrida

Per gestire le chiavi pubbliche è necessario un sistema di **PKI** (**Public Key Infrastructure**) che si occupi della gestione e dello scambio delle chiavi.

<table>
	<thead>
		<tr>
			<th></th>
			<th>Crittografia simmetirca</th>
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


- generalità
- firme digitali
- funzione hash
	- funzione MD5
	- funzione SHA
- algoritmo PGP
- certificati
	- certification authority
	- PKI
	- richiesta di certificato digitale

## <a href="#indice" id="U4">U4 - La sicurezza delle reti</a>
### <a href="#indice" id="U4L1">L1 - La sicurezza nei sistemi informativi</a>
- minacce naturale
- minacce umane
- minacce in rete
- breve storia attacchi informatici
- sicurezza sistema informativo
- sicurezza informatica
- valutazione dei rischi
- principali tipologie di minacce
- attacchi attivi e attacchi passivi
- sicurezza nei sistemi distribuiti

### <a href="#indice" id="U4L2">L2 - La sicurezza delle connessioni con SSL/TLS</a>
- protocollo SSL/TLS
- HTTPS

### <a href="#indice" id="U4L3">L3 - Firewall, Proxy, ACL e DMZ</a>
- i firewall
- classificazione dei firewall
	- personal firewall
	- network firewall
	- packet filter router
	- ACL
	- stateful inspection
	- application proxy
	- DMZ

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