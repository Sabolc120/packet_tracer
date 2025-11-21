# Kisiskolai Hálózati Infrastruktúra Terv (Cisco Packet Tracer)

Ez a projekt egy kisiskolai hálózati környezet szimulációja, amelyet **Cisco Packet Tracer** környezetben valósítottam meg. A projekt célja egy biztonságos, szegmentált és menedzselhető hálózati architektúra bemutatása, amely elkülöníti a tanári és diák forgalmat, valamint központi szolgáltatásokat nyújt.

> **Megjegyzés:** Ez a projekt egy otthoni labor ("Home Lab") környezetben készült demonstrációs céllal, nem egy valós, élő intézmény fizikai leképezése.

## 🏗️ Hálózati Architektúra

A hálózat egy **hierarchikus modellt** követ (bár egyszerűsített formában), amely a következő fő komponensekből áll:

* **Core/Distribution Réteg:** 1 db **Layer 3 Switch** (Cisco 3650), amely az Inter-VLAN routingot (alapértelmezett átjáró) és a VLAN-ok közötti forgalomirányítást végzi.
* **Access Réteg:** 2 db **Layer 2 Switch** (Cisco 2960), amelyek a végpontok (PC-k) csatlakozását biztosítják.
* **Vezeték nélküli hálózat:** Dedikált Wi-Fi hozzáférés a Tanári és Diák hálózatok számára.
* **Szerver Szolgáltatások:** Dedikált szerver a DHCP és egyéb hálózati szolgáltatások (HTTP, DNS) kezelésére.

## 🚀 Implementált Technológiák és Funkciók

A projekt során az alábbi hálózati megoldásokat alkalmaztam a stabilitás és biztonság érdekében:

* **VLAN Szegmentáció:** A hálózat logikai felosztása (Tanári, Diák, Szerver, Menedzsment) a broadcast forgalom csökkentése és a biztonság növelése érdekében.
* **Inter-VLAN Routing:** A Layer 3 switch végzi a VLAN-ok közötti útválasztást, szükségtelenné téve külön router használatát a belső forgalomhoz (Router-on-a-stick helyett SVI alapú routing).
* **DHCP Relay & Server:** Központosított IP-cím kiosztás. A L3 switch `ip helper-address` segítségével továbbítja a kéréseket a központi szervernek.
* **VTP (VLAN Trunking Protocol):** A VLAN adatbázis automatikus szinkronizációja a switchek között (biztonságos jelszóval védve).
* **Port Security:** Szigorú MAC-cím alapú védelem az Access portokon (maximális eszközszám korlátozása, ismeretlen eszköz esetén `shutdown` reakció).
* **Device Hardening:** Jelszavas védelem az privilegizált módhoz (`enable secret`), VTP jelszó, és felesleges szolgáltatások tiltása.

## 📊 IP Címzési Terv és VLAN Konfiguráció

A hálózat a következő IP-tartományokat és VLAN kiosztást használja:

| VLAN ID | VLAN Név | Hálózati Cím | Gateway (SVI) | Megjegyzés |
| :--- | :--- | :--- | :--- | :--- |
| **1** | Management | `10.1.1.0/24` | `10.1.1.254` | Eszközmenedzsment |
| **10** | Tanári | `10.1.10.0/24` | `10.1.10.254` | Tanári PC-k és Wi-Fi |
| **20** | Diák | `10.1.20.0/24` | `10.1.20.254` | Diák PC-k és Wi-Fi |
| **100** | Szerver | `10.1.100.0/24` | `10.1.100.254` | Központi szolgáltatások |

**Kiemelt eszközök:**
* **Szerver (Statikus IP):** `10.1.100.10` (Subnet: `/24`)

## 🔐 Hozzáférési Adatok (Credentials)

A `.pkt` fájl megnyitásához és a konfigurációk módosításához szükséges jelszavak:

* **Enable Secret (Privileged Exec):** `example`
* **VTP Password:** `example`
* **Tanári Wi-Fi (SSID: Tanari):** `tanari1900`
* **Diák Wi-Fi (SSID: Diak):** `diak2500`

## 📂 A Repository Tartalma

* `Iskolai_Halozat_Projekt.pkt`: A Cisco Packet Tracer forrásfájl.
* `Dokumentacio.pdf`: Részletes leírás a topológiáról és a konfigurációs lépésekről (Opcionális).

---
*Készítette: [A Te Neved] - Hálózati Rendszergazda Portfólió*

Readme: AI Alapú, ellenőriztetve. 
