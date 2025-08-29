# Solución para el Almacenamiento

## Problema
El servidor de archivos principal de TechSolutions Inc. presenta fallos de disco que generan **pérdida de datos**.  

Este escenario es crítico porque:
- Los datos son un **activo esencial** para la continuidad de la empresa.  
- La pérdida de información afecta la **productividad de los equipos de trabajo** y la **confianza de los clientes**.  
- La recuperación de datos perdidos implica **altos costos económicos y de tiempo**.  

En un entorno corporativo, la ausencia de redundancia convierte cualquier disco en un **punto único de fallo (SPOF)** que compromete toda la operación.

---

## Propuesta
Implementar un sistema de almacenamiento con **RAID 5**, compuesto por un mínimo de **3 discos duros**.  

### Justificación de RAID 5
- **Redundancia con paridad distribuida**: en caso de que un disco falle, los datos se reconstruyen automáticamente a partir de la información de paridad.  
- **Eficiencia**: aprovecha mejor la capacidad que RAID 1 (solo se pierde el equivalente a un disco en espacio).  
- **Escalabilidad**: permite agregar discos adicionales con relativa facilidad.  
- **Costo/beneficio**: balance ideal entre seguridad, capacidad y rendimiento para una empresa mediana como TechSolutions Inc.  

### Comparación rápida
- **RAID 1**: Duplicación de discos, alta seguridad, pero solo aprovecha el 50% de la capacidad.  
- **RAID 10**: Excelente rendimiento y redundancia, pero requiere mínimo 4 discos → mayor costo.  
- **RAID 5**: Seguridad + capacidad aprovechada (N-1 discos) + buen rendimiento → mejor relación costo-beneficio.  

---

## Ejemplo de Implementación en Linux (con `mdadm`)
Mdadm es una línea de comandos en sistemas operativos Linux para administrar arreglos de discos de software RAID

### 1. Instalar `mdadm`
```bash
sudo apt update
sudo apt install mdadm -y
```
### 2. Creamos un RAID 5 
```bash
sudo mdadm --create --verbose /dev/md0 --level=5 --raid-devices=3 /dev/sdb /dev/sdc /dev/sdd
```
### 3. Verificamos el estado del RAID
```bash
cat /proc/mdstat
```
### 4. Guardamos la configuracion
```bash
sudo mdadm --detail --scan >> /etc/mdadm/mdadm.conf
```
### 5. Creamos un sistema de archivos en el RAID
```bash
sudo mkfs.ext4 /dev/md0
```
### 6. Montamos el RAID en un directorio
```bash
sudo mkdir -p /mnt/raid5
sudo mount /dev/md0 /mnt/raid5
```
### 7. Configuramos el montaje automatico
```bash
/dev/md0   /mnt/raid5   ext4   defaults   0   0
```
