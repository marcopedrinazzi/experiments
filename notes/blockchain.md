# Blockchain 

Blockchain is a distributed legdger.

Ogni blocco contiene data (from: to: amount: in bitcoind), hash del dato, hash del blocco prima.

Proof of work è un meccanismo che rallenta la creazione di altri blocchi. In bitcoin ci vuole circa 10 minuti per aggiungere un blocco alla catena di blocchi. 
La proof of work blocca il tampering dei blocchi perchè se tampero un blocco devo calcolare tutta la proof of work di tutti gli altri blocchi.

Blockchain è basata su una P2P network dove ognuno è libero di aggiungersi. Quando ci si aggiunge si riceve una copia della blockchain. La P2P network è una maniera per verificare anche che quando un blocco nuovo viene creato che questo sia ok. ==> consensus = agreement of which block are valid and which arent.

**Smart contracts** sono programmi memorizzati sulla blockchain e possono essere utilizzati per lo scambio di coin a certe condizioni.
Crowdfunding => Io do i soldi allo smart contract, se il progetto viene finanziato i soldi li manda alle persone del progetto, se il progetto fallisce gli obiettivi i soldi ritornano alle persone grazie allo smart contract.
Gli smart contract sono immutabili e distributi cioè che l'output è validato da tutti sulla rete.

Ethereum => solidity per smart contract.

**Bitcoin hard fork and soft fork**

Bitcoin ha problemi di scalabilità, ha un limite di 7 transazioni/secondo con una dimensione dei blocchi ciascuna di 1MB. **Bitcoin lighting network** risolve i problemi di scalabilità. L'idea principale è che le transazioni day-to-day (compra un caffè) non vengono memorizzate sulla blockchain principale. (off-chain approach)

Bob compra un caffè tutti i giorni. Si crea un payment channel tra negozio e Bob. Deposita 0.05 bitcoin in un multisignature address con la quale il coffeeshop può accedere (il coffee shop deposita 0 perchè non fa refunds). SI accede a questa "safe" solo quando entrambe le parti sono d'accordo. Quando apriamo il payment channel abbiamo un balance sheet che dice come i funds dovrebbero essere distribuiti. Aprire il payment channel avviene sulla main blockchain e permette di far vedere al coffee shop owner che riceverà i soldi che bob ha depositato quando il canale di chiuderà.
Quando il canale è aperto Bob ordina il caffè, il caffè costa 0.005 bitcoin. In seguito aggiorna il balance sheet, toglie 0.005 a quello che lui aveva despositato e il coffee shop ora avrà 0.005 e non piu 0 (quindi riceve il costo del caffè). L'aggiornamento viene firmato con le loro chiavi private di entrambi.
Quando il canale si chiude, si broadcasta il balance sheet, questo viene validato e si rilasciano i fondi nel multi signature address secondo il balance sheet. **QUESTO QUINDI GENERA 1 SOLA TRANSAZIONE SULLA MAIN BLOCKCHAIN E NON 10000 che io posso fare quando il canale di pagamento è aperto**
Richiede in totale due transazione, una di apertura del canale e uno per chiuderla.
Funziona anche con intermediari.

**IOTA** prova a risolvere i problemi di scalabilità. Usa un DAG

**CARDANO**. Lo si considera come la terza generazione di blockchains. Bitcoin prima, Ethereum seconda, cardano e IOTA terza. Ha l'obiettivo di risolvere problemi di interoperabilità, scalabilità, sostenibilità. 

**ERC20 token** esistono sulla ethereum platform (blockchain + ethereum virtual machine che fa andare gli smart contract)
I token esistono sulla ethereum blockchain. La native currency su ethreum blockcahin è ETHER but it can support also other tokens. I token possono rappresentare currency, shares, loyalty points, gold certificates,...
Uno smart contract crea token, gestisce transazione, tiene traccia dei bilanci dei token holder.
To get some tokens bisogna inviare some ETH allo smart contract che da X token di ritorno.
Quando uno smart contract è deployed non può essere piu cambiato/modificato. 
Problema di interoperabilità: exchange deve parlare con il mio contratto. I contratti devono essere diversi e va gestito. ERC20 è la guideline che si usa per creare il proprio token. Name, symbol, decimals. ERC20 è come un interfaccia in un linguaggio di programmazione OO. L'ERC20 facilita la creazione di nuovi token.
Estensione di ERC20, ERC223.

**Proof of work** consuma energia. E' basata sulla soluzione di puzzle crittografici dai miner e questi prendono la miner reward.
Proof of stake has validators not miners. Non fanno mining ma minting/forging. Validators non vengono scelti a caso, fanno un deposito (stake). Più lo stake è alto, più è alta la possibilità che questi vengano scelti come validators.
Se un nodo è scelto per validare il prossimo blocco questo controlla che tutte le sue transazioni all'interno siano valide. Il nodo come premio riceve le fees che sono nel blocco.
I validator perdono parte del loro stake se approvano fradulent transactions.
PoS only select a few validators. Backup del validator si può usare.
PoW everyone mines. Ci sono le mining pools, rendono il tutto meno decentralizzato. Se un gruppo di miners controlla il 51% (almeno) può controllare la blockchain.

**Iterplanetary File System** https://ipfs.io

**Does the GDPR kill blockchain?** Art 16, 17, 18 sono problematici.
Cifrare i dati prima di caricarli.
Memorizzare i dati in una permissioned blochain e non su una public blockchain. (art. 18)
Il problema sono art 16-17 perchè i dati sono immutabili su una blockchain.
Possiamo memorizzare i dati in R/W su un secure server e memorizzare un puntatore a quel server. E Un hash. ==> questo centralizza un po'.
Zero knowledge proof => questo permette di provare che qualcosa è vero senza mostrare i dati. Questo permette di rivelare il meno possibile dei dati. Minimizza la proabilità che qualcuno  stia mentendo.
**Zk-SNARKS**

Wallet serve per memorizzare i coin. Ha un indirizzo pubblico. (Public key). Private key invece prove owenersrhip.

Blockchain serve per ottenere consenso tra una serie di nodi.

**Mining difficulty** cambia nel corso nel tempo per assiucrare che creare un nuovo blocco. Problema: tende a portare a centralization.

**NFT** 
NFT stands for Non-Fungible Token.
Non-fungible means that something cannot be exchanged for another item because it's unique.
For instance, one piece of art is not equal to another.
Both have unique properties.
Fungible items, on the other hand, can be exchanged for one another.
For instance: one dollar or Bitcoin is always equal to another.
Okay, but **what is an NFT?**
NFTs are tokens that live on a blockchain and represent ownership of unique items. Why is that useful?
Well, tracking who owns a digital file is tricky because it can be copied and distributed effortlessly.
So how can you prove who's the original owner when everyone has an identical copy of the file?
NFTs solve this problem.
Imagine that you made a piece of digital art, essentially a JPG, on your computer.
You can create or mint an NFT out of this.
The NFT that represents your art contains a bit of information about it, such as a unique fingerprint of the file, a token name, and a symbol.
This token is then stored onto a blockchain, and you, the artist, become the owner.
Now you can sell that token by creating a transaction on the blockchain.
The blockchain makes sure that this information can never be tampered with.
It also allows you to track who's the current owner of a token and for how much it has been sold in the past.
It's important to note that the artwork itself is not stored within the NFT or the blockchain.
Only its attributes such as the fingerprint or hash of the file, a token name, and symbol, and optionally a link to a file hosted on IPFS.
Now here's where NFT's become weird.
When you buy an NFT that represents artwork, you don't get a physical copy of it.
Heck, most of the time, everyone can download a copy for free.
The NFT only represents ownership, and that is recorded in a blockchain so nobody can tamper with it.
Some say that NFT's give you digital bragging rights.
**And to make it even weirder: while the token owner owns the original artwork, the creator of the NFT retains the copyright and the reproduction rights. So an artist can sell his original artwork as an NFT, but he can still sell prints.**
Aside from digital art, NFT's can also be used to sell concert tickets, domain names, rare in-game items, real estate, and basically anything that is unique and needs proof of ownership.
For example, the founder of Twitter sold his first tweet as an NFT.
Anyone can see that tweet on his profile, but now, only one person can own it.
And that person paid over 2.9 million dollars for it.
I could even make an NFT out of this video.
You could then buy it and be the owner of this video, even though it's free to watch for everyone.
Why are some NFTs worth millions?
Well, their worth is determined by what people are willing to pay for it.
If I'm willing to pay a hundred dollars for a particular NFT, then it's worth a hundred dollars. 
Prices are driven by demand, so be careful because an expensive NFT becomes worthless if nobody wants to buy it.
Okay, one more thing before we end: how do they work technically?
NFTs are smart contracts that live on a blockchain.
In this case, the contract stores the unique properties of the item and keeps track of current and previous owners.
An NFT can even be programmed to give royalties to the creator every time it exchanges hands.
