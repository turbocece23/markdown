# <span style="color:#ffa45a;">I trigger</span>

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

# Stored Procedures

Le stored procedures sono programmi o funzioni che vengono eseguite all'interno del database però richiamabili da applicazioni client come parti di un sito.