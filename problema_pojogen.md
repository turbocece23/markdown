# Problema PojoGen
*C:\projects-nb\tools\development\pojogen*

Il pojogen legge il file oweb20-create.sql, il file mysql che genera l'intero database di OWeb20
Tutte le istanze di "qualcosa"TempId le inserisce nel file update/statement_replica
Ciò che va fatto è, durante il funzionamento di pojogen, inserirsi all'interno, intercettare tutti i "qualcosa"TempID cercare una corrispondenza di questo "qualcosa"TempID all'interno di statement_replica, se è presente (cosa molto probabile), lasciare stare questa istanza, se non è presente, aggiungerla in qualche modo

## ANALISI RIGA PER RIGA: PojoGen
20
Creata la lista che conterrà tutte le righe del file

47-49
Se la riga è un commento, passa avanti

51-56
Viene controllato se la riga presa in esame contiene la parola ```CREATE``` per creare una nuova tabella, se è presente prendi il nome della tabella attuale

57,58
Creato il nuovo oggetto TableStructure e inserito nella lista "tables"

Un possibile inserimento per cercare i **TempID** è prima di riga 61, cioè prima di aver trovato le *Primary Key* e gli *indici* e prima di effettuare il controllo se la query di creazione è finita. In quanto la struttura generale di una query è

```sql
CREATE TABLE nomeSchema nomeTabella (
 `nomeCampo` BIGINT NOT NULL AUTO_INCREMENT,
 `agencyId` BIGINT NULL,
 `commissionTempId` BIGINT NULL,
 `creation` DATETIME NULL DEFAULT CURRENT_TIMESTAMP,
 `lastUpdate` TIMESTAMP NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
 `deletedRecord` TINYINT(1) NULL COMMENT 'cancellato',
 PRIMARY KEY (`commissionId`),
 INDEX `fk_commission_dealer_idx` (`dealerId` ASC),
 [...]
 )
 ENGINE = InnoDB
```

e il nostro **TempId** si trova sempre prima delle primary key, prima di tre campi chiamati
- creation
- lastUpdate
- deletedRecord

Il controllo viene effettato riga per riga, quindi nulla vieta di aggiungere un altro ```If() else``` e nasconderlo in mezzo a quelli pre esistenti, ciò che è importante fare è gestire bene la manipolazione della stringa. Essa è di imperativa importanza perché è colei che ci può dare un idea chiara di cosa abbiamo in mano e come lo possiamo gestire

FORMATAZZIONE DELLA STRINGA DENTRO LO statement_replica
Diciamo di avere per le mani il nome della tabella, il **TempID** nel ```CREATE``` usa sempre questa sintassi
```java
String tableName = "Tabella";
StringBuilder query = new StringBuilder();
query.append("CALL addIndexUnlessExists('oweb20_30002', '");
query.append(tableName.toLowerCase()+"', ");
query.append("'idx_"+tableName.toLowerCase()+"_tempId', ");
query.append("'"+tableName+"TempId ASC', '');");
```

MODIFICA DEL FILE STATEMENT REPLICA

Ordina la lista di nomi delle tabelle.
Leggi finché non trovi ```-- indici per tempId```, quando lo trovi, salta una riga (perché è vuota) inizia a leggere quella dopo.