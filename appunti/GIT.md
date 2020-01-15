# GIT

## <span style="color:#fca40c">Introduzione</span>

Un sistema di controllo di versione dei programmi (VCS, Version Control System), tiene traccia di ciascun cambiamento che avviene nel progetto.<br>
Prima dell'avvento di GIT vi erano solo sistemi basati su file e cartelle (e bestemmie). è il sistema di version control più semplice ma per grandi progetti potrebbe risultare difficile vedere i cambiamenti applicati.<br>
Di VCS ne esistono versioni distribuite e locali, Git è un DVCS (Distributed VCS).<br>
Git nasce come riga di comando, ma alcuni editor sofisticati hanno alcune funzionalità Git già costruite al loro interno, come tool grafici e scorciatorie varie.

## <span style="color:#fca40c">Primi comandi</span>

Inizializzare git su una repository (locale sul pc)
```
git init
```

Per vedere lo stato della repository
```
git status
```

Aggiungiamo i file che dobbiamo caricare su git
```
git add <nomefile>
```

Creiamo il commit che porterà le nostre modifiche su git
```
git commit -m "Messaggio di commit"
```

Per vedere i commit
```
git log --oneline
```

##  <span style="color:#fca40c">Undoing changes</span>

Per tornare ad aggiornamenti precedenti del file quindi controllare un commit che è stato fatto in precedenza
```
git checkout <ID del commit>
```

Per tornare alla versione corrente
```
git checkout master
```

Per taggare un programma con la sua versione
```
git tag -a v1.0 -m "Prima versione del programma"
```

Ora che abbiamo taggato la nostra versione stabile del programma possiamo accedervi tramite il comando
```
git checkout v1.0
```
In questo modo facciamo riferimento alla versione del nostro programma taggata "v1.0"

Per tornare ad un commit precedente ANNULLANDO i cambiamenti successivi (al commit preso in esame), GIT crea un commit uguale a quello specificato, basta che sia avvenuto prima dei o del commit che voglio annullare. GIT non cancella il commit da cancellare, bensì lo "evita" creando un commit che porta il mio file esattamente allo stato specificato
```
git revert <ID del commit>
```

Per tornare alla versione del file tracciato dal commit alla versione precedente senza creare nuovi commit come potrebbe fare il comando "revert"
```
git reset --hard
```
Questo comando funziona in tale maniera: la flag "--hard" cancella le modifiche più recenti al file, senza questa flag, GIT semplicemente sposterebbe il file dai tracked agli untracked, senza annullare le modfiche, ma semplicemente spostandolo come se non venisse incluso nel *git add*

Per eliminare i file non tracciati e pulire la working directory
```
git clean -f
```

## <span style="color:#fca40c">I branch</span>

Sono linee di sviluppo indipendenti<br>
Hanno diversi utilizzi, per esempio: il master può essere visto come "branch di produzione", questa modalità di utilizzo implica però che ci devono essere delle politiche di gestione dei file, perché è molto facile incorrere in dei "merge conflict". Quando voglio pushare un file nel branch che ho modificato aggiungendo le mie funzionalità, potrei andare in conflitto con una copia dello stesso file ma con funzionalità diverse, in questo caso va deciso quale delle due versioni tenere o come modificare il file nel modo più opportuno

Se voglio creare un nuovo branch devo utilizzare il comando
```
git branch
```

Per spostarmi però all'interno del branch devo usare
```
git checkout <nome branch>
```

C'è da dire che ora che ci troviamo in un branch diverso da master, quando eseguiamo il comando *git log* ci verrà mostrato lo storico solamente del branch corrente. I commit precedenti alla creazione del branch sono considerati comunque parte della storia del nuovo branch

Quando eseguiamo questo comando il puntatore HEAD del nostro branch si sposta e non si trova più dove lo abbiamo lasciato, bensì dove si sposta dove gli diciamo noi, in questo caso, in un branch diverso dal master, in caso volessimo tornare al master, dobbiamo usare un altro comando.<br>
Per unire i nostri cambiamenti di un branch con master lo si riposiziona alla stesso punto di master con il comando
```
git rebase [master]
```

## <span style="color:#fca40c">I branch remoti</span>

Scarica i commit che sono stati fatti sul branch remoto che mancano dalla repository locale, inoltre, aggiorna dove il branch remoto punterò. Può essere visto come uno step per scaricare 

```
git fetch
```