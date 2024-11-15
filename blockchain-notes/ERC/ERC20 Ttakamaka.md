# ERC Takamaka

## Gerarchia di implementazione

![hotmoka-erc20-hierarchy](/home/filippofantinato/Desktop/Stage/Blockchain/ERC/images/hotmoka-erc20-hierarchy.png)

### IERC20

Interfaccia con le operazioni base. In takamaka transfer può essere chiamata solo da un contratto.

Approve deve essere chiamata solo da un contratto

#### IERC20View

* totalSupply calcola la quantità di token in circolo
* balanceOf calcola il bilancio di un contratto
* snapshot (non standard) fa uno snapshot dello stato attuale del contratto

### ERC20

* costruttore con nome della moneta e simbolo
* mint serve per stampare moneta e viene chiamato solo dal costruttore

### ERC20Burnable

Concretizzazione che brucia una certa quantità di moneta.

### ERC20Capped

Concretizzazione che assegna una quantità massima di moneta in circolo.

## Inconsistenza

Essendo uno stato distribuito e concorrente, per tenere conto del balanceOf. Per questo in takamaka balanceOf ritorna uno snapshot della blockchain per avere uno stato consistente.