# Solidity

## Smart contract

Uno Smart Contract ci permette di scambiare valuta o modificare lo stato di entità presenti in catena in modo trasparente, senza conflitti evitando servizi di terze parti.

## Caratteristiche di uno Smart Contract

* Immutabile (il codice non lo stato)
* Irrevocabile (non posso cancellarlo)
* Incorruttibile (non posso modificarlo)
* Deterministico (stesso output a parità di input) (EVM macchina a stati)
* Terminabile (lo SC deve concludersi in un tempo limitato)
* Isolato (utilizzo di ‘sandbox’, i.e. EVM o Docker in altri casi)

## Cosa possono/non possono fare

Posso:
- Far eseguire computazioni ai peer della rete (computer distribuito)
- Mantenere la persistenza dei dati (ledger distribuito)
- Trasferire soldi (ether) da un wallet all’altro (anche contract)

Non posso:
- Interagire con qualcosa fuori della mia catena (a meno di oracoli oppure il
nuovo protocollo Polkadot molto interessante)
- Schedulare qualcosa che si ripeta periodicamente

## Flusso di deploy 1.0

1. Codice solidity
2. EVM Bytecode
3. Blocco minato con lo smart contract, ottenuto l'address del blocco
4. Interazione attraverso l'address

## Flusso di esecuzione di SmartContract

1. L'utente invia una transazione all'indirizzo dello SC.
2. La transazione viene inviata (broadcasting) ai nodi (come tutte le altre transazioni)
3. Il miner esegue l'SC e se si conclude con successo viene computato un nuovo stato (con l'aggiornamento delle proprietà)
4. Per ogni istruzione ha un costo di calcolo e si dovrà spendere una certa quantità di soldi in base a quanto è complessa. Viene calcolato in **gas** e corrisponde alla grandezza dell'effort computazionale.

Il costo totale è dato da un costo di base di 21000 GAS (operazioni minime per interagire con lo smart contract durante il deploy). Il costo viene calcolato a seconda del GAS Price, ovver da quanto si è disposti a pagare per GAS. Il costo totale perciò viene calcolato così: 21000 * Gas price. 

## Flusso di mining

Il sender setta un GasPrice (prezzo che il sender è disposto a spendere per 1 gas) ed un gas limit (costo massimo che il sender è disposto a pagare).

I miner sono incentivati ad accettare le transazioni con GasPrice più alto.

Al termine del mining il sender paga il costo esatto e se non è stato speso tutto il budget, allora viene ritornato al sender.

Se fallisce la transazione, il gas usato non viene restituito.

Se la computazione va oltre al gas prestabilito, il contratto viene ucciso.

## GasLimit/GasPrice/GasBlock

* Ogni blocco da minare ha una dimensione
* I minatori aggiungono solo transazioni che ci stiano nel blocco

Più alto imposto il gas limit e meno probabilità ho che la mia transazione venga inserita nel nuovo blocco, visto che posso inserire meno transazioni. 

Conviene sempre impostare il gas limit poco sopra allo stimato.

## Compilazione

File .sol --> .abi || bin

* **.abi:** interfaccia per integrare il codice
* **bin:** codice eseguibile

## Ethereum 2 (Serenity)

* Passaggio da POW a POS (x motivi di consumo energetico e velocità)
* Maggiore sicurezza e scalabilità

### Proof Of Stake

Chi ha più token moneta, ha più probabilità di minare il blocco. Occorre dimostrare di essere in possesso di criptovalute per poter partecipare al sorteggio e aver diritto di veriﬁcare una transazione. Creano i blocchi chi possiede più criptovaluta e dal tempo che la detengono.

Altri «validatori» possono poi attestare di aver visto tale blocco. Quando ci sono abbastanza attestazioni, è possibile aggiungere un blocco alla blockchain. I validatori vengono quindi premiati per la proposta di blocco andata a buon ﬁne.

### Scalabilità di Ethereum 2.0

Questo è possibile usando le shard chains (catene secondarie su blockchain che aﬃancheranno la beacon chain principale) che aumenteranno la capacità del network e miglioreranno la velocità delle transazioni estendendo la rete a 64 blockchain.

### Sicurezza di Ethereum 2.0

La maggior parte dei network in proof of stake hanno un piccolo gruppo di validatori, Ethereum 2.0 richiede invece la presenza di un minimo di 16.384 validatori, il che rende il tutto molto più decentralizzato e quindi sicuro.

## Caratteristiche di Solidity

* Linguaggio orientato agli oggetti
* Forte somiglianza con Javascript
* Tipizzato
* Supporta ereditarietà multipla

### Funzioni

```
function pippo([parameter types])
{public|external|internal|private}
[pure|view|payable]
[return (<return types>)]
{
	
}
```

* **public:** tutti possono accedervi
* **external:** è accessibile solo dall'esterno
* **internal:** è accessibile solo da questo SC o ereditati
* **private:** è accessibile solo da questo SC
* **pure:** la funzione non accederà mai allo stato delle variabili
* **view:** la funzione non altererà in nessun modo lo stato delle variabili
* **payable:** la funzione deve ricevere ether altrimenti la transazione fallirà

### Data location

* **memory:** la variabile rimarrà in un'area temporanea
* **storage:** la variabile viene considerata persistente
* **calldata:** solo per funzioni external (accessibili solo dall'esterno)

### Commenti

* **Single line:** //
* **Multiline:** /* */
* **Ethereum Natural Speciﬁcation:** /// oppure /** */
  Permette di aggiungere le notazioni ai commenti

## DataType

* **bool** boolean_var = false; // default false
* **int8(..256)** int_var = -60313; // default 0 - Esiste anche int, alias for int256
* **uint8(..256)** uint_var = 60313; // default 0 - Esiste anche uint, alias for uint256
* **address** address_var = msg.sender; // default 0x0000000000000000000000000000000000000000
* **bytes1(..32)** bytes_var = "a"; // default “” - Esiste byte (byte1) e bytes(byte32)
* **string** str_var = "GeeksforGeeks"; // default ””
* **enum** enum_var { pop, jazz, rock, rave}

## Strutture

```
struct Studente {
	string name;
	uint matricola;
}

Studente studente1;
Studente studente2 = Studente ("Fabio Pallaro", 100000);
```

## Array

* uint[6] data1;
* uint[] storage myArray;
* myArray.push(1); // add an element to the array
* myArray.push(3); // add another element to the array
* myArray[0]; // get the element at key 0 or first element in the array
* myArray[0] = 20; // update the first element in the array

## Mapping

* mapping(address => uint) balances;
* balances[msg.sender] = 100; //assign a value;
* balances[msg.sender] //read a value;
* balances[unknown_key] //will return the default value of the type, i.e 0

## Chiamate ad altri SmartContract

```
(bool success, bytes memory data) = addressMaster.call(abi.encodeWithSignature("fire(uint8)",1));

require(success);

(bool test, uint8 returnCode, string memory tmp)= abi.decode( data, (bool, uint8, string));

return (test, returnCode, tmp);
```

* **call:** il target contract avrà come msg.sender il caller address, ovvero l'indirizzo dello smart contract
* **delegateCall:** il tagrte contract avrà come msg.sender l'EOA address

## Modificatori

Sono funzioni che hanno il compito di fare delle verifiche su certe condizioni ben specifiche.

Possono essere messi nella firma del metodo così da far eseguire il corpo della funzione, solo se il modificatore ritorna true

Per poter essere eseguito prima del codice, bisogna mettere un **_;** alla fine, altrimenti per  farlo eseguire dopo del codice all'inizio. L'underscore rappresenta il corpo della funzione.

