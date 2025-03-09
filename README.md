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

XSD:
```
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" targetNamespace="http://flussi.mds.it/FlsSiar_3" xmlns:fls="http://flussi.mds.it/FlsSiar_3" xmlns:xs="http://www.w3.org/2001/XMLSchema">
	<xs:simpleType name="tipoTrasmissione">
		<xs:restriction base="xs:string">
			<xs:pattern value="[IVC]{1}"/>
		</xs:restriction>
	</xs:simpleType>
	<xs:simpleType name="annoErogazione">
		<xs:restriction base="xs:int">
			<xs:minInclusive value="2000"/>
			<xs:maxInclusive value="2099"/>
			<xs:totalDigits value="4"/>
		</xs:restriction>
	</xs:simpleType>
	<xs:simpleType name="regioneErogazione">
		<xs:restriction base="xs:string">
			<xs:pattern value="010"/>
			<xs:pattern value="020"/>
			<xs:pattern value="030"/>
			<xs:pattern value="041"/>
			<xs:pattern value="042"/>
			<xs:pattern value="050"/>
			<xs:pattern value="060"/>
			<xs:pattern value="070"/>
			<xs:pattern value="080"/>
			<xs:pattern value="090"/>
			<xs:pattern value="100"/>
			<xs:pattern value="110"/>
			<xs:pattern value="120"/>
			<xs:pattern value="130"/>
			<xs:pattern value="140"/>
			<xs:pattern value="150"/>
			<xs:pattern value="160"/>
			<xs:pattern value="170"/>
			<xs:pattern value="180"/>
			<xs:pattern value="190"/>
			<xs:pattern value="200"/>
			<xs:length value="3"/>
		</xs:restriction>
	</xs:simpleType>
	<xs:simpleType name="codASL">
		<xs:restriction base="xs:string">
			<xs:length value="3"/>
			<xs:pattern value="[0-9]{3}"/>
		</xs:restriction>
	</xs:simpleType>
	<xs:simpleType name="strutturaErogatrice">
		<xs:restriction base="xs:string">
			<xs:length value="6"/>
			<xs:pattern value="[a-zA-Z0-9]{6}"/>
		</xs:restriction>
	</xs:simpleType>
	<xs:simpleType name="oreErogate">
		<xs:restriction base="xs:int">
			<xs:totalDigits value="6"/>
			<xs:minInclusive value="0"/>
			<xs:maxInclusive value="999999"/>
		</xs:restriction>
	</xs:simpleType>
	<xs:element name="FlsSiar_3">
		<xs:complexType>
			<xs:sequence>
				<xs:element maxOccurs="unbounded" ref="fls:Assistenza"/>
			</xs:sequence>
		</xs:complexType>
	</xs:element>
	<xs:element name="Assistenza">
		<xs:complexType>
			<xs:sequence>
				<xs:element ref="fls:Trasmissione"/>
				<xs:element ref="fls:Erogatore"/>
				<xs:element ref="fls:Erogazione"/>
			</xs:sequence>
		</xs:complexType>
	</xs:element>
	<xs:element name="Trasmissione">
		<xs:complexType>
			<xs:attribute name="tipo" type="fls:tipoTrasmissione" use="required"/>
		</xs:complexType>
	</xs:element>
	<xs:element name="Erogatore">
		<xs:complexType>
			<xs:sequence>
				<xs:element name="CodiceRegione" type="fls:regioneErogazione"/>
				<xs:element name="CodiceASL" type="fls:codASL"/>
				<xs:element name="StrutturaErogatrice" type="fls:strutturaErogatrice"/>
			</xs:sequence>
		</xs:complexType>
	</xs:element>
	<xs:element name="Erogazione" nillable="false">
		<xs:complexType>
			<xs:sequence>
				<xs:element name="AnnoErogazione" type="fls:annoErogazione"/>
				<xs:element ref="fls:OreErogate"/>
			</xs:sequence>
		</xs:complexType>
	</xs:element>
	<xs:element name="OreErogate" nillable="false">
		<xs:complexType>
			<xs:sequence>
				<xs:element minOccurs="1" name="OreErogateMMGPLS" type="fls:oreErogate"/>
				<xs:element minOccurs="1" name="OreErogateMedicoSpecialista" type="fls:oreErogate"/>
				<xs:element minOccurs="1" name="OreErogateInfermiere" type="fls:oreErogate"/>
				<xs:element minOccurs="1" name="OreErogateOSS" type="fls:oreErogate"/>
				<xs:element minOccurs="1" name="OreErogateFisioterapista" type="fls:oreErogate"/>
				<xs:element minOccurs="1" name="OreErogateLogopedista" type="fls:oreErogate"/>
				<xs:element minOccurs="1" name="OreErogateTerapistiNeuroPsicomotricitaEtaEvolutiva" type="fls:oreErogate"/>
				<xs:element minOccurs="1" name="OreErogateTecnicoRiabilitazionePsichiatrica" type="fls:oreErogate"/>
				<xs:element minOccurs="1" name="OreErogateTerapistaOccupazionale" type="fls:oreErogate"/>
				<xs:element minOccurs="1" name="OreErogatePsicologo" type="fls:oreErogate"/>
				<xs:element minOccurs="1" name="OreErogateAssistenteSociale" type="fls:oreErogate"/>
				<xs:element minOccurs="1" name="OreErogateEducatoreProfessionale" type="fls:oreErogate"/>
				<xs:element minOccurs="1" name="OreErogateAltroProfessionistaSanitario" type="fls:oreErogate"/>
			</xs:sequence>
		</xs:complexType>
	</xs:element>
</xs:schema>
```

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

### Prerequisiti e dipendenze

Il microservizio può girare su qualsiasi sistema operativo per cui è prevista una JVM (Java Virtual Machine) e utilizza la versione 2.7.17 di Spring Boot.

### Istruzioni per l'installazione

Per poter eseguire la build: 
build system maven,
comando mvn clean package

Per eseguire l'installazione è necessario prendere il jar generato dal build system e copiarlo in una cartella, successivamente all'interno della root folder ( / su Linux mentre C:\ su Windows) creare la cartella sdk e tutte le sottocartelle e i file necessari:
```
 /
 +- sdk
   +- db - la directory in cui viene genrato il db sqllite per la storicizzazione dele anagrafiche
   +- dir - la directory in cui inserire i csv da validare e inviare
   +- esiti - la directory in cui verranno depositati i file con gli esiti delle esecuzioni dell'sdk
   +- log - la directory in cui verranno scritti i log delll'applicativo
   +- progressivo - la directory in cui l'applicativo mantiene un file dat per la generazione degli id di esecuzione
   +- properties - la directory contenente i file di configurazione dell'sdk
      +- config-flusso.properties - file di configurazione principale (da referenziare in fase di avvio)  
      \- configurazioni-anagrafiche.properties - file per la configurazione del recupero delle anagrafiche 
   +- regole - la directory contenente le regole da applicare ai csv
   +- run - la cartella contenente i file di run per ogni singola esecuzione
   +- xmloutput - la directory contenente gli xml di output
   \- sent - la directory in cui vengono spostati gli xml inviati al ministero
``` 
- #### config-flusso.properties
```
nome.flusso=<nome del flusso lato ministero>
flusso.categoria=<categoria del flusso lato ministero>
flusso.codifica=<codice identificativo del flusso lato ministero>
regole.percorso=<path completo al file xml delle regole: /sdk/regole/regole.xml>

xmloutput.percorso=<path completo della folder in cui scrivere l'output>/SDK_{{periodoRiferimento}}_{{idRun}}.xml (/sdk/xmloutput/SDK_{{periodoRiferimento}}_{{idRun}}.xml)

sent.percorso=<path completo della directory in cui spostare gli xml inviati al ministero: /sdk/sent/>
flusso.percorso=<path completo della directory in cui verranno depositati i file csv: /sdk/dir/>
soglia.invio.mds=<numero intero indicante quanti la soglia di record validi per file affinché possa essere inviato l'xml di output: 100>
separatore=<carattere di separazione dei valori nel csv: ~>

run.percorso=<path completo della directory in storicizzare i file di run: /sdk/run>
esito.percorso=<path completo della directory in cui depositare i file di esito: /sdk/esiti>
progressivo.percorso=<path completo della directory in cui generare il file dat dei progressivi: /sdk/progressivo>

url.rest.gaf=<url per l'invio degli xml: https://api.salute.gov.it/api/gaf/upldfunc>
gaf.sender.authorizer.token-issuer.url=<url per l'autenticazione dell'invio: https://nsis-ids.sanita.it/nidp/oauth/nam/token>
gaf.sender.authorizer.token-issuer.grant_type=<flow di autenticazione: verrà fornita dal ministero>
gaf.sender.authorizer.token-issuer.username=<username: verrà fornita dal ministero>
gaf.sender.authorizer.token-issuer.password=<password: verrà fornita dal ministero>
gaf.sender.authorizer.token-issuer.client_id=<client id: verrà fornita dal ministero>
gaf.sender.authorizer.token-issuer.client_secret=<client secret: verrà fornita dal ministero>
gaf.sender.authorizer.token-issuer.scope=<scopes a cui deve appartenere l'utente: verranno forniti dal ministero>
gaf.sender.authorizer.type=<tipo di token di autenticazione: JWT>
gaf.sender.type=REST
gaf.sender.fileType=<categoria del flusso: valorizzare come flusso.categoria>
```

- #### configurazioni-anagrafiche.properties
```
sqlite.database.file.path=<path completo in cui creare il db sqllite: /sdk/db/anagrafica.db>
resilienza.ore=<time to live delle anagrafiche nel DB in ore: 2>

client.rest.headers.x-pplication-id: APP_ID_REGISTRYDOWNLOADER_CLIENT
client.type=REST
client.host=<url del gestore anagrafi: https://api.salute.gov.it/api/gestanag/v1>

rest.authorizer.type=<tipo del token di autorizzazione/autenticazione: JWT>
rest.authorizer.token-issuer.url=<url per la generazione di un token di autenticazione: https://nsis-ids.sanita.it/nidp/oauth/nam/token>
rest.authorizer.token-issuer.grant_type=<tipo di flow da utilizzare per l'autenticazione: client_credentials>
rest.authorizer.token-issuer.username=<username: verrà fornita dal ministero>
rest.authorizer.token-issuer.password=<password: verrà fornita dal ministero>
rest.authorizer.token-issuer.client_id=<client id: verrà fornita dal ministero>
rest.authorizer.token-issuer.client_secret=<client secret: verrà fornita dal ministero>
rest.authorizer.token-issuer.scope=<scopes a cui deve appartenere l'utenza: verrà fornita dal ministero>
```

### Istruzioni di avvio

Per avviare l'applicativo eseguire il seguente comando
```
java -jar <path completo del jar> --config=<path completo al file di configurazione principale>
```
Il comando farà partire il software che rimarrà in attesa di richieste sulla porta 8080

#### Avvio validazione di un csv
```
curl --location --request POST 'http://localhost:8080/v1/flusso/SIAR_OREPROF' \
--header 'Content-Type: application/json' \
--header 'Accept: */*' \
--data-raw '{
    "nomeFile": "test.csv",
    "idClient": "1663" ,
    "modalitaOperativa":"P",
    "annoRiferimento": "2022",
    "periodoRiferimento": "13",
    "codiceRegione": "120"
}'
```

#### Recupero dell'esito di un'elaborazione
```
curl --location --request GET 'http://localhost:8080/v1/flusso/SIAR_OREPROF/info?idRun=34' --header 'Accept: */*'
```

### Detentori di copyright

### Incaricati del mantenimento del progetto open source

### Contatti per segnalazioni

## mantainer:
 Accenture SpA until January 2026




