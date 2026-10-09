###### Oliver Carrasco Quinteiro

---

## Datos de la zona directa db.starwars.lan

**Archivo named.conf.local :**

        zone "starwars.lan" {
        type primary;
        file "/etc/bind/db.starwars.lan";
        };

        zone "20.168.192.in-addr.arpa"{
        type master;
        file "/etc/bind/db.192";
        };

**Archivo db.starwars.lan :**

        $TTL 1D
        @           IN          SOA     darthvader.starwars.lan. admin.exemplo.lan.(
                                        2025101303  ; Serial (YYYYMMDDnn)
                                        8H          ; Refresh
                                        2H          ; Retry
                                        1W          ; Expire
                                        1D )        ; Minimum TTL

        ; Servidores de nomes
        @           IN          NS      darthvader.starwars.lan.
        @           IN          NS      darthsidious.starwars.lan.

        ; Rexistros A dos Servidores de nomes
        darthvader    IN        A       192.168.20.10
        darthsidious  IN        A       192.168.20.11
        skywalker     IN        A       192.168.20.101
        skywalker     IN        A       192.168.20.111
        luke          IN        A       192.168.20.22
        yoda          IN        A       192.168.20.25
        yoda          IN        A       192.168.20.24
        c3p0          IN        A       192.168.20.26
        palpatine     IN        CNAME   darthsidious.starwars.lan.
        @             IN        MX      10  c3p0
        lenda         IN        TXT     "Que a forza te acompanhe"   

**Archivo db.192** 

        $TTL 1D
        @       IN      SOA     darthvader.starwars.lan admino.starwars.lan. (
                                2025101303  ; Serial (YYYYMMDDnn)
                                8H          ; Refresh
                                2H          ; Retry
                                1W          ; Expire
                                1D )        ; Minimum TTL

        ; Servidor de nomes (primario)
        @       IN      NS      darthvader.starwars.lan.
        @       IN      NS      darthsidious.starwars.lan.
        10      IN      PTR     darthvader.starwars.lan.
        11      IN      PTR     darthsidious.starwars.lan.
        101     IN      PTR     skywalker.starwars.lan.
        111     IN      PTR     skywalker.starwars.lan.
        22      IN      PTR     luke.starwars.lan.
        25      IN      PTR     yoda.starwars.lan.
        24      IN      PTR     yoda.starwars.lan.
        26      IN      PTR     c3p0.starwars.lan.

**Salida de comandos**

        root@darthvader:/var/cache/bind# nslookup 192.168.20.11 localhost
        11.20.168.192.in-addr.arpa	name = darthsidious.starwars.lan.

        root@darthvader:/var/cache/bind# nslookup skywalker.starwars.lan localhost
        Server:		localhost
        Address:	127.0.0.1#53

        Name:	skywalker.starwars.lan
        Address: 192.168.20.111
        Name:	skywalker.starwars.lan
        Address: 192.168.20.101

        root@darthvader:/var/cache/bind# nslookup starwars.lan localhost
        Server:		localhost
        Address:	127.0.0.1#53

        *** Can't find starwars.lan: No answer

        root@darthvader:/var/cache/bind# nslookup -q=mx starwars.lan localhost
        Server:		localhost
        Address:	127.0.0.1#53

        starwars.lan	mail exchanger = 10 c3p0.starwars.lan.

        root@darthvader:/var/cache/bind# nslookup -q=ns starwars.lan localhost
        Server:		localhost
        Address:	127.0.0.1#53

        starwars.lan	nameserver = darthvader.starwars.lan.
        starwars.lan	nameserver = darthsidious.starwars.lan.

        root@darthvader:/var/cache/bind# nslookup -q=soa starwars.lan localhost
        Server:		localhost
        Address:	127.0.0.1#53

        starwars.lan
                origin = darthvader.starwars.lan
                mail addr = admin.exemplo.lan
                serial = 2025101303
                refresh = 28800
                retry = 7200
                expire = 604800
                minimum = 86400

        root@darthvader:/var/cache/bind# nslookup -q=txt lenda.starwars.lan localhost
        Server:		localhost
        Address:	127.0.0.1#53

        lenda.starwars.lan	text = "Que a forza te acompanhe"

        root@darthvader:/var/cache/bind# nslookup 192.168.20.11 localhost
        11.20.168.192.in-addr.arpa	name = darthsidious.starwars.lan.

