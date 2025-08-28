# sdk-engine-siaroreprof-java

## Sistema Informativo Assistenza Riabilitativa - Ore annuali professionisti

### Descrizione repository:

Il microservizio ha come scopo  l’acquisizione dei dati inviati dalle Regioni in merito ai trattamenti riabilitativi erogati, nell’ambito dell’assistenza semiresidenziale e residenziale, a carattere intensivo, estensivo e di mantenimento di cui all’articolo 34 del decreto del Presidente del Consiglio dei ministri del 12 gennaio 2017.

I dati richiesti sono relativi al set di informazioni legate ai trattamenti riabilitativi di cui all’art. 1, previa valutazione multidimensionale dell’assistito, presa in carico e progetto riabilitativo individuale (PRI) ovvero piano individuale di assistenza e riabilitazione. Il tracciato 3 (SIAR_OREPROF) comprende le informazioni relative alle prestazioni erogate ad un gruppo di assistiti.

Il Sistema SIAR viene alimentato con le informazioni relative ai trattamenti riabilitativi erogati a partire dal quarto trimestre 2023

L'invio dei file viene effettuato mediante un tracciato XML.
Per ogni tracciato XML, è fornito il relativo schema XSD di convalida a cui far riferimento

#### Struttura XML:

Campo tecnico:
- Tipo

Nodi di riferimento:
- Erogatore
- Erogazione

Campi Erogatore:
- Regione di erogazione (campo chiave)
- Azienda sanitaria di erogazione (campo chiave)
- Struttura erogatrice (campo chiave)

Campi Erogazione:
Anno di erogazione
- Ore totali erogate  MMG/PLS
- Ore totali erogate  Medici specialistici
- Ore totali erogate  Infermieri
- Ore totali erogate  Operatori socio-sanitari
- Ore totali erogate  Fisioterapisti
- Ore totali erogate  Logopedisti
- Ore totali erogate  Terapisti della neuro e psicomotricità dell'età evolutiva
- Ore totali erogate  Tecnici della riabilitazione psichiatrica
- Ore totali erogate  Terapisti occupazionali
- Ore totali erogate  Psicologi
- Ore totali erogate  Assistenti Sociali
- Ore totali erogate  Educatori professionali
- Ore totali erogate  Altri professionisti sanitari

## 📚 XSD di riferimento
Il file xsd è disponibile al percorso [`docs/FlsSiar3.xsd`](docs/FlsSiar3.xsd).


### Struttura repository

La cartella principale è src/main/java che è organizzata nelle seguenti cartelle:

- it.mds.sdk.engine.config che raccoglie i file di configurazione
- it.mds.sdk.flusso.siar.oreprof che contiene il file necessario all'avvio dell'applicazione
- it.mds.sdk.flusso.siar.oreprof.controller che contiene i file che vengono invocati direttamente dal client
- it.mds.sdk.flusso.siar.oreprof.dto che contiene le classi che rappresentano il modello interno di sdk
- it.mds.sdk.flusso.siar.oreprof.mapper che contiene le classi di conversione

Nella cartella src/main/resources sono presenti le seguenti cartelle:
- META-INF che contiene file di configurazione
- sicof xhe contiene file .moustache
- template contiene un file di regole e file .csv, .xml e .xsd

sono presenti in resources anche file di configurazione:
- application.yaml
- config-flusso.properties
- csvHeaderMapping.properties
- logback-spring.xml
- tmp.xml

è presente il file pom.xml (Project Object Model), è un file XML che contiene le informazioni sul progetto e dettagli sulle configurazioni utilizzate da Maven per eseguire la build del progetto
### Istruzioni per l'installazione

Per l'installazione e l'avvio dell'engine seguire la documentazione tecnica dettagliata disponibile all'url [`INSTALL.md`](https://github.com/ministero-salute/sdk-utilities-regole-properties/blob/main/INSTALL.md).

## mantainer:
 Accenture SpA until January 2026




