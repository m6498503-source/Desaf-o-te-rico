# Solución para la Configuración de Red

## Problema
Actualmente, las máquinas virtuales de TechSolutions Inc. utilizan el modo de red **NAT (Network Address Translation)** en VirtualBox.  
Si bien este modo permite a las VMs acceder a internet, presenta varias limitaciones en un **entorno de desarrollo colaborativo**:

- **Falta de comunicación directa**: las VMs no pueden comunicarse entre sí fácilmente.  
- **Aislamiento de la red corporativa**: no se integran con los recursos internos de la empresa (servidores, impresoras, bases de datos).  
- **Dependencia de reglas de reenvío de puertos (port forwarding)**: complejo de administrar cuando hay múltiples servicios.  
- **Dificultad para pruebas colaborativas**: impide simular un entorno real de red compartida.  

---

## Propuesta
Se evaluaron los modos de red que ofrece VirtualBox:

- **NAT (Network Address Translation)**  
  - Pros: conexión a internet sin configuración adicional.  
  - Contras: aislamiento de la red local, sin comunicación directa entre VMs.  

- **Adaptador Puente (Bridged Adapter)**  
  - Pros: la VM se comporta como un dispositivo más dentro de la red física.  
  - Puede comunicarse con otras VMs, con el host y con dispositivos de la red corporativa.  
  - Contras: depende de la red física y de la disponibilidad de direcciones IP.  

- **Red Interna (Internal Network)**  
  - Pros: las VMs pueden comunicarse entre sí en una red privada.  
  - Contras: sin acceso a internet ni a la red corporativa.  

### Se recomienda
Para un entorno de desarrollo colaborativo, el modo **Puente (Bridged Adapter)** es el más adecuado, ya que:  
- Permite a las VMs comunicarse entre sí y con la red corporativa.  
- Facilita las pruebas de aplicaciones en condiciones más cercanas a un entorno de producción.  
- No requiere configuraciones complicadas de reenvío de puertos.  

---

## Ejemplo de Configuración de IP Estática con Netplan

Una vez configurada la VM en modo Puente en VirtualBox, se debe asignar una IP estática para garantizar estabilidad en la comunicación.  

### 1. Editar el archivo de Netplan
```bash
sudo nano /etc/netplan/01-netcfg.yaml
```
### 2. Configuramos la interfaz de red
```bash
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [192.168.1.50/24]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
```
### 3. Aplicacion de los cambios  
```bash
sudo netplan apply
```
### 4. Verificamos la configuracion   
```bash
ip addr show enp0s3
ping 192.168.1.1
```
