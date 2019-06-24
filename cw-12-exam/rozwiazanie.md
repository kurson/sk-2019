```
Potrzebna sieć wifi na każdym piętrze, czyli 3 sieci z maskami 22, ponieważ min. 800 urządzeń
Dla każdego laboratorium maska 24, mogłaby być 26 czyli dla 62 urządzeń, min. potrzeba 35.
Ponieważ w puli adresów publicznych dostępne jest tylko 30 adresów, do adresowania stanowisk i urządzeń podpiętych na wifi wykorzystuję pulę adresów prywatnych, CIDR: 10.0.0.0/8

Właściwe adresy:
  - 188.156.220.161/27 połączenie z internetem
  - 10.1.0.0/22 wifi parter
  - 10.1.4.0/22 wifi pietro 1
  - 10.1.8.0/22 wifi pietro 2
  - Laboratoria - aby zidentyfikować salę i kondygnację, 3 oktet adresu odpowiada numerowi sali:
    - 009: 10.0.9.0/24
    - 013: 10.0.13.0/24
    - 014: 10.0.14.0/24
    - 017: 10.0.17.0/24
    - 115: 10.0.115.0/24
    - 116: 10.0.116.0/24
    - 117: 10.0.117.0/24
    - 122: 10.0.122.0/24
    - 201: 10.0.201.0/24
    - 202: 10.0.202.0/24
    - 203: 10.0.203.0/24
    - 204: 10.0.204.0/24
    
    
  
Konfiguracja:
  PC0 (Główny router)
    enp0s3: internet
    enp0s8 (wifi parter)
      address 10.1.0.0
      netmask 255.255.252.0
    enp0s9 (wifi piętro 1)
      address 10.1.4.0
      netmask 255.255.252.0
    enp0s10 (wifi piętro 2)
      address 10.1.8.0
      netmask 255.255.252.0
    enp0s11 (Serwer LAN)
      address 188.156.220.162
      netmask 255.255.255.224
  
  Serwer LAN
    enp0s3
      address 188.156.220.163
      netmask 255.255.255.224
    enp0s8
      address 10.0.9.255
      netmask 255.255.255.0
    enp0s9
      address 10.0.13.255
      netmask 255.255.255.0
    ...
    (analogicznie dla pozostałych labów)
    ...
    enp0s19
      address 10.0.204.255
      netmask 255.255.255.0`

  DHCP i DNS:
  dla każdego WIFI (parter):
      nano /etc/default/isc-dhcp-server 
        odkomentować ścieżkę do pliku config DHCPDv4_CONF
        dopisać interfejs INTERFACESv4="enp0s8"
      nano /etc/dhcp/dhcpd.conf - dopisać konfiguracje sieci :
        subnet 10.1.0.0 netmask 255.255.252.0 {
          range 10.1.0.2 10.1.3.254;
          option routers 10.1.0.1;
          option domain-name-servers 1.1.1.1, 1.0.0.1;
        }
      systemctl restart isc-dhcp-server
      
   (piętro 1):
      nano /etc/default/isc-dhcp-server 
        odkomentować ścieżkę do pliku config DHCPDv4_CONF
        dopisać interfejs INTERFACESv4="enp0s9"
      nano /etc/dhcp/dhcpd.conf - dopisać konfiguracje sieci :
        subnet 10.1.4.0 netmask 255.255.252.0 {
          range 10.1.4.2 10.1.7.254;
          option routers 10.1.4.1;
          option domain-name-servers 1.1.1.1, 1.0.0.1;
        }
      systemctl restart isc-dhcp-server
      
  (piętro 2):
      nano /etc/default/isc-dhcp-server 
        odkomentować ścieżkę do pliku config DHCPDv4_CONF
        dopisać interfejs INTERFACESv4="enp0s10"
      nano /etc/dhcp/dhcpd.conf - dopisać konfiguracje sieci :
        subnet 10.1.8.0 netmask 255.255.252.0 {
          range 10.1.8.2 10.1.11.254;
          option routers 10.1.8.1;
          option domain-name-servers 1.1.1.1, 1.0.0.1;
        }
      systemctl restart isc-dhcp-server
      
      
  SERWER LAN:
      nano /etc/default/isc-dhcp-server 
        odkomentować ścieżkę do pliku config DHCPDv4_CONF
        dopisać interfejs INTERFACESv4="enp0s8 enp0s9 enp0s10 enp0s11 ... enp0s19"
        
  DHCP dla każdej sali analogicznie (sala 009):
      nano /etc/dhcp/dhcpd.conf - dopisać konfiguracje sieci :
        subnet 10.0.9.0 netmask 255.255.255.0 {
          range 10.0.9.1 10.0.9.254;
          option routers 10.0.9.255;
          option domain-name-servers 1.1.1.1, 1.0.0.1;
        }
      systemctl restart isc-dhcp-server


  Routing:
    Serwer LAN: up ip rotue add default via 188.156.220.162

    Komputery w labach (sala 009): up ip route add default via 10.0.9.62

    Urządzenia na WIFI piętro 0/1/2: up ip route add default 10.1.0/4/8.1

  IP Forwarding:
    W routerach wifi i w serwerze lan:
      nano /etc/sysctl.d/99-sysctl.conf
        odkomentować net.ipv4.ip_forward=1 w 
        
  MASQUERADE:
    PC0 (Główny router):
      iptables -t nat -A POSTROUTING -s 188.156.220.161/27 -o enp0s3 -j MASQUERADE
      iptables -t nat -A POSTROUTING -s 10.1.0.0/22 -o enp0s3 -j MASQUERADE
      iptables -t nat -A POSTROUTING -s 10.1.4.0/22 -o enp0s3 -j MASQUERADE
      iptables -t nat -A POSTROUTING -s 10.1.8.0/22 -o enp0s3 -j MASQUERADE
    Serwer LAN, dla każdej sali analogicznie:
      iptables -t nat -A POSTROUTING -s 10.0.(numer sali).0/26 -o enp0s3 -j MASQUERADE
    Zapisanie: 
      ipatables-save > /etc/iptables.up.rules
      nano /etc/network/interfaces
      (dopisać) post-up iptables-restore < /etc/iptables.up.rules
```
![diagram](Diagram1.png)
