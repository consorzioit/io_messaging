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
il funzionamento di IO, l'applicazione che vuole cambiare il paradigma con 
cui cittadino e PA comunicano, da PA centrino a cittadino centrino.

Tutte le informazioni su IO per sviluppatori si possono trovare al link
[IO Sviluppatori](https://io.italia.it/sviluppatori/) incluso i sorgenti.

Come PA, ovvero comune di Ripalta Cremasca, lo scopo era iniziare a erogare servizi
tramite IO, in particolare: pagamento TARI, MENSA, Minigrest e [CIE](https://www.ipzs.it/ext/carta_identita_elettronica_prodotti.html).

## Documentazione

Il codice è scritto in perl.

Il codice scritto mira a essere molto snello e con pochi fronzoli, non è ottimizzato
se non per lo scopo per cui è nato: riuscire ad interfacciarsi ad mandando messaggi 
che contengano pagamenti (MENSA,TARI,CIE,MiniGrest) o messaggi informativi (BENVENUTO).

esempi di utilizzo

**perl io_servizi_gh.pl codice_fiscale importo numero_avviso servizio**
  
* codice_fiscale: si spiega da solo, necessario per comunicare a IO chi è la persona da contattare
* importo: valore in euro (viene moltiplicato per 100 nel codice, IO accetta solo interi)
* numero_avviso: numero bollettino [pagoPA](https://www.agid.gov.it/it/piattaforme/pagopa)
* servizio: un servizio tra CIE | MENSA | TARI | MINIGREST | BENVENUTO

esempi di comandi

* perl io_servizi_gh.pl TRNNDR99B21G158X 0 0 BENVENUTO 
* perl io_servizi_gh.pl TRNNDR99B21G158X 20 123456789012345678 CIE
* perl io_servizi_gh.pl TRNNDR99B21G158X 50 123456789012345678 MENSA
* perl io_servizi_gh.pl TRNNDR99B21G158X 60 123456789012345678 MINIGREST
* perl io_servizi_gh.pl TRNNDR99B21G158X 150 123456789012345678 TARI 

Nota: per la TARI lo script invia un pagamento come per gli altri servizi. Essendo 
la TARI più complessa è stato fatto uno script a parte che fa parsing sia
dei codici avviso associate alle pratiche tari (rata singola più rate divise)
per un dato codice fiscale inviando 2 messaggi appunto con rata singola
e più rate. Inoltre un altro script fa parsing del dettaglio immobili e invia
un terzo messaggio con i dettagli degli immobili.
  
## Migliorie

Di codice:
- verificare i parametri di input (lunghezza codice fiscale, valore numerico dove necessario, controllare che il servizio sia nell'elenco di quelli supportati)
- salvare il logging degli errori su file invece che su standard output

Di riusabilità:
- i parametri per accedere alle api potrebbero essere spostati in un file di configurazione esterno
- i messaggi inviati ai cittadini ppotrebbero essere a loro volta generalizzati/parametrizzati e spostati sempre nel file di configurazione
- in generale le righe dei messaggi potrebbero essere compattate in una decina visto che la struttura è la medesima, ma cambiano i contenuti

## Contributi
Chiunque può inviare Pull Requests e/o file Issues.

## Autori
Il codice indicato è stato sviluppato da (Andrea Tironi)[https://www.linkedin.com/in/andrea-tironi-381b6a52/].

## Licenza
Ilcodice e' licenziato secondo licenza (CC-0)[https://creativecommons.org/choose/zero/?lang=it].




