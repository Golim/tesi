# Prima pagina
Buongiorno, sono Matteo Golinelli. Oggi parlerò dell'esperienza di tirocinio che ho svolto da febbraio a giugno del 2019 presso l'azienda Digicando. La presentazione ha come titolo "La gestione di ruoli e permessi sulla blockchain Ethereum".

# Digicando
L'azienda Digicando fornisce un servizio di anticontraffazione, certificazione e tracciabilità di prodotti. Inoltre, fornisce un sistema di analisi statistica sugli acquirenti dei prodotti stessi ed un sistema di recensioni affidabili e certificate.

# Architettura
L'architettura attuale del servizio di Digicando è un'architettura classica client-server. Quindi tutti i dati ed il controllo sono centralizzati all'azienda.

L'obiettivo futuro però è di spostare il servizio di anticontraffazione sulla blockchain Ethereum.

L'utilizzo della blockchain porterebbe ad una decentralizzazione del controllo, eliminando la necessità di fiducia dei produttori verso il servizio di Digicando e Digicando stessa.

# Motivazioni
L'adozione della tecnologia blockchain fornisce infatti un'infrastruttura in grado di registrare, certificare e mappare i trasferimenti di proprietà di un prodotto in maniera sicura, immodificabile, trasparente ed aperta al controllo di chiunque o di specifici utenti autorizzati.

# Svantaggi
L'utilizzo della tecnologia blockchain introduce però anche una serie di problematiche. Prima fra tutte la mancanza del concetto di segretezza, ogni dato pubblicato sulla blockchain è infatti potenzialmente visibile a tutti. Questo problema ha portato a varie difficoltà nell’implementazione dell’algoritmo di verifica con chiavi segrete dinamiche brevettato da Digicando, che è
stato quindi modificato.

Una seconda problematica è la scalabilità della blockchain stessa, infatti le transazioni che possono essere processate ogni secondo da una blockchain è molto limitato (si calcola siano circa 15 per Ethereum) e con il crescente numero di utenti di questa tecnologia il problema si sta aggravando.

L'ultima problematica è legata alla possibile introduzione di leggi che limitino le possibilità di utilizzo delle criptovalute e, dato che anche Ethereum ne ha una, di conseguenza la tecnologia blockchain. TODO: migliorare

# Blockchain 1
La blockchain è una struttura dati distribuita, che ha come obiettivo il mantenimento di un registro immodificabile e crescente. Questo registro è composto da blocchi, interconnessi tra loro utilizzando la crittografia.

# Blockchain 2
Infatti, ogni blocco contiene una firma crittografica (chiamata hash) del blocco precedente. Nella forma più basilare di una blockchain, ogni blocco contiene inoltre un timestamp e dei dati riguardanti delle transazioni.

# Blockchain 3
La blockchain ha due caratteristiche principali che la rendono diversa dalle strutture dati tradizionali.

La prima caratteristica particolare è il fatto di essere distribuita: ogni partecipante alla rete della blockchain infatti ne condivide una copia identica a tutte le altre.

La seconda caratteristica è il fatto di essere immodificabile per definizione, infatti una qualsiasi modifica ad un blocco precedentemente aggiunto alla catena invaliderebbe crittograficamente l'intera struttura, dato che le firme non combacerebbero più.

# Ethereum
Ethereum è una blockchain completamente open-source con criptovaluta nativa chiamata Ether. Una criptovaluta è una moneta digitale, la cui fornitura non è controllata da alcun governo o azienda.

Ethereum, inoltre, è programmabile: permette, cioè, di sviluppare ed eseguire applicazioni decentralizzate, chiamate DApp, che beneficiano della criptovaluta e delle caratteristiche della blockchain.

# Problema 1
Durante la fase di sviluppo dell’applicazione distribuita di Digicando si è data priorità allo sviluppo del core dell’applicazione. Alcune caratteristiche e funzioni sono state tralasciate per il futuro.

Una delle principali limitazioni del servizio di Digicando basato sulla blockchain è l'impossibilità di gestire i contratti, cioè i programmi che compongono l'applicazione decentralizzata, da più indirizzi Ethereum. Questo costringe a mantenere una chiave privata condivisa tra tutti gli utenti autorizzati e limita fortemente la flessibilità del sistema nell'aggiunta e rimozione di tali utenti autorizzati.

# Problema 2
Inizialmente la gestione dei ruoli è stata realizzata mediante un sistema di whitelisting di indirizzi Ethereum direttamente all'interno dei contratti stessi. Questo approccio, però, ha comportato un irrigidimento del sistema nel momento di eventuali aggiornamenti ed ha comportato un'aumento della complessità dei contratti interessati, costretti a svolgere più compiti non direttamente correlati al loro scopo.

# Requisiti
Insieme all'azienda sono stati individuati tre requisiti fondamentali del sistema di gestione dei ruoli da sviluppare. Primo fra tutti: il sistema deve lavorare interamente sulla blockchain, per ottenere una perfetta integrazione con il resto dell'applicazione.

Il secondo requisito fondamentale è la dinamicità sulla creazione di nuovi ruoli. In pratica, i ruoli ammessi e gestiti dal sistema non devono essere limitati ad un insieme fisso e non deve essere necessario sviluppare e distribuire un nuovo contratto ogni volta si renda necessario supportare un nuovo ruolo.

Infine, i ruoli devono poter essere gestiti anche in maniera gerarchica.

# Soluzione
Si è deciso di sviluppare due contratti esterni, in sostituzione del sistema di whitelisting degli indirizzi. L'approccio migliore individuato è stato un sistema basato su claim, che gli utenti sono in grado di attribuirsi tra loro e che conferiscono particolari privilegi a chi le riceve.

# Tecnologie utilizzate
Le tecnologie utilizzate per lo sviluppo sono tutte open-source. Le principali sono 3. La prima è Solidity, che è il linguaggio di programmazione per la blockchain Ethereum più famoso ed utilizzato. La seconda è Truffle, cioè è un ambiente di sviluppo ed un framework per il testing, che offre inoltre un insieme di risorse utili allo sviluppo per Ethereum. La terza ed ultima è Ganache, cioè uno strumento per la creazione di blockchain personali, utilizzabili per il testing.

# Contratti 1
Il primo contratto sviluppato si chiama ClaimsRegister ed implementa un registro che memorizza i ruoli emessi, cioè le claim. Fornisce anche due funzioni, una per la verifica della presenza di una singola claim nel registro ed una per la rimozione di una claim precedentemente emessa.

# Contratti 2
Il secondo contratto invece, permette di gestire delle strutture organizzative di ruoli gerarchiche e complesse, come quella in foto, grazie all'implementazione di una funzione di controllo di validità di una catena di claim.

# Registro
Il registro è un mapping, che nel linguaggio di programmazione Solidity rappresenta una tabella hash. Il registro associa un valore a tre chiavi, che sono in ordine: l'emitter, cioè l'indirizzo emettitore della claim, il receiver, cioè l'indirizzo ricevitore e la claim, cioè la chiave di un ruolo che è rappresentata da un array di 32 byte. Il valore è dello stesso tipo della chiave, cioè un array di 32 byte.

# Integrazione
Il processo di integrazione è proseguito per fasi. Per prima cosa è stata studiata l'implementazione attuale, con la creazione di un diagramma delle classi per una più chiara visione d'insieme. Secondo, sono stati individuati i contratti che fanno uso del sistema di whitelisting. Successivamente è stato sostituito il vecchio sistema con il nuovo. In ultimo, è stato effettuato un testing approfondito, sia automatico che manuale, mediante l'utilizzo di blockchain personali.

# Conclusioni
Per concludere, il sistema sviluppato, composto dai due contratti, ha risolto il problema dell'azienda ed ha reso il sistema integrato più flessibile, funzionale e performante.

# Ringraziamenti
Vi ringrazio per l'attenzione, resto disponibile per eventuali domande.