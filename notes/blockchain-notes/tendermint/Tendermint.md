# Tendermint

Corrisponde all'implementazione di un blocco, la quale utilizza la Proof of Stake, Il comportamento della blockchain è definita dai sviluppatori, espandendola specificando cosa vuole fare.

## Proof of Stake

È una variante del Practical Byzantine Fault Tolerance, dove si risolve il problema raggiungendo il consenso attraverso i nodi che si comportano in maniera corretta. In PoS, invece, ci si basa sullo stake (quantità di moneta). 

* Un insieme dinamico V di validatori decidono un prossimo blocco
* V sarà diverso per ogni blocco, ma calcolati dalla storia precedente
* Per ogni altezza H, qualsiasi validatore $v \in V$:
  1. Si identifica (deterministicamente) un validatore $p \in V$, per il quale ci aspetta che dovrebbe aggregare alcune transazioni e proporre un blocco successivo b
  2. Se b è considerato valido, allora si pre-vota b
  3. Contare quanti validatori pre-votano b
  4. Se almeno $\frac{2}{3}$ della rete pre votano b, allora di pre committa b
  5. Contare quanti validatori pre committano b
  6. Se almeno $\frac{2}{3}$ della rete pre committano b, b viene committato e si incrementa H
  7. Tornare al punto b

Per falsificare un blocco bisogna controllare i $\frac{2}{3}$ dei validatori

Se nel primo punto si scegliono i validatori in base allo stake, allora si implementa il Proof of Stake

## Mempool

Quando arriva una transazione, verrà posizionata nella mempool se valida, altrimenti verrà scartata. 

## Pre-vote

Se io vengo selezionato come proponente di un nuovo blocco, seleziono delle transazioni dalla mempool, creo il blocco e lo propongo. In seguito effettuo il pre vote, il pre commit e il commit se i principi descritti sopra sono rispettati.

## Blocco tendermint

![tendemint block](/home/filippofantinato/Desktop/Stage/Blockchain/tendermint/images/tendemint block.png)

* **Validation for block:** firme dei validatori di quel blocco

## Application layer

Non è parte del Tendermint core ed è compito del programmatore implementarle

* Ci si connette al tendermint core via ABCI (application blockchain interface) usando i sockets
* Può essere su una macchina diversa
* Deve essere deterministico

## ABCI

Per essere il più indipendente dall'implementazione, si chiamano dei metodi che verranno implementati dallo sviluppatore: 

* **checkTX:** controlla se una transazione è sintatticamente corretta ed è un filtro d'ingresso
* **beginBlock:** chiamata all'inizio del blocco, riceve informazioni circa l'insieme dei validatori e quali hanno firmato il blocco precedente
* **deliverTX:** chiamato per ogni transazioni e modifica lo stato dell'applicazione
* **endBlock:** chiamato alla fine del blocco, fornendo informazioni circa l'insieme dei validatori per il prossimo blocco
* **commit:** chiamato quando il blocco è stato committato, fornendo l'hash dello stato dell'applicazione
* **query:** chiamato per la lettura su blockchain

## Lo stato

Viene riportato solo l'hash dello stato in blockchain, per consenso. Deve permettere le transazioni tra beginBlock e commit.

* get_data
* put_data
* h=get_hash()

Non è presente l'operazione di checkout, visto che non si può tornare indietro dato che un blocco quando è committato, è committato e basta. Non esistono fork