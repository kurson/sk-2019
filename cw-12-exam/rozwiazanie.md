<p>Potrzebna sieć wifi na każdym piętrze, czyli 3 sieci z maskami 22, ponieważ min. 800 urządzeń
Dla każdego laboratorium maska 24, mogłaby być 26 czyli dla 62 urządzeń, min. potrzeba 35.
Ponieważ w puli adresów publicznych dostępne jest tylko 30 adresów, do adresowania stanowisk i urządzeń podpiętych na wifi wykorzystuję pulę adresów prywatnych, CIDR: 10.0.0.0/8</p>

Właściwe adresy:
  - 188.156.220.161/27 połączenie z internetem
  - 10.1.0.0/22 wifi parter
  - 10.1.4.0/22 wifi pietro 1
  - 10.1.8.0/22 wifi pietro 2
Laboratoria - aby zidentyfikować salę i kondygnację, 3 oktet adresu odpowiada numerowi sali:
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




![diagram](Diagram1.png)
