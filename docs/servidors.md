# Desplegament de Servidors

## Ubuntu
```bash
sudo apt update && sudo apt upgrade -y
```

## Xarxa
```bash
sudo nano /etc/netplan/00-installer-config.yaml
sudo netplan apply
```

## Instal·lació LAMP

=== "Apache"
    ```bash
    sudo apt install apache2 -y
    ```

=== "MySQL"
    ```bash
    sudo apt install mysql-server -y
    sudo mysql_secure_installation
    ```

=== "PHP"
    ```bash
    sudo apt install php libapache2-mod-php php-mysql -y
    ```

!!! tip
    Comprova Apache en el navegador amb la IP del servidor.

---

## Configuració de VirtualHost

Crea un VirtualHost per al teu domini o IP pública:

```bash
sudo nano /etc/apache2/sites-available/rickspain.conf
```

```apache
<VirtualHost *:80>
    ServerAdmin webmaster@rickspain.local
    ServerName rickspain.local
    DocumentRoot /var/www/html

    <Directory /var/www/html>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

```bash
sudo a2ensite rickspain.conf
sudo a2enmod rewrite
sudo systemctl reload apache2
```

---

## Configuració de PHP

Fitxer principal de configuració:

```bash
sudo nano /etc/php/8.x/apache2/php.ini
```

Valors recomanats per a producció:

| Paràmetre | Valor recomanat |
|-----------|----------------|
| `upload_max_filesize` | `20M` |
| `post_max_size` | `25M` |
| `memory_limit` | `256M` |
| `max_execution_time` | `60` |
| `display_errors` | `Off` |
| `log_errors` | `On` |

```bash
sudo systemctl restart apache2
```

---

## Verificació post-instal·lació

Comprova que tots els serveis executen correctament:

```bash
sudo systemctl status apache2
sudo systemctl status mysql
php -v
```

Crea un fitxer de prova PHP per confirmar la integració:

```bash
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
```

!!! warning
    Elimina `info.php` un cop verificat. Exposar phpinfo() en producció és un risc de seguretat.

```bash
sudo rm /var/www/html/info.php
```

---

## Llista de comprovació (Checklist)

- [ ] Ubuntu actualitzat
- [ ] Apache instal·lat i actiu
- [ ] MySQL instal·lat, securitzat i actiu
- [ ] PHP instal·lat i integrat amb Apache
- [ ] VirtualHost configurat
- [ ] Fitxer info.php eliminat
- [ ] Firewall activat (vegeu Seguretat)
