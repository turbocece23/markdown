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
	.hig/*hlight*/ { color:#608f47; }
</style>

# T P S I T

## Indice

- <a href="#U1">U1 - Architetture di rete e formati per lo scambio di dati</a>
	- <a href="#U1L1">**L1** *2* I sistemi distribuiti</a>
	- <a href="#U1L2">**L2** *9* Evoluzione dei sistemi distribuiti e dei modelli architetturali</a>
	- <a href="#U1L3">**L3** *21* Il modello client-server</a>
	- <a href="#U1L4">**L4** *29* Le applicazioni di rete</a>
- <a href="#U3">U3 - I socket e la comunicazione con i protocolli TCP/UDP</a>
	- <a href="#U3L1">**L1** *112* I socket e i protocolli per la comunicazione</a>
- <a href="#U4">U4 - Applicazioni lato server in Java: servlet</a>
	- <a href="#U4L1">**L1** *202* Le servlet</a>

## <a href="#indice" id="U1">U1 - Architetture di rete e formati per lo scambio di dati</a>
### <a href="#indice" id="U1L1">L1 - I sistemi distribuiti</a>

Due sviluppi importanti a partire dalla metà degli anni Ottanta: avvento dei microprocessori e la realizzazione di reti di computer ottenuto collegando singoli computer per realizzare sistemi di calcolo complessie potenti.

Le architetture dei **sistemi informativi** si sono sviluppate ed evolute nel corso degli anni successivi passando da schemi centralizzati a modelli distribuiti.

- Nei **sistemi centralizzati** le applicazioni girano in un singolo processore, o comunque su un solo host, l'unico componente autonomo nel sistema che è condiviso da vari utenti e tutte le risorse del componente sono sempre accessibili
- Nei **sistemi distribuiti** le applicazioni sono costituite da più processi, cooperanti, eseguiti in parallelo su un insime di unità di elaborazione autonome: sono quindi sistemi ottenuti dall'aggregazione di singole CPU, sistemi di memorizzazione e periferiche.

> Un sistema informatico si dice distribuito se almeno una delle seguenti due condizioni è verificata:

> - **elaborazione distribuita**: le applicazioni risiedono su più host che collaborano tra loro
> - **base di dati distribuita**: il patrimonio informativo è ospitato su più host

Su ogni componente del **sistema distribuit** viene eseguito un programma che può essere differente sia per il compito che svolge che per il ruolo di elaborazione. Alle **applicazioni** vengono dati nomi diversi in base ai diversi ruoli che svolgono:

- <span class="hig">**client**</span> (client): utilizzatore dei serivizi messi a disposizione da altre applicazioni
- <span class="hig">**server**</span> (servente): fornitore di servizi usati da altre applicazioni
- <span class="hig">**actor**</span> (attore): assume in diverse situazioni sia il ruolo di cliente che quello di servente

> Differenza tra sistemi distribuiti e sistemi paralleli:

> - un **sistema distribuio** è un insieme di computer indipendenti che *comunicano*e *possono cooperare* per risolvere problemi
> - un **sistema parallelo** è un insieme di computer che *comunicano* e *cooperano* per risolvere velocemente problemi di grandi dimensioni

#### Classificazione dei sistemi distribuiti

Tre grandi famiglie:

- <span class="hig">sistemi di calcolo distribuiti</span>
	- configurati per il calcolo ad alte prestazioni come:
		- **cluster** computing
		- **grid** computing
- <span class="hig">sistemi informativi distribuiti</span>
	- oltre al **web**, le nuove tecnologie mobile hanno fatto da volano nell'evoluzione dei sistemi informativi tradizionali
- <span class="hig">sistemi distribuiti pervasivi</span>
	- nuova generazione di sistemi che hanno tipicamente connessioni di rete wireless e che generalmente sono sottoparti di sistemi più grandi, tra di essi rientrano i **sistemi domestici**, la **peronal area network** (*PAN*), il **wearable computing** e le **reti di sensori**

#### Benefici della distribuzione

- **Affidabilità**<br>Grazie alla sua rindondanza intrinseca un SD è in grado di *sopravvivere* a un guasto di un suo componente
- **Integrazione**<br>È la capacità che ha un SD di integrare componenti spesso eterogenei tra loro, sia per tipologia hardware sia per sistema operativo. Ogni componente deve poter interfacciarsi allo stesso modo con il sottosistema di comunicazione del sisema distribuito, attraverso l'uso di protocolli standard concordati.<br>Sono stati definiti appositi linguaggi come XML e notazioni, come JSON, per favorire lo scambio di informazioni nel Web.
- **Trasparenza**<br>Come trasparenza si intende il concetto di "vedere" il SD non come un insieme di componenti ma come un unico sistema di elaborazione: l'utente non deve accorgersi che sta interagendo con un sistema distribuito ma deve avere la percezione di utilizzare un singolo elaboratore. Vi sono otto forme di trasparenza:
	- di **accesso**: si devono nascondere le differenze nella rappresentazione di dati e nelle modalità di accesso alle risorse, cisì che si possa accedere a risorse locali e remote con le stesse operazioni
	- di **locazione**: si deve nascondere dove è localizzata una risorsa e negare l'accesso se non si conosce la sua ubicazione
- **Economicità**<br>Generalmente i SD offrono un miglior rapporto prezzo/qualità dei sistemi centralizzati basati su mainframe
- **Apertura**<br>Con la definizione di protocolli standard si favorisce l'apertura all'hardware e al software di fornitori diversi in modo da avere:
	- interoperabiltà
	- portabilità
	- ampliabilità
- **Connettività e collaborazione**<br>Nei sistemi distribuiti la possibilità di condividere risorse hardware e software comporta vantaggi economici. Lo scambio e la condivisione di informazioni/risorse arricchisce ogni utilizzatore.
- **Prestazioni e scalabilità**<br>La crescita di un SD con l'aggiunta di nuove risorse fornisce a tutti i suoi componenti un miglioramento delle prestazioni e permette di sostenere l'aumento del carico di richieste: questa possibilità prende il nome di *scalabilità orizzontale*
- **Tolleranza ai guasti**<br>La possibilità di replicare risorse offre una certa garanzia di tolleranza ai gausti. In questa situazione si parla di "guasto parziale", cioè che non influenza pesantemente il funzionamento del sistema

#### Svantaggi legati alla distribuzione

- **Produzione del software**<br>I programmatori del secolo scorso hanno dovuto modificare il proprio stile di programmazione per poter realizzare SD. È avvenuto in tre fasi:
	- definizione dello standard TCP/IP
	- sviluppo delle architetture Web
	- diffondersi del linguaggio Java, che permette a programmi di essere eseguiti su macchine anche completamente differenti tra loro
- **Complessità**<br>I SD sono più complessi di quelli centralizzati, è anche più difficile saggiare la performance di un SD rispetto ad un unico componente
- **Sicurezza**<br>Con la connessione di più host tra loro si crea la possiblità di accedere a dati e risorse anche a chi non ne ha il diritto, prima bastava proteggere il sistema dall'accesso fisico delle persone ai locali.
- **Comunicazione**<br>Il trasferimento a distanza delle informazioni richiede nuove tipologie di sistmei di telecomunicazioni, sia cablati che wireless

### <a href="#indice" id="U1L2">L2 - Evoluzione dei sistemi distribuiti e dei modelli architetturali</a>

<table>
	<thead>
		<tr>
			<td></td>
			<th>Dati Singoli</th>
			<th>Dati Multipli</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th>Istruzioni Singole</th>
			<td class="testocentro">SISD</td>
			<td class="testocentro">SIMD</td>
		</tr>
		<tr>
			<th>Istruzioni Multiple</th>
			<td class="testocentro">MISD</td>
			<td class="testocentro">MIMD</td>
		</tr>
	</tbody>
</table>

#### SISD
Tutte le macchine che hanno una singola CPU
#### SIMD
Più flussi di dati paralleli sottoposti ad un singolo flusso di informazioni: presenti più processori che eseguno la stessa istruzione su flussi di dati diversi
#### MISD
Più istruzioni sullo stesso flusso di dati, più processori con la propria memoria effettuano operazione diverse sugli stessi dati
#### MIMD
Comprende tutte le tipologie di computer composti da più CPU che lavorano su stream di informazioni indipendenti

### <a href="#indice" id="U1L3">L3 - Il modello client-server</a>

Un insieme host che gestiscono una o più risorse detti server o serventi e un insime di client o clienti che richiedono l'accesso ad alcune risorse ai server.

> Un **servizio** è un entità astratta che viene fornito da uno o più server che lavorano su macchine spesso differenti e che cooperano via rete.

### <a href="#indice" id="U1L4"> L4 - Le applicazioni di rete</a>

Il livello applicazione implementa vari protoclli, tra cui:

- **SNMP 161,162** (Simple Network Management Protocol)
- **SMTP 25** (Simple Mail Transfer Protocol)
- **POP3 110** (Post Office Protocol)
- **FTP 21** (File Transfer Protocol)
- **HTTP 80** (HyperText Transfer Protocol)
- **DNS 53** (Domain Name System)

In generale un'applicazione di rete è costituita da un insieme di programmi che vengono eseguiti su due o più computer contemporaneamente, questi operano interagendo tra loro utilizzando delle risorse comuni, accedendo cioè **concorrentemtente** ai database

#### Identificazione mediante Socket

Affinché un processo, presente su un determinato host invii un messaggio a un qualsiasi altro host, il processo mittente deve identificare il processo destinatario in modo univoco. L'identificazione deve tenere conto di due informazioni, l'**indirizzo IP** e il **processo** appartenente a quel determinato host

<table>
	<thead>
		<tr>
			<th>Nome</th>
			<th colspan="2">Processo</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td class="testocentro" style="color: dodgerblue;">Indirizzo IP</td>
			<td class="testocentro" style="color: orangered;">Protocollo</td>
			<td class="testocentro" style="color: orangered;">Porta</td>
		</tr>
		<tr>
			<td class="testocentro" style="color: dodgerblue;">Globalmente Unico</td>
			<td colspan="2" class="testocentro" style="color: orangered;">Specifico dell'host</td>
		</tr>
	</tbody>
</table>

#### Scelta dell'architettura per l'applicazione di rete

- client server
- peer-to-peer (P2P)
- architetture ibride (dove convivono client-server e P2P)

#### Client-Server

Deve esserci un **server attivo** che offre un servizio, restando in attesa che uno o più client si connettano a esso per poter rispondere alle richieste che gli vengono effettuate.

#### Peer-to-Peer

Un sistema **P2P** è formato da un insieme di entità autonome capaci di auto organizzarsi, che condividono un insieme di risorse distribuite presenti all'interno di una rete. Il sistema utilizza tali risorse per fornire una determinata funzionalità in modo completamente o parzialmente decentralizzato.

- **P2P decentralizzato**: ogni peer è sia client che server, è impossibile localizzare una risorsa mediante un indirizzo IP statico, vengono effettuati nuovi meccanismi di indirizzamento, definiti a livello superiore rispetto al livello IP, il sistema P2P è capace di adattarsi a un continuo cambiamento dei nodi partecipanti, mantenendo connettività e prestazioni accettabili senza richiedere l'intervento di alcuna entità centralizzata
- **P2P centralizzato**:  ha un server centrale che conserva informazioni sui peer e risponde alle richieste su quelle informazioni effettuando quindi la ricerca in modalità centralizzata
- **P2P ibrido**: è un P2P parzialmente centralizzato dove sono presenti alcuni peer (detti *supernodi* o *super-peer*) determinati dinamicamente che hanno la funzione di indicizzare: gli altir nodi sono chiamati *leaf peer*

## <a href="#indice" id="U3">U3 - I socket e la comunicazione con i protocolli TCP/UDP</a>
### <a href="#indice" id="U3L1">L1 - I socket e i protocolli per la comunicazione</a>

Ogni singola connessione viene identificata in modo univoco attraverso una struttura detta **association**

<table>
	<tbody>
		<tr>
			<td rowspan="2" class="testocentro" style="color: seagreen;"><b>Protocollo: TCP/UDP [...]</b></td>
			<td class="testocentro" style="color: firebrick"><b>Indirizzo IP (locale)</b></td>
			<td class="testocentro" style="color: deepskyblue;"><b>Indirizzo IP (remoto)</b></td>
		</tr>
		<tr>
			<td class="testocentro" style="color: firebrick"><b>Porta (locale)</b></td>
			<td class="testocentro" style="color: deepskyblue;"><b>Porta (remota)</b></td>
		</tr>
	</tbody>
</table>

## <a href="#indice" id="U4">U4 - Applicazioni lato server in Java: servlet</a>
### <a href="#indice" id="U4L1">L1 - Le servlet</a>

Applicazioni che permettono ad utenti connessi da host localizzati in ogni parte del globo di accedere a informazioni presenti su server remoti.

Tramite pagine HTML e mediante un semplice form, l'utente comila dei cami e li invia ad un server, il quale li elabora e risponde inviandogli l'esito della compilazione.

Le applicazioni remote sfruttano sostanzialmente due tecniche:

- **Common Gateway Interface** (**CGI**)<br>Un programma CGI che viene eseguito sul server e al quale vengono passati i dati letti nel form. Può essere realizzato con qualunque linguaggio di programmazione che può leggere da standard input e scrivere nello standard output
- **Servlet**<br>Usano il linguaggio Java e sono classi particolari con molte affinità con le applet
	- Le CGI vengono eseguite dal sistema operativo quindi meno portabili delle Servlet che vengono eseguite dalla JVM integrata nel web server
	- Gli script CGI vengono caricati ed eseguiti una volta per ogni richiesta, richiedono quindi sempre un notevole tempo di latenza. Le servlet invece vengono caricate una sola volta e viene creato un thread per ogni richiesta.
	- A vantaggo degli script CGI c'è la possibilità di utilizzare pressoché qualsiasi linguaggio, mentre le servlet sono classi Java e quindi devono essere scritte in Java