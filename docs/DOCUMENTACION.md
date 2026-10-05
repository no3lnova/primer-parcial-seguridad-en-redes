# Documentación del laboratorio

## Datos académicos

| Campo | Información |
|---|---|
| Estudiante | Noel Elias Nova Vargas |
| Matrícula | 20242293 |
| Institución | Instituto Tecnológico de las Américas (ITLA) |
| Asignatura | Seguridad en Redes |
| Evaluación | Primer Parcial |

## 1. Propósito

Documentar el laboratorio de Seguridad en Redes en el que se emplea un firewall FortiGate para segmentar redes por VLAN, aplicar políticas de tráfico, utilizar NAT y controlar el acceso a servidores y destinos definidos mediante FQDN.

## 2. Objetivos

- Registrar la topología y el direccionamiento configurados.
- Documentar las políticas identificadas en el equipo FortiGate.
- Dejar evidencia verificable de las pruebas de acceso y bloqueo.
- Mantener en el repositorio capturas, respaldos saneados y video de demostración.

## 3. Componentes y topología

Se conoce un FortiGate-VM64-KVM en versión 7.0.9, identificado como **FGT-1**, con un enlace hacia el **ISP** y redes internas separadas en VLAN 10, 20 y 30. En la VLAN de servidores se identifican un Web Server y un DB-Server.

```text
                         ISP
                          |
                 Enlace 203.0.113.0/30
                          |
                  FortiGate FGT-1
                 FortiGate-VM64-KVM
                      v7.0.9
                    /    |     \
             VLAN 10  VLAN 20  VLAN 30
               USR      ADM      SRV
                                /   \
                       Web Server   DB-Server
                       10.229.3.194 10.229.3.195
```


## 4. Plan de direccionamiento conocido

| Segmento / equipo | Red o dirección | Observaciones |
|---|---:|---|
| VLAN 10 — USR | `10.229.3.0/25` | Rango de red informado |
| VLAN 20 — ADM | `10.229.3.128/26` | Rango de red informado |
| VLAN 30 — SRV | `10.229.3.192/28` | Contiene los servidores indicados |
| Web Server | `10.229.3.194` | VLAN 30 — SRV, según el plan informado |
| DB-Server | `10.229.3.195` | VLAN 30 — SRV, según el plan informado |
| Enlace FortiGate–ISP | `203.0.113.0/30` | Direcciones de interfaz por confirmar |

Las direcciones de gateway y las máscaras individuales de host no se agregan porque no se han confirmado por captura o archivo de configuración.

## 5. Plataforma

- **Producto:** FortiGate-VM64-KVM.
- **Versión:** 7.0.9.
- **Nombre del equipo:** FGT-1.
- **Entorno de virtualización:** KVM, de acuerdo con el nombre de la imagen informado.

## 6. Políticas, NAT y objetos

Se proporcionaron los siguientes nombres y propósitos generales. Registra los parámetros exactos (interfaces, origen, destino, servicio, acción, NAT, estado y orden) a partir de la GUI o de la configuración exportada.

| Elemento | Propósito conocido | Parámetros por verificar |
|---|---|---|
| `VLAN10-INTERNET` | Política de VLAN 10 hacia Internet | Interfaces, servicios, acción, NAT y contadores |
| `VLAN20-INTERNET` | Política de VLAN 20 hacia Internet | Interfaces, servicios, acción, NAT y contadores |
| `USUARIOS-WEB` | Política de usuarios hacia el Web Server | Origen, servicio/puerto, destino y acción |
| `MYSQL-3306` | Bloqueo de MySQL por TCP/3306 | Interfaces, origen/destino, ubicación/orden y contadores |
| NAT | Traducir tráfico según la política configurada | Tipo y parámetros efectivos por regla |
| `FQDN-ARCHIVE-UBUNTU` | Objeto de dirección de tipo FQDN | Nombre DNS asociado y resolución observada |
| `FQDN-SECURITY-UBUNTU` | Objeto de dirección de tipo FQDN | Nombre DNS asociado y resolución observada |


## 7. Procedimiento y registro de pruebas


| ID | Prueba | Resultado esperado a validar | Resultado observado | Evidencia |
|---|---|---|---|---|
| P-01 | Confirmar versión y nombre del equipo | FGT-1 y FortiOS 7.0.9 | Pendiente | `images/` |
| P-02 | Confirmar VLAN e interfaces | VLAN 10/20/30 con las redes indicadas | Pendiente | `images/` |
| P-03 | Probar salida a Internet desde VLAN 10 | Según política `VLAN10-INTERNET` y NAT | Pendiente | `images/` |
| P-04 | Probar salida a Internet desde VLAN 20 | Según política `VLAN20-INTERNET` y NAT | Pendiente | `images/` |
| P-05 | Probar acceso autorizado al Web Server | Según política `USUARIOS-WEB` | Pendiente | `images/` |
| P-06 | Probar acceso TCP/3306 al DB-Server | Debe quedar bloqueado por `MYSQL-3306` | Pendiente | `images/` |
| P-07 | Verificar objetos FQDN | Nombre y resolución corresponden a lo configurado | Pendiente | `images/` |
| P-08 | Revisar registros y contadores | Evidencia del tráfico permitido/bloqueado | Pendiente | `images/` |

