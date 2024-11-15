# Principi blockchain

## Cos'è?

La blockchain è una nuova tipologia di registro distribuito, il quale è strutturato come una catena di blocchi contenenti le transazioni. Il conseso è distribuito su tutti i nodi della rete e tutti possono partecipare al processo di validazione delle transazioni da includere nel registro.

## Distributed ledger

### Cosa sono

Le distributed ledger technology sono sistemi basati su un registro distribuito, ossia sistemi in cui tutti i nodi di una rete possiedono la medesima copia di un database che può essere letto e modificato in modo indipendente dai singoli nodi 

### Regola del consenso e crittografia 

Tutti i nodi che possiedono una copia del database possono consultarlo, ma devono passare da un ente centrale (oppure più soggetti validatori) per modificarne i dati. Nei sistemi di Distributed Ledger le modifiche al registro vengono regolate tramite algoritmi di consenso. Tali algoritmi permettono di raggiungere il consenso tra le varie versioni del registro, nonostante esse vengano aggiornate in maniera indipendente dai partecipanti della rete. Oltre agli algoritmi di consenso, per mantenere la sicurezza e l’immutabilità del registro, Distributed Ledger e Blockchain fanno anche un ampio utilizzo della crittografia.

### Caratteristiche principali

Una distributed ledger technology è caratterizzata dalle seguenti proprietà:

* **Tipologia di rete**
* **Meccanismo**
* **Struttura del registro**

Le soluzioni più propriamente dette Blockchain, aggiungono due ulteriori caratteristiche che non necessariamente si trovano nei sistemi Distributed Ledger:

* **trasferimenti**
* **asset**

### Permission Ledger e Permissionless Ledger

Sulla base della tipologia di rete, si distingue tra sistemi:

* **permissioned:** reti in cui per accedere bisogna registrarsi e identificarsi, perciò essere autorizzati da un ente centrale o dalla rete stessa
* **permissionless:** reti in cui chiunque può accedere senza autorizzazione

Nei sistemi **permissioned** il meccanismo di consenso è più semplice: quando un nodo propone una l’aggiunta di una transazione, ne viene verificata la validità e si vota a maggioranza sull’opportunità di aggiungerla al registro.

In sistemi **permissionless**, invece, i meccanismi di consenso sono più complessi (basati ad esempio Proof of Work o Proof of Stake) per evitare che un soggetto malevolo possa creare numerose identità fittizie e influenzare il processo di modifica del registro.

### Caratteristiche dei sistemi Blockchain

Nelle soluzioni blockchain il registro è strutturato come una catena di blocchi contenenti più transazioni e i blocchi sono tra di loro concatenati tramite crittografia (come ad esempio in **Bitcoin** o **Ethereum**). Vi sono poi soluzioni in cui registro è formato da tangle, dove cioè le transazioni vengono processate in parallelo (ad esempio **IOTA**), o altri casi ancora in cui il registro è formato da una catena di transazioni (ad esempio **Ripple**).

I sistemi Blockchain, in genere consentono di effettuare dei trasferimenti o più genericamente delle transazioni. Tali trasferimenti possono essere semplici o più evoluti a seconda del livello di programmabilità consentito dalla piattaforma.

L’ultima caratteristica dei sistemi Blockchain è il fatto che esista un **asset** univoco da trasferire che può essere una criptovaluta o un token. Tale asset può essere nativamente digitale o fisico con un corrispettivo digitale. Le tecnologie Internet of Things possono aiutare a creare corrispondenza tra asset fisico e digitale.

## La storia

La prima versione della blockchain è stata rilasciata nel 2009, come nuova tipologia di registro distribuito per la criptovaluta bitcoin. Tra le novità introdotte dai Bitcoin, il fatto che ogni transazione fosse legittimata da una rete decentralizzata e non dalle autorità centrali. Seppur breve, la storia di questa criptovaluta ha segnato e stimolato l'evoluzione delle tecnologie Blockchain, tra sperimentazioni, perplessità e un hype mediatico senza precedenti.

## Caratteristiche

* **Digitalizzazione:** trasformazione dei dati in formato digitale.
* **Decentralizzazione:** le informazioni vengono registrate distribuendole tra più nodi per garantire sicurezza informatica e resilienza dei sistemi.
* **Tracciabilità dei trasferimenti:** ciascun elemento sul registro è tracciabile in ogni sua parte e se ne può risalire all’esatta provenienza.
* **Disintermediazione:** il contenuto del registro è trasparente e visibile a tutti ed è facilmente consultabile e verificabile.
* **Immutabilità del registro:** una volta scritti sul registro, i dati non possono essere modificati senza il consenso della rete.
* **Programmabilità dei trasferimenti:** possibilità di programmare determinate azioni che vengono effettuate al verificarsi di certe condizioni.

## Internet of value

Consiste in tutti quei sistemi che rendono possibile scambiarsi valore su internet con la stessa semplicità con cui oggi vengono scambiate le informazioni.

È definita come una rete digitale di nodi che si trasferiscono valore attraverso un sistema di algoritmi e regole crittografiche che permette di raggiungere il consenso, anche in assenza di fiducia, sulle modifiche da apportare a un registro distribuito che tiene traccia dei trasferimenti di asset digitali univoci. 

All'interno di quest'Universo orbitano dunque diverse galassie, o  meglio diverse piattaforme che permettono lo sviluppo di soluzioni Blockchain. Queste piattaforme possono essere categorizzate all'interno di due grandi gruppi: permissionless e permissioned.

* **Blockchain permissionless:** sono quelle in cui chiunque può partecipare al processo di validazione delle transazioni e chiunque può diventare un nodo della rete. Tra le permissionless le più famose sono Bitcoin ed Ethereum, tuttavia ne esistono molte altre che hanno generato una propria moneta crittografica (oltre 900).
* **Blockchain permissioned:** sono caratterizzate da un accesso alla rete ristretto ad alcuni partecipanti autorizzati e da un processo di validazione demandato a un gruppo ristretto di attori. Tra queste si ricordano Corda e Hyperledger.

In questa classificazione si inseriscono alcune soluzioni ‘ibride’ come Ripple che per esempio permettono a chiunque di partecipare alla rete, ma solo ad alcuni di occuparsi della validazione delle transazioni.

