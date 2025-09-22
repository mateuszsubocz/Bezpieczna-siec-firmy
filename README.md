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
