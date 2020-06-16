<style>
	h2
	{
		padding-top: 0.7%;
		padding-left: 0.7%;
		padding-right: auto;
		padding-bottom: auto;
		width: 100%;
		color: white;
		background-color: #C01B2D;
	}
</style>
## 1 - Physical layer
Si occupa della trasmissione dei flussi di bit (di dati) attraverso **i mezzi fisici di interconnessione**.<br>
Tra i suoi compiti c’è quello di **realizzare la topologia fisica della rete**, in base alla quale viene definito come connettere fra loro i dispositivi che compongono la rete stessa.<br>
I dispositivi che operano a questo livello sono le **schede di rete** e gli **hub**. In quanto segue faremo uso delle schede di rete.

## 2 - Data Link layer
Ha come funzione principale quella di **rendere affidabile il collegamento** che è stato definito al livello 1. Si occupa della trasmissione dei dati tra due dispositivi appartenenti alla stessa rete, attraverso l’indirizzamento fisico.<br>
I dispositivi che operano a questo livello sono i **bridge** e gli **switch**.

## 3 - Network Layer
**Si occupa dell’instradamento** (o **routing**) dei dati inviati (sotto forma di pacchetti) da un dispositivo della rete a un destinatario non appartenente alla stessa rete, attraverso l’indirizzamento logico (che identifichi univocamente mittente e destinatario).<br>
I dispositivi che operano a questo livello sono **i router**, che useremo nella nostra rete. 

## 4 - Transport Layer
Si occupa della consegna dell’intero messaggio da mittente a destinatario, cioè della comunicazione end-to-end (tra i due end system o sistemi finali), ed è **responsabile dell’affidabilità dei dati**.

## 5 - Session Layer
Gestisce il dialogo tra i due end system.

## 6 - Presentation Layer
Controlla la sintassi delle informazioni scambiate. Tra i suoi compiti ci sono **traslazione**, **crittografia** e **compressione**.

## 7 - Application Layer
Fornisce all’utente un’interfaccia per accedere alla rete.