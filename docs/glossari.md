# Glossari de Termes

Referència ràpida dels termes tècnics utilitzats en aquesta documentació.

---

## A

**Apache**
: Servidor web de codi obert. Rep peticions HTTP/HTTPS dels clients i retorna els fitxers o executa scripts PHP. És el component "A" del stack LAMP.

**apt**
: Gestor de paquets d'Ubuntu/Debian. S'utilitza per instal·lar, actualitzar i eliminar programari del sistema.

**auth.log**
: Fitxer de log d'Ubuntu que registra tots els intents d'autenticació, connexions SSH i accions sudo. Ubicació: `/var/log/auth.log`.

---

## B

**Backup**
: Còpia de seguretat de dades. En el context d'aquest projecte, fa referència principalment als dumps de MySQL i als fitxers de configuració del sistema.

**bind-address**
: Paràmetre de MySQL que controla quines interfícies de xarxa escolta el servidor. Posar-lo a `127.0.0.1` impedeix connexions remotes.

---

## C

**Certbot**
: Eina de la Electronic Frontier Foundation (EFF) per obtenir i renovar certificats SSL de Let's Encrypt automàticament.

**chmod**
: Comanda Unix per canviar els permisos d'accés d'un fitxer o directori.

**chown**
: Comanda Unix per canviar el propietari (owner) i el grup d'un fitxer o directori.

**Cron**
: Planificador de tasques del sistema operatiu Linux. Permet executar comandes automàticament en intervals definits.

---

## D

**DocumentRoot**
: Directori del servidor que conté els fitxers accessibles públicament a través del servidor web. Per defecte: `/var/www/html`.

**Dump (SQL)**
: Exportació de l'estructura i dades d'una base de dades en format SQL. S'utilitza per a backups i migracions.

---

## F

**Fail2Ban**
: Eina de seguretat que analitza els logs del sistema i bloqueja temporalment les IPs que intenten accedir amb credencials incorrectes (atacs de força bruta).

**Firewall**
: Sistema que filtra el tràfic de xarxa. En Ubuntu s'utilitza `ufw` (Uncomplicated Firewall) per gestionar les regles de manera senzilla.

---

## H

**Hardening**
: Procés de reducció de la superfície d'atac d'un sistema eliminant serveis innecessaris, configurant permisos adequats i aplicant polítiques de seguretat.

**HTTPS**
: Protocol HTTP xifrat mitjançant SSL/TLS. Garanteix la confidencialitat i integritat de les comunicacions entre client i servidor.

---

## L

**LAMP**
: Acrònim de **L**inux + **A**pache + **M**ySQL + **P**HP. Stack de tecnologies de codi obert per desplegar aplicacions web del costat del servidor.

**Let's Encrypt**
: Autoritat de certificació gratuïta i automàtica que proporciona certificats SSL/TLS per a dominis públics.

**Logrotate**
: Utilitat del sistema que gestiona la rotació, compressió i eliminació automàtica de fitxers de log per evitar que ocupin massa espai.

---

## M

**MySQL**
: Sistema de gestió de bases de dades relacional (RDBMS) de codi obert. És el component "M" del stack LAMP.

**mysqldump**
: Comanda de MySQL per exportar bases de dades a fitxers SQL.

---

## N

**Netplan**
: Utilitat de configuració de xarxa d'Ubuntu. Utilitza fitxers YAML per definir la configuració de les interfícies de xarxa.

---

## P

**PHP**
: Llenguatge de programació d'scripting del costat del servidor. És el component "P" del stack LAMP. S'integra amb Apache mitjançant `libapache2-mod-php`.

**Principi de mínim privilegi**
: Principi de seguretat que estableix que cada usuari o procés ha de tenir únicament els permisos mínims necessaris per realitzar les seves funcions.

---

## S

**SCRUM**
: Marc de treball àgil per a la gestió de projectes. Organitza el treball en sprints iteratius amb rols definits (Product Owner, Scrum Master, equip de desenvolupament).

**SSH (Secure Shell)**
: Protocol de comunicació xifrat que permet l'accés remot segur a un servidor. Per defecte utilitza el port 22 (en aquest projecte, canviat a 2222).

**SSL/TLS**
: Protocols criptogràfics que proporcionen comunicació segura a través d'una xarxa. SSL és el predecessor de TLS; en la pràctica s'usen de forma intercanviable.

**sudo**
: Comanda que permet a un usuari executar una altra comanda amb privilegis d'administrador (root), de manera temporal i auditada.

**systemctl**
: Comanda per gestionar serveis del sistema en sistemes Linux que utilitzen systemd (iniciar, aturar, habilitar, comprovar estat).

---

## U

**UFW (Uncomplicated Firewall)**
: Interfície simplificada per gestionar `iptables` a Ubuntu. Permet definir regles de firewall amb comandes senzilles.

---

## V

**VirtualHost**
: Configuració d'Apache que permet servir múltiples llocs web des d'un mateix servidor, cadascun amb el seu propi domini o IP.

---

## W

**www-data**
: Usuari i grup del sistema operatiu amb el qual s'executa Apache. Els fitxers del servidor web han de ser propietat d'aquest usuari per garantir un accés correcte.
