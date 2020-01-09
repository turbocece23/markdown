---
title: macchine_virtuali
tags: [Import-ef50]
created: '2019-11-07T09:59:25.607Z'
modified: '2019-11-13T09:51:51.063Z'
---

Il file di configurazione della macchina virtuale è un XML
ed è possibile aggiungere al file manualmente quante schede di rete vogliamo

a parte le tre versioni stable, unstable testing di debian, eiste
anche la versione testing

noi useremo la versione buster senza componenti aggiuntive

Nome utente: Utente Di Servizio
nick: uds
password e psw di root: lasolita

GPT rispetto a UEFI permette un numero illimitato di partizioni
creo una partizione primaria da 4.0GB
con opzione di mount discard e noatime attivate di nome linuxroot
e la restante come swap

installiamo il sistema di base

usiamo solo software libero 
deselezioniamo server ssh

installiamo GRUB

Linux ha l'ora di greenwich impostata di default

Programmi da installare (da root)
	apt install less joe tcpdump mtr-tiny cowsay
	apt install sudo
Aggiungo uds al gruppo sudo
	adduser uds sudo
	
	apt clean
	
shutdown -h now per spegnere la macchina virtuale
------------------------------------------------------------------------
SERVER
Clono la macchina virtuale
serverbrunello con MAC nuovo
clone COMPLETO della macchina virtuale
dentro la macchina virtuale cambio /etc/hostname con il nome del server(cognome)
poi edito /etc/hosts

------------------------------------------------------------------------
ROUTER
routerbrunello
sistema BSD
FreeBsd 32bit
128 MB di ram
disco VDI di 64 MB
la avvio, scelgo la iso di m0n0wall

03/10
Nelle impostazioni di rete
scheda 1 connessa con bridge
scheda 2 in rete interna
scheda 3 rete interna con nome "DMZ"

accendo il router
avvio del setup delle interfacce (1)
non eseguiamo il setup delle VLAN
immetto em1 per la impostazione della LAN
em0 per la WAN

poi mi sposto nel client con monowall acceso
accedo a root e installo una serie di programmi
lightdm (un gestore grafico del login)
apt install lightdm mate firefox-esr firefox-esr-l10n-it
"Debian è un po' talebano" 03/10
riavvio la macchina, ci sono due metodi:
da root /etc/init.d/lightdm restart
dhclient enp0s3

dati di accesso a m0n0wall
admin - mono

creare una regola nel firewall che permetta il traffico dell'indirizzo
per accedere dalla macchina il m0n0wall vedere screenshot

nel router modifico i dati di accesso
nome: router brunello
password: lasolita

nella opt1 abilito la rete optionale 1 e la chiamo DMZ indirizzo
192.168.101.1/24

edito le regole della dmz, blocco tutto quello generato nella DMZ
che ha come destinazione la LAN
poi come seconda regola, lascio passare tutto quello che è generato
nella DMZ dappertutto
ma siccome la regola block viene prima, quella è più importanta e controllata
per prima
------------------------------------------------------------------------

Quando scarichiamo firefox scarichiamo un eseguibile, e il programma si installa
abbiamo scaricato firefox + le librerie necessarie per far funzionare il programma
se installo thunderbird accadono le stesse cose, si può installare senza firefox?
si, quando aggiorniamo firefox, non si aggiornano le stesse librerie di thunderbird

sotto linux (gestito da distributori) non ci sono innesti esterni, chi fa debian
modifica molti dei programmi perché essi possano essere eseguiti senza problemi
e come facessero già parte di Debian nativamente.

Il play store è un distributore che fornisce software per android già adatto
all'utilizzo sul dispositivo, molte delle distro di linux funziano come il play
store, c'è un marketplace di programmi da cui vengono installati programmi
applicativi

su linux se vengono scaricate le librerie per thunderbird (per esempio) e poi
si vuole installare firefox, il sistema operativo non riscarica le librerie
perché sono state già installate precedentemente

su linux posso avere più versioni delle stesse librerie grazie ad un sistema
di connessione fra pc e versione di librerie utilizzate a differenza di windows
in cui devo avere solo una versione di una libreria

"essere sempre in emergenza vuol dire non saper gestire la normalità" 26/09/2019

I pacchetti deb di Debian contengono anche un file di configurazione modello
che servono a configurare in maniera semi-automatica la configurazione del sistema.
La configurazione di sistema non viene rimossa (se ad esempio faccio apt remove
firefox) perché se reinstallo un programma viene riutilizzata la sua configurazione
di sistema. Il livello ulteriore è il purge, in cui rimuovo anche la configurazione

In Debian vi è un reticolo di file di configurazione, una cartella .d contiene
file di configurazione aggiuntivi a quelli installati di base. Come il corrispettivo
ubuntu/debian di adblock, esso non modifica i file di configurazione di firefox
perché rischia di escludere gli altri plug in dai file .conf, per evitare ciò
aggiunge i file di cui ha bisogno in una cartella come sources.list.d, una cartella
col nome simile che però conterrà i file di cui ha bisogno

apt update
apt upgrade
apt dist-upgrade

gli utlimi due sono simili con l'unica differenza che dist-upgrade (aggiorna i
pacchetti fregandosene delle interdipendenze fra pacchetti) è un comando
più drastico e può provocare gravi interruzioni ai servizi

10/10/2019
sul monowall impostiamo la dmz con range 192.168.101.100 192.168.101.199
impostiamo le impostazioni di rete del server su rete interna connessa a DMZ

12/10/2019
Imposto sul m0n0wall la regola che il server abbia IP statico 192.168.101.250
nelle impostazioni del dhcp server
Inoltre imposto l'alias del pc ospitante (172.30.4.10) a host-pcospitante
Nelle impostazioni delle regole del firewall posso impostare la sorgente non specificando
l'indirizzo ma l'alias del host appena impostato

Per la rete 172.30.4.0/24 imposto l'alias lan-labsistemi

17/10/2019
per la migrazione dei computer nelle loro relative reti, dentro il file
/etc/network/interfaces

da iface enp0s3 inet dhcp
diventa
iface enp0s3 inet static
    address 172.30.4.110
    
12/12/2019
VLAN MAC BASED
Una porta access in cui passano trame ethernet non taggate (untagged)
le quali vengono distinte fra trame VOIP e non VOIP e conseguentemente
veicolate nella VLAN corretta

19/12/2019

PER FAR ANDARE L'HTTPS
https://hallard.me/enable-ssl-for-apache-server-in-5-minutes/
/etc/apache2/sites-available/000-default.conf
https://www.digitalocean.com/community/tutorials/how-to-create-a-ssl-certificate-on-apache-for-debian-8

Creare una VPN a livello m0n0wall con il pc9 di michele
Come controparte per la VPN metto l'indirizzo della macchina con cui voglio
creare la mia VPN, viene decisa una chiave che sarà simmetrica.
il primo passo sarà pingare il client della macchina 2 dalla macchina 1

IPsec è un protocollo vecchio, craeto prima che venisse implementato il NAT
l'IPsec è una sostizione del livello 3, viene sostituito dal router e cripta
i contenuto dal livello 3 in su fino a che il pacchetto non arriva al client
di destinazione. Quando il pacchetto arriva, il client che riceve il messaggio è
in grado di decrittare il pacchetto perché vede che l'indirizzo di sorgente è quello
della macchina controparte.

Protocollo
Livello
Protocollo

    IP----------------->
1 2 3    4   5   6   7
    IPsecX---X---X---X->

IPSec crea due livelli 3, "uno sotto e uno sopra", quello più in basso
ancora in chiaro, serve al client di destinazione per controllare qual'è la sorgente
del pachetto
