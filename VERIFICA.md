# Verifiche Create: Raw 1.0.0

Minecraft 1.21.1, NeoForge 21.1.250, Create 6.0.10 e Java 21.

Build completata; 64 GameTest sul server e 14 test JUnit superati. Avvio client con Create, JEI e mondo di prova riuscito.

Il confronto diretto con BeltBlockEntity verifica tutti e quattro gli orientamenti con RPM positivi e negativi, le capability e il segno delle animazioni. I nastri in movimento e il Rawer ricevono gli stessi RPM nei test di alimentazione. Girare il modello di 180° non cambia il flusso a parità di alimentazione.

Verificati inversione del motore, orientamenti, integrazioni con nastri e inventari, recupero dei contenuti, ricette, componenti, tag di esclusione, configurazione, sincronizzazione e continuità delle animazioni.

La verifica visiva delle animazioni, delle scene Ponder e del menu config resta da effettuare in gioco. Non sono certificate tutte le combinazioni di modpack o shader esterni.

Durata predefinita del ciclo ridotta a 60 tick (3 secondi).

Lo ZIP sorgente è stato estratto e ricompilato separatamente con configurazione nuova: durata predefinita 60 tick, 64 GameTest e 14 JUnit superati. Il JAR ricompilato è identico per ogni contenuto a quello distribuito.
