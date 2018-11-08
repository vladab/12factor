## VII. Port binding
### Export services via port binding

Web apps are sometimes executed inside a webserver container.  For example, PHP apps might run as a module inside [Apache HTTPD](http://httpd.apache.org/), or Java apps might run inside [Tomcat](http://tomcat.apache.org/).

**The twelve-factor app is completely self-contained** and does not rely on runtime injection of a webserver into the execution environment to create a web-facing service.  The web app **exports HTTP as a service by binding to a port**, and listening to requests coming in on that port.

In a local development environment, the developer visits a service URL like `http://localhost:5000/` to access the service exported by their app.  In deployment, a routing layer handles routing requests from a public-facing hostname to the port-bound web processes.

This is typically implemented by using [dependency declaration](./dependencies) to add a webserver library to the app, such as [Tornado](http://www.tornadoweb.org/) for Python, [Thin](http://code.macournoyer.com/thin/) for Ruby, or [Jetty](http://www.eclipse.org/jetty/) for Java and other JVM-based languages.  This happens entirely in *user space*, that is, within the app's code.  The contract with the execution environment is binding to a port to serve requests.

HTTP is not the only service that can be exported by port binding.  Nearly any kind of server software can be run via a process binding to a port and awaiting incoming requests.  Examples include [ejabberd](http://www.ejabberd.im/) (speaking [XMPP](http://xmpp.org/)), and [Redis](http://redis.io/) (speaking the [Redis protocol](http://redis.io/topics/protocol)).

Note also that the port-binding approach means that one app can become the [backing service](./backing-services) for another app, by providing the URL to the backing app as a resource handle in the [config](./config) for the consuming app.


## VII. Dodeljivanje portova
### Omogucite pristup servisima dodeljivanjem portova

Web al=plikacije se ponekad izvrsavaju unutar kontejnera sa webserverom. Na primer, PHP aplikacije mogu poekad da se izvršavaju kao modul unutar [Apache HTTPD](http://httpd.apache.org/), ili Java aplikacije mogu da se pokrecu unutar [Tomcat](http://tomcat.apache.org/).

**Aplikacija koja prati princip 12 faktora nema eksterne zavisnosti** što je čini nezavisnom od drugih modula na serveru. Web aplikacija **obezbeđuje pristup HTTP servisu dodeljivanjem jedinstvenog porta**, i prati sve dolazeće zahteve na tom portu.

U lokalnoj development okruženju, da bi koristio uslugu koju pruža aplikacija, programer može otvoriti URL adresu kao što je `http://localhost:5000/`. A za aplikacije koje se izvršavaju u produkcionom okruženju, svim zahtevima upravlja navigacioni sloj koji prosležuje te zahteve servisu na dodeljenom portu.

Ovo je tipično implementirano koriščenjem [deklarisanjem eksternih zavisnosti](./dependencies) da bi se aplikaciji dodala biblioteka za webservis, kao što je [Tornado](http://www.tornadoweb.org/) za Python, [Thin](http://code.macournoyer.com/thin/) za Ruby, ili [Jetty](http://www.eclipse.org/jetty/) za Javu ili druge jezike bazirane na JVM.

HTTP nije jedini servis koje se može eksportovati dodljeivanjem portova. Skoro svaka vrsta serverskog softwera može se pokrenuti dodeljivanjem portova na kojem se proces pokreće i čeka dolazeće upite. Primeri uključuju [ejabberd](http://www.ejabberd.im/) (komuniciranje putem [XMPP](http://xmpp.org/)), i [Redis](http://redis.io/) (komuniciranje kroz [Redis protokol](http://redis.io/topics/protocol)).

Važno je napomenuti i to da dodeljivanjem portova aplikacija može da se izvršava i kao [servis za podršku](./backing-services) za drugu aplikaciju, tako što će omogućiti URL servisu za podršku kao resurs koji se postavlja u [kongiguraciji](./config) te aplikacije.