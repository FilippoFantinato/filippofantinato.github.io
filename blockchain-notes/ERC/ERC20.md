# ERC20 Tokens

## Cosa sono

Sono monete virtuali costruite su altre blockchain e possono essere usate per gestire le quote. Un token ERC-20 non è altro che un contratto intelligente che ha una struttura dati prestabilita. Questa struttura è progettata per facilitare l'implementazione di varie funzionalità sulla blockchain di Ethereum, facilitando il lavoro di creazione per gli sviluppatori. 

Lo standard ERC20 regolarizza la creazione e gestione di token. I token ERC-20 sono, in linea di principio, smart contract che vengono eseguiti nella blockchain di Ethereum. Funzionano all'interno di uno schema programmatico stabilito dal team di Ethereum. Questo schema è abbastanza ampio da consentire usi diversi senza interrompere il funzionamento della blockchain di Ethereum. Ad esempio, sono in grado di portare una sottocontabilità parallela al libro principale di Ethereum, avendo una propria unità di conto. Tutto questo senza che si mescolino i saldi Ether degli indirizzi garantendo però, la trasparenza, la tracciabilità e la sicurezza che la rete Ethereum fornisce.

## Perchè sono stati creati

La motivazione principale degli sviluppatori durante la creazione di qualcosa di così vasto, è stata principalmente di voler crear un sistema de capacità multipla. Tutto questo sotto un'interfaccia standard riutilizzabile per altre applicazioni: dai portafogli agli scambi decentralizzati. Tutto questo sotto a un API che garantisce agli sviluppatori i seguenti vantaggi:

1. **Uniformità in programmazione**. L'API è standard e stabile, il che facilita il compito di programmare utilizzandolo. Ciò rende facile per i programmatori creare un nuovo software basato sulle capacità di Ethereum.
2. **Riduce la complessità della programmazione**. Dato che l'API è semplice, il suo utilizzo riduce la complessità del software creato per utilizzarla. Questo si traduce in una migliore lettura, sicurezza e verificabilità del codice scritto.
3. **Supporto per più linguaggi di programmazione e miglioramenti nella portabilità**. Poiché l'API dei token è gratuita, è possibile programmarla in diversi linguaggi di programmazione. Ciò facilita notevolmente la capacità di creare un software specifico. Alcuni dei linguaggi supportati per questa attività sono Solidity, JavaScript, C, C ++, Python, Java e Go.
4. **Meno complessità nella comprensione di ogni tipo di token implementato**. Ciò è dovuto al fatto che saranno tutti basati sugli stessi principi di funzionalità.
5. **Maggiore sicurezza**, soprattutto grazie a funzionalità come token allowance.
6. **Minor rischio di rottura dei contratti**, non essendoci impedimenti o incompatibilità. Questo grazie al fatto che l'API sia stabile, il che comporta che le modifiche introdotte lo migliorino , ma senza interrompere mai la compatibilità.

## Caratteristiche principali

1. **Hanno un nome o un identificatore e un simbolo associato**. Attraverso questi due valori è possibile identificare e differenziare i token l'uno dall'altro all'interno della blockchain di Ethereum.
2. **È in grado di gestire gli aspetti economici di base della sua emissione**. Dati come il sistema di precisione decimale e l'emissione totale sono una parte fondamentale del token nella sua struttura dati.
3. **Gestisce un'interfaccia per controllare e rivedere i bilanci degli indirizzi dei suoi proprietari**. In questo modo il token è in grado di riportare il saldo totale dei fondi contenuti in uno specifico indirizzo.
4. **Può gestire il sistema di trasferimento in modo originario**. Questo grazie al fatto che il token possiede funzioni per gestire i trasferimenti di fondi.
5. **Inoltre, il token è in grado di gestire autonomamente prelievi parziali di fondi da un indirizzo**. Ad esempio, se a Juan viene dato il permesso di prelevare 1000 ETH dal conto di Maria, Juan può ritirare 250 ETH al primo prelievo. Nei prelievi successivi, Juan può terminare il prelievo del resto dei fondi, ma può salire solo fino a 1000 ETH. Una caratteristica che si chiama "Approvato" e che dipende da un'altra chiamata "Fornitura".

## Operazioni

* **Total supply:** quanti soldi sono stati stampati di questa moneta (token).
* **Transfer:** trasferimento di token.
* **Balance of:** vedere quanti soldi ha un account.
* **Allowance:** quantità di token a nome mio che un account gestore può gestire.
* **Approve:** per mandare in gestione dei soldi si usa la funzione approve, facendoli gestire da qualcuno di cui mi fido. In seguito il gestore può trasferire i soldi come se fossi io.

## OpenZepplin

È l'implementazione più famosa di ERC20.

## Tokenizzazione

