## VI. Processes
### Execute the app as one or more stateless processes

The app is executed in the execution environment as one or more *processes*.

In the simplest case, the code is a stand-alone script, the execution environment is a developer's local laptop with an installed language runtime, and the process is launched via the command line (for example, `python my_script.py`).  On the other end of the spectrum, a production deploy of a sophisticated app may use many [process types, instantiated into zero or more running processes](./concurrency).

**Twelve-factor processes are stateless and [share-nothing](http://en.wikipedia.org/wiki/Shared_nothing_architecture).**  Any data that needs to persist must be stored in a stateful [backing service](./backing-services), typically a database.

The memory space or filesystem of the process can be used as a brief, single-transaction cache.  For example, downloading a large file, operating on it, and storing the results of the operation in the database.  The twelve-factor app never assumes that anything cached in memory or on disk will be available on a future request or job -- with many processes of each type running, chances are high that a future request will be served by a different process.  Even when running only one process, a restart (triggered by code deploy, config change, or the execution environment relocating the process to a different physical location) will usually wipe out all local (e.g., memory and filesystem) state.

Asset packagers like [django-assetpackager](http://code.google.com/p/django-assetpackager/) use the filesystem as a cache for compiled assets.  A twelve-factor app prefers to do this compiling during the [build stage](/build-release-run). Asset packagers such as [Jammit](http://documentcloud.github.com/jammit/) and the [Rails asset pipeline](http://ryanbigg.com/guides/asset_pipeline.html) can be configured to package assets during the build stage.

Some web systems rely on ["sticky sessions"](http://en.wikipedia.org/wiki/Load_balancing_%28computing%29#Persistence) -- that is, caching user session data in memory of the app's process and expecting future requests from the same visitor to be routed to the same process.  Sticky sessions are a violation of twelve-factor and should never be used or relied upon.  Session state data is a good candidate for a datastore that offers time-expiration, such as [Memcached](http://memcached.org/) or [Redis](http://redis.io/).


## VI. Procesi
### Pokrenuti aplikaciju kao jedan ili više procesa koji ne čuvaju stanje

Aplikacija koja se izvršava u okruženju kao jedan ili više procesa.

U najednostavnijem slučaju, aplikacioni kod je nezavisna skripta, a okruženje u kome se izvršava aplikacija je laptop developera sa instaliranim programskim jezikom, a proces se pokreće preko komandne linije (na primer, `python my_script.py`). Sa druge strane, na produkciji izvršavanje aplikacije moze zahtevati [različite vrste procesa, pokrenitu kao više procesa](./concurrency).

**Prema pravilima 12faktora, procesi su bez stanja i [nezavisni](http://en.wikipedia.org/wiki/Shared_nothing_architecture).** Bilo koji podatak koje je potrebno sačuvati mora biti sačuvan u servisu koji čuva stanje [servis za podršku](./backing-services), najčesće u bazi podataka.

Memorijska lokacija ili fajl sistem procesa može biti iskoriščen kao privremeni, transkacioni keš. Na primer, preuzimanje velikog dokumenta, operacije nad tim velikim dokumentom, i čuvanje rezultata operacije u bazi podataka. Aplikacija po pravilima 12fakotra nikad ne podrazumeva da će, bilo šta što je keširano u memoriji ili na disku, ikada biti upotrebljeno za budući zahtev ili zadatak -- kako su obično uvek aktivni više različitih procesa, velike su šanse da će nove zahteve izvršavati različiti procesi. Čak iako se izvršava samo jedan proces, pri restartu sistema (pokrenut pri postavaljanju novog koda, promeni konfiguracije, ili okruženje je pomeilo proces na drugu fizičku lokaciju) celokupno lokalno stanje bi bilo izbrisano (memorija ili fajl sistem).

Alati za pakovanje datoteka koje koristi aplikacija [django-assetpackager](http://code.google.com/p/django-assetpackager/) koriste fajl sistem kao keš memoriju za kompajliranje datoteka. Aplikacija koja prati pravila 12fakotra preferira da se proces kompaliranja izvršava u [fazi generisanja paketa](/build-release-run). Alati za pakovanje kao što su [Jammit](http://documentcloud.github.com/jammit/) i [Rails asset pipeline](http://ryanbigg.com/guides/asset_pipeline.html) mogu biti konfigurisani da upakuju datoteketokom faze generisanja paketa.

Neki web sistemi se oslanjaju na ["lepljuvu sesiju"](http://en.wikipedia.org/wiki/Load_balancing_%28computing%29#Persistence) -- što znači da keširaju sesiju korisnika u aplikacionoj memoriji, i izvršavanje budučih zahteva od istok korsinika biće preusmereno na isti proces. Lepljive sesije krše pravila 12faktora i nikad se ne treba oslanjati. Podaci o sesiji su dobri primeri za korisščenje sisteme za čuvanje podataka koji nude opciju da podaci budu izbrisani posle definisanog vremena [Memcached](http://memcached.org/) ili [Redis](http://redis.io/).