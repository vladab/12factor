## XI. Logs
### Treat logs as event streams

*Logs* provide visibility into the behavior of a running app.  In server-based environments they are commonly written to a file on disk (a "logfile"); but this is only an output format.

Logs are the [stream](https://adam.herokuapp.com/past/2011/4/1/logs_are_streams_not_files/) of aggregated, time-ordered events collected from the output streams of all running processes and backing services.  Logs in their raw form are typically a text format with one event per line (though backtraces from exceptions may span multiple lines).  Logs have no fixed beginning or end, but flow continuously as long as the app is operating.

**A twelve-factor app never concerns itself with routing or storage of its output stream.**  It should not attempt to write to or manage logfiles.  Instead, each running process writes its event stream, unbuffered, to `stdout`.  During local development, the developer will view this stream in the foreground of their terminal to observe the app's behavior.

In staging or production deploys, each process' stream will be captured by the execution environment, collated together with all other streams from the app, and routed to one or more final destinations for viewing and long-term archival.  These archival destinations are not visible to or configurable by the app, and instead are completely managed by the execution environment.  Open-source log routers (such as [Logplex](https://github.com/heroku/logplex) and [Fluentd](https://github.com/fluent/fluentd)) are available for this purpose.

The event stream for an app can be routed to a file, or watched via realtime tail in a terminal.  Most significantly, the stream can be sent to a log indexing and analysis system such as [Splunk](http://www.splunk.com/), or a general-purpose data warehousing system such as [Hadoop/Hive](http://hive.apache.org/).  These systems allow for great power and flexibility for introspecting an app's behavior over time, including:

* Finding specific events in the past.
* Large-scale graphing of trends (such as requests per minute).
* Active alerting according to user-defined heuristics (such as an alert when the quantity of errors per minute exceeds a certain threshold).


## XI. Logovi
### Tretirajte logove kao tok događaja

*Logovi* pružaju uvid u ponašanje pokrenute aplikacije. U serverskim okruženjima, oni su obično zapisani u dokumentu na fajl sistemu (datoteka *logfile*); međutim, ovo je samo format snimanja.

Logovi su lista agregiranini, vremenski tok [događaja](https://adam.herokuapp.com/past/2011/4/1/logs_are_streams_not_files/) prikupljeni iz različitih pokrenutih procesa i servisa za podršku. Logovi u svom originalnom obliku obično se pojavljuju u tekstualnom formatu, pri čemu jedan događaj uzima jednu linuju u fajlu (mada prilikom bacanja izuzetka, tačke pozivanja mogu da se nalaze u viće linija). Logovi nemaju određeni početak ili kraj, već stalno se nadovezuju novi događaji tokom rada aplikacije.

**Aplikacija koja prati prinicipe 12 faktora nije odgovorna za preusmeravanja i čuvanje svog izlaznog toka.** Ne bi trebalo da čuva ili upravlja log datotekama. Umesto toga, svaki pokrenuti proces unosi svoj ne beferisan tok događaja na `stdout`. Dok radi u lokalnom orkuženju, programer može pratiti ponašanje aplikacije tako što će pregledati tok u prozoru terminala.

U stejdžing ili produkcionom okruženju, svaki izlaz procesa biće snimljen u okruženju u kome se izvršava, prikupljen zajedno sa ostalim izlaznim tokavima aplikacije, da bi se zatim ti agregirani događaji preusmerili na jednu ili viče destinacija gde se mogu pregledati ili arhivirati. Ove destinacije na kojima se arhiviraju logovi nisu vidljivi ili se mogu konfigurisati u palikaciji, vec se kompletno upravljaju unutar okriženja u kome se izvršavaju. Za ovu svrhu možete koristiti softver otvorenog koda kao što su [Logplex](https://github.com/heroku/logplex) i [Fluentd](https://github.com/fluent/fluentd).

Tok događaja aplikacije mogu se usmeriti ka datoteci, ili se pregledati u realnom vremenu u terminalu pregledavanjem repa toka dogažaja. Najznačajnije je da se tok dogažaja može poslati na sistem za indeksitranje kao čto je [Splunk](http://www.splunk.com/), ili sistem za skladištenje velike količine podataka kao što je [Hadoop/Hive](http://hive.apache.org/). Ovi sistemi omogučavaju veliku snagu i fleksibilnost za introspektivno ponašanje aplikacije tokom vremena, uključujući:

* Pretraživanje određenih događaja u prošlosti,
* Vizualizacija statističkih podataka o trendovima (npr. upiti u minuti).
* Aktivno slanje obaveštenja na osnovu unapred definisane heuristike (npr. kada broj grešaka prevazilazi dozvoljenu vrednost).
