# Blockchain

## Cos'è?

La blockchain è una nuova tipologia di registro distribuito, il quale è strutturato come una catena di blocchi contenenti le transazioni. Il conseso è distribuito su tutti i nodi della rete e tutti possono partecipare al processo di validazione delle transazioni da includere nel registro.

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

## Crittografia

Le tecnologie di blockchain fanno uso di funzioni di hash e di crittografia asimmetrica. Uno degli algoritmi di hash più utilizzati anche in ambito blockchain è SHA-256, il quale produce un digest di 256 bit.

La tecnica di crittografia asimmetrica è utilizzata nella comunicazione tra mittente e destinatario di un messaggio. Ad ogni partecipante alla comunicazione sono associate una chiave privata e una chiave pubblica.

## Composizione di un blocco

Consiste in una struttura dati, la quale contiene ogni transazione. Un blocco è definito dai seguenti campi:

* **Blocksize:** varia a seconda dell'implementazione della blockchain.
* **Blockheader:** formato da diversi campi tra cui il timestamp del blocco e l'hash del blocco precedente
* **Transaction counter:** numero di transazioni contenute nel corpo del blocco
* **Transactions:** il corpo del blocco, formato da una lista non vuota di transazioni.

Il primo blocco è detto genesis block. Per poter aggiungere una transazione alla blockchain, un nodo deve creare la transazione e propagarla agli

