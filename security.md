# Solución para la Seguridad

## Problema
La red actual de TechSolutions Inc. presenta varias vulnerabilidades críticas debido a la falta de controles centralizados y estandarizados de seguridad:

- **Acceso no controlado a servicios internos**: cualquier dispositivo en la red podría intentar conectarse a servicios sensibles sin restricciones.  
- **Ausencia de un firewall centralizado**: no existen políticas claras que regulen qué tráfico está permitido o bloqueado.  
- **Exposición a ataques externos**: los servicios carecen de filtros adecuados, lo que aumenta el riesgo de intrusiones.  
- **Falta de segmentación y monitoreo**: dificulta identificar accesos indebidos o patrones sospechosos.  

Estas debilidades comprometen la **confidencialidad, integridad y disponibilidad** de los sistemas de la empresa.  

---

## Propuesta
Implementar **UFW (Uncomplicated Firewall)** en los servidores de TechSolutions Inc. como herramienta de control de acceso.  

### Beneficios de UFW
- **Simplicidad**: interfaz clara para la administración de reglas de firewall.  
- **Estandarización**: mismo esquema de reglas en todos los servidores.  
- **Mayor seguridad**: solo se permite el tráfico estrictamente necesario.  
- **Control granular**: posibilidad de permitir acceso únicamente desde direcciones IP autorizadas.  

---

## Ejemplo de Implementación con UFW

### 1. Instalar UFW (si no está instalado)
```bash
sudo apt update
sudo apt install ufw -y
```
### 2. Definir politicas por defecto
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```
### 3. Permitimos solo el acceso de SSH desde direcciones IP especificas
```bash
sudo ufw allow from 192.168.1.100 to any port 22
```
### 4. Denegamos el trafico SSh no autorizado
```bash
sudo ufw deny 22
```
### 5. Permitimos los servicios esenciales como HTTP y HTTPS
```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```
### 6. Activamos UFW
```bash
sudo ufw enable
```
### 7. Verificar estado y reglas aplicadas
```bash
sudo ufw status verbose
```
