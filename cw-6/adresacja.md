Struktura adresu IP
-------------------

```192.168.100.192```
```255.255.255.0```

Adres sieci
-----------

1. 
2.
3.

Adres rozgłoszeniowy
-----------

1. 
2.
3.


Podział na równą ilość podsieci
-------------------------------

```2^S >= n```

Chcemy 7 -> 2^3 >= 7

Maska -> 255.255.255.11100000 -> 255.255.255.224 -> /27


Wprowadzenie
------------

------------------------------
| dziesiętnie |  binarnie   | 
| --------- |:-------------| 
| ``10``  | 00001010 |
| ``92``  | 01011110 |
| ``37``  | 00010101 |
| ``240`` | 11101111 |
| ``192`` | 11000000 |
| ``255`` | 11111110 |
| ``128`` | 10000000 |
| ``168`` | 10011110 |


------------------------------
| binarnie |  dziesiętnie   | 
| --------- |:-------------| 
| ``00100000``  |  32 |
| ``11111000``  | 248 |
| ``10100000``  | 160 |
| ``00110000`` | 48  |
| ``10101100`` | 172 | 
| ``01000000`` | 64  |
| ``11111100`` | 252 |
| ``01100010`` | 96  |
 
Notacja CIDR
------------
 
------------------------------
| maska |  /(X) x - liczba bitów   | 
| --------- |:-------------| 
| ``255.255.255.0``   | /24 |
| ``255.128.0.0``     | /9 |
| ``255.255.252.0``   | /22 |
| ``255.255.254.0``   | /23 |
| ``255.255.255.240`` | /28 |
| ``255.240.0.0``     | /12 |

------------------------------
| CIDR |  Maska   | 
| --------- |:-------------| 
| ``/8``    | 255.0.0.0 |
| ``/20``   | 255.255.240.0 |
| ``/30``   | 255.255.255.252 |
| ``/16``   | 255.255.0.0 |
| ``/27``   | 255.255.224.0 |
| ``/11``   | 255.224.0.0 |


Liczba hostów
-------------

------------------------------
| sieć |  liczba   | 
| --------- |:-------------| 
| ``10.0.0.0/8``    | 16777216 |
| ``172.16.0.0/16``   | 65536 |
| ``192.168.1.0/24``   | 256 |
| ``192.168.1.0/27``   | 32 |
| ``192.168.1.0/29``   | 8 |
| ``192.168.1.0/31``   | 2 |

* liczba 0 w masce?
4294967296

Parametry na podstawie adresu
-----------------------------

Mając dany adres hosta i maskę znajdź:
  * adres sieci
  * początkowy adres hosta w sieci
  * liczbę hostów w zadanej podsieci ```2^(32 bity - bity maski maska) - 2 (siec i broadcast)```
  * końcowy zakres adresu hosta w sieci
  * adres rozgłoszeniowy
  
  ------------------------------
| Parametr |  wartość   | 
| --------- |:-------------| 
| ``ip``    | 192.168.1.145 | 
| ``maska``   | 255.255.255.128 | 
| ``adres sieci``   | 192.168.1.128 |
| ``liczba hostów``   | 128 |
| ``host - min``   | 192.168.1.129 | 
| ``host - max``   | 192.168.1.254 | 
| ``broadcast``   | 192.168.1.255 | 
 
Zadanie
------------

0. Znajdz wszystkie parametry sieci dla hosta o adresie 172.16.128.64 / 16
  
------------------------------
| Parametr |  wartość   | 
| --------- |:-------------| 
| ``ip``    | 172.16.128.64 | 
| ``maska``   | 255.255.0.0 | 
| ``adres sieci``   | 172.16.0.0 |
| ``liczba hostów``   | 65536 |
| ``host - min``   | 172.16.0.1 | 
| ``host - max``   | 172.16.255.254 | 
| ``broadcast``   | 172.16.255.255 | 

1.
  * Podziel sieć ```192.168.1.0``` na 16 równych podsieci
  
----------------------------------------------------------
| Adres sieci |  zakres hostów   | Adres Rozgłoszeniowy |
| --------- |:-------------|  :---------------|
| ``192.168.1.0``    | 192.168.1.1 - 192.168.1.14 | 192.168.1.15 |
| ``192.168.1.16``    | 192.168.1.17 - 192.168.1.30 | 192.168.1.31 |
| ``192.168.1.32``    | 192.168.1.33 - 192.168.1.46 | 192.168.1.47 |
| ``192.168.1.48``    | 192.168.1.49 - 192.168.1.62 | 192.168.1.63 |
| ``192.168.1.64``    | 192.168.1.65 - 192.168.1.78 | 192.168.1.79 |
| ``192.168.1.80``    | 192.168.1.81 - 192.168.1.94 | 192.168.1.95 |
| ``192.168.1.96``    | 192.168.1.97 - 192.168.1.110 | 192.168.1.111 |
| ``192.168.1.112``    | 192.168.1.113 - 192.168.1.126 | 192.168.1.127 |
| ``192.168.1.128``    | 192.168.1.129 - 192.168.1.142 | 192.168.1.143 |
| ``192.168.1.144``    | 192.168.1.145 - 192.168.1.158 | 192.168.1.159 |
| ``192.168.1.160``    | 192.168.1.161 - 192.168.1.174 | 192.168.1.175 |
| ``192.168.1.176``    | 192.168.1.177 - 192.168.1.190 | 192.168.1.191 |
| ``192.168.1.192``    | 192.168.1.193 - 192.168.1.206 | 192.168.1.207 |
| ``192.168.1.208``    | 192.168.1.209 - 192.168.1.222 | 192.168.1.223 |
| ``192.168.1.224``    | 192.168.1.225 - 192.168.1.238 | 192.168.1.239 |
| ``192.168.1.240``    | 192.168.1.241 - 192.168.1.254 | 192.168.1.255 |

2. 
  * Podziel sieć ``172.16.0.0/16`` na 6 równych podsieci.
  
----------------------------------------------------------
| Adres sieci |  zakres hostów   | Adres Rozgłoszeniowy |
| --------- |:-------------|  :---------------|
| ``172.16.0.0``    | 172.16.0.1 - 172.16.42.168 | 172.16.42.169 |
| ``172.16.42.170`` | 172.16.42.171 - 172.16.85.83 | 172.16.85.84 |
| ``172.16.85.85``  | 172.16.85.86 - 172.16.127.254 | 172.16.127.255 |
| ``172.16.128.0``  | 172.16.128.1 - 172.16.160.168 | 172.16.42.169 |
| ``172.16.160.170``| 172.16.160.171 - 172.16.213.83 | 172.16.213.84 |
| ``172.16.213.85`` | 172.16.213.86 - 172.16.255.254 | 172.16.255.255 |

3. 
  * Podziel sieć ``192.168.1.0/24``, tak aby każda podsieć miała 11 użytkowników.
----------------------------------------------------------
| Adres sieci |  zakres hostów   | Adres Rozgłoszeniowy |
| --------- |:-------------|  :---------------|
| ``192.168.1.0``    | 192.168.1.1 - 192.168.1.11 | 192.168.1.12 |
| ``192.168.1.13``    | 192.168.1.14 - 192.168.1.25 | 192.168.1.26 |
| ``192.168.1.27``    | 192.168.1.28 - 192.168.1.39 | 192.168.1.40 |
itd.

4. 
  * Podziel sieć ``10.0.0.0/8`` na 5 podsieci. 
    * Podsieć A ma posiadać 100 000 użytkowników,
    * B – 10 000 użytkowników
    * C – 3 000 użytkowników
    * D – 500 użytkowników
    * E – 2 użytkowników.
    
----------------------------------------------------------
| Adres sieci |  zakres hostów   | Adres Rozgłoszeniowy |
| --------- |:-------------|  :---------------|
| ``10.0.0.0``    | 10.0.0.1 - 10.1.134.160 | 10.1.134.160 |
| ``10.1.134.161``    | 10.1.134.162 - 10.1.173.179 | 10.1.173.180 |
| ``10.1.173.181``    | 10.1.173.182 - 10.1.185.107 | 10.1.185.108 |
| ``10.1.185.109``    | 10.1.185.110 - 10.1.187.98 | 10.1.187.99 |
| ``10.1.187.100``    | 10.1.187.101 - 10.1.187.102 | 10.1.187.103 |