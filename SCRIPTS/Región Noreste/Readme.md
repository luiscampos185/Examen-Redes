# Proyecto de Red Corporativa - Región Noreste (NE)

Este repositorio contiene el diseño y configuración de la infraestructura de red para la sucursal Noreste de la empresa JuanMark. El proyecto implementa una arquitectura jerárquica enfocada en la alta disponibilidad, seguridad y segmentación de servicios.

## Descripción General

La topología conecta con tres regiones externas (Centro, Noroeste, Sureste) mediante enlaces WAN. La red local (LAN) utiliza redundancia de puerta de enlace, prevención de bucles de capa 2 y distribución dinámica de direcciones IP.

## Tecnologías Implementadas

* **HSRP:** Redundancia de primer salto con balanceo de roles (Activo/Standby).
* **Rapid PVST+:** Árbol de expansión por VLAN para balanceo de carga de enlaces.
* **DHCP:** Servidor centralizado en switch de distribución.
* **Port Security:** Restricción de acceso físico en puertos de usuario.
* **SSHv2:** Gestión remota cifrada.
* **Wireless:** Acceso inalámbrico mediante Access Point autónomo.

## Información de Red

### VLANs Configuradas
La VLAN 97 se utiliza como Nativa en enlaces troncales.

| ID | Nombre | Subred | Uso |
| :--- | :--- | :--- | :--- |
| **97** | NE_TI | 148.60.97.0/24 | Gestión (Nativa) |
| **98** | NE_VENTAS | 148.60.98.0/24 | Ventas |
| **99** | NE_COMPRAS | 148.60.99.0/24 | Compras |
| **100** | NE_SERVICIOS | 148.60.100.0/24 | Servidores |

### Direccionamiento Clave

| Dispositivo | Interfaz | Rol | IP | Gateway HSRP |
| :--- | :--- | :--- | :--- | :--- |
| **LaSilla** | G0/0.x | Router Activo | .2 | .1 |
| **LaVaca** | G0/1.x | Router Standby | .3 | .1 |
| **SW2** | SVI | Servidor DHCP | .4 | .1 |
| **ElCabrito** | S0/2/0 | Borde WAN | .13 | N/A |

## Detalles de Configuración

1.  **Redundancia HSRP:**
    * **Router LaSilla:** Configurado con prioridad 110 (Activo).
    * **Router LaVaca:** Configurado con prioridad 100 (Standby).
    * **Preempt:** Habilitado para recuperación automática.

2.  **Topología STP:**
    * **Switch 3:** Root Bridge para VLANs 97, 98 y 99.
    * **Switch 4:** Root Bridge para VLAN 100.

3.  **Seguridad:**
    * Puertos de acceso limitados a 1 dirección MAC (sticky).
    * Acción de violación: Shutdown.
    * Acceso administrativo exclusivo por SSH.

## Credenciales de Acceso

* **Usuario:** ADMIN
* **Password:** cisco111
* **Enable Secret:** cisco123
* **Dominio:** juanmark.com

## Instrucciones de Validación

1.  Abrir el archivo `JuanMark-Noreste.pkt` en Cisco Packet Tracer.
2.  Verificar que las PCs obtengan direccionamiento IP por DHCP.
3.  Comprobar conectividad mediante ping hacia la Gateway Virtual (`148.60.XX.1`).
4.  Validar redundancia apagando la interfaz LAN del router LaSilla y confirmando la continuidad del servicio a través de LaVaca.
