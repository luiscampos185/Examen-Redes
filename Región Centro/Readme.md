# Proyecto de Red Corporativa - Región Centro (CE)

Este repositorio contiene el diseño y configuración de la infraestructura de red para la sede central (Centro) de la empresa JuanMark. El proyecto implementa una arquitectura robusta enfocada en la gestión centralizada de servicios inalámbricos (WLC), seguridad profunda en Capa 2 y enrutamiento inter-regional.

## Descripción General

La Región Centro actúa como el nodo de interconexión principal. La topología gestiona el tráfico hacia las regiones remotas (Norte, Sur) y provee servicios a edificios corporativos. La red local (LAN) utiliza segmentación por VLANs, gestión inalámbrica y mecanismos de defensa contra ataques de suplantación (Spoofing/MITM).

## Tecnologías Implementadas

* **Router-on-a-Stick:** Enrutamiento InterVLAN centralizado mediante subinterfaces 802.1Q.
* **WLC (Wireless LAN Controller):** Gestión unificada de Puntos de Acceso (Lightweight APs).
* **DHCP:** Servidor configurado en el Router para gestión dinámica de direcciones.
* **Defense-in-Depth (L2):** Implementación conjunta de Port Security, DHCP Snooping y Dynamic ARP Inspection (DAI).
* **RIPv2:** Protocolo de enrutamiento dinámico para la WAN.
* **SSHv2:** Gestión remota con autenticación local.

## Información de Red

### VLANs Configuradas
La **VLAN 34** se utiliza como Nativa en enlaces troncales y para la gestión de infraestructura inalámbrica.

| ID | Nombre | Subred | Uso |
| :--- | :--- | :--- | :--- |
| **33** | CE_TI | 148.60.33.0/24 | Gestión TI / Servidores |
| **34** | CE_WLAN | 148.60.34.0/24 | Gestión WLC/APs (Nativa) |
| **35** | CE_VENTAS | 148.60.35.0/24 | Ventas |
| **36** | CE_COMPRAS | 148.60.36.0/24 | Compras |
| **37** | CE_PRACT | 148.60.37.0/24 | Practicantes |

### Direccionamiento Clave

| Dispositivo | Interfaz | Rol | IP |
| :--- | :--- | :--- | :--- |
| **Router_Centro** | G0/0.x | Gateway (Subinterfaces) | .33.1 - .37.1 |
| **WLC-Centro** | Mgmt | Controladora Wireless | 148.60.34.10 |
| **Router_Centro** | S0/2/0 | Enlace WAN | 148.60.200.18 |
| **Switches L2/L3** | Vlan34 | Gestión (SVI) | .34.6 - .34.9 |

## Detalles de Configuración

### Enrutamiento y DHCP
* **Router_Centro:** Actúa como Gateway predeterminado para todas las VLANs.
* **Pools DHCP:** Configurados con exclusión de las primeras 10 IPs para cada subred.

### Diseño Inalámbrico (WLC)
* **Modelo:** Cisco 2504 WLC.
* **Gestión:** VLAN 34 (Tráfico de control CAPWAP).
* **Mapeo de SSIDs:**
    * SSID *JuanMark-Ventas* -> Mapeado a interfaz lógica VLAN 35.
    * SSID *Practicantes* -> Mapeado a interfaz lógica VLAN 37.

### Seguridad (Defense-in-Depth)
* **Port Security:** Máximo 1 MAC por puerto (Sticky), acción por defecto.
* **DHCP Snooping:** Activo en VLANs 33-37. Uplinks confiables (Trust), acceso no confiable.
* **DAI (ARP Inspection):** Validación de correspondencia MAC-IP para prevenir Man-in-the-Middle.
* **SSHv2:** Acceso remoto seguro habilitado.

### Credenciales de Acceso

* **Usuario Local:** `ADMIN`
* **Password:** `123`
* **Dominio:** `JuanMark.com`
