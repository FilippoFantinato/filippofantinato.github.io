# Solidity

## Caratteristiche

* Imperativo
* Orientato ad oggetti
* In continua evoluzione
* Non fortemente tipizzato
* Ortogonalità

* Sequence
* Conditional
* Repetition
* Turing completo

## ABI

Fornendolo al client Ethereum, da informazioni di signature al blocco.

## Tipi

* **address:** 20 byte del blocco dove è mappato il contratto, oppure la transazione
  * i cast non falliscono
  * Ha un campo chiamato balance
  * Non può esistere un operatore instanceOf
* **bytes**
* **string**
* **arrays**
* **enumerations**
* **struct**

### Mappings

* Default value 0
* Non c'è un containsKey
* Non è possibile iterare sulla mappa

### Informazioni di una transazione

* **msg.sender:** l'indirizzo del chiamante o contratto
* **msg.value:** gli ether pagati per la transazione
* **msg.gasleft**: quanto rimaneva da consumare del gas limit
* **msg.data**: il payload della transazione
* **msg.sig:** i primi 4 bytes del msg.data (il selettore del metodo)
* **tx.gasprice:** il prezzo del gas utilizzato durante la transazione
* **tx.origin:** l'indirizzo dell'EOA originale

Il msg.sender può essere anche un altro contratto, il tx.origin sicuramente un EOA

### Informazioni di un indirizzo

* **address.balance:** il bilancio di un indirizzo (EOA o contratto)
* **address.transfer(x):** manda x wei all'indirizzo, lanciando un'eccezione in caso di f
* **address.send(x):** manda x wei all'indirizzo, ritornando false se fallisce
* **address.call(p):** chiama una funzione che si trova in un altro contratto, non mantenendo il contesto di chiamata
* **address.callcode(p):** chiama una funzione che si trova in un altro contratto, mantenendo il contesto di chiamata (le variabili del contratto)
* **address.delegatecall(p):** chiama una funzione che si trova in un altro contratto, mantenendo il contesto di chiamata (le variabili del contratto), il msg.sender e il msg.value

### Informazioni di un blocco

* **block.coinbase**: l'indirizzo del miner
* **block.difficulty:** la difficoltà della proof of work
* **block.gaslimit:** il massimo gas che può essere speso nel blocco corrente
* **block.number:** l'altezza corrente del blocco
* **block.timestamp:** il mining time

## Le unità di codice

* **contract:** simile ad una classe
* **interface**
* **library:** un contratto che verrà usato da altri contratti e ha solo funzioni

## Modificatori

* **public:** può essere chiamata da chiunque
* **external:** come public, ma se chiamata dallo stesso contratto genera una nuova transazione, costa meno gas rispetto ad una funzione public
* **internal:** come protected
* **private:** può essere chiamato solo dentro al contratto

## Side effect modificatori

* **view:** la funzione non può modificare lo stato
* **pure:** la funzione non può ne leggere e ne modificare lo stato
* **payable:** la funzione può ricevere dei pagamenti

## Ritorno

```
function min(int a, int b) pure public returns(int) {
	return a < b ? a : b;
}

function split(int n, int divisor) pure public returns(int, int) {
	return (n / divisor, n % divisor);
}

function split2(int n, int divisor) pure public returns(int quotient, int rest) {
	quotient = n / divisor;
	rest = n % divisor;
}
```

## Costruttori

```
contract Test {
    constructor(uint _i) public {
        i = _i;
    }
}
```

## Modificatori

Al posto del _; viene posizionato il corpo del metodo a cui è stato applicato.

```
modifier onlyOwner {
	require(msg.sender = owner);
	_;
}

function destroy() public onlyOwner {
	...
}
```

## Ereditarietà

Si può ereditare da un contratto con la parola chiave **is**.

### Supercostruttori

Si possono invovare chiamandoli direttamente dalla classe ereditata.

## Asserzioni

* **require(condition[, msg]):** controlla qualcosa che potrebbe andare storto.
* **assert(condition[, msg]):** controlla se un dato è come me lo aspetto
* **revert([msg]):** blocca la transazione e si perde il gas

## Events

Servono per informare l'esterno che è successo qualcosa, pensata per lo sviluppo di DApps.

## Tipizzazione

Solidity non è fortemente tipato:

* Non controlla i cast
* Non controlla il tipo degli oggetti

## Gas consumption

È possibile calcolare il gas di una funzione. Non si può capire quanto gas serve per eseguire una funzione.

La funzione estimate gas di web3 può calcolare il gas di funzioni semplici, ma quando iniziano a complicarsi non è affidabile

I cicli su array dinamici e le chiamate a contratti esterni sconosciuti, rischiano di alzare il gas.

## withDraw pattern

È bene separare la funzione di pagamento da un'altra funzione di che ha un altro scopo, visto che ia funzione send o trasnfer può fallire.

## Reentrancy

Invocazione ricorsiva di una funzione di pagamento ridefinita.

Attualmente non c'è il rischio di reentrancy perchè è stato imposto una quantità massima di gas (2300) per le funzioni send e transfer. 

Per pagare qualsiasi unità di gas si può chiamare la funzione di basso liberllo msg.sender.call.value(amount)("")