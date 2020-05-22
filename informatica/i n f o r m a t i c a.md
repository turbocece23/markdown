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
</style>

# Indice

1. Introduzione ai database
2. Fasi di progettazione di un DB
3. Vincoli di integrità
4. Linguaggio SQL
	- DDL e DML
5. Transazioni
6. Stored procedures
7. Ristrutturazione
8. Trigger
9. Algebra relazionale
10. Normalizzazione
	- 1FN
	- 2FN
	- 3FN
	- BCNF
11. Viste

## <span class="sep">════════════════════════════</span>

# Fasi

## Le fasi di progettazione di un database
- **Concettuale**: permette di costruire e definire una rappresentazione corretta e completa della realtà di interesse.
Presa in input una realtà di riferimento, genera un diagramma ER
- **Logica**: trasforma il diagramma ER in uno schema logico, efficiente rispetto alle strutture del sistema di gestione che si intende utilizzare
Preso in input un diagramma ER genera uno schema logico delle relazioni rappresentato tramite tabelle
- **Fisica**: implementa lo schema logico definendone gli aspetti fisici di memorizzazione e rappresentazione in memoria di massa
Preso in input lo schema logico con le tabelle le implementa nella memoria di massa

## <span class="sep">════════════════════════════</span>

# Introduzione

## Differenza tra sistema informatico e sistema informativo:

- **Sistema informativo**: è un insiema organizzato di strumenti automatici, procedure, norme, risorse, dati, orientato alla gestione delle informazioni, con gestione si intende la raccolta, archiviazione e scambio delle informazioni necessarie alle attività operative, di gestione, di controllo dell’organizzazione. Per esempio il sistema informativo di un’università contiene i dati riguardanti gli studenti, i docenti, le relazioni fra insegnanti ed aule, i corsi...
- **Sistema informatico**: è l’insieme degli strumenti informatici utilizzati per il trattamento automatico delle informazioni. Quindi potremmo dire che il sistema informatico è l’insieme dei strumenti informatici che consentono l’automazione (in genere solo parziale) del sistema informativo

## I DBMS

Un DBMS (come SQL server, Access, MySQL..) è un insieme di strumenti software che, partendo dalle specifiche dell’utente, è in grado di gestire dati strutturali. È quindi un’interfaccia tra gli sviluppatori, gli utenti del DB e il sistema di elaborazione

## I livelli di un DBMS
- Fisico: riguarda la memorizzazione dei dati, organizzati in file, record e strutture di accesso
- Logico: Riguarda la struttura logica assunta dai dati registrati, quindi il loro schema  astratto
- Esterno: si riferisce al modo in cui ciascun utente vede i dati che vengono messi a disposizione secondo il formato richiesto

## <span class="sep">════════════════════════════</span>

# Vincoli

Vincoli **intra**-relazionali (all’interno della tabella)
- di tupla
- di chiave
- not null
- di dominio
 
Vincoli **inter**-relazionali (che riguardano le chiavi esterne)
- integrità relazionale

## <span class="sep">════════════════════════════</span>

# SQL

Structured Query Language, è un linguaggio per l’interrogazione e la gestione di basi di dati

Comandi SQL, divisi in 3 categorie: DDL,DML,DCL:
- DDL = Data Definition Language (Create, Alter, Drop)
- DML = Data Manipulation Language (Insert, Select, Delete, Update)
- DCL = Data Control Language

## DDL
Data Definition Language (Create, Alter, Drop)

## DML
Data Manipulation Language (Insert, Select, Delete, Update)

## <span class="sep">════════════════════════════</span>

# Transazioni

Una transazione è una sequenza di operazioni, che può concludersi positivamente o
negativamente, in caso positivo il risultato delle operazioni deve essere permanente (**commit work**), mentre in caso negativo si deve tornare allo stato prima della transazione (**rollback**).

Le Transazioni rispettano le proprietà **ACID**

**A**tomicity, **C**onsistency, **I**solation, e **D**urability

- <span style="color:#fa4545">Atomicità</span>: il processo deve essere suddivisibile in un numero finito di unità indivisibili, chiamate transazioni. L'esecuzione di una transazione perciò deve essere per definizione o totale o nulla e non sono ammesse esecuzioni parziali. Un processo, anche parziale, invece, in quanto insieme di transazioni può non essere elementare (Un processo è costituito da più transazioni).
- <span style="color:#fa4545">Coerenza</span>: il database rispetta i vincoli di integrità, sia a inizio che a fine transazione. Non devono verificarsi contraddizioni (incoerenza dei dati) tra i dati archiviati nel DB.
- <span style="color:#fa4545">Isolamento</span>: ogni transazione deve essere eseguita in modo isolato e indipendente dalle altre transazioni, l'eventuale fallimento di una transazione non deve interferire con le altre transazioni in esecuzione.
- <span style="color:#fa4545">Durabilità</span> detta anche persistenza, si riferisce al fatto che una volta che una transazione abbia richiesto un commit work, i cambiamenti apportati non dovranno essere più persi. Per evitare che nel lasso di tempo fra il momento in cui la base di dati si impegna a scrivere le modifiche e quello in cui li scrive effettivamente si verifichino perdite di dati dovuti a malfunzionamenti, vengono tenuti dei registri di log dove sono annotate tutte le operazioni sul DB.

## <span class="sep">════════════════════════════</span>

# Stored procedures

Durante lo sviluppo di un applicazione client le richieste per l'interrogazione di dati possono essere inviate direttamente al database. dal programma, tramite istruzioni, oppure è possibile creare piccoli programmi o funzioni all'interno del database e poi farle eseguire dal programma esterno. Queste procedure si chiamano Stored Procedure.

Fanno parte di una branca del linguaggio *SQL* che prende il nome di **T-SQL**.

Una stored procedure può accettare parametri di input, restituire al client risultati tabellari o scalari, richiamare istrudzioni DDL (Data Definition Language) e DML (Data Manipulation Language)

Un linguaggio è detto **dichiarativo** o **logico** quando le istruzioni descrivono le relazioni che intercorrono tra i dati, lo sviluppatore descrive l'insieme delle relazioni che sussistono tra i dati e il risultato atteso.

Un linguaggio dichiarativo viene invece denominato **procedurale** quando per esso non si ragiona in termini di relazioni tra dati ma intermini di assegnazione di valori ad uno spazio di memoria, i linguaggi procedurali fanno infatti parte della più ampia famiglia dei linguaggi imperativi

Le stored procedure accettano parametri in input (IN), parametri in output (OUT) e vi è anche una combinazione di questi due che si chiama (INOUT)

## <span class="sep">════════════════════════════</span>

# Ristrutturazione

Fasi:

- **Analisi delle rindondanze**: si decidere se mantenere o eliminare eventuali ridondanze (ripetizioni) presenti nello schema
- **Partizionamento di entità e associazioni**: si decide se è opportuno partizionare concetti dello schema, i più sottoconcetti più semplici, o viceversa, accorpare concetti separati in un unico concetto
- **Eliminazione delle gerarchie "Is A"**: il modello relazionale non rappresenta le gerarchie, e quindi vanno sono sostituite da entità e associazioni
- **Selezione delle chiavi primarie**: si seleziona un identificatore per quelle entità che ne hanno più di uno. Vengono invece eliminate le identificazioni esterne
- **Normalizzazione**: degli attributi composti o multipli

## <span class="sep">════════════════════════════</span>

# Trigger

Sono eventi che vengono mandati in esecuzione quando si verificano determinate condizioni come di tempo o a seguito di altre operazioni avvenute sul database

## Il paradigma E C A
- Evento: al verificarsi di un azione predeterminata, il trigger si attiva in maniera automatica 
- Condizione: perché il mio trigger si attivi deve essere soddisfatta una determinata condizione
- Azione: il trigger, in base al risultato dell'operazione ottenuta dalla condizione, ottengo un output descritto dal mio trigger

## Trigger a livello di istruzione
I trigger a livello di istruzione vengono eseguiti una sola volta per ogni istruzione DML, per esempio se viene eseguita una singola istruzione DML *INSERT* avesse inserito 500 righe in una tabella, un trigger a livello di istruzione viene eseguito una sola volta.

## Trigger a livello di tupla
I trigger a livello di tupla vengono eseguiti tante volte quante sono le righe di una tabella specificata come ingresso, per esempio se esiste un trigger a livello di tupla per l'esempio precedente, esso si attiva 500 volte, una volta per ogni riga della tabella.

## Sintassi

- BEFORE e AFTER: si verificano prima o dopo di un'istruzione predeterminata
- INSTEAD OF: si attivano e si sostituiscono ad una determinata azione
- DEFINER: determina i privilegi da applicare quando il trigger è attivo
- TRIGGER_TIME: rappresenta il tipo di trigger (BEFORE o AFTER)
- TRIGGER_EVENT: indica il tipo che attiva il trigger (come insert)

## <span class="sep">════════════════════════════</span>

# Algebra

## Definizione
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

## <span style="color:#f76b2a">L'interrogazione dei dati</span>
L'operazione fondamentale per manipolare una base di dati è l'*interrogazione*. Con l'interrogazione si esegue l'accesso ai dati desiderati, dopo aver ottentuo questo accesso è possibile:

- modificarli (**update**)
- cancellarli (**delete**)
- inserirne di nuovi (**insert**)
- aggiungerne (**append**)
- ingorarli

## <span class="sep">════════════════════════════</span>

# Normalizzazione

Non è una metodologia di progettazione, è bensì una procedura che permette di trasformare schemi non normalizzati in schemi che soddisfano una forma normale

Se una relazione non è normalizzata essa presenta alcuni difetti:
- Rindondanze
- Comportamenti poco desiderabili durante gli aggiornamenti

La tabella iniziale vine scomposta in più tabelle che complessivamente forniscono le stesse informazioni della tabella di partenza, vengono mantenute le dipendenze tra attributi, ogni attributo però ora dipende direttamente da una chiave. Vengono quindi evitati problemi di rindondanza e di inconsistenza dei dati. Cosa importante, non ci deve essere perdita complessiva delle informazioni.

## 1FN

Ogni attributo è elementare, non ci sono righe uguali, non ci sono attributi di gruppo o ripetuti (come i figli a carico).

## 2FN
È in prima forma normale e non ci sono attributi non-chiave che dipendono parzialmente dalla chiave (A->B).

## 3FN
È in seconda forma normale e non ci sono attributi non chiave che dipendono transitivamente dalla chiave (non dipendono da attributi i quali dipendono dalla chiave, **A**->B-C)

## BCNF

Una relazione è in forma normale di Boyce-Codd quando in essa ogni determinante è una chiave candidata, cioè ogni attributo dal quale dipendono altri attributi può svolgere la funzione di chiave (cosa?)

Una relazione è in forma normale di *Boyce-Codd* se e solo se, per ogni dipendenza funzionale X->Y, X è una chiave candidata.

Una relazione in **BCNF** (*Boyce-Codd Normal Form*) è anche in **2FN** e in **3FN**, perché la BCNF esclude che un determinante (X) possa essere composto solo da una parte della chiave (violerebbe la **2FN**), o che possa essere esterno alla chiave (violerebbe la **3FN**).

Quindi una relazione che rispetta la forma normale di Boyce-Codd è anche in terza forma normale (è già in 1FN, in 2FN e quindi ora è in 3FN, tipo evoluzione finale di un Pokémon), ma non è vero l'opposto, cioè che una relazione in **3FN** è anche in **BCFN**.

## <span class="sep">════════════════════════════</span>

# Viste

Tabelle virtuali con "durata temporanea", da usare in sostituzione alle **Join**, la vista viene aggiornata solo all'esecuzione della query che la genera.