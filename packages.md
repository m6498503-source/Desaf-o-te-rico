# Solución para la Gestión de Paquetes

## Problema
Actualmente, los administradores de TechSolutions Inc. instalan los paquetes de software de forma **manual** en cada servidor.  
Este enfoque presenta varias limitaciones:

- **Inconsistencia en versiones**: diferentes equipos pueden terminar con versiones distintas del mismo software, lo que genera incompatibilidades.  
- **Pérdida de tiempo**: se repite el mismo proceso en múltiples servidores.  
- **Consumo de ancho de banda**: cada instalación descarga los paquetes desde internet, saturando la red corporativa.  
- **Mayor probabilidad de errores**: al depender de tareas manuales, aumenta la posibilidad de errores de configuración o dependencias rotas.  

---

## Propuesta
Configurar un **repositorio espejo (mirror local)** de los repositorios oficiales de Ubuntu/Debian mediante la herramienta **`apt-mirror`**.  

### Beneficios del mirror local
- **Consistencia**: todos los servidores utilizan las mismas versiones de software.  
- **Eficiencia**: las descargas se realizan desde la red interna, sin saturar la conexión a internet.  
- **Velocidad**: las instalaciones y actualizaciones son más rápidas al no depender de servidores externos.  
- **Control**: la empresa puede decidir qué paquetes están disponibles en su entorno.  

---

## Ejemplo de Configuración en Ubuntu/Debian

### 1. Instalar `apt-mirror`
```bash
sudo apt update
sudo apt install apt-mirror -y
```
