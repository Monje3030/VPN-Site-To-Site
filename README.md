# 🛡️ Implementación de VPN Site-To-Site - Fortinet

## 📖 1. Descripción del Proyecto
Este laboratorio consiste en la interconexión segura de dos infraestructuras de red local (**Sede BRANCH** y **Sede HQ**) a través de un túnel **IPsec VPN**. El direccionamiento se ha configurado utilizando la matrícula **2023-0331** para personalizar los segmentos WAN y garantizar un entorno de pruebas controlado.

## 🕸️ 2. Topología de Red
La red utiliza dos Firewalls FortiGate (6.4.x / 7.x), un router Cisco como ISP y nodos VPCS para pruebas de end-to-end.

<img width="1119" height="866" alt="image" src="https://github.com/user-attachments/assets/eec58aad-62bb-479b-a468-d870ec9cc9c9" />

### 📋 Tabla de Direccionamiento
| Dispositivo | Interfaz | Dirección IP | Gateway |
| :--- | :--- | :--- | :--- |
| **PC-BRANCH** | eth0 | `192.168.33.10/24` | `192.168.33.1` |
| **FGT-BRANCH** | port2 (LAN) | `192.168.33.1/24` | N/A |
| **FGT-BRANCH** | port1 (WAN) | `10.33.1.1/30` | `10.33.1.2` |
| **ISP-Router** | Gi0/0 - Gi0/1 | `10.33.1.2 - 10.33.2.2` | N/A |
| **FGT-HQ** | port1 (WAN) | `10.33.2.1/30` | `10.33.2.2` |
| **FGT-HQ** | port2 (LAN) | `192.168.3.1/24` | N/A |
| **PC-HQ** | eth0 | `192.168.3.10/24` | `192.168.3.1` |

---

## ⚙️ 3. Configuración del Túnel IPsec

### Fase 1 (IKE Phase 1)
Se definieron los parámetros de intercambio de llaves y autenticación:
- **Encryption/Auth:** DES / SHA256  
- **DH Group:** 2  
- **Keylife:** 28,800 sec  


<img width="2324" height="287" alt="image" src="https://github.com/user-attachments/assets/dfe478ab-bc8f-4839-b8d5-9585c7421457" />


<img width="754" height="250" alt="image" src="https://github.com/user-attachments/assets/88503c3e-af13-426b-a7a5-2c3785654c52" />


<img width="1147" height="703" alt="image" src="https://github.com/user-attachments/assets/cc68ac4b-5e1e-4c1a-a742-892e6fad7a89" />

## Video demostrativo

https://youtu.be/aVlomPpslnc

### Demostración de que el tráfico viaja de forma encapsulada. El paquete salta del Gateway local directamente al destino remoto a través de la interfaz de túnel, omitiendo el ruteo público del ISP.

<img width="952" height="129" alt="image" src="https://github.com/user-attachments/assets/547a3f77-1d39-4dda-bf11-bfc1b539ab0e" />
