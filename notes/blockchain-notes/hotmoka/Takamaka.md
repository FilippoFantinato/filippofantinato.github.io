# Takamaka

## Cos'è

Takamaka è un subset di java che passa le verifiche di un nodo Hotmoka. Usa le code annotations per implementare aspetti contract-based:

## Annotazioni

* **@FromContract:** sono funzioni che possono essere chiamate solo da un altro contratto. La funzione caller() ritorna il contratto chiamante.
* **@Payable:** annota qualsiasi cosa che richiede il pagamento di unità in cripto valute.
* **@View:** l'esecuzione legge solo informazioni e viene eseguito gratis.

Ha anche la libreria io-takamaka-code che sarebbe la stdlib di takamaka

## Scrittura di smart contract

Per utilizzare la stdlib di takamaka aggiungere questa dipendenza a maven.

```xml
<dependencies> <dependency>
    <groupId>io.hotmoka</groupId>
    <artifactId>io-takamaka-code</artifactId>
    <version>1.0.0</version>
</dependency> </dependencies>
```

