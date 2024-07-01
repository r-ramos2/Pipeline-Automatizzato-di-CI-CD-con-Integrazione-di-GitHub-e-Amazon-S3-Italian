# Pipeline Automatizzato di CI/CD con Integrazione di GitHub e Amazon S3

## Panoramica
Questa guida fornisce i passaggi per configurare un **Pipeline di Integrazione Continua/Distribuzione Continua (CI/CD)** utilizzando GitHub e Amazon S3. Seguendo questi passaggi, sarà in grado di automatizzare il processo di distribuzione della Sua applicazione, garantendo che sia sempre aggiornata con le ultime modifiche al codice. Questo pipeline Le aiuterà a creare un'applicazione sicura, scalabile e full-stack in grado di gestire alti livelli di traffico.

## Configurazione del Repository GitHub
Questa sezione La guiderà attraverso il processo di configurazione di un repository GitHub che sarà la fonte per il Suo pipeline di CI/CD.

1. Crei un account GitHub.
2. Crei un nuovo repository dove risiederà il Suo progetto.
3. Carichi tutti i file del Suo progetto.

## Configurazione del Bucket S3
Questa sezione fornisce i passaggi per configurare un bucket Amazon S3. Questo bucket servirà come ambiente di distribuzione per la Sua applicazione.

1. Apra S3 in una scheda separata.
2. Clicchi su "Create Bucket".
3. Inserisca le seguenti informazioni: Nome del bucket="qualsiasi nome univoco a livello globale o MyFirstApp123456", Regione AWS="scelga quella più vicina al paese in cui lo utilizzerà o scelga US-East-1 come predefinito". **Nota**: Il nome del bucket deve essere univoco a livello globale tra tutti i nomi di bucket esistenti in Amazon S3.
4. In "Block public access (impostazioni del bucket)", deselezioni tutte le opzioni. **Nota**: Deselezionare queste opzioni renderà il Suo bucket accessibile pubblicamente. Assicurisi di volerlo fare.
5. Lasci le impostazioni predefinite e clicchi su "Create bucket".
6. In "Buckets", selezioni "Properties".
7. In "Static website hosting", clicchi su "Edit".
8. In "Static website hosting", selezioni "Enable".
9. In "Tipo di hosting", selezioni "Host static website".
10. In "Index", scriva "index.html".
11. Lasci le impostazioni predefinite e clicchi su "Save changes".
12. In "Buckets", selezioni "Permission".
13. In "Bucket Policy", clicchi su "Edit".
14. Inserisca la politica JSON fornita in questo progetto. Se non dispone della politica JSON, può trovarla [qui](https://github.com/r-ramos2/Pipeline-Automatizzato-di-CI-CD-con-Integrazione-di-GitHub-e-Amazon-S3-Italian/blob/main/s3_public_read_policy.json).
15. Sostituisca "arn:aws:s3:::Nome-del-bucket/*" con l'ARN del bucket nella parte superiore dello schermo. **Nota**: L'ARN del bucket è un identificatore univoco per il Suo bucket.
16. Clicchi su "Save changes".

## Configurazione di CodePipeline
Questa sezione è il cuore del Suo pipeline di CI/CD. La guiderà attraverso il processo di configurazione di un pipeline in AWS CodePipeline, che automatizza il processo di distribuzione dal Suo repository GitHub al Suo bucket Amazon S3.

1. Apra CodePipeline in una scheda separata.
2. Clicchi su "Create pipeline".
3. Inserisca le seguenti informazioni: Nome del pipeline="qualsiasi nome o MyPipeline123456", Tipo di pipeline="V1", Nome del ruolo="includa dettagli come il servizio AWS che sta utilizzando, la regione AWS e il nome del progetto originale". **Nota**: La definizione del tipo di pipeline V1 contiene i parametri standard di pipeline, fase e livello di azione. La definizione del tipo di pipeline V2 estende la definizione per aggiungere sezioni di configurazioni aggiuntive come trigger e variabili.
4. Selezioni la casella "Consente ad AWS CodePipeline di creare un ruolo di servizio in modo che possa essere utilizzato con questo nuovo servizio", quindi clicchi su "Next".
5. In "Provider di origine", selezioni "GitHub (Versione 2)".
6. In "Connessione", clicchi su "Connect to GitHub".
7. In "Crea connessione GitHub App", inserisca Nome connessione="qualsiasi nome o MyPipeline123456".
8. Clicchi su "Connect to GitHub", quindi clicchi su "Install a new app".
9. Nella schermata di GitHub, scorrere verso il basso fino a "Accesso al repository".
10. Selezioni il repository a cui desidera concedere l'accesso, quindi clicchi su "Save" e poi su "Connect".
11. In "Connessione", clicchi sulla connessione GitHub appena creata.
12. In "Nome repository", selezioni il bucket S3 corrispondente.
13. In "Trigger del pipeline", selezioni "Push in a branch".
14. In "Nome del branch", selezioni "main".
15. In "Formato dell'artifact di output", selezioni "Codice di pipeline predefinito", quindi clicchi su "Next".
16. In "Build - opzionale", scegli in base alle Sue necessità o "Salta la fase di build", quindi clicchi su "Next".
17. Inserisca le seguenti informazioni: Provider di distribuzione=Amazon S3, Regione=La Sua regione attuale, Bucket=Il Suo bucket S3, Chiave dell'oggetto S3=clicchi su "Estrai file prima del deploy", quindi clicchi su "Next" e infine su "Create pipeline".
18. Attendere che la schermata mostri segni verdi per Source e Deploy.

## Fase di Test
Questa sezione La guiderà attraverso il processo di test del Suo pipeline di CI/CD.

1. Apra S3 in una scheda separata.
2. In "Buckets", selezioni "Properties".
3. In "Static website hosting", clicchi sull'URL sotto "Endpoint del sito web del bucket".
4. Apri il repository GitHub con il Suo progetto, apporti una modifica e salvi.
5. Apri CodePipeline e verifica che la modifica sia rilevata.
6. Aggiorni l'URL sotto "Endpoint del sito web del bucket" e osservi la modifica.

## Pulizia
Per evitare costi inutili, verifichi che non ci siano risorse sottostanti ancora in esecuzione.

Ecco come può svuotare e terminare il CodePipeline:
1. Vada al pannello di controllo di CodePipeline.
2. Clicchi sul pipeline che desidera eliminare.
3. Clicchi sul pulsante "Delete" per eliminare il pipeline.

Ecco come può svuotare ed eliminare il bucket S3:
1. Vada al pannello di controllo di S3.
2. Clicchi sul bucket che desidera eliminare.
3. Clicchi sul pulsante "Empty" per eliminare tutti gli oggetti del bucket.
4. Una volta che il bucket è vuoto, clicchi sul pulsante "Delete" per eliminare il bucket.
**Nota**: Potrebbe essere necessario eliminare la policy del bucket prima di poter eliminare il bucket.

## Conclusione
In questo progetto, abbiamo dimostrato come distribuire un pipeline di Integrazione Continua/Distribuzione Continua (CI/CD) utilizzando GitHub e Amazon S3. Seguendo questi passaggi, abbiamo creato un pipeline CI/CD completamente funzionale che distribuisce un'applicazione in un bucket Amazon S3 ogni volta che ci sono modifiche pushate al repository GitHub. Non esiti a inviarci suggerimenti per migliorare il codice.

## Ringraziamenti
Questo tutorial è adattato dal [Tutorial: Create a pipeline that uses Amazon S3 as a deployment provider website](https://docs.aws.amazon.com/codepipeline/latest/userguide/tutorials-s3deploy.html) fornito da Amazon Web Services. Ringraziamo AWS per aver fornito questa preziosa risorsa, che ha servito come base per il tutorial "Pipeline Automatizzato di CI/CD con Integrazione di GitHub e Amazon S3".
