# Trabajo Práctico Integrador - Computación Aplicada
**Universidad de Palermo**

## Integrantes del Grupo
- Juan Manuel Gonzalez Kapnik
- Santino Fassanella

## Descripción del Proyecto
Configuración completa de un servidor Debian con los siguientes servicios:
- SSH (autenticación por clave pública)
- Apache + PHP
- MariaDB
- Sistema de backups automatizado

## Estructura de Archivos

### Archivos Comprimidos
- `root.tar.gz` - Directorio /root
- `etc.tar.gz` - Configuraciones del sistema
- `opt.tar.gz` - Scripts personalizados
- `proc.tar.gz` - Información de particiones
- `www_dir.tar.gz` - Archivos del servidor web
- `backup_dir.tar.gz` - Directorio de backups
- `var.tar.gz.part*` - Directorio /var (splitteado)

### Para reconstruir /var
```bash
cat var.tar.gz.part* > var.tar.gz
tar -xzf var.tar.gz
```

## Configuraciones Implementadas

### 1. Entorno
- Hostname: TPServer
- Password root: palermo
- Red: IP estática 192.168.0.227/24

### 2. Servicios
- **SSH**: Puerto 22, autenticación por clave pública
- **Apache**: Servidor web en puerto 80, DocumentRoot: /www_dir
- **MariaDB**: Base de datos 'ingenieria' con usuario 'lcars'

### 3. Almacenamiento
- Disco adicional: 10GB
  - /dev/sdb1 (3GB) → /www_dir
  - /dev/sdb2 (5GB) → /backup_dir
- Montaje automático configurado en /etc/fstab

### 4. Backup
- Script: `/opt/scripts/backup_full.sh`
- Backups automáticos:
  - `/var/log` → Diario a las 00:00
  - `/www_dir` → Lunes, Miércoles, Viernes a las 23:00

## Instrucciones de Uso

### Conectarse por SSH
```bash
ssh -i clave_privada.txt root@192.168.0.227
```

### Acceder al sitio web
```
http://192.168.0.227
```

### Ejecutar backup manual
```bash
/opt/scripts/backup_full.sh /directorio/origen /backup_dir
```

## Notas Técnicas
- Sistema operativo: Debian GNU/Linux 11 (Bullseye)
- Kernel: 5.10.0-30-amd64
- Virtualización: VirtualBox 7.x
