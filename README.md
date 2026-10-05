# Primer Parcial — Seguridad en Redes

**Estudiante:** Noel Elias Nova Vargas  
**Matrícula:** 20242293  
**Institución:** Instituto Tecnológico de las Américas (ITLA)  
**Asignatura:** Seguridad en Redes

## Descripción

Documentación del laboratorio de segmentación, conectividad y control de tráfico realizado con FortiGate. Se registran la topología y el direccionamiento conocidos, las políticas indicadas para el ejercicio y los espacios destinados a evidencias. Los resultados de pruebas se completarán cuando se tomen y revisen las capturas; no se presentan como exitosas pruebas que todavía no estén documentadas.

## Componentes conocidos

- **Firewall:** FortiGate-VM64-KVM, versión 7.0.9; nombre de equipo FGT-1.
- **ISP:** red de tránsito conectada al FortiGate por `203.0.113.0/30`.
- **VLAN 10 — USR:** `10.229.3.0/25`.
- **VLAN 20 — ADM:** `10.229.3.128/26`.
- **VLAN 30 — SRV:** `10.229.3.192/28`.
- **Web Server:** `10.229.3.194`.
- **DB-Server:** `10.229.3.195`.

Las interfaces, puertas de enlace, direcciones exactas de los extremos del enlace ISP, servicios permitidos y destinos de los objetos FQDN se deben confirmar con las capturas o la configuración final del laboratorio.

## Políticas y objetos indicados para el laboratorio

Políticas mencionadas: `VLAN10-INTERNET`, `VLAN20-INTERNET`, `USUARIOS-WEB` y `MYSQL-3306` (bloqueo de MySQL por TCP/3306). También se indicaron NAT y los objetos FQDN `FQDN-ARCHIVE-UBUNTU` y `FQDN-SECURITY-UBUNTU`. Los parámetros completos de cada regla y el resultado de las pruebas se documentarán al verificarlos en FortiGate.

## Documentación

Consulta [docs/DOCUMENTACION.md](docs/DOCUMENTACION.md) para la descripción del laboratorio, tabla IP, controles y registro de pruebas.

## Evidencias y entregables

- [images/README.md](images/README.md): lista de capturas que se deben agregar.
- [configs/README.md](configs/README.md): espacio para respaldos y configuración saneada.
- [video/README.md](video/README.md): espacio para el video de demostración.

## Estado de verificación

La información de topología anterior proviene de los datos disponibles del laboratorio. Las pruebas de conectividad, NAT, acceso web, bloqueo TCP/3306 y resolución/uso de FQDN quedan **pendientes de evidencias**. Actualiza esta sección y la documentación después de verificar cada resultado.
