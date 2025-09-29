# Planung – AD & Cloud Setup Sheet

| Kategorie | Wert |
|---|---|
| **Projektname** | M159 – Neue Gesamtstruktur & Client (AWS) |
| **Datum** | 22.09.2025 |
| **Verantwortlicher** | Lionel Schoch / Team M159 |
| **Cloud-Anbieter** | AWS |

---

## Netzwerk Setup

| Beschreibung | Details |
|---|---|
| VPC Name | M159-VPC |
| VPC CIDR Block | 10.0.0.0/16 |
| Subnetze | private-subnet-1: 10.0.1.0/24 (DC + Client) |
| Verfügbare Zonen | USA (Nord-Virginia) |
| Route Tables | Internes Routing VPC, kein Internet Gateway für Private Subnet |
| NAT / Internet Zugriff | Nur NAT Gateway (falls notwendig z. B. für Updates vom DC) |

---

## Sicherheitsgruppen & Ports

| Sicherheitsgruppe | Zweck / Zugehörigkeit | Eingehend | Ausgehend |
|---|---|---|---|
| SG-DC | Domänencontroller (SRV-DC01) | RDP 3389 erlauben nur von Admin IP;<br>DNS 53 TCP/UDP;<br>LDAP 389;<br>Kerberos 88;<br>SMB 445;<br>RPC 135 + RPC dynamic ports 49152-65535; <br>Zeit/NTP 123 UDP | Alles innerhalb VPC erlaubt; ausgehend alles erlaubt |
| SG-Client | Windows Client (CL1) | RDP 3389 nur von Admin IP; <br>alle relevanten Ports vom DC zulassen | Ausgehend alles |
| Admin Zugriff | Falls separate SG nötig | SSH / RDP von Admin IP | — |

---

## EC2 Instanzen / Server Setup

| Name | Rolle | Instance Type | Betriebssystem | Private IP | Hostname |
|---|---|---|---|---|---|
| SRV-DC01 | Domänencontroller / DNS | t3.medium | Windows Server 2025 | 10.0.2.10 | SRV-DC01 |
| CL1 | Client | t3.small | Windows Server 2025 | 10.0.2.20 | CL1 |

---

## AD Struktur & Domäne

| Parameter | Wert |
|---|---|
| Gesamtstruktur | tbz.local |
| Domäne | tbz.local |
| NetBIOS Name | TBZ |
| Standort (Site) | Default / eine Site wenn nur ein DC |
| DNS Server Rolle | Auf SRV-DC01 |
| Globaler Katalog | Ja |

---

## AD User & Gruppe

| Parameter | Anmeldenamen | Passwort |
|---|---|
| Administrator | Administrator | rsa passwd |
| Max Musterman | mmustermann | Boppelsen8113 |



---

## Zeit / Synchronisation

| Komponente | Zeitquelle / NTP Einstellungen |
|---|---|
| SRV-DC01 | Amazon NTP |
| CL1 | Sync mit DC / über Domäne |

---

## DNS Setup

| Element | Beschreibung |
|---|---|
| Vorwärts-Lookupzone | tbz.local |
| Reverse-Lookupzone | 10.0.2.0/24 |
| DNS Records geprüft | SRV-DC01 A / PTR; SRV Records AD |

---

## Domänenbeitritt Client

| Beschreibung | Details |
|---|---|
| Domänenname | tbz.local |
| Credentials für Join | Administrator |
| Hostname Client | CL1 |
| Neustart erforderlich | Ja, nach dem Join |

---

## Test & Validierung

| Testfall | Erwartetes Ergebnis |
|---|---|
| Pingen DC vom Client | klappt (Name + FQDN → 10.0.1.10) |
| DNS Auflösung prüfen | `nslookup tbz.local` → IP des DC |
| ADUC auf DC | Computerobjekt „CL1“ erscheint unter **Computers** |
| Zeitdifferenz | < 5 Minuten |
| RDP Zugriff | Nur Admin IP zugänglich |

---

## Sonstige / Bemerkungen

- DSRM Passwort setzen und sicher dokumentieren  
- Sicherstellen, dass Security Groups korrekt sind, sonst Probleme bei AD Kommunikation  
- Updates & Patches: DC evtl. Zugriff ins Internet über NAT, sonst manuell  
- Backup Strategie: ggf. Snapshot der DC-Instanz vor größeren Änderungen  

