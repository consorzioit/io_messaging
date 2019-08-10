# Codice Perl per IO (io.italia.it)

## Sommario

- [IO](#IO)
- [Documentazione](#Documentazione)
- [Migliorie](#Migliorie)
- [Contributi](#Contributi)
- [Autori](#Autori)
- [Licenza](#licenza)

## IO

Il codice presente nel repository è stato utilizzato nella closed beta di [IO](https://io.italia.it) che ha visto 
coinvolto il comune di [Ripalta Cremasca](https://www.comune.ripaltacremasca.cr.it),
con partner tecnologico [ConsorzioIT](https://www.consorzioit.net).

Lo scopo della partecipazione alla closed beta, come ConsorzioIT, era quello di capire
il funzionamento di IO, l'app per smartphone che vuole cambiare il paradigma con 
cui cittadino e PA comunicano, da PA centrico a cittadino centrico.

Tutte le informazioni per sviluppatori su IO si possono trovare al link
[IO Sviluppatori](https://io.italia.it/sviluppatori/), incluso i sorgenti dell'app.

Come PA, ovvero comune di Ripalta Cremasca, lo scopo era iniziare a erogare servizi
tramite IO, in particolare: pagamento TARI, MENSA, Minigrest e [CIE](https://www.ipzs.it/ext/carta_identita_elettronica_prodotti.html),
inviando messaggi ai cittadini tramite l'app IO. Inoltre e' possibile
inviare un messaggio di Benvenuto dall'amministrazione comunale, quando
un cittadino attiva IO.

## Documentazione

Il codice è scritto in perl.

Il codice mira a essere molto snello e con pochi fronzoli, non è ottimizzato
se non per lo scopo per cui è nato: riuscire ad interfacciarsi mandando messaggi tramite IO
che contengano pagamenti (MENSA,TARI,CIE,MiniGrest) o messaggi informativi (BENVENUTO).

esempi di utilizzo

**perl IO_Messaging.pl codice_fiscale importo numero_avviso servizio**
  
* codice_fiscale: si spiega da solo, necessario per comunicare a IO chi è la persona da contattare
* importo: valore in euro (viene moltiplicato per 100 nel codice, IO accetta solo interi)
* numero_avviso: numero avviso del bollettino [pagoPA](https://www.agid.gov.it/it/piattaforme/pagopa)
* servizio: un servizio tra CIE | MENSA | TARI | MINIGREST | BENVENUTO 

esempi di comandi

* perl IO_Messaging.pl TRNNDR99B21G158X 0 0 BENVENUTO 
* perl IO_Messaging.pl TRNNDR99B21G158X 20 123456789012345678 CIE
* perl IO_Messaging.pl TRNNDR99B21G158X 50 123456789012345678 MENSA
* perl IO_Messaging.pl TRNNDR99B21G158X 60 123456789012345678 MINIGREST
* perl IO_Messaging.pl TRNNDR99B21G158X 150 123456789012345678 TARI 

Nota: per la TARI lo script invia un pagamento come per gli altri servizi. Essendo 
la TARI più complessa è stato fatto uno script a parte che fa parsing sia
dei codici avviso associati alle pratiche tari (rata singola più rate divise)
per un dato codice fiscale inviando 2 messaggi appunto con rata singola
e più rate. Inoltre un altro script fa parsing del dettaglio immobili e invia
un terzo messaggio con i dettagli degli immobili. In caso si sia interessati
anche a questi script aprire una issue con la richiesta.

Nota: lo script non prevede l'invio del promemoria nel messaggio, messo tra
commenti nella %req. Il promemoria permette di mettere a calendario 5 giorni
prima della scadenza un memo per il pagamento.
  
## Migliorie

Di codice:
- verificare i parametri di input (lunghezza codice fiscale, valore numerico dove necessario, controllare che il servizio sia nell'elenco di quelli supportati)
- salvare il logging degli errori su file invece che su standard output

Di riusabilità:
- i parametri per accedere alle api potrebbero essere spostati in un file di configurazione esterno
- i messaggi inviati ai cittadini ppotrebbero essere a loro volta generalizzati/parametrizzati e spostati sempre nel file di configurazione
- in generale le righe dei messaggi potrebbero essere compattate in una decina visto che la struttura è la medesima, ma cambiano i contenuti

Grazie a [Marco Tironi](https://www.linkedin.com/in/marco-tironi-77406958/) per i consigli sulle migliorie.

## Contributi
Chiunque può inviare Pull Requests e/o file Issues.

## Autori
Il codice è stato sviluppato da [Andrea Tironi](https://www.linkedin.com/in/andrea-tironi-381b6a52/).

## Licenza
Il codice e' licenziato secondo licenza [CC-0](https://creativecommons.org/choose/zero/?lang=it).




