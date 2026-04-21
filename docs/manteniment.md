# Manteniment del Sistema

## Actualitzacions del sistema

Executa actualitzacions periòdicament (recomanat setmanalment):

```bash
sudo apt update && sudo apt upgrade -y
sudo apt autoremove -y
sudo apt autoclean
```

---

## Monitoratge de recursos

### CPU i memòria en temps real

```bash
top
# O amb una vista més amigable:
htop
```

### Ús de disc

```bash
df -h
du -sh /var/www/html
du -sh /var/log/*
```

!!! warning
    Si `/var/log` ocupa molt espai, revisa la rotació de logs (`logrotate`).

### Processos actius

```bash
ps aux --sort=-%mem | head -20
```

---

## Gestió de logs (Logrotate)

Comprova la configuració de rotació de logs d'Apache:

```bash
cat /etc/logrotate.d/apache2
```

Forçar rotació manual:

```bash
sudo logrotate -f /etc/logrotate.conf
```

---

## Reinici de serveis

```bash
sudo systemctl restart apache2
sudo systemctl restart mysql
sudo systemctl restart ssh
```

Comprova que tots els serveis s'inicien automàticament en reiniciar el sistema:

```bash
sudo systemctl is-enabled apache2
sudo systemctl is-enabled mysql
sudo systemctl is-enabled ssh
```

Per activar l'inici automàtic:

```bash
sudo systemctl enable apache2
sudo systemctl enable mysql
```

---

## Neteja de fitxers temporals

```bash
sudo find /tmp -type f -atime +7 -delete
sudo journalctl --vacuum-time=30d
```

---

## Comprovació de ports oberts

```bash
sudo ss -tulnp
sudo netstat -tulnp
```

---

## Calendari de manteniment recomanat

| Freqüència | Tasca |
|------------|-------|
| Diari | Revisar logs d'error d'Apache i MySQL |
| Setmanal | `apt update && apt upgrade`, verificar backups |
| Mensual | Revisar usuaris actius, comprovar espai de disc |
| Trimestral | Revisar regles de firewall, renovar certificats SSL |

!!! info
    Documenta sempre els canvis realitzats durant el manteniment indicant data, responsable i descripció del canvi.
