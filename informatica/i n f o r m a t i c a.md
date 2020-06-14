<style type="text/css">
	.sep
	{
		color:#ffa11a;
		text-align: center;
	}
	h1
	{
		color: #ee2020;
	}
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

	a:link { color: white; }
	a:visited { color: white; }
	ol a:link { color: black; }
	ol a:visited { color: black; }
	.hig/*hlight*/ { color:#32739C; }
</style>

# Indice

<ol>
	<li><a href="#intro">Introduzione ai database</a></li>
	<li><a href="#fasi">Fasi di progettazione di un DB</a></li>
	<li><a href="#vincoli">Vincoli di integrità</a></li>
	<li><a href="#sql">Linguaggio SQL</a></li>
	<li><a href="#transazioni">Transazioni</a></li>
	<li><a href="#stored">Stored procedures</a></li>
	<li><a href="#ristrutturazione">Ristrutturazione</a></li>
	<li><a href="#trigger">Trigger</a></li>
	<li><a href="#algebra">Algebra relazionale</a></li>
	<li><a href="#normalizzazione">Normalizzazione</a></li>
	<li><a href="#viste">Viste</a></li>
</ol>

## <a id="intro" href="#indice">Introduzione</a>
### Introduzione alle basi di dati
Una **base di dati** (o database) è una raccolta di *dati logicamente correlati* ed è utilizzata per *modellare una realtà*.

I dati sono memorizzati su un supporto di massa e progettati per essere fruiti da diverse applicazioni e utenti.

Una base di dati deve essere:

- **Sicura**: progettata in modo da impedire che venga danneggiata da danni accidentali
- **Integra**: le operazioni effettuate da utenti autorizzate non provocano una perdita di consistenza dei dati
- **Consistente**: i dati devono essere significativi ed effettivamente utilizzati nelle applicazioni
- **Condivisibile**: applicazioni e utenti diversi devono poter accedere ai dati comuni
- **Persistente**: deve avere un tempo di vita non limitato alle singole esecuzioni dei programmi che lo utilizzano (come le viste)
- **Scalabile**: deve mantenere intatte le proprie performance all'aumentare della quantità di dati

### Differenza tra sistema informatico e sistema informativo:
- **Sistema informativo**:<br>è un insieme organizzato di strumenti automatici, procedure, norme, risorse, dati, orientato alla gestione delle informazioni. Con gestione si intende la raccolta, archiviazione e scambio delle informazioni necessarie alle attività operative, di gestione, di controllo dell'organizzazione. Per esempio il sistema informativo di un'università contiene i dati riguardanti gli studenti, i docenti, le relazioni fra insegnanti ed aule, i corsi...
- **Sistema informatico**:<br>è l'insieme degli strumenti informatici utilizzati per il trattamento automatico delle informazioni. Quindi potremmo dire che il sistema informatico è l'insieme dei strumenti informatici che consentono l'automazione (in genere solo parziale) del sistema informativo

### Modelli di dati
Un **modello di dati** è un insieme di concetti e di costrutti utilizzati per organizzare i dati di interesse e descriverne la struttura e la dinamica.

- **Modelli concettuali**: Permettono di rappresentare i concetti in modo indipendente da ogni sistema cercando di descrivere i concetti del mondo reale
	- **Modello E-R**
- **Modelli Logici**: Consentono una specifica rappresentazione dei dati
	- **Modello Gerarchico**: record connessi tra loro secondo strutture ad albero, manutenzione complessa perché la cancellazione di una tupla comporta la cancellazione di tutti i record connessi
	- **Modello Reticolare**: organizzato in un reticolo, struttura complessa a grafo
	- **Modello Relazionale**: basato sul concetto di insiemi e di record, le connessioni/corrispondenze derivano da record di tabelle diverse
	- **Modello a Oggetti**: estende alla base di dati il concetto di programmazione ad oggetti

### I DBMS
Un DBMS (come SQL server, Access, MySQL..) è un insieme di strumenti software che, partendo dalle specifiche dell'utente, è in grado di gestire dati strutturali. È quindi un'interfaccia tra gli sviluppatori, gli utenti del DB e il sistema di elaborazione

I dati gestiti sono:

- tanti
- importanti
- condivisi
- interrogati
- aggiornati

Un DBMS deve essere:

- **Efficiente**: capace di svolgere sempre le operazioni richieste
- **Efficace**: capace di rendere produttive e semplici le attività richieste dagli utenti

Un DBMS deve permettere 4 le operazioni di:

- **Creazione**
- **Inserimento**
- **Aggiornamento**
- **Interrogazione**

### I livelli di un DBMS
- **Fisico o Interno** (**DML**, Data Manipulation Language): riguarda la memorizzazione dei dati, organizzati in file, record e strutture di accesso
- **Logico o Concettuale** (**DDL, DCL**, Data Definition Language e Data Control Language): Riguarda la struttura logica assunta dai dati registrati, quindi il loro schema  astratto
- **Esterno** (**DMCL**, Device Media Control Language): si riferisce al modo in cui ciascun utente vede i dati che vengono messi a disposizione secondo il formato richiesto



## <a href="#indice" id="fasi">Fasi</a>
### Le fasi di progettazione di un database
- **Concettuale**: permette di costruire e definire una rappresentazione corretta e completa della realtà di interesse.
	- Presa in input una realtà di riferimento, genera un diagramma ER
- **Logica**: trasforma il diagramma ER in uno schema logico, efficiente rispetto alle strutture del sistema di gestione che si intende utilizzare.
	- Preso in input un diagramma ER genera uno schema logico delle relazioni rappresentato tramite tabelle
- **Fisica**: implementa lo schema logico definendone gli aspetti fisici di memorizzazione e rappresentazione in memoria di massa.
	- Preso in input lo schema logico con le tabelle le implementa nella memoria di massa

### La progettazione Concettuale
La realtà di riferimento rappresentata in uno schema ER sarà descritta attraverso:

- **Entità**, ciò che esiste all'interno della realtà e si vuole modellare in modo da rappresentarne le caratteristiche
- **Attributi** che definiscono le caratteristiche dell'entità presa in esame, definiti da caratteristiche come:
	- Nome
	- Formato o Tipo di attributo
	- Dimensione
	- Valore
	- Opzionalità
- **Associazioni o Relazioni** che connettono le varie entità
	- *Associazione totale*: il legame tra entità deve essere sempre presente
	- *Associazione parziale*: quando il legame tra le entità può non esserci
	- La molteplicità/cardinalità di un associazione indica quante istanze possono trovarsi in relazione tra le 2 entità, queste possono essere di diverse tipologie:
		- 1:1 o biunivoca: a 1 istanza di A corrisponde 1 istanza di B
		- 1:N o semplice: a 1 istanza di A possono corrispondere una o più istanze di B e a ogni istanza di B solo un istanza di A
		- N:M o complessa: a ogni istanza di A possono corrispondere una o più istanze di B e viceversa



## <a href="#vincoli" id="intro">Vincoli di integrità</a>

Vincoli **intra**-relazionali (all'interno della tabella):

- **di tupla**: coinvolge più valori della stessa tupla (come "30" e "con Lode")
- **di chiave**: la chiave di una relazione non consente valori null o duplicati
- **not null**: il campo con il seguente vincolo deve avere un valore
- **di dominio**: per ogni attributo bisogna specificare il tipo di dato

Vincoli **inter**-relazionali (che riguardano le chiavi esterne):

- **Vincolo di integrità referenziale**: gli attributi di una data tabella (slave) possono assumere soltanto dei valori specificati in un'altra tabella (master). L'**integrità referenziale** è l'insieme di regole che garantiscono l'integrità dei dati quando si hanno relazioni con chiave esterne.

Vincoli di **cancellazione**:

- **Restrizione**: cancella il padre solo se non ci sono figli
- **Cascata**: cancella sia il padre che i figli
- **Nullo**: la chiave esterna nel figlio viene impostata a null
- **Default**: la chiave esterna nel figlio viene impostata ad un valore di default
- **Nessun effetto**: non viene fatto il controllo di chiave esterna

Vincoli di **inserimento/modifica**:

- **Dipendente**: si può inserire/modificare un figlio solo se esiste un padre
- **Automatico**: se il padre non esiste viene creato
- **Nullo**: la chiave del padre nel figlio viene impostata a null
- **Default**: la chiave del padre nel figlio viene impostata ad un valore di default
- **Nessun effetto**: non viene fatto il controllo

## <a href="#indice" id="sql">SQL</a>
Structured Query Language, è un linguaggio per l'interrogazione e la gestione di basi di dati

Comandi SQL, divisi in 3 categorie: DDL,DML,DCL:

- DDL = Data Definition Language (Create, Alter, Drop) - agisce sullo schema del database
- DML = Data Manipulation Language (Insert, Select, Delete, Update) - agisce sui dati del tatabase
- DCL = Data Control Language - gestisce i permessi nel DB



## <a href="#indice" id="transazioni">Transazioni</a>
Una transazione è una sequenza di operazioni, che può concludersi positivamente o
negativamente, in caso positivo il risultato delle operazioni deve essere permanente (**commit work**), mentre in caso negativo si deve tornare allo stato prima della transazione (**rollback**).

Le Transazioni rispettano le proprietà **ACID**

**A**tomicity, **C**onsistency, **I**solation, e **D**urability

- <span style="color:#fa4545">Atomicità</span>: il processo deve essere suddivisibile in un numero finito di unità indivisibili, chiamate transazioni. L'esecuzione di una transazione perciò deve essere per definizione o totale o nulla e non sono ammesse esecuzioni parziali. Un processo, anche parziale, invece, in quanto insieme di transazioni può non essere elementare (Un processo è costituito da più transazioni).
- <span style="color:#fa4545">Coerenza</span>: il database rispetta i vincoli di integrità, sia a inizio che a fine transazione. Non devono verificarsi contraddizioni (incoerenza dei dati) tra i dati archiviati nel DB.
- <span style="color:#fa4545">Isolamento</span>: ogni transazione deve essere eseguita in modo isolato e indipendente dalle altre transazioni, l'eventuale fallimento di una transazione non deve interferire con le altre transazioni in esecuzione.
- <span style="color:#fa4545">Durabilità</span> detta anche persistenza, si riferisce al fatto che una volta che una transazione abbia richiesto un commit work, i cambiamenti apportati non dovranno essere più persi. Per evitare che nel lasso di tempo fra il momento in cui la base di dati si impegna a scrivere le modifiche e quello in cui li scrive effettivamente si verifichino perdite di dati dovuti a malfunzionamenti, vengono tenuti dei registri di log dove sono annotate tutte le operazioni sul DB.



## <a href="#indice" id="stored">Stored procedures</a>
Durante lo sviluppo di un applicazione client le richieste per l'interrogazione di dati possono essere inviate direttamente al database. dal programma, tramite istruzioni, oppure è possibile creare piccoli programmi o funzioni all'interno del database e poi farle eseguire dal programma esterno. Queste procedure si chiamano Stored Procedure.

Fanno parte di una branca del linguaggio *SQL* che prende il nome di **T-SQL**.

Una stored procedure può accettare parametri di input, restituire al client risultati tabellari o scalari, richiamare istruzioni DDL (Data Definition Language) e DML (Data Manipulation Language)

Le stored procedure accettano parametri in input (IN), parametri in output (OUT) e vi è anche una combinazione di questi due che si chiama (INOUT)



## <a href="#indice" id="ristrutturazione">Ristrutturazione</a>
Fasi:

- **Analisi delle ridondanze**: si decidere se mantenere o eliminare eventuali ridondanze (ripetizioni) presenti nello schema
- **Raggruppamento o divisione di entità e associazioni**: si decide se è opportuno partizionare concetti dello schema, i più sotto-concetti più semplici, o viceversa, accorpare concetti separati in un unico concetto
- **Eliminazione delle gerarchie "Is A" (le generalizzazioni/specializzazioni)**: il modello relazionale non rappresenta le gerarchie, e quindi vanno sono sostituite da entità e associazioni
- **Selezione delle chiavi primarie**: si seleziona un identificatore per quelle entità che ne hanno più di una. Vengono invece eliminate le identificazioni esterne
- **Normalizzazione**: degli attributi composti o multipli



## <a href="#indice" id="trigger">Trigger</a>
Sono eventi che vengono mandati in esecuzione quando si verificano determinate condizioni come di tempo o a seguito di altre operazioni avvenute sul database

### Il paradigma E C A
- Evento: al verificarsi di un azione predeterminata, il trigger si attiva in maniera automatica 
- Condizione: perché il mio trigger si attivi deve essere soddisfatta una determinata condizione
- Azione: il trigger, in base al risultato dell'operazione ottenuta dalla condizione, ottengo un output descritto dal mio trigger

### Trigger a livello di istruzione
I trigger a livello di istruzione vengono eseguiti una sola volta per ogni istruzione DML, per esempio se viene eseguita una singola istruzione DML *INSERT* avesse inserito 500 righe in una tabella, un trigger a livello di istruzione viene eseguito una sola volta.

### Trigger a livello di tupla
I trigger a livello di tupla vengono eseguiti tante volte quante sono le righe di una tabella specificata come ingresso, per esempio se esiste un trigger a livello di tupla per l'esempio precedente, esso si attiva 500 volte, una volta per ogni riga della tabella.

### Sintassi
- BEFORE e AFTER: si verificano prima o dopo di un'istruzione predeterminata
- INSTEAD OF: si attivano e si sostituiscono ad una determinata azione
- DEFINER: determina i privilegi da applicare quando il trigger è attivo
- TRIGGER_TIME: rappresenta il tipo di trigger (BEFORE o AFTER)
- TRIGGER_EVENT: indica il tipo che attiva il trigger (come insert)



## <a href="#indice" id="algebra">Algebra relazionale</a>
### Definizione
È un linguaggio:

- formale
- procedurale
- per formulare interrogazioni

ed è basato su *5* operazioni fondamentali:

- Operazioni
	- Fondamentali
		- Unarie
			- Selezione σ
			- Proiezione ∏
		- Binarie
			- Unione ∪
			- Differenza −
			- Prodotto Cartesiano X
	- Derivate
		- Binarie
			- Intersezione ∩
			- Join (Due triangoli distesi che si danno un bacino tipo ><)
				- Semi-join (Due triangoli che si danno un bacino ma uno non ha il culo [la base])
			- Divisione ÷

Tipi di Join

- **Inner Join**: fa corrispondere ad un elemento di una tabella un elemento uguale in un'altra tabella
- **Cross Join**: seleziona tutte le possibili combinazioni di righe e colonne da entrambe le tabelle
- **Full Join**: unisce tutte le righe di entrambe le tabelle, lasciando nulli i valori che non trovano corrispondenza
- **Left Join**: restituisce tutti i valori della tabella a sinistra e solo quelli che soddisfano la condizione da quella di destra
- **Right Join**: restituisce tutti i valori della tabella a destra e solo quelli che soddisfano la condizione da quella di sinistra
- **Self Join**: usata su una tabella serve a mettere in relazione alcuni dati all'interno della stessa tabella

### L'interrogazione dei dati
L'operazione fondamentale per manipolare una base di dati è l'*interrogazione*. Con l'interrogazione si esegue l'accesso ai dati desiderati, dopo aver ottenuto questo accesso è possibile:

- modificarli (**update**)
- cancellarli (**delete**)
- inserirne di nuovi (**insert**)
- aggiungerne (**append**)
- ignorarli



## <a href="#indice" id="normalizzazione">Normalizzazione</a>
Non è una metodologia di progettazione, è bensì una procedura che permette di trasformare schemi non normalizzati in schemi che soddisfano una forma normale. La **normalizzazione** quindi è un processo di tipo graduale che realizza un'ottimizzazione progressiva a partire da relazioni non normalizzate fino a raggiungere un certo livello di normalizzazione.

Se una relazione non è normalizzata essa presenta alcuni difetti:
- Ridondanze
- Comportamenti poco desiderabili durante gli aggiornamenti

La tabella iniziale vine scomposta in più tabelle che complessivamente forniscono le stesse informazioni della tabella di partenza, vengono mantenute le dipendenze tra attributi, ogni attributo però ora dipende direttamente da una chiave. Vengono quindi evitati problemi di ridondanza e di inconsistenza dei dati. Cosa importante, non ci deve essere perdita complessiva delle informazioni.

L'obiettivo è quello di:

- minimizzazione della ridondanza
- minimizzazione delle anomalie di
	- inserimento
	- cancellazione
	- modifica

Si ha **dipendenza funzionale** tra attributi quando il valore di un insieme di attributi **A** determina un singolo valore dell'attributo **B** e si indica con **A -> B**. Si dice anche che **B** dipende da **A** o che **A** è un determinante per **B**.

Si ha dipendenza transitiva quando **A** determina **B** e **B** determina **C**. Si dice allora che **C** dipende transitivamente da **A**

> <span style="color:#14A1FA">**Dipendenza transitiva**</span>: **A -> B -> C**<br>C dipende transitivamente da A

> <span style="color:#14A1FA">**Dipendenza funzionale**</span>: **A -> B**<br>B dipende da A<br>A è un determinante di B

### 1FN

**Il dominio di un attributo (valori che può assumere) deve comprendere solo valori atomici (semplici, indivisibili)**. Ogni attributo è elementare, non ci sono righe uguali, non ci sono attributi di gruppo o ripetuti.

### 2FN
È in prima forma normale e **non ci sono attributi non-chiave che dipendono parzialmente dalla chiave**.

La seconda forma normale riguarda quindi le tabelle in cui la chiave primara sia composta da più attributi e stabilisce che tutte le colonne corrispondenti a quegli attributi dipendano dall'intera chiave primaria (e non da una sua parte).

### 3FN
È in seconda forma normale e non ci sono attributi non chiave che dipendono transitivamente dalla chiave (non dipendono da attributi i quali dipendono dalla chiave, **A**->B-C)

### BCNF
Una relazione è in forma normale di *Boyce-Codd* se e solo se, per ogni dipendenza funzionale X->Y, X è una chiave candidata.

Una relazione in **BCNF** (*Boyce-Codd Normal Form*) è anche in **2FN** e in **3FN**, perché la BCNF esclude che un determinante (X) possa essere composto solo da una parte della chiave (violerebbe la **2FN**), o che possa essere esterno alla chiave (violerebbe la **3FN**).

Quindi una relazione che rispetta la forma normale di Boyce-Codd è anche in terza forma normale (è già in 1FN, in 2FN e quindi ora è in 3FN, tipo evoluzione finale di un Pokémon), ma non è vero l'opposto, cioè che una relazione in **3FN** NON è anche in **BCFN**.

Esistono quarta e quinta forme normali ma non le abbiamo studiate.

## <a href="#indice" id="viste">Viste</a>
Tabelle virtuali con "durata temporanea", da usare in sostituzione alle **JOIN**, la vista viene aggiornata solo all'esecuzione della query che la genera.