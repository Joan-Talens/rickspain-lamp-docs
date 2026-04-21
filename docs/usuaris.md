# Gestió d’Usuaris

## Usuaris

### admin-web
```bash
sudo adduser admin-web
sudo usermod -aG www-data admin-web
```

### db-backup
```bash
sudo adduser db-backup
```

!!! warning
    No utilitzar root per tasques diàries.

## Política
- Principi de mínim privilegi  
- Separació de rols  

---

## Gestió de Sudo

Concedeix permisos sudo només als usuaris que ho necessitin:

```bash
sudo visudo
```

Exemple per a un administrador específic:

```
joan ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart apache2
```

!!! warning
    Evita concedir `NOPASSWD: ALL` en entorns de producció.

---

## Permisos de directoris web

Assigna correctament la propietat dels fitxers del servidor web:

```bash
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html
```

Per a fitxers que requereixen escriptura (uploads, cache):

```bash
sudo chmod -R 775 /var/www/html/uploads
```

---

## Política de contrasenyes

Instal·la el mòdul de qualitat de contrasenyes:

```bash
sudo apt install libpam-pwquality -y
sudo nano /etc/security/pwquality.conf
```

Configuració mínima recomanada:

```
minlen = 12
dcredit = -1
ucredit = -1
lcredit = -1
ocredit = -1
```

---

## Auditoria d'usuaris

Llista tots els usuaris del sistema:

```bash
cut -d: -f1 /etc/passwd
```

Comprova qui té accés sudo:

```bash
grep -Po '^sudo.+:\K.*$' /etc/group
```

Consulta els últims accessos:

```bash
last -n 20
```

!!! info
    Revisa periòdicament els usuaris inactius i elimina'ls si ja no es necessiten.
