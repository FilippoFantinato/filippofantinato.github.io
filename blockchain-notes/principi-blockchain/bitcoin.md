# Bitcoin

Lo scopo di bitcoin è di creare una moneta decentralizzata pubblica, per la prima volta. Nessuno può distruggere la rete.

I programmi con cui si interagisce con bitcoin vengono chiamati wallet e interrogano un ledger, in una rete mondiale p2p.

## Wallets

* **Desktop wallets**
* **Mobile wallets**
* **Web wallets**
* **Hardware wallets**
* **Paper wallets**

Inizialmente crea il proprio indirizzo bitcoin (corrispettivo all'iban) che verrà utilizzato per svolgere tutte le operazioni. Questo indirizzo verrà creato localmente e non comunicato alla blockchain inizialmente. La creazione dell'indirizzo è casuale e si basa su un generatore di numeri casuali sicuro (uniformemente distribuito equamente). L'indirizzo si deriva dalla chiave privata e può essere anche condiviso, non è un dato sensibile.

Per wallet si intende anche il file contenente le coppie di chiavi. In seguito questo file verrà criptato da una password, così da renderlo sicuro.

Dopo aver creato il wallet, bisogna caricare il wallet. Il modo più semplice è chiedere a qualcuno che ha già dei bitcoin, di venderglieli. Altri modi:

* Comprare bitcoin da un venditore di bitcoin.
* Guadagnare bitcoin lavorando (incluso il mining ma non solo).
* Usare dei bitcoin ATM
* Cambiare soldi veri con bitcoin

**Primo caso**

* Il seller specifica sul suo wallet l'indirizzo bitcoin di Alice come destinatario
* Il wallet di joe firma la transazione con la chiave privata.
* Viene spedita la transazione, attraverso internet, alla blockchain e viene condivisa a tutti i pc della rete blockchain. Dopo un paio di minuti viene processata e il wallet di Alice si accorge che è stata processata una transazione con destinatario un'indirizzo di quale lui è proprietario.
* Di seguito aggiorna la quantità di soldi.
* Per spenderli farà la cosa inversa

## Transazioni

Una transazione sarà composta da un hash code ed avranno un input e un output (o più). Ogni transazione avrà anche un costo di fees (commissioni) che andranno al miner per ringraziarlo di aver calcolato il blocco. I blocchi sono indivisibili e non si può pagare il costo esatto se non divisibile per l'unità.

Una transazione può essere spesa (TXO), oppure ancora da spendere (UTXO).

* **Typical transaction:** paga qualcuno ed ottieni il resto
* **Aggregating Transaction:** aggrega note piccole dentro una più larga
* **Distribuzione:** un input paga più output

### Preparazione di una transazione

* Il wallet ha una lista di tutte le UTXO di Alice (o se non ce l'ha interroga la rete bitcoin per ottenerli)
* Seleziona le UTXO in base ad un algoritmo.
* Si specificano gli output di destinazione e i soldi da pagare (aggiungendo i fees)
* Calcola il resto se presente.
* La differenza sarà la commissione (fee).
* Ha costruito la struttura dati con tutte le informazioni.

### Invio di una transazione

1. Invio della transazione ad un nodo della rete bitcoin p2p.
2. Viene eseguito il flooding della transazione nella rete bitcoin.
3. Il destinatario nota che è stata spedita una transazione con se come destinatario (attraverso un polling). La transazione non è stata ancora confermata
4. Dopo circa 10 minuti la transazione sarà processata dalla rete e il destinatario lo noterà (è stato creato un blocco nella rete). La transazione è stata confermata. Più pago come fee, prima verrà processata.
5. Dopo circa un'ora sarà stata ulteriormente confermata, visto che verranno aggiunti altri blocchi sopra di esso. Sono ulteriori conferme e la transazione ora è finalizzata.

In base all'esigenza, si può ritenere completata la transazione anche nel punto 3. Per altri prodotti si possono aspettare il punto 4 o 5 in base all'importanza.

### Miners and rewards

Sono alcuni nodi della rete bitcoin che creano i blocchi contenenti ciascuno più transazioni. Il miner, dopo aver creato un blocco, verrà ricompensato con le fees delle transazioni. Il miner riceverà anche una costante k chiamata inflazione, la quale raggiungerà il valore 0 il giorno nel quale 21.000.000 di bitcoin verranno generati. Non ci sarà più inflazione e non verranno creati, perciò, più bitcoin.

Il lavoro del miner è il seguente:

* Rimane sempre in ascolto della rete P2P, in attesa di Dtransazioni.
* Quando ha abbastanza transazioni sono state memorizzate nella mempool, alcune di loro (tipicamente quelle con fees maggiore).

Dopo circa 10 minuti ci sarà una gara a chi processa prima la transazione e ne crea il conseguente blocco:

* Prenderà input con tutti input già processati.
* Crea il blocco (struttura dati) con le transazioni una dopo l'altra
* Aggiunge la transazione coin base transaction, la quale ha 0 input e come indirizzo quello del miner (soldi percepiti)
* Aggiunge un puntatore al blocco precedente 
* Aggiunge al blocco l'indirizzo del miner, per confermare che ha svolto il lavoro lui
* Aggiunge il nonce (conferma dei calcoli)
* Se non ci sono peer più veloci, allora informa tutti e crea il blocco, altrimenti ha perso e non guadagnerà nulla.
* Si aggiorna il manpool, con le transazioni non incluse nel blocco.

Le fees dipendono dalla lunghezza della transazione.

Altezza: numero del blocco

Profondità: numero dei blocchi posizionati sopra. Più è in profondità il blocco, più è difficile cambiarlo.

### Composizione di una transazione

* **vins:** transazione di input
  * **unlock:** script
* **vouts:** transazione di ouput
  * **lock:** abilita l'uso di quel denaro a qualcuno

## Crittografia

Nella blockchain si utilizzano due principali sistemi di criptazione:

* **Hash:** per compattare informazioni complesse in una rappresentazione molto più semplice, puntatore a strutture dati indipendente dalla macchina oppure per il mining (per risolvere un problema computazionale complesso)
* **Signatures:** per firmare una struttura dati

Non la usano per nascondere dati. Tutti i dati sono pubblici.

### Indirizzi bitcoin

* Private key: 256 bits

* Public key: 256 bits

* Bitcoin address: 160 address

La chiave pubblica viene generata dalla chiave privata attraverso un'algoritmo di hash. In seguito si riduce un'ulteriore algoritmo di hash per ridurre la lunghezza dell'indirizzo.

In seguito ottengo il mio indirizzo in base 58 per ridurre ancora di più la lunghezza di esso.

### Checksum

È stato aggiunto anche un checksum alla fine dell'indirizzo, così da facilitare l'inserimento corretto.

Consiste negli ultimi 4 cifre del risultato... 

### Deterministic wallet

Nel wallet viene memorizzato solo un seed, dal quale stream si ottengono tutte le chiave derivate. Solo il seed dovrà essere memorizzato, backupato e mantenuto privato. 

Questo seed può essere 512 bit o anche di più. In alternativa, si possono memorizzare 12 parole dalle quali si può recuperare il seed. Viene aggiunta anche una password SOT da 2048 bit per evitare attacchi a dizionario.

Non esistono password sbagliate, ma semplicemente verrà generato un seed diverso dal mio.

Esiste anche un algoritmo che permette di passare da chiave pubblica a chiave pubblica, senza passare da quella privata.

## SCRIPT

È il linguaggio di programmazione utilizzato da bitcoin per rilascio e l'aggancio della moneta ed è turing incompleto. Il tempo di esecuzione è predecibile. È in notazione postfissa.

La validità di un programma scritto in Script è data da se termina con uno stack non vuoto e con in cima true.

La validità serve per verificare se qualcuno può spendere i soldi.

### P2PKH script (pay to public key hash)

Da la prova di ownership

```
<sig> <PubK> DUP HASH160 <address> EQUALVERIFY CHECKSIG
```

* **sig:** firma digitale di TX con la chiave privata
* **PubK:** chiave pubblica
* **DUP:** duplica la cima dello stack
* **HASH160:** RIPEMD160(SHA256(PubK)) da chiave pubblica a indirizzo
* **Address:** indirizzo bitcoin del destinatario dei soldi
* **EQUALVERIFY:** verifica che address e l'output di HASH160 coincidano
* **CHECKSIG:** verifica la firma di chi può usare i soldi. Confronta  il sig con il PubK

### Lock script

```
DUP HASH160 <address> EQUALVERIFY CHECKSIG
```

### Unlock script

```
<sig> <PubK>
```

## Blocco

* **Previous block header hash:** codice hash del blocco precedente.
* **Timestamp:** messa dal computer miner
* **Difficoltà:**
* **Nonce:** 
* **Merkle root:** hash derivante da tutte le transazioni

### Merkle root

Un albero di merkle è un albero dove l'hash di un nodo corrisponde agli hash dei suoi figli. I figli avranno gli hash, nella blockchain, delle transazioni.

Serve per controllare se è stata aggiunta una transazione K.

L'albero dei merkle si trova in una memoria virtuale del blocco e serve solo per rispondere. Si salva solo la radice.

Mantenendo l'albero binario bilanciato, è molto veloce.

## Mining

Serve per garantire la sicurezza della rete, infatti ogni blocco generato deve rispettare delle regole del consenso:

* La struttura dei blocchi deve essere sintatticamente corretta
* Ogni transazione deve avere un input, eccetto per quelle coinbase
* Ogni transazione deve avere almeno un output
* Le transazioni trasferiscono solo i bitcoin, eccetto per quelle coinbase
* Quantità di soldi giusta
* Le transazioni devono essere valide (P2PHK script)
* Gli input delle transazioni devono essere unspent

### Costruzione di un blocco all'altezza H

* Prelevazione di un certo numero di transazioni valide dalla mempool
* Aggiunta della coinbase transaction
* Computazione della merkle tree root
* Creazione dell'header del blocco
  * Aggiunta hash del blocco H-1
  * Timestamp
  * Merkle tree root
  * Nonce
  * Difficulty

Se riceve il blocco H che sta anche lui creando da un altro computer, allora verificherà che è valido (verifica le regole del consenso). Se è valido ha perso e lo inserisce nella sua blockchain ed inizia a lavorare al blocco H+1.

La creazione del blocco è difficile in maniera random.

### Proof of work

L'hash del blocco valido deve essere più piccolo di una difficoltà costante.

1. Sceglie un numero nonce a caso.
2. Calcola l'hash dell'header.
3. Se l'hash è minore della difficoltà, allora bene.
4. Altrimenti deve tornare al primo punto.

Più piccola è la difficoltà, peggio è.

### Fork

La main history è il fork con la storia più lunga

## Consesous attack

Se ho il 51% della potenza di calcolo dell'intera rete, posso riscrivere la main history generando una storia più lunga.