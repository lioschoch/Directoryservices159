# Directory Services – Übersicht

## Definition
Aus technischer Sicht ist ein Verzeichnisdienst nichts anderes als eine spezialisierte **Datenbank**, die Objekte und deren Attribute hierarchisch speichert und verwaltet.

---

## Kernaufgaben eines Directory Services
1. Authentifizierung  
2. Autorisierung  
3. Zentrale Benutzer- und Ressourcenverwaltung  
4. Bereitstellung von Richtlinien  

---

## Beispiele für Objekte (Ressourcen)
- Benutzer  
- Computer  
- Gruppen  
- Drucker  
- Freigaben  

---

## Merkmale eines Directory Services
- Hierarchische Struktur  
- Zentralisiert  
- Replizierbar  
- Standardisierte Protokolle (LDAP/Kerberos)  
- Skalierbar  

---

## Zusammenhang: Objekt – Attribut – Wert
Korrekte Aussagen:  
- ✔ Benutzerattribute haben einen Namen und einen Wert  
- ✔ Das Benutzerpasswortattribut bestehend aus Namen und Wert ist ein Benutzerattribut  
- ✔ Der Vorname ist ein Benutzerattribut  

---

## Objektklasse
Eine **Objektklasse** ist eine Vorlage, die definiert, welche Attribute ein bestimmtes Objekt besitzen darf oder muss.

---

## Nachteile eines Directory Services
- Hohe Komplexität und Verwaltungsaufwand  
- Zentrale Abhängigkeit (Single Point of Failure)  

---

## IT-Situationen
- **Mit Directory Service:** Unternehmen mit vielen Mitarbeitern und Computern, die zentral verwaltet werden müssen.  
- **Ohne Directory Service:** Kleines Büro mit wenigen unabhängigen Rechnern.  

---

## Administratoren
- **Lokaler Administrator:** Hat volle Rechte nur auf einem einzelnen Rechner.  
- **Domänenadministrator:** Hat volle Rechte über die gesamte Domäne hinweg.  

---

## Domänencontroller
- **Aufgabe:** Bereitstellung und Verwaltung des Directory Services inkl. Authentifizierung und Autorisierung.  
- **Abkürzung DC:** Domain Controller  

---

## Weitere Abkürzungen
- **OU / OE:** Organizational Unit / Organisationseinheit  

---

## Begriffe
- **On-Premises:** IT-Infrastruktur wird lokal im eigenen Rechenzentrum betrieben.  
- **MS AD DS vs. Entra ID:** AD DS ist lokal (on-premises), Entra ID ist Microsofts Cloud-Verzeichnisdienst.  
- **Intune, MDM & MAM:** Intune = Cloud-Tool zur Verwaltung; MDM = Geräteverwaltung; MAM = App- und Datenverwaltung.  
- **Tenant:** Isolierte Instanz einer Cloud-Umgebung (z. B. Microsoft 365-Mandant).  
- **Hybrid-AD-Umgebung:** AD-Umgebung mit Entra ID Integration.  

---
