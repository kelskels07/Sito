In questa relazione spiegheremo come funziona l’architettura Client-Server e P2P. L’obiettivo della relazione è comprendere come avviene lo scambio di dati tra più computer utilizzando il protocollo TCP, mettendo in pratica i concetti di socket, thread e comunicazione concorrente. Durante il lavoro abbiamo sviluppato programmi in Java capaci di inviare e ricevere file, prima tramite un server centrale e poi tramite un’architettura P2P più evoluta, in cui ogni nodo può comportarsi sia da client che da server.
Infine, abbiamo confrontato le due soluzioni misurando i tempi di trasferimento, soprattutto nel caso di file di grandi dimensioni, per capire quale architettura risulti più efficiente e perché.



CLIENT–SERVER vs P2P EVOLUTO
Architettura e gestione del file

Nell’architettura Client–Server è presente un server centrale che possiede inizialmente il file. Tutti i client devono necessariamente connettersi a questo server per poterlo scaricare. Il server si occupa di gestire le richieste e di inviare il file ai client; anche se è possibile utilizzare thread separati per consentire più trasferimenti simultanei, tutti i flussi di dati passano comunque dal server. Questo approccio rende l’architettura semplice da implementare e da controllare, ma introduce un possibile collo di bottiglia, soprattutto nel caso di file di grandi dimensioni o di un numero elevato di client connessi contemporaneamente.

Nel P2P evoluto, invece, non esiste un nodo centrale fisso. Ogni peer può svolgere contemporaneamente il ruolo di client e server. Quando un peer scarica un file, o anche solo una parte di esso, può immediatamente iniziare a condividerlo con altri peer della rete. Questo modello distribuito consente di scaricare lo stesso file da più sorgenti contemporaneamente, riducendo il carico su un singolo nodo e sfruttando in modo più efficiente la banda disponibile.

Velocità di trasferimento

Nel modello Client–Server, la velocità di trasferimento dipende fortemente dalla capacità del server e dal numero di client che richiedono il file. All’aumentare dei client, il tempo complessivo di distribuzione del file cresce in modo quasi lineare, perché il server deve comunque gestire tutte le connessioni e i flussi di dati.

Nel P2P evoluto, invece, più peer possiedono già il file (o parti di esso), più download possono avvenire in parallelo da sorgenti diverse. Questo riduce significativamente il tempo complessivo di trasferimento, soprattutto per file di grandi dimensioni e reti con molti peer attivi. In questi scenari, il P2P risulta generalmente più veloce rispetto al modello Client–Server.

Scalabilità e affidabilità

Dal punto di vista della scalabilità, l’architettura Client–Server presenta dei limiti evidenti: se il server è lento, sovraccarico o va offline, tutti i client ne risentono. Tuttavia, è un modello semplice da implementare e gestire, particolarmente adatto a scenari con pochi client o per test in ambienti controllati.

Il P2P evoluto è invece altamente scalabile: all’aumentare del numero di peer cresce anche la capacità complessiva della rete di distribuire i file. Inoltre, è più tollerante ai guasti, perché la disconnessione di un singolo peer non impedisce agli altri di continuare lo scambio dei dati. Di contro, la sua implementazione è più complessa, soprattutto quando si devono gestire più file, frammentazione e sincronizzazione dei dati.

Esempio di trasferimento di un file da 50 MB

Supponiamo di trasferire un file di 50 MB (52.428.800 byte) in una rete locale con 3 peer e una velocità media di 10 MB/s.

Nel caso Client–Server TCP, il server invia il file ai client uno alla volta. Ogni trasferimento richiede circa 5 secondi (50 MB ÷ 10 MB/s). Di conseguenza, il tempo totale per servire tre client è di circa 15 secondi (5 s per ciascun client).

Nel P2P evoluto, invece, il peer iniziale possiede il file e lo fornisce al primo peer in circa 5 secondi. Nel frattempo, una volta ottenuto il file (o parti di esso), il primo peer può già iniziare a condividerlo con gli altri. In questo modo, i download avvengono in parallelo e il tempo complessivo necessario affinché tutti i peer ottengano il file si avvicina a 5 secondi.

Se il file viene ulteriormente suddiviso in frammenti (ad esempio da 5 MB ciascuno), ogni peer può scaricare frammenti diversi contemporaneamente da più fonti, riducendo ancora di più il tempo totale di trasferimento, che può scendere anche a 3–4 secondi.

Conclusioni

In conclusione, l’architettura Client–Server è semplice, centralizzata e adatta a reti piccole o a scenari di test, ma presenta limiti di scalabilità e prestazioni. Il P2P evoluto, invece, è un’architettura distribuita, più veloce e scalabile, particolarmente indicata per la condivisione di file di grandi dimensioni in reti con molti peer. La scelta tra i due modelli dipende quindi dal numero di nodi, dalla dimensione dei file e dal tipo di rete considerata.



SITOGRAFIA

[- WIKIPEDIA.org]([[url])
[- ACADEMY.YOUNGPLATFORM]([url](https://academy.youngplatform.com/blockchain/peer-to-peer-p2p-client-server-cosa-sono-come-funzionano/))
[- FASTWEB.it]([url](https://www.fastweb.it/fastweb-plus/digital-magazine/cosa-e-come-funziona-p2p/))
[-POINTBITCOIN.it]([url](https://checkpointbitcoin.it/rete-peer-to-peer-bitcoin/))

