###### Oliver Carrasco Quinteiro

---

## Datos de la zona directa db.starwars.lan

**Archivo named.conf.local :**

*zone "starwars.lan" {  
    type primary;  
    file "/etc/bind/db.starwars.lan";  
};*

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
  
; Rexistros A dos Servidores de nomes  
darthvader    IN        A       192.168.20.10  
skywalker     IN        A       192.168.20.101  
skywalker     IN        A       192.168.20.111  
luke          IN        A       192.168.20.22  
darthsidious  IN        A       192.168.20.11  
yoda          IN        A       192.168.20.25  
yoda          IN        A       192.168.20.24  
c3p0          IN        A       192.168.20.26  
palpatine     IN        CNAME   darthsidious  
              IN        MX      10  c3p0.starwars.lan  
lenda         IN        TXT     "Que a forza te acompanhe"  
darthsidious  IN        NS      darthsidious.starwars.lan     