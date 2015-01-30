# Labnetz-Doku #

## Dieses Dokument ##

Die Dokumente in diesem Repository beschreiben den Stand des Labornetzes vom 29.1.2015

## Ziele ##

Das Labor soll zuverlässig an das Internet angebunden sein. Geräte und Infrastruktur sollen aus dem lokalen Netz erreichbar sein.

## Netz ##

Das Labor ist über Moritz' Wohnung an das Internet angebunden. Damit das Labor nach außen hin nicht unter Mo's privater IP-Adresse surft, wird jeglicher Internettraffic, den das Lab erzeugt, durch einen VPN-Tunnel geleitet.

Der Zentrale Router hat 4 Ethernet-Interfaces:
  * eth0 führt (auf Umwegen) zu Moritz' Modem
  * an eth1 wird DHCP ausgegeben, hier werden auch die Clients verbunden

### heinrich (defendo) ###

Auf dem Interface `eth0` VLANs an:
  * `14` zu Moritz
  * `8` zum Hotelturm

Da das Default-VLAN uns hier nicht weiterhilft, muss das Modul `8021q` geladen sein, was in der `/etc/modules` vermerkt ist.

Damit weiterhin nicht automatisch Moritz' Router als Default-Route auf heinrich gepushed wird, ist in der `/etc/dhcp/dhclient.conf` in der mit `request` beginnenden Zeile der Parameter `routers` entfernt.

#### Configs ####

  * `/etc/dhcp/dhclient.conf` [link](heinrich/etc/dhcp/dhclient.conf)
  * `/etc/network/interfaces` [link](heinrich/etc/network/interfaces)
  * `/etc/openvpn/client.conf` [link](heinrich/etc/openvpn/client.conf)
  * `/etc/iptables/rules.v4` [link](heinrich/etc/iptables/rules.v4)

### exit ###

exit macht outbound NAT.

#### configs ####

  * `/etc/openvpn/server.conf` [link](exit/etc/openvpn/server.conf)

### APs (TP-Link WR841ND) ###

Sind als "dumme" Access-Points konfiguriert, d.h. sie setzen einfach das LAN auf WLAN um.

SSIDs:
  * Labor 2.0 - Passphrase ist allgemein bekannt.


## Numbering ##

IP Range: `172.16.0.1/24`

Reserved/Fixed IPs:
  * `172.16.0.1` Gateway (defendo)
  * `172.16.0.10` AP Nordseite
  * `172.16.0.11` AP Südseite

DHCP Range for clients:
  * `172.16.0.50 - 172.16.0.254`
