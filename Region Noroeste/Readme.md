# Proyecto de Red Corporativa - Región Noroeste (NW)

Este repositorio contiene el diseño y configuración de la infraestructura de red para la sucursal Noroeste. El proyecto implementa una arquitectura basada en la alineación lógica de segmentos IP con VLANs, soportando IPv4/IPv6 y enrutamiento centralizado.

## Descripción General

La topología conecta con tres regiones externas (Centro, Noreste, Sureste) e Internet mediante enlaces seriales. La red local (LAN) utiliza un diseño de Router-on-a-Stick para el enrutamiento entre VLANs, con gestión centralizada de dominios de difusión y seguridad en capa de acceso.

## Tecnologías Implementadas

* **Dual Stack (IPv4/IPv6):** Implementación simultánea de protocolos de direccionamiento.
* **Router-on-a-Stick:** Enrutamiento InterVLAN mediante subinterfaces lógicas.
* **VTP:** Protocolo de Trunking de VLANs en modo Servidor.
* **DHCP:** Servidor configurado en el Router para asignación dinámica.
* **Port Security:** Restricción de acceso físico con aprendizaje "Sticky".
* **SSH:** Gestión remota cifrada con llaves RSA.
* **RIP:** Enrutamiento dinámico para convergencia con otras regiones.

## Información de Red

### VLANs Configuradas
La VLAN 9 se utiliza como Nativa en enlaces troncales y para gestión.

| ID | Nombre | Subred IPv4 | Prefijo IPv6 | Uso |
| :--- | :--- | :--- | :--- | :--- |
| **9** | NW_TI | 148.60.9.0/24 | ...:9::/64 | Gestión TI (Nativa) |
| **5** | NW_MKT | 148.60.5.0/24 | ...:5::/64 | Marketing |
| **6** | NW_VENTAS | 148.60.6.0/24 | ...:6::/64 | Ventas |
| **7** | NW_COMPRAS | 148.60.7.0/24 | ...:7::/64 | Compras |

### Direccionamiento Clave

| Dispositivo | Interfaz | Rol | IP Gateway |
| :--- | :--- | :--- | :--- |
| **R1 (Router)** | G0/0.x | Gateway / DHCP | .1 (Subinterfaces) |
| **SW3** | VLAN 9 | VTP Server | .4 |

## Detalles de Configuración

1.  **Enrutamiento InterVLAN:**
    * **Router R1:** Configurado con encapsulamiento dot1q en subinterfaces (G0/0.5, .6, .7, .9).
    * **Direccionamiento:** El 3er octeto (IPv4) y 4to hexteto (IPv6) coinciden con el ID de VLAN para facilitar administración.

2.  **Gestión de VLANs (VTP):**
    * **Switch 3:** Modo Server.
    * **Switches 1, 2, 4:** Modo Client.
    * **Dominio:** NOROESTE.

3.  **Seguridad de Puertos:**
    * Puertos de acceso limitados a 1 dirección MAC.
    * Aprendizaje de direcciones: Sticky.
    * Acción de violación: Shutdown.

4.  **Enlaces Troncales:**
    * Modo estático (`mode trunk`) sin negociación DTP.
    * Filtrado de VLANs activado (Allowed VLAN 5,6,7,9).

## Credenciales de Acceso

* **Usuario:** ADMIN
* **Password:** cisco111
* **Enable Secret:** cisco123
* **Dominio:** juanmarket.com
* **VTP Password:** cisco123

## Instrucciones de Validación
1.  Abrir el archivo `JuanMark-Noreste.pkt` en Cisco Packet Tracer.
2.  Verificar que las PCs obtengan IP y DNS mediante DHCP (`ipconfig /all`).
3.  Comprobar conectividad mediante ping a las regiones remotas:
    * Noreste: `148.60.98.103`.
    * Sureste: `148.60.65.8`.
    * Centro: `148.60.33.12`.
4.  Validar acceso seguro SSH al Switch VTP Server (`148.60.9.4`).
5.  Confirmar bloqueo de puerto conectando un dispositivo no autorizado (Port Security).
