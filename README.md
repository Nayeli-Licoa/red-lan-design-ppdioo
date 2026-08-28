# Diseño e Implementación de Red LAN — Metodología PPDIOO

![Universidad de Guayaquil](https://img.shields.io/badge/Universidad-Universidad%20de%20Guayaquil-blue.svg)
![Curso](https://img.shields.io/badge/Materia-Dise%C3%B1o%20de%20Red-orange.svg)
![Cisco](https://img.shields.io/badge/Simulaci%C3%B3n-Cisco%20Packet%20Tracer-1BA0D7.svg)

Proyecto académico de la materia **Diseño de Red** en la Universidad de Guayaquil. Consiste en el diseño estructurado y la simulación de una red LAN real para el **Cuerpo de Bomberos del Cantón Valencia** (Provincia de Los Ríos, Ecuador), aplicando la metodología **PPDIOO** (Prepare, Plan, Design, Implement, Operate, Optimize) y realizando un levantamiento de información en sitio.

---

## Equipo del Proyecto y Rol Individual

Proyecto grupal (5 integrantes) desarrollado en la materia **Diseño de Red**, Universidad de Guayaquil.

### Mi responsabilidad específica en el proyecto:
- **Selección y justificación técnica de dispositivos (Fase Design):** evaluación e integración de routers Cisco 2911 (principal) y Cisco 2811 (interno), switch Cisco 2960-24TT, y terminales VoIP (teléfonos IP Cisco 7960 y radios base Home-VoIP).
- **Revisión y corrección de la simulación en Packet Tracer:** identifiqué falencias en la topología inicial construida por el equipo (falta de segmentación lógica, sin VLANs) y corregí la simulación hasta lograr una configuración funcional con VLANs, subinterfaces 802.1Q (Router-on-a-Stick) y DHCP por subred.

---

## Desarrollo por fases PPDIOO

### 1️⃣ Fase Prepare (Preparar)
- **Caso de estudio:** Cuerpo de Bomberos del Cantón Valencia (25 empleados en total).
- **División operativa:** Área Administrativa (4 PCs, 2 teléfonos) y Área Operativa (4 radios base, 3 radios de vehículo, 8 radios portátiles, 2 teléfonos convencionales).
- **Requisitos críticos:** alta velocidad, estabilidad y cero interrupciones en la transmisión durante situaciones de emergencia.
- **Restricción presupuestaria:** presupuesto municipal limitado; el diseño prioriza maximizar la vida útil del hardware existente y garantizar disponibilidad con equipos Cisco estándar.

### 2️⃣ Fase Plan (Planificar)
- **Levantamiento de requerimientos:** conectividad simultánea para ~21 dispositivos finales.
- **Prioridades técnicas:**
  - Separación del tráfico administrativo y operativo por seguridad y rendimiento.
  - Priorización de calidad de servicio (CoS 802.1p) para baja latencia en llamadas VoIP de emergencia.
  - Definición de esquemas de respaldo (canales de contingencia: telefonía convencional, celular, radio).

### 3️⃣ Fase Design (Diseñar)

**Topología lógica y jerárquica:**

`ISP / Red Externa` ➔ **Router Principal (Cisco 2911)** ➔ **Router Interno (Cisco 2811 — Inter-VLAN Routing)** ➔ **Switch Central (Cisco 2960)** ➔ `Dispositivos finales`

**Esquema de segmentación (VLANs) y direccionamiento IP:**

| VLAN | Nombre | Propósito | Red / Máscara | Gateway | Puertos Switch |
|:---:|:---:|:---|:---:|:---:|:---:|
| **10** | `ADMIN` | PCs y VoIP administrativos | `192.168.10.0/24` | `192.168.10.1` | `Fa0/2 - Fa0/7` |
| **20** | `OPERAT` | Radios VoIP y voz operativa | `192.168.20.0/24` | `192.168.20.1` | `Fa0/8 - Fa0/13` |
| **WAN** | `LINK` | Interconexión entre routers | `10.0.0.0/30` | N/A | `Gi0/0 - Gi0/1` |

**Protocolos aplicados en el diseño:**
- **Capa 2:** IEEE 802.1Q (trunking), STP con `portfast` en puertos de acceso, IEEE 802.1p / CoS (prioridad de tráfico VoIP).
- **Capa 3:** subinterfaces `dot1Q`, enrutamiento estático, servidor DHCP por pool de VLAN.

### 4️⃣ Fase Implement (Implementar)

Debido a que el alcance del proyecto fue de carácter académico y de simulación en Cisco Packet Tracer, la fase de implementación se estructuró como una **propuesta técnica teórica**, sin despliegue físico real. El plan documentado cubre 6 etapas: preparación del entorno, instalación física de dispositivos, cableado y energización, configuración de infraestructura, pruebas de conectividad y documentación final, proyectado a un tiempo estimado de **4 a 6 semanas**.

---

## Mejoras propuestas

Firewall perimetral, redundancia de enlaces (HSRP/VRRP), switch multicapa, ACLs entre VLANs, servidor de monitoreo (Zabbix/PRTG/Nagios), cableado categoría 6A y autenticación 802.1X.

## Contenido de este repositorio

- Capturas del diseño lógico y físico de la red (Cisco Packet Tracer)
- Esquema de direccionamiento IP y tabla de VLANs
- Plan estimado de implementación con cronograma (diagrama de Gantt)

##  Aprendizajes

Aplicar una metodología formal de diseño de redes (PPDIOO) de principio a fin, levantar requisitos reales en una institución, diseñar segmentación con VLANs y direccionamiento IP, y resolver problemas de configuración concretos en una simulación hasta lograr su correcto funcionamiento.
