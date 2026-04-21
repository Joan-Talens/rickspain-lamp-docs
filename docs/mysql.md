# Gestió de MySQL

## Accedir a MySQL

```bash
sudo mysql -u root -p
```

---

## Crear base de dades i usuari

```sql
CREATE DATABASE rickspain_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'rickspain_user'@'localhost' IDENTIFIED BY 'Contrasenya_Segura!';
GRANT ALL PRIVILEGES ON rickspain_db.* TO 'rickspain_user'@'localhost';
FLUSH PRIVILEGES;
```

!!! warning
    Substitueix `Contrasenya_Segura!` per una contrasenya robusta. Mai facis servir credencials per defecte en producció.

---

## Operacions bàsiques

```sql
SHOW DATABASES;
USE rickspain_db;
SHOW TABLES;
DESCRIBE nom_taula;
```

---

## Còpia de seguretat (Backup)

### Exportar una base de dades

```bash
mysqldump -u root -p rickspain_db > /backup/rickspain_db_$(date +%F).sql
```

### Restaurar una base de dades

```bash
mysql -u root -p rickspain_db < /backup/rickspain_db_2024-01-01.sql
```

### Automatitzar el backup diari (Cron)

```bash
crontab -e
```

Afegeix la línia següent per fer backup cada dia a les 2:00 AM:

```
0 2 * * * mysqldump -u root -pContrasenya rickspain_db > /backup/rickspain_$(date +\%F).sql
```

!!! tip
    Emmagatzema els backups en una ubicació externa al servidor (NAS, S3, etc.) per garantir la recuperació en cas de fallada de disc.

---

## Configuració de seguretat MySQL

```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

Paràmetres recomanats:

```ini
# Limita les connexions remotes (només localhost)
bind-address = 127.0.0.1

# Desactiva el plugin auth socket per a usuaris no root
default_authentication_plugin = mysql_native_password
```

```bash
sudo systemctl restart mysql
```

---

## Comprovar l'estat de MySQL

```bash
sudo systemctl status mysql
sudo mysqladmin -u root -p status
```

---

## Llista de comprovació (Checklist)

- [ ] Base de dades creada amb charset utf8mb4
- [ ] Usuari de l'aplicació creat (no root)
- [ ] Permisos mínims assignats
- [ ] Backup automatitzat configurat
- [ ] `bind-address` limitat a localhost
- [ ] Contrasenya de root canviada
