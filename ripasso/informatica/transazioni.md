# Le transazioni

Una transazione è una sequenza di operazioni, che può concludersi positivamente o
negativamente, in caso positivo il risultato delle operazioni deve essere permanente (**commit work**), mentre in caso negativo si deve tornare allo stato prima della transazione (**rollback**).

Le Transazioni rispettano le proprietà **ACID**

**A**tomicity, **C**onsistency, **I**solation, e **D**urability

- <span style="color:#fa4545">Atomicità</span>: il processo deve essere suddivisibile in un numero finito di unità indivisibili, chiamate transazioni. L'esecuzione di una transazione perciò deve essere per definizione o totale o nulla e non sono ammesse esecuzioni parziali. Un processo, anche parziale, invece, in quanto insieme di transazioni può non essere elementare (Un processo è costituito da più transazioni).
- <span style="color:#fa4545">Coerenza</span>: il database rispetta i vincoli di integrità, sia a inizio che a fine transazione. Non devono verificarsi contraddizioni (incoerenza dei dati) tra i dati archiviati nel DB.
- <span style="color:#fa4545">Isolamento</span>: ogni transazione deve essere eseguita in modo isolato e indipendente dalle altre transazioni, l'eventuale fallimento di una transazione non deve interferire con le altre transazioni in esecuzione.
- <span style="color:#fa4545">Durabilità</span> detta anche persistenza, si riferisce al fatto che una volta che una transazione abbia richiesto un commit work, i cambiamenti apportati non dovranno essere più persi. Per evitare che nel lasso di tempo fra il momento in cui la base di dati si impegna a scrivere le modifiche e quello in cui li scrive effettivamente si verifichino perdite di dati dovuti a malfunzionamenti, vengono tenuti dei registri di log dove sono annotate tutte le operazioni sul DB.
