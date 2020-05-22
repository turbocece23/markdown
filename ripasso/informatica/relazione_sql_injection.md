# <span style="color:#f51339;">SQL Injection</span>
### <span style="color:#b6b6b6;">Brunello Cesare 5AI AS 2019/2020</span>

## <span style="color:#bf0b3b;">1 Introduzione</span>

L'SQL Injection è una tecnica di attacco usata per attaccare basi di dati che consiste nell'inserire del codice malevolo in campi di input nei quali non viene esercitato un sufficiente controllo.

I malintenzionati sono quindi in grado di sfruttare questa vulnerabilità per eseguire comandi dal server che normalmente non sarebbero in grado di far eseguire.

Questa tecnica di attacco può essere utilizzata durante la fase di **information retrival** (cioè la raccolta di informazioni che precede un attacco) oppura può costituire in sé **l'attacco** in quanto se il database non è protetto a sufficienza l'hacker può causare gravi danni alterando i dati nelle tabelle o cancellando intere strutture.

## <span style="color:#bf0b3b;">2 Esempio</span>

Prendiamo ad esempio una semplice pagina che dato in input un ID ci restituisce l'utente collegato e la sua password.

<span style="color:#ff1245;">**IMPORTANTE:**</span> una pagina simile di per sè è già poco sicura e non verrà mai utilizzata in un ambiente professionale perché non richiede nessuna autenticazione e per trovare tutti gli utenti ci vorrebbe comunque poco tempo. Si potrebbe usare come pagina di esempio un login, ma per comodità dell'esempio useremo questa pagina.

<div align="left">
<form method="POST" action="" autocomplete="off">
<input type="text" name="cercaid" placeholder="ID" value="1">
<input type="submit" name="invia" value="Cerca">
</form>


<table>
<tr>
<th bgcolor="#ffa45a" style="color:gray">ID</th>
<th bgcolor="#ffa45a" style="color:gray">Username</th>
<th bgcolor="#ffa45a" style="color:gray">Password</th>
</tr>
<tr>
<td style="color:#80b6cc; text-align:center;"><b>1</b></td>
<td>cesare</td>
<td style="text-align:right;">cesarepswd</td>
</tr>
</table>
</div>

## <span style="color:#bf0b3b">3 Codice del form</span>

Lasciamo vuota l'action, in questo modo il risultato verrà mostrato nella stessa pagina nella tabella sottostante

```HTML
<form method="POST" action="" autocomplete="off">
	<input type="text" name="cercaid" placeholder="ID">
	<input type="submit" name="invia" value="Cerca">
</form>
```

La query che viene eseguita nel DB è questa

```SQL
SELECT ID, username, password FROM user WHERE ID = '$input';
```

In cui:

- **ID**: campo ID della nostra tabella
- **username:** nome utente
- **password:** password dell'utente
- **user:** tabella da cui prendiamo i dati
- **$input:** ID immesso dall'utente nel form

## <span style="color:#bf0b3b">4 Iniezione del codice</span>

Per testare se la nostra pagina è vulnerabile all'SQL Injection, inseriamo nel campo di input questa stringa

```SQL
'OR '1'='1
```

Questa stringa cambierà la struttura della query che andremo ad eseguire nella pagina, infatti la query risultante avrà poi questo aspetto

```SQL
SELECT ID, username, password FROM user WHERE ID = ''OR '1'='1';
```
Il primo apice "chiude" l'input, il resto del codice aggiunge una condizione che controlla se 1 è uguale a 1
```SQL
OR '1'='1'
```
Questa condizione rende la query sempre verificabile, ciò significa che nonostante il confronto tra l'ID immesso e quello preso in esame nella query sono errati, la condizione appena aggiunta fa sì che il risultato sia accettato ugualmente. Ora abbiamo accesso a tutti i dati nel database


<div align="center">
<table>
<tr>
<th bgcolor="#ffa45a" style="color:gray">ID</th>
<th bgcolor="#ffa45a" style="color:gray">Username</th>
<th bgcolor="#ffa45a" style="color:gray">Password</th>
</tr>
<tr>
<td style="color:#80b6cc; text-align:center;"><b>1</b></td>
<td>cesare</td>
<td style="text-align:right;">cesarepswd</td>
</tr>
<tr>
<td style="color:#80b6cc; text-align:center;"><b>2</b></td>
<td>elena</td>
<td style="text-align:right;">elenapswd</td>
</tr>
<tr>
<td style="color:#80b6cc; text-align:center;"><b>3</b></td>
<td>cassandra</td>
<td style="text-align:right;">cassandrapswd</td>
</tr>
<tr>
<td style="color:#80b6cc; text-align:center;"><b>4</b></td>
<td>yeboah</td>
<td style="text-align:right;">yeboahpswd</td>
</tr>
<tr>
<td style="color:#80b6cc; text-align:center;"><b>5</b></td>
<td>nismo</td>
<td style="text-align:right;">nismopswd</td>
</tr>
</table>
</div>

## <span style="color:#bf0b3b">5 Come difendersi</span>

Tramite l'uso della funzione ```mysql_real_escape_string()``` la quale provvederà a rimuovere gli apici dall'input immesso.

Ma la nostra pagina non è ancora sicura, perché immettendo la stringa

```SQL
1 OR 1=1
```

Otterremo lo stesso risultato di prima, in quanto il numero 1 verrà usato com input primario per il campo ID e la condizione verrà aggiunta ugualmente.

Si può pensare di effettuare la ricerca anziché tramite l'ID, tramite l'username, in tal modo dobbiamo preoccuparci solamente che l'input inserito dall'utente contenga solo lettere, per farlo possiamo utilizzare JavaScript e le Espressioni Regolari, chiamate anche Regex.

<span style="color:#f79616">**Codice HTML**</span>

```HTML
<form method="POST" action="" autocomplete="off" name="CercaUtente">
	<input type="text" name="nome" onkeyup="controlla(document.CercaUtente.nome)">
	<input type="submit" name="invia" id="invia" value="Cerca">
</form>

```

<span style="color:#f79616">**Codice JavaScript**</span>

```JS
function controlla(inputtxt)
{
	var regex;

	//Espressione regolare
	regex = /^[A-Za-z- ]+$/;
	
	//Se il testo inserito contiene solamente lettere allora
	if(inputtxt.value.match(regex))
	{
		//Abilita il bottone di invio
		document.getElementById("invia").disabled=false;
		return true;
	}else
	{
		//Avverti l'utente
		alert("L'input deve contenere solo lettere");
		//Disabilita il bottone di invio
		document.getElementById("invia").disabled=true;
		return false;
	}
};
```

Analizzando meglio l'espressione regolare usata nella funzione capiamo che questa permette all'utente l'inserimento di sole lettere, dalla "A" alla "Z" e dalla "a" alla "z", qualunque altro carattere farà scattare la funzione che disabiliterà il bottone di invio e avvertirà l'utente del suo errore o del suo fallito tentativo di craccarci il database.