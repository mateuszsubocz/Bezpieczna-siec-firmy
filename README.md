# Projekt bezpiecznej sieci firmy

# 1. Cel projektu i zadania do realizacji

 - Stworzenie bezpiecznej sieci dla firmy z oddziałami położonymi na 3 różnych piętrach.
   - 1 Piętro: Oddział marketingu i sprzedarzy, HR i Logistyki,
   - 2 Piętro: finansów i rachunkowości, Admina i P-REL,
   - 3 Piętro: ICT oraz Serwerowni.
 
Projekt sieci zawiera wdrożenie zapory firewall ze strefami outside-inside oraz strefą zdemilitaryzowaną (DMZ). Serwery z usługą Active Directory odpowiedzialną za zarządzanie i uwierzytelnianie użytkoników komputerów itp zostanie umieszczona na wewnątrz firewall’a, więc strefy tj. DNS, DHCP będą również wewnątrz natomiast serwery odpowiedzialne za np.: FTP, e-mail itd. Zostaną umieszczone na zewnątrz. Topologia sieci jest typu collapsed. W strefie DMZ umieszczone DHCP, DNS, FTP, WEB, email i SMTP. Do cześći infrastruktury ICT firmy zostały włączone:
- ISP - Firma zakupiła subskrypcje dwóch IPS’ów - SEACOM i Safaricom, żeby zapewnić stałe połączenie internetowe (SEACOM IPv4 to 105.100.50.0/30, a Safaricom 197.200.100.0/30).
- Bezpieczeństwo sieciowe - Dwa firewalle Cisco 5500-x, żeby poprawić bezpieczeństwo sieci.
- Routing sieci - Zarówno firewalle jak i switch będą używane zamiast routera.
- Infrastruktura switchy - zostały zakupione i wdrożone do projektu 2 rodzaje switchy - cisco 2960 i 3650 multiswitche. 24 portowe.
- Serwery i wirtualizacja - Dwa fizyczne serwery zostaną użyte do wirtualizacji przez hypervisora, żeby osiągnąc wiele maszyn wirtualnych dla różnych serwisów. W razie porażki jest będą też postawione dwa serwery DHCP, działające w tym samym czasie.
- Infrastruktura bezprzewodowa - Zostanie użyty Cisco Wireless LAN Controller (WLC), oraz po jednym Lightweight Access Point (LAP) na każdy oddział.
- VoIP i Telefony - Cisco Voice Gateway zostanie użyty do umożliwienia serwisu telefonowego w sieci.

Wirtualna reprezentacja obiektu:

<img width="320" height="320" alt="image" src="https://github.com/user-attachments/assets/7eea2b6e-731e-4e1f-854e-796cf76ad9cc" />

Zadania do realizacji:
- Zaplanowanie i stworzenie topologii
- Wprowadzenie podstawowych ustawień do wszystkich urządzeń + ssh
- Przypisanie vlan i dostęp i porty trunk na l2 i l3
  - STP Portfast i PBDUguard na portach dostępu
- Kanał Ether
- Zaplanowanie i wdrożenie adresacji
- HSRP oraz Inter-Vlan routing na switchach L3
- OSPF na zaporze firewall, ruterach i switchach
- Poziomy i strefy bezpieczeństwa firewall
  - Routing firewall - OSPF + statyczny routing
- Polityka inspekcji
- Konfiguracja polityki inspekcji firewall
- Konfiguracja VoIP

# Opis pomieszczeń

Piętro 3:

<img width="1151" height="743" alt="Pietro3" src="https://github.com/user-attachments/assets/78f8fcdb-fa39-462f-af2b-78c26b850efb" />


Piętro 2:

<img width="666" height="610" alt="Pietro2" src="https://github.com/user-attachments/assets/9457be50-168d-43be-80df-4fe78a854f77" />


Piętro 1:

<img width="666" height="576" alt="Pietro1" src="https://github.com/user-attachments/assets/e2231ef8-87a1-4244-a073-fa52a2be71e7" />

- Każde piętro ma ok. 100m^2

# 2. Projekt fizyczny

<img width="311" height="268" alt="Fiz pietro 1 i 2" src="https://github.com/user-attachments/assets/3deaf211-538f-45bc-b014-18c0138758e8" />
<img width="317" height="267" alt="fiz pietro 3" src="https://github.com/user-attachments/assets/68eb400f-6599-4961-b25f-153a84d94179" />

Okablowanie biur Piętra 1 i 2 (potrzebne 16 gniazd)

Okablowanie biura i Server-room na piętrze 3 (potrzebne 11 gniazd)

Użyty zostanie kabel prosty, łączący idący pod podłogą oraz gniazda RJ45 , oznaczony kolorem fioletowym. Kolorem czerwonym został oznaczony kabel typu crossover, łączący Routery z firewallem i ISP, ISP z FTP,oraz firewall ze switchami biurowymi

Widok szafy serwerowej (kable crossover zostały ozaczone kolorem pomarańczowym)

<img width="860" height="687" alt="okablowanie" src="https://github.com/user-attachments/assets/e3673035-d47c-4b80-a8ca-1f2fbce7fc6c" />

# 3. Projekt logiczny

| Kategoria  | Sieć i maska    | Adresy hostów                   | Brama domyślna | Adres rozgłoszeniowy |
|------------|-----------------|---------------------------------|----------------|-----------------------|
| Management | 192.168.10.0/24 | 192.168.10.1 DO 192.168.10.254 | 129.168.10.1   | 192.158.10.255        |
| WLAN       | 10.20.0.0/16    | 10.20.0.1 DO 10.20.255.254     | 10.20.0.1      | 10.20.255.255         |
| LAN        | 172.16.0.0/16   | 172.16.0.1 DO 172.16.255.254   | 172.16.0.1     | 172.16.255.255        |
| VoIP       | 172.30.0.0/16   | 172.30.0.1 DO 172.30.255.254   | 172.30.0.1     | 172.30.255.254        |
| DMZ        | 10.11.11.0/27   | 10.11.11.1 DO 10.11.11.30      | 10.11.11.1     | 10.11.11.31           |
| Serwery    | 10.11.11.37/27  | 10.11.11.33 DO 10.11.11.62     | 10.11.11.33    | 10.11.11.63           |

Pomiędzy Cloud, ISP, Firewallem, Ruterami and Switchem l3

| NO.              | Network Address    |
|------------------|--------------------|
| CLOUD Area       | 8.0.0.0/8         |
| ISP1 – Internet  | 20.20.20.0/30     |
| ISP2 – Internet  | 30.30.30.0/30     |
| ISP1 – FWL1      | 105.100.50.0/30   |
| ISP1 – FWL2      | 105.100.50.4/30   |
| ISP2 – FWL1      | 205.200.100.0/30  |
| ISP2 – FWL2      | 205.200.100.4/30  |
| FWL1 – MLSW1     | 10.2.2.0/30       |
|FWL1 to-MLSW2 	   |	10.2.2.4/30       |
|FWL2 to-MLSW1 	   |	10.2.2.8/30       |
|FWL2 to-MLSW2    	|	10.2.2.12/30      |

