Proyecto de Red Nacional - JuanMark.com

Descripción del Proyecto
Este proyecto consiste en el diseño e implementación de la infraestructura de red para la compañía **JuanMark**. El objetivo es interconectar diferentes regiones geográficas de México mediante una topología WAN, asegurando servicios de alta disponibilidad, seguridad y convergencia.

El diseño global abarca la red `148.60.0.0/16` e implementa **Dual Stack (IPv4 e IPv6)**[cite: 16, 42].

Topología: Región Noroeste
Este repositorio contiene la configuración específica de la Región Noroeste, la cual actúa como un punto crítico de la red al albergar la conexión a **Internet** y funcionar como el **Servidor VTP** maestro para toda la organización.

Características de la Región
* **Rol VTP:** Server (Administra las VLANs de todas las regiones: Centro, Noreste, Sureste).
* **Protocolo de Ruteo:** RIPv2 y RIPng (IPv6).
* **Direccionamiento:** Dual Stack (IPv4 / IPv6) con prefijo global `2006:AFEA:B0CA::/48`.


## Tecnologías Implementadas
De acuerdo a los requerimientos técnicos, se han configurado los siguientes servicios:

1.  **VTP (Vlan Trunking Protocol):**
    * Modo: **Server**
    * Dominio: `juanmark`
    * Versión: 2
    * *Todas las VLANs de la organización (33-37, 65-68, 97-100) se crean aquí.*

2.  **Seguridad de Capa 2:**
    * **Trunks:** Configurados sin negociación (`switchport nonegotiate`) para evitar DTP.
    * **SSH:** Habilitado en todos los dispositivos para gestión remota segura (v2).
    * **Seguridad de Puertos:** Restricción de MACs en puertos de acceso.

3.  **Servicios de Red:**
    * **DHCPv4:** Pools configurados para asignación dinámica de IPs en cada VLAN.
    * **Ruteo Inter-VLAN:** Configurado mediante *Router-on-a-Stick* en el Gateway Noroeste.

 Instrucciones de Despliegue (Multiusuario)
Para integrar esta región con el resto de la topología nacional:

1.  **Requisitos:** Cisco Packet Tracer 8.x o superior.
2.  **Conexión VPN:** Asegurarse de estar conectado a la VPN del equipo para la funcionalidad Multiusuario.
3.  **Pasos:**
    * Abrir el archivo `.pkt` de la región Noroeste.
    * Verificar que el estado del puerto "Multiusuario" esté en *Listening*.
    * Coordinar con las regiones **Centro** y **Noreste** para establecer el enlace en las IPs WAN designadas.

*Proyecto para la materia de conmutación: JuanMark.com*

