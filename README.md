# Create: Raw 1.0.0

Addon per Minecraft 1.21.1, NeoForge 21.1.250 e Create 6.0.10. Richiede Java 21.

Il Rawer inverte le ricette della fornace caricate dal mondo, incluse quelle delle altre mod con ingredienti grezzi rappresentabili e validi. Gli esempi grafici dei tag vuoti o di ingredienti personalizzati non validi sono esclusi. La velocità minima predefinita è 128 RPM; sotto questa soglia rifiuta nuovi ingressi, conserva eventuali oggetti già caricati e sospende la lavorazione, la ventola e il nastro interno. Gli alberi seguono la rete cinetica. A 128 RPM consuma 1024 SU e lavora un oggetto ogni 60 tick (3 secondi). La velocità aumenta gli oggetti del lotto, non riduce la durata del ciclo; il limite configurabile è 16. Con il limite standard di Create di 256 RPM il lotto è di due oggetti.

## Crafting

Il Rawer si ottiene con 25 Mechanical Crafters disposti 5×5. Schema:

```text
CCCCC
CAIAC
SIKIS
CAIAC
CCCCC
```

C = Andesite Casing (14); A = Andesite Alloy (4); I = Industrial Iron Block (4); S = Shaft (2); K = Clock (1). Risultato: 1 Rawer. Non è una ricetta del banco da lavoro normale. Ricetta caricata e verificata contro la griglia meccanica nativa Create: corrispondenza, risultato e rifiuto dell’ingrediente errato.

## Utilizzo e integrazioni

- Piazzamento: se trova un nastro adiacente già in movimento (anche un blocco più basso), sceglie ingresso/uscita seguendo il suo percorso e mantiene l’asse compatibile con la fonte cinetica. Se i nastri danno indicazioni contrastanti o sono fermi, usa l’orientamento del giocatore; la chiave permette di correggerlo. Invertendo gli RPM si scambiano ingresso e uscita orizzontali, anche su una macchina già piazzata. Nastri interni, ventola e percorso degli oggetti invertono il verso; un oggetto già in lavorazione prosegue dalla posizione corrente verso la nuova uscita. Da fermo mantiene l’ultimo verso, anche dopo il salvataggio. Ingresso dall’alto e uscita tramite chute sotto restano disponibili nei rispettivi ruoli.
- Due prese per gli alberi, trasversali alla linea ingresso/uscita; quattro orientamenti orizzontali e rotazione con la chiave Create. Il flusso segue la convenzione dei nastri Create per asse e RPM, indipendentemente dal lato scelto al piazzamento.
- Ingresso dalla faccia indicata dal modello o dall’alto: nastri, funnel, hopper/chute, Mechanical Arm e oggetti gettati sulla macchina. È consentito solo quando la velocità raggiunge la soglia configurata (128 RPM predefiniti), anche nel verso negativo. Accetta un solo lotto per volta (normalmente 1 oggetto a 128 RPM, 2 a 256 RPM). Gli oggetti successivi restano fuori mentre il lotto è pronto, in lavorazione o l’output è bloccato. Se una ricetta richiede più oggetti cotti per ottenere un ingrediente grezzo, consente di completare quella quantità prima di chiudere l’ingresso.
- Nastri un blocco più in basso: ingresso dal lato corretto o sotto il Rawer; gli oggetti in attesa restano sul nastro e riprendono il percorso quando la macchina viene rimossa. Supportata anche l’uscita verso un nastro più basso in movimento. Gli oggetti senza ricette inverse di smelting vengono rifiutati da tutti gli ingressi automatici.
- Uscita dalla faccia opposta o dal basso: funnel, nastri, inventari e Mechanical Arm. In assenza di un ricevitore o ostacolo espelle gli oggetti; se un ricevitore è pieno o l’uscita è bloccata conserva l’output e attende.
- Chute o Smart Chute direttamente sotto il Rawer: hanno priorità sull’espulsione laterale e prelevano dall’uscita tramite Create. Con uno scivolo pieno, bloccato o con filtro incompatibile l’output resta nella macchina. Uno Smart Chute con quantità esatta può accumulare risultati compatibili da più lotti, mantenendo un solo lotto in lavorazione, fino alla quantità richiesta e al limite dello stack.
- Filtro Create sopra/sotto. Senza filtro sorteggia il materiale grezzo per ogni oggetto. Un filtro sceglie tra i risultati compatibili; se non esistono risultati compatibili l’ingresso lavorato viene scartato.
- Mano vuota per recuperare tutti gli oggetti conservati. La rottura recupera inventario, output in attesa e il Filter dedicato una sola volta.
- Engineer’s Goggles, stress di rete, comparatori, Threshold Switch, Display Link (stato, quantità, RPM e stress) e categorie Ponder Create.
- Tooltip Create con stress cinetico, dettagli tramite Shift e RPM minimi nella palette marrone/oro. Con il valore predefinito di 8 SU/RPM il livello nativo è High; a 128 RPM il consumo totale è 1024 SU.
- JEI opzionale: categoria delle ricette inverse, Rawer come catalizzatore e possibili risultati alternati in un singolo slot; quantità e componenti rispettati. L’integrazione legge le ricette del mondo, incluse le altre mod. Installare JEI separatamente: non è contenuto nel JAR Rawer né obbligatorio. In sviluppo usare `./gradlew -PwithJei=true runClient` (JEI 19.21.0.247).
- Tre scene Ponder tradotte in inglese e italiano, con base bianca nello stile Create, Rawer alla stessa altezza dei nastri, come nella beta 1.0.4, oggetti in attesa durante il ciclo, anteprima coerente con il risultato e progresso animato ogni tick.

La texture del nastro scorre verso l’uscita; il bordo d’ingresso risale verso il piano e quello d’uscita scende, coerentemente con il percorso dell’oggetto, in entrambi i renderer e nei quattro orientamenti. Ventola e nastro condividono una fase continua: cambiare RPM o fermarsi non riporta l’animazione a un angolo precedente.

Le ricette inverse che richiedono più oggetti di quanti possano entrare nello slot (64 o il limite dell’item) vengono escluse dall’ingresso e da JEI. La selezione casuale e il progresso vengono salvati; quantità e componenti delle ricette sono rispettati. Un reload invalida le ricette memorizzate. La configurazione del server relativa alla lavorazione viene sincronizzata nel block entity per la visualizzazione client.

## Configurazione

Il pulsante Config della mod apre l’interfaccia nativa Create/Catnip: sfondo, ingranaggio, pulsanti ed editor dei valori. Common Config → Rawer contiene stress per RPM, RPM minimi, durata del processo e massimo lotto e tag bloccati in ingresso. Le categorie Client e Server sono disabilitate perché non contengono impostazioni della mod. Il file resta `config/createraw-common.toml`. Su server dedicati va modificato il file del server; l’editor del client modifica solo il file locale. Il salvataggio aggiorna la rete cinetica e i dati visualizzati dal client, anche quando la macchina è ferma.

### Esclusioni per tag

`blockedInputTags = "c:nuggets"` rifiuta le pepite esclusivamente in ingresso, anche quando altre mod aggiungono ricette di smelting che producono pepite. L’output può ancora essere una pepita. Aggiungere altri tag per escludere intere categorie dal Rawer, per esempio `"c:nuggets,c:ingots"`; usare `""` per disabilitare le esclusioni. Accetta identificatori `namespace:path`, senza `#`. Si modifica da Common Config → Rawer nel campo testo nativo Create (tag separati da virgole). Il campo conserva anche elenchi oltre 32 caratteri. Gli identificatori incompleti o invalidi appaiono in rosso e non vengono accodati per il salvataggio; resta valido l’ultimo testo corretto. Reset e annullamento aggiornano anche il testo visibile. Le modifiche si applicano ai Rawer già piazzati. Gli input diventati vietati già presenti nella macchina restano recuperabili a mano; non vengono distrutti. Le ricette della fornace e degli altri blocchi non vengono eliminate. JEI applica le esclusioni del server ricevute al collegamento e ai reload, aggiornando le ricette nascoste senza duplicarle. Anche RPM minimi, stress e valori dimostrativi del Ponder ricevono i valori del server; questi non sostituiscono la configurazione locale del server integrato. Su server dedicato modificare la lista sul server.

## Aggiornamento da versioni precedenti

Le configurazioni esistenti mantengono il valore salvato: impostare `stressImpactPerRPM = 8.0` in `config/createraw-common.toml` oppure aprire il menu configurazione della mod → Common Config → Rawer e salvare il valore 8.0. Le modifiche aggiornano anche i Rawer già collegati senza riavvio. Non cancellare la configurazione: le altre preferenze possono restare invariate. Le nuove installazioni usano automaticamente 8 SU/RPM.

## Build e verifiche

Con JAVA_HOME impostato a Java 21:

```sh
./gradlew build
./gradlew test runGameTestServer
./gradlew runClient
```

Il JAR installabile è in `build/libs/createraw-1.0.0.jar`. Non installare il JAR `-sources`. Il mod `createraw_tests` è solo di sviluppo ed è escluso dal JAR della mod e dall’avvio client/server normale. La prima build scarica le dipendenze; `--offline` funziona solo con una cache completa.

Verifica del 3 ottobre 2026: 64 GameTest sul server NeoForge/Create reale e 14 test JUnit di rotazione e continuità delle animazioni passati; build completata. Controllati JSON, traduzioni, placeholder e chiavi Ponder. Il client 1.0.0 ha caricato Create, JEI (62 gruppi ricette Rawer) e un mondo di prova; la verifica visiva delle scene Ponder, delle animazioni e del nuovo menu config resta da effettuare in gioco. Questi test non certificano ogni modpack o ogni combinazione di automazione Create.

Owner: notzessentialz. Developer: Pigiazza. [Modrinth](https://modrinth.com/mod/createraw), [CurseForge](https://www.curseforge.com/minecraft/mc-mods/create-raw/preview), [GitHub](https://github.com/NotA-Essential-Z/Create-Raw).

Mod distribuita con licenza MIT, inclusa nel JAR e nei sorgenti. Le dipendenze mantengono le proprie licenze.
