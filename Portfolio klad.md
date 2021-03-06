# Windows Server II Portfolio EP1 (Klad)

Link naar github repository: <https://github.com/Avran2611/WinServer2>

![sc](img/01.jpg)

## Voorbereiding

### **1. Installatie Virtual Box**

Vooraleer we van start kunnen gaan met het creëren van de opzet van deze opdracht moeten we Virtual Box installeren. We zullen Virtual Box gebruiken om onze omgeving en servers te virtualiseren op 1 host systeem.

1. Ga naar <https://www.virtualbox.org/wiki/Downloads> en download de recentse versie van Virtual Box voor het gepaste besturingssysteem. In ons geval Windows.

![screenshot](img/vbox/01.jpg)

2. Open het `.exe` bestand en doorloop de installatie
   
3. Vervolgens keren we terug naar <https://www.virtualbox.org/wiki/Downloads> om het VirtualBox Extension Pack te downloaden.

![sc](img/vbox/02.jpg)

4. Open het `exe` bestand en doorloop de isntallatie

---

### **2. VM's aanmaken**

Nu kunnen we beginnen met het aanmaken van de verschillende VM's die we nodig hebben om bovenstaande opstelling te bereiken.
Een klein overzicht van wat we nodig hebben:

- Domeincontroller (domain controller 1 EP1-DC-ALFA)
- Webserver (Exchange Server EP1-WEB)
- Deployment Server (EP1-SCCM)
- Certificate Server (Exchange Server EP1-CA)
- Windows Client (client EP1-CLT1 - EP1-CLT3)

Hiervoor zullen enkele ISO's voor nodig zijn. Download ze hier:

- Windows Server 2019: <https://software-download.microsoft.com/download/sg/17763.379.190312-0539.rs5_release_svc_refresh_SERVER_EVAL_x64FRE_en-us.iso>
- Windows 10: <https://www.microsoft.com/nl-nl/software-download/windows10>

#### **VM Domeincontroller**

De eerste VM die we zullen configureren is die van de domeincontroller. Open VirtualBox en klik bovenaan op `nieuw`.

![sc](img/VMs/01.jpg)

Geef de nieuwe VM de naam `EP1-DC-ALFA` en selecteer Windows 2019 als versie. Klik vervolgens op `volgende`

![sc](img/VMs/02.jpg)

Kies nu hoeveel RAM u wilt toekennen aan de VM. In ons geval gebruiken we de default van 2048 MB. Klik op `volgende`

![sc](img/VMs/03.jpg)

Selecteer nieuwe harde schijf aanmaken en klik op `volgende`

Kies dan voor VDI (Virtual Disk Image) en klik op `volgende`

Kies voor dynamisch gealloceerd en klik op `volgende`

Kies een locatie en ken een grootte toe. 50 GB zou voldoende moeten zijn. Klik vervolgens op `aanmaken`

![sc](img/VMs/07.jpg)

Nu gaan we de netwerkkaarten van de VM configureren. Selecteer de nieuwe VM links en klik vervolgens op `instellingen`

![sc](img/VMs/08.jpg)

Klik links op netwerk en verifiëer volgende instellingen:

![sc](img/VMs/09.jpg)

Voor adapter 2 kiezen we voor intern netwerk. We geven dit de naam LAN10

![sc](img/VMs/10.jpg)

Ten slotte gaan we de Windows Server ISO klaarzetten voor installatie op onze nieuwe virtuele machine. Klik bij Opslag op Optisch station en selecteer de juiste ISO.

![sc](img/VMs/11.jpg)

We zijn klaar met onze eerste VM voor te bereiden. We doen de resterende VM's analoog met onderstaande instellingen per VM. De instellingen die niet gespecifieerd worden blijven hetzelfde als de domeincontroller VM. Exacte configuratie van de IP adressen doen we later.

#### **VM Web Server**

- **Besturingssysteem:** Windows Server 2019
- **Naam:** Exchange Server EP1-WEB
- **NIC Configuratie:** 1 adapter op intern netwerk LAN10

#### **VM Deployment Server**

- **Besturingssysteem:** Windows Server 2019
- **Naam:** EP1-SCCM
- **NIC Configuratie:** 1 adapter op intern netwerk LAN10

#### **VM Certificate Server**

- **Besturingssysteem:** Windows Server 2019
- **Naam:** EP1-CA
- **NIC Configuratie:** 1 adapter op intern netwerk LAN10

#### **VM's  Client 1**

- **Besturingssysteem:** Windows 10
- **Naam:** EP1-CLT1
- **NIC Configuratie:** 1 adapter op intern netwerk LAN10

Je beginscherm zou er nu als volgt moeten uitzien:

![sc](img/VMs/12.jpg)

### **3. Installatie Windows Server 2019**

De installatie van Windows Server verloopt analoog op elke machine.

Selecteer EP1-DC-ALFA uit de lijst en klik bovenaan op starten.

![sc](img/WinServ19/01.jpg)

We zullen nu de stappen doorlopen om Windows Server 2019 te installeren.

1. Kies de gewenste taal, tijdformaat en type toetsenbord

    ![sc](img/WinServ19/02.jpg)

Klik vervolgens op `Next` en op `Install Now`

2. Kies voor Standard Evaluation (Desktop Experience) en klik op `Next`

   ![sc](img/WinServ19/03.jpg)

Accepteer de overeenkomst

3. Kies voor `Custom: Install Windows only (advanced)` als installatietype

    ![sc](img/WinServ19/04.jpg)

4. Klik vervolgens op `new` en `Apply` om een nieuwe partitie aan te maken op de (virtuele) harde schijf

   ![sc](img/WinServ19/05.jpg)

Windows kan een opmerking geven dat er een extra partitie wordt aangemaakt die gereserveerd is voor het systeem. Klik hier op `oke`

5. Selecteer de Primary partitie en klik op `Next`

   ![sc](img/WinServ19/06.jpg)

De setup begint nu met het installeren van Windows Server 2019. De machine zal een aantal keer automatisch opnieuw opstarten.

7. Op het volgende scherm wordt gevraagd om een wachtwoord in te geven. Ik kies hier voor `DC-root`. Klik vervolgens op `Finish`

   ![sc](img/WinServ19/07.jpg)

8. Om windows te ongrendelen klikt u bovenaan op `Invoer` > `Toetsenbord` > `Invoeren Ctrl+Alt+Del`

   ![sc](img/WinServ19/08.jpg)

Log vervolgens in met uw gekozen wachtwoord. Server Manager zal automatisch openen.

9. Nu kunnen we ook de ISO uit het optische station verwijderen door rechts te klikken op `Optisch station` en dan te klikken op `Schijf van virtueel station verwijderen`

   ![sc](img/WinServ19/09.jpg)

Windows Server 2019 is nu geïnstalleerd op EP1-DC-ALFA. Herhaal deze stappen nu voor EP1-WEB, EP1-SCCM en EP1-CA.

### **4. Installatie Windows 10**

De installatie van Windows 10 gebeurd redelijk analoog met die van Windows Server. We installeren Windows 10 voorlopig enkel op `EP1-CLT1`.

Check of het ISO bestand van Windows 10 in het optische station geplaatst is en start de machine.

1. Kies de gewenste taal, tijdformaat en type toetsenbord. (Analoog aan windows server)
2. Windows vraagt om een licentiesleutel in te geven. Klik hier op `I don't have a product key`

   ![sc](img/Win10/01.jpg)

3. Kies voor Windows 10 Pro en klik op `Next`

   ![sc](img/Win10/02.jpg)

   Windows begint nu met de installatie

4. Vervolgens vraagt Windows nogmaals om uw taal en toetsenbord in te stellen
5. Kies voor `Set up for personal use` en klik op `Next`

   ![sc](img/Win10/04.jpg)

6. Klik linksonder op `Offline account` en geef een gebruikernaam en wachtwoord in. Wij gebruiken hier CLTuser1 als gebruikernaam en CLT-root als paswoord.

   ![sc](img/Win10/05.jpg)

7. Ten slotte vraagt windows of een aantal services moeten worden ingeschakeld. Dit zijn services zoals locatie, diagnostic reports enzovoort. Antwoord op alles neen.

Windows 10 is nu succescol geïnsalleerd op EP1-CLT1

## Configuratie van de servers

### Configuratie **EP1-DC-ALFA**

#### **IP Configuratie**

Eerst en vooral gaan we EP1-DC-ALFA voorzien van de juiste netwerkinstellingen. Log in op EP1-DC-ALFA. Server Manager zou automatisch moeten opstarten. Op het dashboard klik je op `Configure this local server`

![sc](img/DC/01.jpg)

Eerst veranderen we de hostnaam. Klik op de naam om deze te veranderen:

![sc](img/DC/02.jpg)

Klik vervolgens op `Change` en geef een de nieuwe hostnaam in. We gebruiken `EP1-DC-ALFA`

![sc](img/DC/03.jpg)
![sc](img/DC/04.jpg)

Klik op `OK` en herstart de machine

Een server heeft ook een statisch ip adres nodig om te functioneren. Deze gaan we nu configureren

Om een onderscheid te kunnen maken tussen de twee netwerkadapters die we eerder configureerden op deze machine, gaan we één van de kabels uittrekken en de adapters juist hernoemen in windows. In de VirtualBox instellingen van EP1-DC-ALFA gaat u naar `Netwerk` en kiest u één van de adapters. Klik dan op `Geavanceerd` en deselecteer `Kabel aangesloten`. Klik vervolgens op `OK`. Merk op dat we hier de kabel van het WAN adapter ontkoppelden

![sc](img/DC/05.jpg)

Nu kunnen we in windows de adapters juist hernoemen. Navigeer naar `Control Panel` > `Network and Internet` > `Network and Sharing Center` > `Change adapter settings` en hernoem de adapters

![sc](img/DC/06.jpg)

Nu kunnen we de kabel weer aankoppelen in VirtualBox

Binnen onze omgeving heeft EP1-DC-ALFA een statisch ip adres op het LAN10 netwerk. Rechtsklik op het LAN10 adapter en klik op `Properties`.

![sc](img/DC/08.jpg)

Selecteer `Internet Protocol Version 4 (TCP/IPv4)` en klik op `Properties`

![sc](img/DC/09.jpg)

Selecteer `Use the following IP address` en geef volgende adressen in:

![sc](img/DC/10.jpg)

#### **Rollen installeren**

We gaan op EP1-DC-ALFA de Active Directory Domain Services (AD DS) installeren en vervolgens de server promoveren tot Active Directory Domain Controller (AD DC).

Op het dashboard in Server Manager klikt u op `Add roles and features`

![sc](img/DC/11.jpg)

Selecteer `Role-based or feature-based installation` en klik op `Next`

Selecteer op het volgende scherm `Select a server from the server pool` en selecteer EP1-DC-ALFA. Klik op `Next`

![sc](img/DC/12.jpg)

Selecteer `Active Directory Domain Services` uit de lijst en klik op `Add Features`. Klik vervolgens op `Next` tot het confirmation scherm. Vink hier aan dat de server automatisch mag herstarten tijdens de installatie en klik op `Install`

![sc](img/DC/13.jpg)
