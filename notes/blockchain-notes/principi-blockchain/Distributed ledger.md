# Distributed ledger

## Cosa sono

Le distributed ledger technology sono sistemi basati su un registro distribuito, ossia sistemi in cui tutti i nodi di una rete possiedono la medesima copia di un database che può essere letto e modificato in modo indipendente dai singoli nodi 

## Regola del consenso e crittografia 

Tutti i nodi che possiedono una copia del database possono consultarlo, ma devono passare da un ente centrale (oppure più soggetti validatori) per modificarne i dati. Nei sistemi di Distributed Ledger le modifiche al registro vengono regolate tramite algoritmi di consenso. Tali algoritmi permettono di raggiungere il consenso tra le varie versioni del registro, nonostante esse vengano aggiornate in maniera indipendente dai partecipanti della rete. Oltre agli algoritmi di consenso, per mantenere la sicurezza e l’immutabilità del registro, Distributed Ledger e Blockchain fanno anche un ampio utilizzo della crittografia.

## Caratteristiche principali

Una distributed ledger technology è caratterizzata dalle seguenti proprietà:

* **Tipologia di rete**
* **Meccanismo**
* **Struttura del registro**

Le soluzioni più propriamente dette Blockchain, aggiungono due ulteriori caratteristiche che non necessariamente si trovano nei sistemi Distributed Ledger:

* **trasferimenti**
* **asset**

## Permission Ledger e Permissionless Ledger

Sulla base della tipologia di rete, si distingue tra sistemi:

* **permissioned:** reti in cui per accedere bisogna registrarsi e identificarsi, perciò essere autorizzati da un ente centrale o dalla rete stessa
* **permissionless:** reti in cui chiunque può accedere senza autorizzazione

Nei sistemi **permissioned** il meccanismo di consenso è più semplice: quando un nodo propone una l’aggiunta di una transazione, ne viene verificata la validità e si vota a maggioranza sull’opportunità di aggiungerla al registro.

In sistemi **permissionless**, invece, i meccanismi di consenso sono più complessi (basati ad esempio Proof of Work o Proof of Stake) per evitare che un soggetto malevolo possa creare numerose identità fittizie e influenzare il processo di modifica del registro.

## Caratteristiche dei sistemi Blockchain

Nelle soluzioni blockchain il registro è strutturato come una catena di blocchi contenenti più transazioni e i blocchi sono tra di loro concatenati tramite crittografia (come ad esempio in **Bitcoin** o **Ethereum**). Vi sono poi soluzioni in cui registro è formato da tangle, dove cioè le transazioni vengono processate in parallelo (ad esempio **IOTA**), o altri casi ancora in cui il registro è formato da una catena di transazioni (ad esempio **Ripple**).

I sistemi Blockchain, in genere consentono di effettuare dei trasferimenti o più genericamente delle transazioni. Tali trasferimenti possono essere semplici o più evoluti a seconda del livello di programmabilità consentito dalla piattaforma.

L’ultima caratteristica dei sistemi Blockchain è il fatto che esista un **asset** univoco da trasferire che può essere una criptovaluta o un token. Tale asset può essere nativamente digitale o fisico con un corrispettivo digitale. Le tecnologie Internet of Things possono aiutare a creare corrispondenza tra asset fisico e digitale.