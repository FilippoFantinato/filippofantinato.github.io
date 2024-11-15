# Ethereum

## Cos'è

L'idea è creare una blockchain dove è possibile eseguire dei programmi touring-complete.

Ogni smart contract modifica lo stato (una mappa chiave valore) di ogni blocco.

**Bitcoin:** una transazione consiste in un cambiamento di UTXO

**Ethereum:** una transazione consiste in un cambiamento di una mappa chiave valore

In entrambi i casi le transazioni devono essere deterministiche.

## Wallet

Stessa cosa di bitcoin.

Le commissioni tendono ad essere proporzionali alla complessità del codice

## EOA (Externally Owned Accounts)

Chiave privata, dalla quale deriva chiave pubblica e dalla quale deriva l'indirizzo.

Un blocco può contenere o un EOA, oppure un contratto eseguibile.

Quando si fa una transazione, c'è un EOA di sorgente e un EOA di destinazione.

## Ethereum clients

Un Ethereum client è un applicativo che comunica con la rete Ethereum. Sono presenti molti Ethereum clients, così da evitare, in caso di bug, rendere più difficile riscrivere la storia.

### Full nodes

Nodi con tutta la blockchain (per fare query) e prendono parte al mining.

### Remote clients

A client remote che delega un full node per tutte le operazioni.

### Networks

Le varie reti blockchain: mainet, testnet o una local blockchain.

## Crittografia

Un indirizzo Ethereum è simile ad un bitcoin, tranne per il fatto che usa Keccak-256 come hash function (sha-3 originale).

Costruzione indirizzo: chiave privata --ECDSA--> chiave pubblica --Keccak-256-->hash --las 20 bytes-->

Ethereum non usa un checksum.

#### ICAP

Standard proposto aggiungendo un checksum di 2 caratteri:

```
XE + 2 caratteri di checksum + 30 cifre in base 36
```

Possono solo mantenere 5 caratteri a zero iniziali. È molto simile all'IBAN.

### EIP-55

Il checksum viene salvato nell'indirizzo come caratteri maiuscoli.

Viene confrontato l'indirizzo con l'hash di esso e, se l'hash in posizione di una lettera dell'address è >= 8, allora viene messa in maiuscolo quella lettera. 

## Transazione

Una transazione è un messaggio firmato originato da un EOA, trasmesso dalla rete Ethereum e memorizzata nella blockchain Ethereum:

* **nonce:** numero progressivo collegato alla transizione effettuate da un EOA
* **gas price:** massimo costo che sono disposto a pagare in unità di gas
* **gas limit:** massima quantità di gas che sono disponibile a spendere
* **to:** l'indirizzo del destinatario
* **value:** valore di ether da scambiare
* **data:** nome del metodo e parametri, codice del contratto o, se si vogliono scambaìiare soldi, si lascia vuoto
* **v,r,s:** firma ECDSA del EOA

L'indirizzo originario EOA è dato da v,r,s.

L'id della transazione è l'hash o il suo byte encoding.

La transazione potrà costare gas price * gas limit al massimo.

### Tipi di transazione

**Scambio di moneta**

![transaction-money](/home/filippofantinato/Desktop/Stage/Blockchain/ethereum/images/transaction-money-exchange.png)

**Caricamento di un contratto**

![transaction-contract-loading](/home/filippofantinato/Desktop/Stage/Blockchain/ethereum/images/transaction-contract-loading.png)

**Chiamata di un contratto**

![transaction-constract-calling](/home/filippofantinato/Desktop/Stage/Blockchain/ethereum/images/transaction-constract-calling.png)

### Ciclo di vita di una transazione

1. Creo la transazione e la firmo con la chiave privata
2. Spedisco la transazione 
3. Raggiungo un nodo che memorizza la transazione nella sua mempool
4. La preleva per elaborarla (proof of work)
5. Crea il blocco da aggiungere alla blockchain (contenente cosa è stato fatto)

Una transazione induce un cambiamento di stato della blockchain ethereum.

### Nonce

È un numero progressivo che viene incrementato ad ogni transazione.

Ogni nodo, quando arriva una transazione, controlla il nonce di essa e se è minore di n+1 (con n il numero di transazione che ha effettuato un EOA) viene rigettata, mentre invece se è più grande di n+1 allora viene ritardata la sua esecuzione. 

Questo garantisce un ordine alle transazioni, lanciarne quanto ne vogliono e evita la rielaborazione di esse.

In bitcoin non c'è bisogno del nonce, perchè gli input sono stati già spesi. In Ethereum invece non si scambiano solo soldi, ma anche esecuzione di programmi

### Transazione con moneta (pagamento)

Il ricevitore è un EOA, il quale può esistere o no.

il ricevitore è un contratto: 

* ci sarò un metodo payable specificato dal data, sarà eseguito e incrementerà il bilancio del valore
* se non c'è data: 
  * c'è un metodo payable di fallback, per poter pagare
  * se non c'è una fallback function, allora il bilancio verrà incrementato e basta
  * se non è payable la fallback function, allora la transazione fallirà

### Transazione per invocare un metodo di un contratto

* La signing key specifica il caller
* Il campo to corrisponde ad una chiamata di contratto
* Il campo data sarà il metodo corrispondente da invocare

Il campo data sarà calcolato nel seguente modo:

1. Prendere la firma della callee come una stringa
2. Calcolare il suo Keccak256 hash
3. Prendere i primi 4 bytes (function selector)
4. Aggiungere i parametri e serializzare tutto

### Transazione per la creazione di un contratto

1. La signing key specifica il caller
2. No indirizzo (indirizzo zero)
3. Nel campo data andrà il bytecode del contratto
4. Il valore ritornato sarà i'indirizzo del contratto

### Firma di una transazione (ECDSA)

Le transazioni sono digitalmente firmate prima di essere mandate alla rete Ethereum.

La firma serve a tre scopi:

1. Garantisce che la transazione sia stata creata dal sender (authenticity)
2. Garantisce che il sender non può essere negato di aver mandato la transazione (non repudiation)
3. Garantisce che la transazione non sia stata alterata (integrity)

Per evitare che una transazione possa essere eseguita su più reti Ethereum, è stato introdotto un campo numerico chiamato chain identifier prima di firmarlo.

Differentemente da Bitcoin, non si può firmare una transazione più volte. Per oviare a questo si può programmare uno smart contract per fare questo.

## Lo stato di Ethereum

Lo stato di Ethereum è una mappa chiave valore data come singleton. Ogni nodo mantiene una propria copia privata di questo database. 

**Memorizza il bilancio di un EOA**

```
put(address of EOA, balance)								O(L + size( value ))
```

**Leggi il bilancio di un EOA**

```
value=get(address of EOA)													O(L)
```

**Leggi l'hash dell'ultima transazione**

```
h=get_hash()																O(1)
```

**Installa uno smart contract**

```
put(hash(address of EOA, nonce of EOA), bytecode of smart contract)
```

hash(address of EOA, nonce of EOA) è l'indirizzo dello smart contract

**Memorizzo in un campo di uno smart contract**

```
put(hash(address of smart contract, n) , v)
```

**Lettura di un campo di uno smart contract**

```
get(hash(address of smart contract, n))
```

Le collisioni hanno una probabilità minima di accadere.

### L'hash dello stato

In bitcoin l'header del blocco contiene l'hash delle transazioni.

In Ethereum l'header del blocco contiene l'hash dello stato finale di quel blocco. Questo viene fatto per forzare i nodi ad eseguire le transazioni, così devono per forza eseguire le transazioni e non possono metterne di a caso.

In caso di fork verrà svolto l'undo dello stato di tutte le transazioni non appartenenti alla main history. Per svolgere l'undo bisognerà eseguire l'operazione di checkout

```
checkout(old_block.header.state.hash)										O(1)
```

Per fare tutto questo, Ethereum mantiene tutti gli stati intermedi.

### Merkle-Patricia tries

1. Una rappresentazione compatta di uno stato precedente, attraverso una rappresentazione per differenza, mantenendoli come percorsi alternativi
2. Una veloce computazione quando lo stato è aggiornato (derivato dai merkle tree)
3. Accesso rapido al valore associato a ciascuna chiave data
4. Veloce cambiamento di visione, considerando come radice un nodo precedente

Le hashmaps non soddisfano questi requisiti

### PATRICIA(Practical Algorithm To Retrieve Information Coded In Alphanumeric)

Alberi dove si possono cercare delle parole, in base al loro prefisso in comune e il loro termine. Sono presenti dei lookahead per decidere dove andare.

Per collegare i vari nodi si utilizza il loro hash.

