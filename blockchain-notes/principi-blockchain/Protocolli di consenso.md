# Protocolli di consenso

## Proof of Work

In PoW i nodi partecipanti competono tra loro per diventare leader, ovvero per guadagnare il diritto di aggiungere il prossimo blocco alla catena, cercando di risolvere un problema computazionale, che consiste in un puzzle crittografico.
Il nodo che, utilizzando le risorse a sua disposizione, presenta per primo la soluzione, viene ricompensato per il lavoro svolto. Questo lavoro viene denominato mining e i nodi validatori sono pertanto miners. Per favorire una velocità accettabile nel processo di validazione, mantenendo allo stesso tempo un buon grado di sicurezza, la soluzione al problema è pensata in modo da essere computazionalmente complessa da trovare, ma di facile verifica.
Per diventare leader, ogni nodo è costantemente impegnato nella computazione di un valore generato come output di una funzione hash, che prende in input l’header del nuovo blocco, costituito dai seguenti campi:

* Hash del blocco precedente;
* Numero di versione del blocco;
* Timestamp del blocco;
* Merkle root delle transazioni: una breve rappresentazione delle transazioni contenute nel blocco proposto;
* Nonce: un numero esadecimale casuale, da modificare ad ogni tentativo.

Un nodo guadagna la possibilità di validare il blocco proposto quando il valore di hash da esso computato è minore o uguale ad una soglia detta target, ovvero:

```
hash(header_block) <= target
```

dove header_block rappresenta, per convenzione, la concatenazione degli argomenti di input della funzione hash sopra elencati.

## Proof of Stake

Nei sistemi basati su Proof-of-Stake il consenso viene raggiunto tramite selezione pseudocasuale del leader incaricato della creazione del successivo blocco. Mentre questa scelta in PoW si basa unicamente sulla potenza di calcolo dei nodi validatori, in PoS essa avviene in funzione dell’interesse (stake) di ciascun nodo nel prendere parte al sistema. 

Lo stake in PoS è generalmente rappresentato dall’ammontare di criptovaluta impegnato come garanzia da ogni partecipante, anche detto stakeholder. Maggiore è questo valore, maggiore è l’interesse del nodo a mantenere un comportamento corretto e una migliore solidità della rete e maggiore è la probabilità che il nodo in questione venga eletto come leader. Come previsto da PoW, anche in PoS il validatore ha diritto al riconoscimento di una ricompensa, in questo caso sotto forma di onorario. 

In PoS l’attività di creazione di un nuovo blocco è spesso detta minting (coniazione) o forging (forgiatura) e un validatore è un minter o forger. Per evitare che venga sempre selezionato il nodo più “ricco” della rete e garantire la casualità della scelta, in aggiunta allo stake di ogni nodo, contribuiscono all’elezione ulteriori criteri, che cambiano da un’implementazione all’altra di PoS.

I criteri più spesso utilizzati sono due:

* **Randomized Block Selection:** il leader è scelto sulla base di una formula che combina il totale dello stake di un nodo con informazioni relative all’ultimo blocco della catena. In questo tipo di implementazione di PoS, ad ogni blocco è associato un campo denominato generation signature.
  Ogni nodo firma questo parametro con la propria chiave pubblica e ne calcola l’hash. Vengono considerati i primi 8 byte del valore ottenuto, denominati hit del nodo. Il nodo stesso calcola un valore target nel seguente modo: 

  ```
                          𝑡𝑎𝑟𝑔𝑒𝑡 = 𝑆 ∗ 𝐵e ∗ 𝑡𝑎𝑟𝑔𝑒𝑡
  ```

  dove S è il tempo trascorso dalla validazione dell’ultimo blocco, B~e~ è lo stake effettivo del nodo e targetb è un valore chiamato base target, che è calcolato in funzione dei metadati dell’ultimo blocco e regola la velocità di validazione della rete. Affinché un nodo venga eletto come validatore, questo algoritmo prevede che:
  
  ```
                                  ℎ𝑖𝑡 < 𝑡𝑎𝑟𝑔𝑒𝑡 
  ```
  
  
  
  Il valore del target cresce con il passare del tempo e con esso cresce il range dei valori di hit per i quali vale la (4.3). In questo modo, anche se ci sono pochi nodi attivi sulla rete, uno di essi prima o poi genererà un blocco.
  
* **Coin Age-based Selection:** si basa sul concetto di invecchiamento (utilizzato già nella blockchain di Bitcoin per assegnare priorità alle transazioni nella rete) e prevede che lo stake di ciascun nodo venga moltiplicato per il numero di giorni in cui è rimasto invariato, cioè non è stato speso (generalmente il minimo è 30 giorni). Il valore così ottenuto è detto coin age e rappresenta la probabilità del nodo di essere scelto come leader. Quando ciò accade la sua coin age viene azzerata.

## Delegated Proof-of-Stake

Nella strategia di DPoS l’intero processo per il raggiungimento del consenso è suddiviso in due parti: 

* la prima consiste nell’elezione di un gruppo di nodi creatori ad opera dell’intera comunità della rete
* la seconda nell’effettiva creazione dei blocchi

Chiunque può decidere di partecipare al processo di validazione, candidandosi e convincendo la comunità di partecipanti di avere i requisiti per svolgere il proprio compito senza causare intoppi al sistema. I candidati che vengono eletti sono detti “testimoni” (witnesses) e comprendono un sottoinsieme della totalità dei partecipanti. 

In modo simile a quanto avviene in PoS per la scelta del leader, in DPoS è lo stake dei partecipanti a determinare il peso del loro voto. Al termine di ogni votazione, che avviene ad intervalli prestabiliti, vengono selezionati come testimoni i primi N nodi che hanno raggiunto il punteggio più alto sulla base del meccanismo appena mostrato, dove N è un parametro specifico del sistema. I testimoni eletti vengono disposti in ordine casuale e viene loro richiesto di produrre e proporre un blocco in un tempo prefissato. Quando viene il suo turno ogni testimone i crea un blocco con le transazioni ricevute dalla rete, lo firma e lo propaga a tutti i partecipanti. Se un delegato non riesce a produrre un blocco nel suo turno (ad esempio perché è andato offline o non completa in tempo la procedura), l’evento viene registrato dal sistema e può portare, previa votazione della rete, all’ espulsione del nodo dal gruppo dei testimoni. Quando l’N-esimo di questi crea il suo blocco, l’ordine viene rimescolato e il ciclo ricomincia.

## Proof of Authority

La strategia alla base di PoA può essere vista come una variante ottimizzata del metodo di consenso previsto da PoS, in cui, invece dello stake, ciò che ciascuno mette in gioco è la propria reputazione. Per partecipare come nodi attivi nel processo di validazione dei blocchi è infatti requisito fondamentale la verifica della propria identità. Quando un partecipante vuole diventare validatore, si propone come tale certificando i propri dati anagrafici. Questo avviene in diversi modi a seconda dell’implementazione adottata, ad esempio può essere chi gestisce la blockchain ad occuparsi interamente della verifica affidandosi ad enti esterni, oppure le identità dei validatori possono essere registrate direttamente sulla blockchain, ad esempio tramite smart contracts, firmati con codici ottenuti mediante tradizionali meccanismi di autenticazione multifattoriale. Così come avviene in DPoS, nella Proof-of-Authority esiste un gruppo ristretto di nodi abilitati alla validazione dei blocchi, detti authorities. Ad ogni authority è associato un id unico, tramite cui viene identificato il partecipante che agisce sulla blockchain. Per mantenere il proprio status, le authorities sono tenute a preservare la sicurezza e l’efficienza della rete: se ad esempio tentasse di validare transazioni fraudolente, oppure involontariamente non riuscisse a garantire prestazioni ottimali nel suo lavoro di validazione, il partecipante perderebbe i propri privilegi e la sua reputazione ne verrebbe danneggiata.