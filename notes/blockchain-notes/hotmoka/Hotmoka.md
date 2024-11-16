# Hotmoka

## Cos'è

È un'implementazione open source di una rete di nodi, non solo blockchain perciò. Consiste in un application layer di tendermint core.

## API

```
[add|post]JarStore(request):TransactionReference

[add|post]ConstructorCall(request):StorageReference

[add|post|run]InstanceMethodCall(request):StorageValue

[add|post|run]StaticMethodCall(request):StorageValue

subscribeToEvents(key):Subscription

getState(StorageReference):State
```

* add calls are synchronous (wait for the result)
* post calls are asynchronous (yield a future)
* run calls are synchronous and only for read-only methods

## OO State

![OO state](/home/filippofantinato/Desktop/Stage/Blockchain/hotmoka/images/oo-state.png)

La blockchain è una semplice blockchain tendermint. 

Per quanto riguarda lo stato, invece, è una mappa da richiesta a risposta (hash richiesta a hash risposta). Viene rappresentato come Merkle tree. È stata creata una mappa chiamata hitories, dove per ogni oggetto è presente l'hash di tutte le request (vengono mantenuti gli hash solo delle ultime request che vanno a modificare lo stato dell'oggetto). 

## API State

1. **Ottenere il jar dall'hash:** accedere alla mappa Responses e trovare il jar
2. **Ottenere l'oggetto obj**: accedere alla mappa Histories a obj, collezionare ogni hash, accedere alla mappa di risposte e aggiornare obj per ricostruirlo
3. **Mettere request/response nello stato:** espandere la risposta con hash(request) => response. Se la risposta contiene aggiornamenti ad un oggetto, si aggiunge anche hash(request) alla storia dell'oggetto corrispondente.
4. **h=get_hash():** calcola l'hash dal Merkle-Patricia tries for la risposta e la storia
5. Non c'è checkout

## Parametri della rete

![hotmoka-net-parameters](/home/filippofantinato/Desktop/Stage/Blockchain/hotmoka/images/hotmoka-net-parameters.png)

**Rosso:** oggetto java

**Viola:** informazioni

* **takamakaCode:** indirizzo ad una libreria installata. È un jar
* **chainID:** id delle rete
* **allowsUnsignedFaucet:** la rete mette a disposizione un faucet per ricavare i soldi
* **maxFaucet:** dimensione massima di soldi da prelevare
* **gasPrice:** è al minimo perchè la rete non è usata
* **numberOfValidators:** numero di validatori
* **gamete:** account con tutti i soldi concentrati (chi ha installato la rete)
* **gasStation:** oggetto java per la gestione del gas
* **validators**: oggetto java per la gestione dei validatori
* **signature:** tipo di firma da utilizzare
* **manifest**: 

## L'esecuzione di un metodo

**Le specifiche della richiesta**

* Oggetto del pagante, del ricevitore e gli argomenti
* Classpath, firma del metodo
* Nonce, chain id, gas price, gas limit
* Firma della richiesta

**La computazione della risposta**

1. Crea un classloader form del jar nello stato della classpath
2. Ricostruisce, dallo stato, gli oggetti in input (deseralizzazione)
3. Esegue il metodo su una normale Java Virtual Machine (in RAM)
4. Alla fine, identifica gli aggiornamenti agli oggetti del metodo chiamato
5. Serializza gli aggiornamenti in una risposta
6. Aggiornamento della richiesta e della risposta nello stato

## Aggiornamento dello stato di un campo

Quando viene creato un'istanza di un oggetto di classe C, tutti i campi vengono duplicati aggiungendoci il suffisso old_.

Quando una transazione ha inizio, old_i assume il valore di i all'inizio e se poi viene modificato i, allora si confronta con il suo campo old.

## Enforce del gas limits

Viene aggiunto un counter static long, che viene incrementato ad ogni iterazione di un ciclo e viene confrontato con il gasLimit impostato. Se il counter lo supera allora viene lanciata l'eccezione OutOfGasError

## Verifica e strumentazione del jar

### Verifica

* Objects stored in state extend Storage
* Non-deterministic or non-terminating library code is not used
* No synchronization
* No native code
* No dangerous bytecodes
* No finalizers
* No static fields (mostly)
* Code annotations are used correctly
* ...

### Strumentazione

* Fields of Storage classes get duplicated
* Gas metering is weaved into the code
* Code annotations get implemented by magic
* ... 