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

El diagrama es lógico y usa solo los datos conocidos. No especifica puertos físicos, subinterfaces, puertas de enlace ni extremos del enlace ISP porque esos valores no están confirmados en el contexto disponible.

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

No se infiere el dominio asociado a los objetos FQDN ni la configuración detallada de las reglas. Añade esos datos tras verificarlos en FGT-1 y elimina cualquier secreto antes de guardar configuraciones en este repositorio.

## 7. Procedimiento y registro de pruebas

Completa fecha, método y evidencia después de ejecutar cada prueba. En “Resultado observado”, escribe lo que realmente ocurrió y cualquier mensaje relevante. No marques una prueba como aprobada sin evidencia.

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

**Fecha de ejecución:** pendiente.  
**Entorno/cliente usado en las pruebas:** pendiente.  
**Observaciones:** pendiente.

## 8. Evidencias

Guarda capturas numeradas en `images/` y usa los nombres sugeridos en [images/README.md](../images/README.md). Evita que se vean contraseñas, claves, tokens o datos personales ajenos al trabajo. Cada captura debe mostrar suficiente contexto para identificar equipo, regla o prueba.

## 9. Configuración de respaldo

Guarda en `configs/` únicamente archivos necesarios para reproducir o revisar el laboratorio. Revisa y elimina credenciales, claves privadas, tokens, contraseñas y otros secretos antes de publicar. La guía está en [configs/README.md](../configs/README.md).

## 10. Video de demostración

Añade el enlace o archivo final cuando esté disponible, con una breve descripción y fecha. Ver [video/README.md](../video/README.md).

## 11. Resultados y conclusión

**Resultados:** pendientes de ejecución y evidencia. Completar con el comportamiento observado para cada prueba de la tabla; distinguir claramente entre resultado esperado y resultado obtenido.

**Conclusión:** completar después de revisar las pruebas. Explicar qué controles quedaron comprobados y qué ajustes fueron necesarios, usando únicamente resultados observados.
