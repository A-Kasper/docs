BGP Konzentrator einrichten
---------------------------

Der BGP Konzentrator ist der Backboneseitige unserer zwei Freifunk Server, er übernimmt Routing, NAT, Connection tracking, GRE Tunnel und BGP Sessions.

Für den Vserver benötigen wir eine zusätzliche öffentliche IPv4 Adresse, diese könnt ihr beim Rechenzentrum kaufen, nennt sich z.B. Failover IP. Für diese IP Adresse muss im Kundeninterface eine MAC Adresse erstellt werden, die dann im Proxmox auf der Netzwerkkarte des Vservers konfiguriert wird.

Nachdem der Server neu gestartet ist und das Webinterface wieder erreichbar ist auf der linken Seite den Server auswählen und dann oben rechts 'Create VM'

.. image:: http://freifunk-mk.de/gfx/proxmox-6.png
----

Im Reiter 'General' eine Freie ID und einen Namen festlegen.

.. image:: http://freifunk-mk.de/gfx/proxmox-7.png
----

Im Reiter 'OS' 'Linux 4.x/3.x/2.6 Kernel auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-8.png
----

Im Reiter 'CD/DVD' das ISO Image auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-9.png
----

Im Reiter 'Hard Disk' als 'Bus' 'VirtIO' einstellen, die Festplattengröße auf 8GB begrenzen und als Format 'qcow2' wählen. Größere Festplatten machen Backups, Rollbacks und co nur aufwändiger. Kleiner als 8GB geht auch, z.b. 6GB wesentlich weniger dann aber nicht mehr.

.. image:: http://freifunk-mk.de/gfx/proxmox-10.png
----

Im Reiter 'CPU' zwei Prozessorkerne zuweisen. Einer tut es in der Regel auch, wichtig ist, dass wir nur eine CPU / Socket zuweisen, sonst verschluckt sich das System. Als CPU kann man host wählen, das tut der Performance gut und HA nutzen wir ohnehin nicht.

.. image:: http://freifunk-mk.de/gfx/proxmox-11.png
----

Im Reiter 'Memory' unter 'Automatically allocate memory within this range' 256 -1024MB festlegen. Weniger als 256 hindert einige Maschinen beim booten, mehr als 1024 werden nicht benötigt.

.. image:: http://freifunk-mk.de/gfx/proxmox-12.png
----

Im Reiter 'Network' als Netzwerkkarte 'VirtIO' auswählen und die MAC Adresse der für diesen Vserver zu verwendenden öffentlichen IPv4 Adresse eintragen. Bridged Mode übernehmen wir so und solange vmbr0 unsere wan bridge ist auch.

.. image:: http://freifunk-mk.de/gfx/proxmox-13.png
----

Bestätigen und Anlegen, auswählen und anschließend starten.

.. image:: http://freifunk-mk.de/gfx/proxmox-14.png

.. image:: http://freifunk-mk.de/gfx/proxmox-15.png
----

Fehlermeldungen während der Startphase werden unten im Log-Fenster angezeigt, erscheinen immer "oben", jedoch mit einigen Sekunden verzögerung. Details lassen sich ausklappen. Auf einigen Systemen ist es notwendig, die Harddisk auf "Writeback(insecure)" zu schalten, um das System zu starten zu können.

Hinweis: Wenn das System später läuft, nicht vergessen, den Starttyp "at boot time" zu stellen.

.. image:: http://freifunk-mk.de/gfx/proxmox-16.png
----
Und nach installation das Iso aus dem lauffwerk nehmen, denn wenn die Datei irgendwann mal vom Storage gelöscht werden booten die Maschinen mangels iso nicht mehr.

Ubuntu Server Installieren
^^^^^^^^^^^^^^^^^^^^^^^^^^

Die VM Links auswählen und oben rechts starten und die Konsole öffnen

.. image:: http://freifunk-mk.de/gfx/proxmox-17.png
----

Deutsch als Sprache auswählen und nun Ubuntu Server Installieren

.. image:: http://freifunk-mk.de/gfx/proxmox-18.png

.. image:: http://freifunk-mk.de/gfx/proxmox-19.png
----

Als Installationssprache jetzt nochmal Deutsch auswählen, die Auswahl trotz unvollständiger Unterstützung bestätigen und als nächstes das Tastaturlayout auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-20.png

.. image:: http://freifunk-mk.de/gfx/proxmox-21.png

.. image:: http://freifunk-mk.de/gfx/proxmox-22.png

.. image:: http://freifunk-mk.de/gfx/proxmox-23.png

.. image:: http://freifunk-mk.de/gfx/proxmox-24.png

.. image:: http://freifunk-mk.de/gfx/proxmox-25.png
----

Sobald der Server versucht das Netzwerk automatisch zu konfigurieren, dies abbrechen und die Manuelle Netzwerkkonfiguration auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-26.png

.. image:: http://freifunk-mk.de/gfx/proxmox-27.png

.. image:: http://freifunk-mk.de/gfx/proxmox-28.png
----

Die IP zur mac ist beispielsweise die 555.666.777.888

.. image:: http://freifunk-mk.de/gfx/proxmox-29.png
----

Die subnetzmaske von 255.255.255.0 bleibt in der Regel so

.. image:: http://freifunk-mk.de/gfx/proxmox-30.png
----

Die Gateway Adresse sollte man beim Rechenzentrum bekannt sein.

Bei einem großen Französichen RZ (OVH/Soyoustart) ist das IPv4 Gateway immer auf der 254, also 555.666.777.254

.. image:: http://freifunk-mk.de/gfx/proxmox-31.png
----

Als DNS geht z.B. der 8.8.8.8 von google.

.. image:: http://freifunk-mk.de/gfx/proxmox-32.png
----

Der Rechnername ist frei wählbar

.. image:: http://freifunk-mk.de/gfx/proxmox-33.png
----

Der Domainname ist hier einzutragen

.. image:: http://freifunk-mk.de/gfx/proxmox-34.png
----

Und der Benutzername.

.. image:: http://freifunk-mk.de/gfx/proxmox-35.png

.. image:: http://freifunk-mk.de/gfx/proxmox-36.png
----

Das Kennwort sollte sicher sein und nicht bereits für einen anderen Zweck in Verwendung.

.. image:: http://freifunk-mk.de/gfx/proxmox-37.png
----

Da auf dem Server keine Persönlichen Dateien gespeichert werden sollen ist es nicht notwendig den Persönlichen Ordner zu verschlüsseln.

.. image:: http://freifunk-mk.de/gfx/proxmox-38.png
----

Zeitzone Prüfen und bestätigen.

Festplatte manuell formatieren

.. image:: http://freifunk-mk.de/gfx/proxmox-39.png
----

Freien speicherplatz auswählen und enter

.. image:: http://freifunk-mk.de/gfx/proxmox-40.png
----

Partitionstabelle erstellen

.. image:: http://freifunk-mk.de/gfx/proxmox-41.png
----

Freien speicherplatz auswählen und enter

.. image:: http://freifunk-mk.de/gfx/proxmox-42.png
.. image:: http://freifunk-mk.de/gfx/proxmox-43.png
----

Partitionsgröße 7 GB Primär am Anfang

.. image:: http://freifunk-mk.de/gfx/proxmox-44.png
.. image:: http://freifunk-mk.de/gfx/proxmox-45.png
.. image:: http://freifunk-mk.de/gfx/proxmox-46.png
----

Bootflag auf 'ein' setzen und 'Anlegen beenden'

.. image:: http://freifunk-mk.de/gfx/proxmox-47.png
----

Freien Speicherplatz auswählen und enter

.. image:: http://freifunk-mk.de/gfx/proxmox-48.png
----

Einen neue Partition erstellen

.. image:: http://freifunk-mk.de/gfx/proxmox-49.png
----

Größe bestätigen

.. image:: http://freifunk-mk.de/gfx/proxmox-50.png
----

Primär

.. image:: http://freifunk-mk.de/gfx/proxmox-45.png
----

Benutzen als 'Auslagerungsspeicher (SWAP)'

'Anlegen beenden'

.. image:: http://freifunk-mk.de/gfx/proxmox-51.png
----

'Partitionierung beenden'

.. image:: http://freifunk-mk.de/gfx/proxmox-52.png
----

Ja schreiben, noch sind ja keine Daten vorhanden, die überschrieben werden könnten.

.. image:: http://freifunk-mk.de/gfx/proxmox-53.png
----

Warten...

Proxy leer lassen

.. image:: http://freifunk-mk.de/gfx/proxmox-54.png
----

Warten...

Automatische Sicherheitsaktualisierungen auswählen

.. image:: http://freifunk-mk.de/gfx/proxmox-55.png
----

Openssh server auswählen (Leertaste benutzen) und weiter

.. image:: http://freifunk-mk.de/gfx/proxmox-56.png
----

Warten...

Die Installation des GRUB Bootloader bestätigen

.. image:: http://freifunk-mk.de/gfx/proxmox-57.png
----

Weiter

.. image:: http://freifunk-mk.de/gfx/proxmox-58.png
----

SSH
^^^

Die weitere Konfiguration soll per SSH Zugriff erfolgen, daher richten wir diesen zuerst ein und sichern den SSH Server ab.

vom PC aus per SSH mit dem Server verbinden

::

	ssh root@555.666.777.888

Nun den SSH Public Key auf dem Server hinterlegen

::

	mkdir .ssh
	cd .ssh
	nano authorized_keys

In die noch leere Datei den Key eintragen und den Editor wieder verlassen.

Als nächstes die SSH Verbindung beenden

::

	exit

Und unter Verwendung des SSH Keys erneut verbinden

::

	ssh root@555.666.777.888

Wenn der Key nicht als default im System hinterlegt ist muss zusätzlich der Pfad zum Key angeben werden.

Liegt der Key meinsshkey im Benutzerordner

::

	ssh -i ~/meinsshkey root@555.666.777.888

Nun den Password login auf dem Server deaktivieren, dazu die sshd_config editieren

::

	sudo nano /etc/ssh/sshd_config

Die Zeile

::

	#PasswordAuthentication yes

ändern in

::

	PasswordAuthentication no
	UsePAM no

Achtung, auch wenn yes auskommentiert ist besteht die Möglichkeit sich per Password zu verbinden, erst wenn no gesetzt ist und nicht auskommentiert ist, ist der Zugriff nur noch per Key möglich.

Um es den Script-Kiddies und Bots etwas schwerer zu machen, sollte der Port 22 auf einen hohen Port (mindestens über 1024) verändert werden. Dazu die Zeile

::

	Port 22

ändern z.B. in

::

	Port 62954

WICHTIG: Diesen Port muss man sich dann merken, da man ihn später beim Aufruf von ssh angeben muss. Ändernt man diesen Port, muss dieser auch in der Ferm config (weiter unten beschrieben) geändert werden, da ferm sonst nur ssh auf Port 22 zu lässt.

Den Editor wieder verlassen und den SSH Server neu starten um die Einstellungen zu übernehmen

::

	sudo /etc/init.d/ssh restart

Benutzer hinzufügen
^^^^^^^^^^^^^^^^^^^

Um weiteren Admins Zugriff auf den Server zu ermöglichen sollten dringend weitere Benutzer angelegt werden

::

	sudo adduser BENUTZERNAME --ingroup sudo

Es muss ein Kennwort angegeben werden, dieses kann der Benutzer später per passwd nach belieben ändern, die weiteren abfragen nach Name, Mail usw. müssen nicht ausgefüllt werden und könnnen einfach mit Enter bestätigt werden.

Für den neuen Benutzer muss ebenfalls der ssh Schlüssel des jeweiligen Nutzers im Nutzerordner hinterlegt werden.

Systemaktualisierung
^^^^^^^^^^^^^^^^^^^^

Als nächstes steht die Systemaktualisierung an, dafür einmal

::

	sudo apt-get update
	sudo apt-get dist-upgrade

Pakete installieren
^^^^^^^^^^^^^^^^^^^

::

	sudo apt-get install bird bird6 xinetd vnstat vnstati gdebi lighttpd git ferm

* bird übernimmt das BGP routing
* bird6 tut das selbe für IPv6
* ferm hilf beim erstellen von IPtables Regeln
* vnstat monitort den Netzwerktraffic
* vnstati erzeugt daraus Grafiken
* lighttpd stellt diese zum Abruf bereit
* gdebi ermöglicht uns die Installation des Check_mk Agents
* xinetd übernimmt die Übertragung der Monitoring Daten
* git wird für die Konfigurationsscripte benötigt.

-> **Nein! Ferm soll beim Systemstart nicht geladen werden! Wird später nach der Konfiguration aktiviert.**

Hinzufügen einer Schnittstelle eth1
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Nun muss im Proxmox für die vm eine eth1 hinzugefügt werden, die auf der vmbr1 hängt und virtio verwendet.

.. image:: http://freifunk-mk.de/gfx/proxmox-59.png

.. image:: http://freifunk-mk.de/gfx/proxmox-60.png

Danach die vm einmal durchbooten.


Eulenfunk BGP-Konzentrator-Konfigurator
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
**Ist leider noch Baustelle hier...** Bis auf weiteres geht es mit unten bei ferm_einrichten_ weiter.

**Die genauen Hintergründe sollten verstanden werden und sind weiter unten beschrieben!**

Um die Konfiguration zu vereinfachen, wurde ein Script geschrieben, welches die nötigen Parameter abfragt und daraus die Konfigurationsdateien, bzw. Auszüge daraus erzeugt. Diese müssen dann nur noch an die richtige Stelle kopiert werden.

Die nachfolgenden Schritte müssen als User root ausgeführt werden, daher wechseln wir zunächst dahin:

::

	sudo -i


::

	mkdir -p /opt/eulenfunk/konzentrator
	cd /opt/eulenfunk/konzentrator
	git clone https://github.com/eulenfunk/ff-bgp-konzentrator-konfigurator.git
	cd ff-bgp-konzentrator-konfigurator
	./bgp-konzentrator-setup.sh

::

Das Script fragt dann die nötigen Werte ab.

Beschreibung der abgefragten Werte
..................................

Allgemeine Parameter
++++++++++++++++++++
AS Nummer vom FF-RL
	Hier wird die Nummer des autonomen Systems vom Freifunk Rheinland eingetragen. Aktuell ist das 201701.
Eigene AS Nummer
	Ihr benötigt ein eigenes autonomes System. Die Nummer davon gebt ihr hier an. TODO: Link auf Beschreibung zur Beschaffung eines eigenen AS...
Zugewiesene FFRL-IPV4-Exit-Adresse
	Vom Freifunk Rheinland bekommt ihr eine Exit-Adresse. Darauf wird der gesamte IPv4 Verkehr aller an diesem Konzentrator angeschlossenen Supernodes bzw. der darüber verbundenen Clients ge-NAT-ed.
Zugewiesenes FFRL-IPV6-Netz
	Der IPv6 Prefix, der euch vom Freifunk Rheinland zugewiesen wurde.
Eigene öffentliche IPV4 Adresse
	Bei der Einrichtung der VM für diesen Konzentrator habt ihr eine IPv4-Adresse konfiguriert, über die ihr euch auch auf dem Konzentrator eingeloggt habt. Also die IPv4-Adresse von *eth1*.
Eigener SSH-Port
	Wenn ihr bei der Konfiguration vom *sshd* einen anderen Port als 22 eingetragen habt, gebt ihr diese hier ein. Damit wird sichergestellt, dass die Firewall (ferm ...) Verbindungen zu dem alternativen Port überhaupt zulässt. Wenn ihr euch hier vertut, kommt ihr nach dem Neustart nicht mehr per SSH auf euren Server!

Konfiguration für GRE-Tunnel nach XXX_Y
+++++++++++++++++++++++++++++++++++++++
Ihr solltet vom Freifunk Rheinland Adressen für 4 Tunnel zum Backbone bekommen haben, jeweils zwei in Berlin und zwei in Düsseldorf. In diesem Abschnitt werden diese konfiguriert. Die folgenden Werte müsst ihr jeweils einmal pro Tunnel passend -- also 4 Mal -- eingeben:

IPV4 Adresse für Tunnelendpunkt auf Backbone-Server
	Die IPv4 Adresse für den Tunnelendpunkt auf dem **Backbone-Server**.
IPV4 Adresse für Tunnelendpunk auf Konzentrator
	Die zugehörige IPv4 Adresse für den Tunnelendpunkt auf **eurem Konzentrator**.
IPV6 Adresse auf Konzentrator
	Zusätzlich zu den IPv4-Adressen habt ihr eine IPv6 Adresse für den Tunnel bekommen. Die Adresse mit der ()...)::**1**/64  hinten ist die Adresse auf eurem Konzentrator. Diese gebt ihr hier an. (Die passende Adresse auf dem Backbone-Ende wird durch das Script daraus abgeleitet).

**TODO: Die bird6.conf Einträge für **filter hostroute** passen noch nicht! Hier stehen statisch die Werte vom Fichtenfunk drin...**

Ausgaben
++++++++
Das Script erzeugt folgende Dateien:

* bird.conf.bgp
* bird6.conf.bgp
* interfaces.bgp
* ferm.conf.bgp
* 20-ff-config.conf.bgp

::

Die erzeugten Dateien sollten nun **überprüft** werden (Beschreibung hierzu siehe unten) und dann an die passenden Stellen kopiert werden:

::

	cp bird.conf.bgp /etc/bird/bird.conf
	cp bird6.conf.bgp /etc/bird/bird6.conf
	cp ferm.conf.bgp /etc/ferm/ferm.conf
	cp 20-ff-config.conf.bgp /etc/sysctl.d/20-ff-config.conf
	cat interfaces.bgp >> /etc/network/interfaces

::

Da nun ein eventueller alternativer SSH-Port in die ferm.conf eingetragen wurde, kann das Firewalling aktiviert werden:

::

	update-rc.d ferm defaults


Danach kann das System rebootet werden. Die Konfigurationen für die Supernodes werden später wie unten beschrieben angelegt.

.. _ferm_einrichten:

Ferm einrichten
^^^^^^^^^^^^^^^^

Ferm lädt beim Systemstart ein Script und erzeugt Iptables Regeln. In folgender Konfigurationsdatei muss die IP Adresse fürs source NAT angepasst werden, dies ist die Adresse über die die Daten ins Internet gehen sollen, (nicht die IPv4 Adresse des Vservers).
Falls man zuvor den ssh Port geändert hat, muss hier "ssh" durch die Port nummer ersetzt werden

::

	sudo nano /etc/ferm/ferm.conf

::

	# -*- shell-script -*-
	#
	#  Configuration file for ferm(1).
	#

	domain (ip ip6) {
		table filter {
			chain INPUT {
				policy ACCEPT;

				proto gre ACCEPT;

				# connection tracking
				mod state state INVALID DROP;
				mod state state (ESTABLISHED RELATED) ACCEPT;

				# allow local packet
				interface lo ACCEPT;

				# respond to ping
				proto icmp ACCEPT;

				# allow IPsec
				proto udp dport 500 ACCEPT;
				proto (esp) ACCEPT;

				# allow SSH connections
				# proto tcp dport 62954 ACCEPT;
				proto tcp dport ssh ACCEPT;
			}
			chain OUTPUT {
				policy ACCEPT;

				# connection tracking
				#mod state state INVALID DROP;
				mod state state (ESTABLISHED RELATED) ACCEPT;
			}
			chain FORWARD {
				policy ACCEPT;

				# connection tracking
				mod state state INVALID DROP;
				mod state state (ESTABLISHED RELATED) ACCEPT;
			}
		}

		table mangle {
			chain PREROUTING {
				interface tun-ffrl-+ {
					MARK set-mark 1;
				}
			}

			chain POSTROUTING {
				# mss clamping
				outerface tun-ffrl-+ proto tcp tcp-flags (SYN RST) SYN TCPMSS clamp-mss-to-pmtu;
			}
		}

		table nat {
			chain POSTROUTING {
				# nat translation
				outerface tun-ffrl-+ saddr 172.16.0.0/12 SNAT to 185.66.19x.xx;
				policy ACCEPT;
			}
		}
	}

Nat IPv4 einrichten
^^^^^^^^^^^^^^^^^^^

* Mit dieser öffentlichen IPv4 werden alle Anfragen ins Internet erledigt.

Um die IP Adresse über die die Daten zum Freifunk Rheinland gehen sollen einzurichten muss folgender Abschitt in die 'interfaces' eingetragen werden.

::

	sudo nano /etc/network/interfaces

::

	auto tun-ffrl-uplink
	iface tun-ffrl-uplink inet static
        address 185.66.19x.xx
        netmask 255.255.255.255
        pre-up ip link add $IFACE type dummy
        post-down ip link del $IFACE

Um die 'Kabelverbindung' zum Rheinland herzustellen werden GRE Tunnel für jeden Backbone Standort angelegt

::

	auto  tun-ffrl-ber-a
	iface tun-ffrl-ber-a inet tunnel
        mode            gre
        netmask         255.255.255.254
        address         100.64.2.xxx
        dstaddr         100.64.2.xxx
        endpoint        185.66.195.0
        local          	xx.xxx.xx.xx
        ttl             255
        mtu             1400
        post-up ip -6 addr add 2a03:2260:0:xxx::2/64 dev $IFACE


* Startet das Interface automatisch (Namen anpassen)
* Legt das Interface an (Namen anpassen)
* modus GRE Tunnel
* Die netzmaske bleibt immer gleich
* Die Interne IP vom eigenen Tunnelende
* Die interne IP vom Backbone Tunnelende
* Die öffentliche IPv4 vom Backbone Standort
* Die eigene öffentliche IPv4
* Die TTL bleibt immer gleich
* Die Mtu bleibt auch gleich
* Die interne IPv6 vom eigenen Tunnelende


Aktuell gibt es zwei Standorte die je redundant ausgebaut sind:

+------------+--------------+------------+
|Standort    |Devicename    |Endpoint    |
+------------+--------------+------------+
|Berlin a    |tun-ffrl-ber-a|185.66.195.0|
+------------+--------------+------------+
|Berlin b    |tun-ffrl-ber-b|185.66.195.1|
+------------+--------------+------------+
|Düsseldorf a|tun-ffrl-dus-a|185.66.193.0|
+------------+--------------+------------+
|Düsseldorf b|tun-ffrl-dus-b|185.66.193.1|
+------------+--------------+------------+

Bird einrichten
^^^^^^^^^^^^^^^

::

	sudo nano /etc/bird/bird.conf

Die Bird conf für IPv4

::

	#Hier muss die Nat IPv4 angegeben werden
	router id 185.66.19x.xx;

	protocol direct announce {
        table master; # implizit
        #Hier muss die Nat IPv4 angegeben werden
        import where net ~ [185.66.195.xx/32];
        interface "tun-ffrl-uplink";
	};

	protocol kernel {
        table master;
        device routes;
        import none;
        export filter {
			#Hier muss die Nat IPv4 angegeben werden
			krt_prefsrc = 185.66.195.xx;
            accept;
        };
        kernel table 42;
	};

	protocol device {
        scan time 15;
	};

	function is_default() {
        return (net ~ [0.0.0.0/0]);
	};

	#Das Temlate wendet wiederkehrende Werte auf die einzelnen BGP Sessions an
	template bgp uplink {
		#Hier muss die eigene AS Nummer eingetragen werden
        local as 65xxx;
        import where is_default();
        export where proto = "announce";
	};

	#Dieser Block muss für alle Backbone Standorte wiederholt werden
	protocol bgp ffrl_ber_a from uplink {
		#Dies ist die eigene Adresse im GRE Tunnel
        source address 100.64.X.xxx;
        #Dies ist die BaCkbone Adresse im GRE Tunnel und das AS des FFRL
        neighbor 100.64.X.xxx as 201701;
	};




Die Bird conf für IPv6

::

	#Auch bei IPv6 muss als Router ID die IPv4 Nat angegeben werden
	router id 185.66.195.xx;

	protocol direct announce {
        table master; # implizit
        #Das eigene (vom FFRL zugeteilte) IPv6 Netz
		import where net ~ [2a03:2260:120:xxx::/56];
		interface "tun-ffrl-uplink";
	};

	protocol kernel {
		table master;
		device routes;
		import none;
		export filter {
			#  setze src addr beim route-export in kernel tabelle
			#Das eigene (vom FFRL zugeteilte) IPv6 Netz als Quelladresse
			krt_prefsrc = 2a03:2260:120:xxx::1;
			accept;
		};
		kernel table 42;
	};

	protocol device {
		scan time 15;
	};

	function is_default() {
		return (net ~ [::/0]);
	};

	template bgp uplink {
		#Die eigene AS Numemer
		local as 65xxx;
		import where is_default();
		export where proto = "announce";
	};

	#Dieser Block wird je standort wiederholt
	protocol bgp ffrl_ber_a from uplink {
		#Eigene IPv6 im GRE Tunnel
		source address 2a03:2260:0:xxx::2;
		#Backbone IPv6 im GRE Tunnel und AS des FFRL
		neighbor 2a03:2260:0:xxx::1 as 201701;
	};

Routing
^^^^^^^

* Forwarding im Netfilter aktivieren damit die Pakete von einem Interface zum nächsten kommen
* Zweite Netzwerkkarte einrichten zur Verbindung mit den Supernodes
* Einrichtung von Iptables Regeln inclusive NAT mit Ferm
* Routingregeln einrichten mithilfe von ip route und ip rule

Forwarding und Performance-Tuning
.................................
Über sysctl müssen einige Kernel-Parameter gesetzt werden, um das Forwarding zu aktivieren und die Netzwerkperformance zu erhöhen.

::

	sudo nano /etc/sysctl.d/20-ff-config.conf

folgende Zeilen dort eintragen

::

	net.ipv4.ip_forward=1
	net.ipv6.conf.all.forwarding=1
	net.ipv4.tcp_window_scaling = 1
	net.core.rmem_max = 16777216
	net.ipv4.tcp_rmem = 4096 87380 16777216
	net.ipv4.tcp_wmem = 4096 16384 16777216
	net.ipv4.conf.default.rp_filter=2
	net.ipv4.conf.all.rp_filter=2

Einrichtung der eth1
....................

In der /etc/network/interfaces legen wir eine eth1 an um den Traffic vom Supernode über eine vmbr des Blechs entgegen zu nehmen

::

	sudo nano /etc/network/interfaces

::

	auto eth1
	iface eth1 inet static
        address 172.31.254.254
        netmask 255.255.255.0

Routing
.......
Zum Routing werden Regeln benötigt, die die Pakete aus dem Freifunk Netz und die Pakete vom FFRL Backbone in eine gesonderte Tabelle (Tabelle 42) leiten. In dieser Tabelle wird vom bird per BGP eine Defaultroute ins Backbone gesetzt und manuell Routen zum eigenen Freifunk Netz (zu den Supernodes).

Um eine Menge Handarbeit zu sparen wird das anlegen der Rules für die einzelnen Communities/Supernodes per Script erledigt.

Das Script gibt es hier: https://github.com/eulenfunk/scripts/tree/master/konzentrator

Zuerst müssen die Verzeichnisse für die scripte angelegt werden, dann die scripte heruntergeladen und ausführbar gemacht werden.

::

	sudo mkdir -p /opt/eulenfunk/konzentrator/config
	cd /opt/eulenfunk/konzentrator
	sudo wget https://raw.githubusercontent.com/eulenfunk/scripts/master/konzentrator/bgp-konzentrator-rc.sh
	sudo wget https://raw.githubusercontent.com/eulenfunk/scripts/master/konzentrator/supernode.sh
	sudo chmod +x *.sh


Damit das Script auch beim boot seine Arbeit verrichten kann muss es in die rc.local eingetragen werden.


::

	sudo nano /etc/rc.local

::

	#!/bin/sh -e
	# rc.local
	/opt/eulenfunk/konzentrator/bgp-konzentrator-rc.sh
	exit 0


Im Ordner **config** wird je Supernode ein config file angelegt. Die Beschreibung zum Hinzufügen von Supernodes erfolgt im Dokument "Supernode einrichten".


Monitoring
^^^^^^^^^^

Das Monitoring beinhaltet folgende Komponenten:

* Check_MK ermöglicht das zentrale Monitoring aller Systemdaten aller eingebundenen Server
* vnstat erstellt Traffic Statistiken, die sich auf der shell anzeigen lassen
* vnstati generiert daraus Grafiken
* lighttpd stellt diese zum Abruf aus dem Internet bereit

Check_MK Agent imstallieren
...........................

Den Check_MK Agent steht in der Weboberfläche des Check_MK als .deb Paket bereit:

In die CheckMK-Instanz per Webbrowser einloggen. Dann suchen:

::

        -> WATO Configuration (Menü/Box)
        -> Monitoring Agents
        -> Packet Agents
        -> check-mk-agent_1.2.6p15-1_all.deb _(Beispiel)_

Den Download-Link in die Zwischenablage kopieren.
Im ssh-terminal nun eingeben: (die Download-URL ist individuell und der Name des .deb-Paketes ändert sich ggf.)

::

        wget --no-check-certificate https://monitoring.freifunk-mk.de/heimathoster/check_mk/agents/check-mk-agent_1.2.6p15-1_all.deb

Um das .deb Paket zu installieren wird gdebi empfohlen, ausserdem benötigt der Agent xinetd zum ausliefern der monitoring Daten. Die Installation von gdebi kann durchaus einige Dutzend Pakete holen. Das ist leider normal.
Per SSH auf dem Server. (Auch hier: Name des .deb-Files ggf. anpassen)

::

	apt-get install gdebi xinetd
	gdebi check-mk-agent_1.2.6p15-1_all.deb

Anschließend noch das Konzentrator-Modul hinzufügen: 

::

	cd /usr/lib/check_mk_agent/local
	wget -O konzentrator https://raw.githubusercontent.com/eulenfunk/check_mk/master/konzentrator
	chmod +x konzentrator


Der Rechner hält ab nun Daten zum Abruf bereit.


_ToDo: Neuen Rechner im CheckMK eintragen in richtige Gruppe & Monitoring scharf schalten.
Alternativ JJX Bescheid sagen, der kümmert sich dann darum.

vnstat einrichten
.................

folgender Befehl

::

	vnstat

sollte so ein Ergebnis ausgeben

::

	Database updated: Thu Feb 25 02:58:22 2016

	   eth0 since 02/02/16

			  rx:  20.50 GiB      tx:  13.98 GiB      total:  34.48 GiB

	   monthly
				rx      |     tx      |    total    |   avg. rate
		 ------------------------+-------------+-------------+---------------
		   Feb '16     20.50 GiB |   13.98 GiB |   34.48 GiB |  138.78 kbit/s
		 ------------------------+-------------+-------------+---------------
		 estimated     24.65 GiB |   16.81 GiB |   41.45 GiB |

	   daily
				rx      |     tx      |    total    |   avg. rate
		 ------------------------+-------------+-------------+---------------
		 yesterday      7.46 GiB |    1.64 GiB |    9.10 GiB |  883.93 kbit/s
		 today      8.19 MiB |   11.23 MiB |   19.43 MiB |   14.87 kbit/s
		 ------------------------+-------------+-------------+---------------
		 estimated        64 MiB |      88 MiB |     152 MiB |


==Hier sollte jetzt stehen aus welchem git man sich das script für den cronjob zum erzeugen der Bilder zieht und wo man die index.html für den lighttpd bekommt==
