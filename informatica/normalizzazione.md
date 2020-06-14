# <span style="color:#E53434">**▲▼▲ Normalizzazione ▼▲▼**</span>

La forma normale di una base di dati ne garantisce la qualità, cioè l'assenza di determinati difetti:

Non è una metodologia di progettazione, è bensì una procedura che permette di trasformare schemi non normalizzati in schemi che soddisfano una forma normale

Se una relazione non è normalizzata essa presenta alcuni difetti:
- Ridondanze
- Comportamenti poco desiderabili durante gli aggiornamenti

Solitamente le forme normali sono definite a partire dal modello ER

Prendiamo ad esempio, così, a caso, una tabella:

|Impiegato|Stipendio|Progetto|Bilancio|Funzione|
|:---:|:---:|:---:|:---:|:---:|
|Rossi|20|Marte|2|tecnico|
|Verdi|35|Giove|15|progettista|
|Verdi|35|Venere|15|progettista|
|Neri|55|Venere|15|direttore|
|Neri|55|Giove|15|consulente|
|Neri|55|Marte|2|consulente|

Che. Merda. Vi sono problemi di *rindondanza dei dati*, *anomalie di aggiornamento*, *anomalie di cancellazione*, *anomalie di inserimento*.

Il processo di normalizzazione sottopone uno schema a una serie di test per certificare se soddisfa una data forma normale, infatti esistono:
- Prima forma normale (**1NF**)
- Seconda forma normale (**2NF**)
- Terza forma normale (**3NF**)
- Forma normale di Boyce e Codd (**BCNF**)
- (**4NF** e **5NF**)

## <span style="color:#E53434">**Normalizzazione delle relazioni**</span>

La normalizzazione dei dati è un processo di analisi degli schemi forniti, basato sulle loro dipendenze funzionali (spiegate qui sotto) e chiavi primarie, per raggiungere le proprietà desiderate di
- minimizzazione della ridondanza
- minimizzazione delle anomalie di
	- inserimento
	- cancellazione
	- modifica

Schemi ER inadeguati, vengono scomposti in schemi ER più piccoli che superano i test e pertanto
possiedono le proprietà desiderate.

## <span style="color:#E53434">**La dipendenza funzionale**</span>

Se la **chiave Primaria** è l'insieme di uno o più attributi che identificano in modo univoco un record della tabella, la **chiave candidata** è ogni insieme di uno o più attributi che possono svolgere la funzione di chiave primaria (significa che ci possono essere più chiavi candidate ma una sola chiave primaria)

L'**attributo no chiave** è un campo che non fa parte della chiave primaria (grazie al cazzo)

Per esempio

> Inventario(NumeroInventario, Prodotto, Magazzino, Quantità IndirizzoMagazzino)

- *NumeroInventario* è una chiave candidata
- (*Prodotto*, *Magazzino*) è una chiave candidata
- *Prodotto* NON è una chiave candidata
- *Magazzino* NON è una chiave candidata
- (*Prodotto*, *Magazzino*, *Quantità*) non è una chiave candidata perché contiene al suo interno un sottoinsieme di attributi che sono già chiave candidata

Si ha **dipendenza funzionale** tra attributi quando il valore di un insieme di attributi **A** determina un singolo valore dell'attributo **B** e si indica con **A -> B**. Si dice anche che **B** dipende da **A** o che **A** è un determinante per **B**.

Se un attributo, è chiave candidata (quindi può essere PK) di una relazione, allora è determinante di ogni attributo della relazione e viceversa (per esempio: la classe 5AI è la chiave primaria, la classe 5AI individua i suoi componenti, tutti i suoi componenti a loro volta individuano la classe 5AI), un attributo che determina tutti gli attributi è chiave candidata (e quindi è fruibile per essere eletta PK).

- *NumeroInventario* è determinante di ogni attributo (è candidata)
- (*Prodotto* *Magazzino*) è determinante di ogni attributo (è candidata)
- *Magazzino* è determinante di *IndirizzoMagazzino* (l'indirizzo del magazzino fa riferimento all'indirizzo del magazzino che possiede quello specifico codice identificativo, in caso il codice cambi, deve cambiare anche l'indirizzo)

Si ha dipendenza transitiva quando **A** determina **B** e **B** determina **C**. Si dice allora che **C** dipende transitivamente da **A**

Per riassumere:

> <span style="color:#14A1FA">**Dipendenza transitiva**</span>: **A -> B -> C**<br>C dipende transitivamente da A

> <span style="color:#14A1FA">**Dipendenza funzionale**</span>: **A -> B**<br>B dipende da A<br>A è un determinante di B

## <span style="color:#E53434">**Prima forma normale (1NF)**</span>

Il dominio di un attributo (valori che può assumere) deve comprendere solo valori atomici (semplici, indivisibili) e il valore di qualsiasi attributo in una tupla è un valore singolo del dominio.

Del tipo:

|Codice|Nome|Figli a carico|
|:---:|:---:|:---:|
|0001|Arminio|Giorgino, Astolfo, Dionisio|
|0002|Amalia|Romano, Perticone|

This, this is no good. Il dominio di *Figli a carico* non è atomico.

Se piuttosto creiamo un altra tabella:

|Codice|Nome|
|:---:|:---:|
|0001|Arminio|
|0002|Amalia|

|Codice Impiegato|Codice figlio|Nome|
|:---:|:---:|:---:|
|001|1|Giorgino|
|001|2|Astolfo|
|001|3|Dionisio|
|002|1|Romano|
|002|2|Perticone|

Allora otteniamo una relazione in **1FN**

## <span style="color:#E53434">**Seconda forma normale (2FN)**</span>

È in prima forma normale, tutti i suoi attributi non-chiave devono dipendere dall'intera chiave, cioè non possiede attributi che dipendono soltanto da una parte della chiave.

La seconda forma normale elimina la dipendenza parziale dagli attributi della chiave. Per esempio:

Partiamo dalla tabella T1(**A1**,**A2**,A3,A4,A5) con
- (**A1**,**A2**) -> A3
- **A1** -> A4
- **A2** -> A5

Può essere normalizzata in tale maniera aggiungendo due tabelle:

- T2(**A1**,**A2**,A3)
- T3(**A1**,A4)
- T4(**A2**A5)

La seconda forma normale riguarda quindi le tabelle in cui la chiave primara sia composta da più attributi e stabilisce che, in questo caso, tutte le colonne corrispondenti a quegli attributi dipendano dall'intera chiave primaria (e non da una sua parte).

## <span style="color:#E53434">**Terza forma normale (3FN)**</span>

È in seconda forma normale e tutti gli attributi non chiave devono dipendere direttamente dalla chiave, cioè non deve possedere attributi che dipendono da altri attributi che non sono chiavi.

Pertanto la **3FN** elimina la dipendenza transitiva degli attributi chiave. Per esempio:

Partiamo dalla tabella T1(**A1**,A2,A3,A4) con:
- A2 -> A4

Questa tabella non è in **3FN**, per farlo dobbiamo aggiungere una tabella e rendere A2 chiave primaria della nuova tabella che si crea

- T2(**A1**,A2,A3)
- T3(**A2**,A4)

Per tanto la **3FN** stabilisce che non esistano dipendenze tra le colonne di una tabella se non basate sulla chiave primaria

# <span style="color:#11C213">**○○○ In sintesi ○○○**</span>

La tabella iniziale vine scomposta in più tabelle che complessivamente forniscono le stesse informazioni della tabella di partenza, vengono mantenute le dipendenze tra attributi, ogni attributo però ora dipende direttamente da una chiave. Vengono quindi evitati problemi di rindondanza e di inconsistenza dei dati. Cosa importante, non ci deve essere perdita complessiva delle informazioni.

### <span style="color:#11C213">**► 1FN ◄**</span>
Ogni attributo è elementare, non ci sono righe uguali, non ci sono attributi di gruppo o ripetuti (come i figli a carico).

### <span style="color:#11C213">**► 2FN ◄**</span>
È in prima forma normale e non ci sono attributi non-chiave che dipendono parzialmente dalla chiave (A->B).


### <span style="color:#11C213">**► 3FN ◄**</span>
È in seconda forma normale e non ci sono attributi non chiave che dipendono transitivamente dalla chiave (non dipendono da attributi i quali dipendono dalla chiave, **A**->B-C)

E ora, non ultima per importanza, ma perché fa paura...

## <span style="color:#E53434">**Forma normale di Boyce-Codd**</span>

Una relazione è in forma normale di Boyce-Codd quando in essa ogni determinante è una chiave candidata, cioè ogni attributo dal quale dipendono altri attributi può svolgere la funzione di chiave (cosa?)

Una relazione è in forma normale di *Boyce-Codd* se e solo se, per ogni dipendenza funzionale X->Y, X è una chiave candidata.

Una relazione in **BCNF** (*Boyce-Codd Normal Form*) è anche in **2FN** e in **3FN**, perché la BCNF esclude che un determinante (X) possa essere composto solo da una parte della chiave (violerebbe la **2FN**), o che possa essere esterno alla chiave (violerebbe la **3FN**).

Quindi una relazione che rispetta la forma normale di Boyce-Codd è anche in terza forma normale (è già in 1FN, in 2FN e quindi ora è in 3FN, tipo evoluzione finale di un Pokémon), ma non è vero l'opposto, cioè che una relazione in **3FN** è anche in **BCFN**.