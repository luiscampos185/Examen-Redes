 Topología de Red Empresarial JuanMark (Región Sureste)

 Descripción del Proyecto

Este repositorio aloja la configuración y topología de red de la Región Sureste para la empresa JuanMark, diseñada en Cisco Packet Tracer. El objetivo principal es simular un entorno de red empresarial jerárquico, robusto y altamente disponible, implementando soluciones de redundancia de gateway, agregación de enlaces, enrutamiento dinámico y seguridad de acceso.

La topología está estructurada con una Capa de Distribución redundante y una Capa de Acceso segmentada mediante VLANs.

---

Estructura de la Topología y Requisitos Cumplidos

Segmentación de VLANs (Región Sureste)

| VLAN ID | Nombre | Prefijo de Red | Función |
| :---: | :--- | :--- | :--- |
| **65** | Ventas | 148.60.65.0/24 | Acceso de usuarios y dispositivos de Ventas. |
| **66** | Gestión TI | 148.60.66.0/24 | Gestión de infraestructura (WLC, Routers, Switches). |
| **67** | Compras | 148.60.67.0/24 | Acceso de usuarios y dispositivos de Compras. |
| **68** | MKT | 148.60.68.0/24 | Acceso de usuarios y dispositivos de Marketing. |

Protocolos Implementados

| Protocolo | Dispositivos | Propósito |
| :--- | :--- | :--- |
| **HSRP** | Routers Itzamná / Yum Kaax | Redundancia de Gateway (Failover automático). |
| **RIPv2** | Routers | Enrutamiento dinámico entre redes. |
| **VTP** | Switches (Server/Client) | Propagación centralizada de las VLANs. |
| **EtherChannel (PAgP)** | Switches de Distribución | Agregación de enlaces para mayor ancho de banda y redundancia. |
| **WLC** | Controlador y APs | Acceso inalámbrico segmentado y centralizado. |
| **SSH** | Global | Acceso seguro a la línea de comandos de todos los dispositivos. |

---

 Credenciales de Acceso

**¡Importante!** Se requiere un usuario y contraseña para acceder a la línea de comandos de todos los Routers y Switches, de acuerdo con el requisito de seguridad SSH.

| Dispositivo | Usuario | Contraseña |
| :--- | :--- | :--- |
| **Routers (Itzamná, Yum Kaax)** | `admin` | `Cisco123` |
| **Switches** | `admin` | `Cisco123` |

---

Instrucciones de Uso

Para explorar la topología y verificar el correcto funcionamiento de los protocolos:

1.  **Clonar el repositorio:** `git clone https://aws.amazon.com/es/what-is/repo/`
2.  **Abrir Cisco Packet Tracer** (Versión 8.x o superior).
3.  **Abrir el archivo `.pkt`** de la Región Sureste.
4.  **Verificar la Conectividad (Capa 3):**
    * Utilizar la **PC Cableada de Ventas** (IP estática: `148.60.65.11`).
    * Hacer `ping` al Gateway (HSRP VIP: `148.60.65.1`).
    * Hacer `ping` a la red de gestión (Router: `148.60.66.3`).
5.  **Verificar la Seguridad (SSH):**
    * Desde la PC de Ventas, acceder al router de respaldo: `ssh -l admin 148.60.66.3` (Contraseña: `Cisco123`).
6.  **Revisar Configuración:** Entrar al CLI de cualquier dispositivo y usar comandos como `show run`, `show standby brief`, y `show etherchannel summary`.


 Archivos del Proyecto

* **Topología:** `JuanMark-Sureste.pkt`
* **Scripts de Configuración:** (Ver carpetas del repositorio, que contienen scripts limpios por dispositivo).




**Edgar Alexis**
