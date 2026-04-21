# Resolució de Problemes

Guia de diagnosi per als problemes més comuns de la infraestructura LAMP.

---

## Apache no s'inicia

**Símptomes:** `sudo systemctl start apache2` falla.

**Diagnosi:**

```bash
sudo systemctl status apache2
sudo apache2ctl configtest
sudo journalctl -xe | grep apache
```

**Causes habituals:**

| Causa | Solució |
|-------|---------|
| Port 80 ja en ús | `sudo ss -tulnp | grep :80` → identifica el procés i atura'l |
| Error de sintaxi en la config | `sudo apache2ctl configtest` mostra la línia exacta |
| VirtualHost mal configurat | Revisa `/etc/apache2/sites-available/` |

---

## MySQL no s'inicia

**Diagnosi:**

```bash
sudo systemctl status mysql
sudo journalctl -xe | grep mysql
sudo cat /var/log/mysql/error.log | tail -30
```

**Causes habituals:**

| Causa | Solució |
|-------|---------|
| Disc ple | `df -h` → allibera espai |
| Fitxer de socket corrupte | `sudo rm /var/run/mysqld/mysqld.sock` i reinicia |
| Permisos incorrectes | `sudo chown -R mysql:mysql /var/lib/mysql` |

---

## PHP no processa fitxers .php

**Símptomes:** El navegador descarrega el fitxer .php en lloc d'executar-lo.

**Solució:**

```bash
# Verifica que el mòdul PHP per Apache estigui actiu
sudo a2enmod php8.x
sudo systemctl restart apache2

# Comprova que la directiva AddType és present
grep -r "application/x-httpd-php" /etc/apache2/
```

---

## Error de connexió a la base de dades

**Símptomes:** L'aplicació web mostra "Could not connect to database".

**Diagnosi:**

```bash
# Prova la connexió manualment
mysql -u rickspain_user -p -h localhost rickspain_db

# Verifica que MySQL escolta a localhost
sudo ss -tulnp | grep 3306
```

**Causes habituals:**

- Credencials incorrectes al fitxer de configuració de l'aplicació
- `bind-address` no és `127.0.0.1`
- Usuari sense permisos sobre la BD (`GRANT ALL PRIVILEGES`)

---

## No es pot connectar per SSH

**Símptomes:** `ssh usuari@ip -p 2222` retorna "Connection refused".

**Diagnosi des del servidor (accés físic o consola):**

```bash
sudo systemctl status ssh
sudo ufw status
sudo grep "Port" /etc/ssh/sshd_config
```

**Causes habituals:**

| Causa | Solució |
|-------|---------|
| SSH no actiu | `sudo systemctl start ssh` |
| Port bloquejat pel firewall | `sudo ufw allow 2222` |
| Port canviat sense reiniciar | `sudo systemctl restart ssh` |

---

## Pàgina web mostra error 403 (Forbidden)

**Causa**: Permisos incorrectes als fitxers web.

```bash
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html
sudo chmod -R 644 /var/www/html/*.php
```

---

## Pàgina web mostra error 500 (Internal Server Error)

**Diagnosi:**

```bash
sudo tail -50 /var/log/apache2/error.log
```

Errors habituals:

- Sintaxi PHP incorrecta (`php -l fitxer.php`)
- `.htaccess` amb directives no permeses → verifica `AllowOverride All` al VirtualHost
- Mòdul PHP desactivat

---

## Espai de disc ple

```bash
df -h
du -sh /var/log/* | sort -h
sudo journalctl --disk-usage
```

Allibera espai:

```bash
sudo apt autoremove -y && sudo apt autoclean
sudo journalctl --vacuum-time=14d
sudo find /var/log -name "*.gz" -delete
```

!!! caution
    Abans d'eliminar logs, assegura't que no els necessites per a auditoria o diagnosi.
