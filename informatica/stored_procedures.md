# Le stored procedures

Fanno parte di una branca del linguaggio *SQL* che prende il nome di **T-SQL**.

Durante lo sviluppo di un applicazione client le richieste per l'interrogazione di dati possono essere inviate direttamente al database. dal programma, tramite istruzioni, oppure è possibile creare piccoli programmi o funzioni all'interno del database e poi farle eseguire dal programma esterno. Queste procedure si chiamano Stored Procedure.

Una stored procedure può accettare parametri di input, restituire al client risultati tabellari o scalari, richiamare istrudzioni DDL (Data Definition Language) e DML (Data Manipulation Language)

Un linguaggio è detto **dichiarativo** o **logico** quando le istruzioni descrivono le relazioni che intercorrono tra i dati, lo sviluppatore descrive l'insieme delle relazioni che sussistono tra i dati e il risultato atteso.

Un linguaggio dichiarativo viene invece denominato **procedurale** quando per esso non si ragiona in termini di relazioni tra dati ma intermini di assegnazione di valori ad uno spazio di memoria, i linguaggi procedurali fanno infatti parte della più ampia famiglia dei linguaggi imperativi

Le stored procedure accettano parametri in input (IN), parametri in output (OUT) e vi è anche una combinazione di questi due che si chiama (INOUT)