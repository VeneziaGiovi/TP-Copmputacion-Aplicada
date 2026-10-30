# TP Integrador - Computación Aplicada (CDA-101)

Universidad de Palermo - Segundo parcial

## Integrantes
- Valentino Arias Giovi - 0151758
- Ivan Rago - Legajo

## Infraestructura
Máquina virtual Debian 11 (bullseye) en VirtualBox, hostname `TPServer`, IP estática `192.168.1.100` en modo puente.

| Servicio | Puerto | Detalle |
|---|---|---|
| SSH | 22 | Acceso de root solo con clave pública |
| Apache + PHP 7.4 | 80 | Sirve `index.php` y `logo.png` desde `/www_dir` |
| MariaDB | 3306 (solo local) | Base `ingenieria`, usuario `lcars` |

Almacenamiento: disco adicional de 10 GB (`sdc`) con dos particiones ext4 tipo 83, `sdc1` (3 GB) en `/www_dir` y `sdc2` (6 GB) en `/backup_dir`, montadas automáticamente por UUID desde `/etc/fstab`.

Backups: script `/opt/scripts/backup_full.sh`, programado con cron:
- Todos los días a las 00:00: `/var/log`
- Lunes, miércoles y viernes a las 23:00: `/www_dir`

## Contenido del repositorio
| Archivo | Descripción |
|---|---|
| root.tar.gz | Directorio /root |
| etc.tar.gz | Directorio /etc (configuración del sistema) |
| opt.tar.gz | Directorio /opt (incluye el script de backup) |
| proc.tar.gz | Directorio /proc (sin /proc/kcore) |
| www_dir.tar.gz | Partición /www_dir (sitio web) |
| backup_dir.tar.gz | Partición /backup_dir (backups generados) |
| var.tar.gz.part_aa a part_ad | Directorio /var dividido en 4 partes de 10 MB |
| diagrama_topologico.png | Diagrama topológico de la infraestructura |

## Reconstruir /var
```
cat var.tar.gz.part_* > var.tar.gz
tar -xzf var.tar.gz
```
