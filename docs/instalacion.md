## GNU Health

> Este documento registra las decisiones, instalaciones, configuraciones, problemas y soluciones realizadas durante la construcción del laboratorio.

---

## 1. Punto de partida

**Fecha de inicio:** 06/09/2026

El laboratorio se construye desde cero con el objetivo de estudiar y documentar la implementación de un entorno de GNU Health orientado a Historia Clínica.

La instalación y configuración se documentan progresivamente, registrando no solamente el resultado final sino también las decisiones técnicas tomadas durante el proceso.

---

## 2. Entorno de trabajo

### 2.1 Decisión de virtualización

Se decidió utilizar una máquina virtual para ejecutar GNU Health y mantener separado el entorno de desarrollo del sistema operativo principal.

El equipo ya contaba con WSL2 y Hyper-V, por lo que se evaluó la convivencia con estas tecnologías antes de instalar VirtualBox.

La decisión fue utilizar **Oracle VirtualBox** para ejecutar la máquina virtual de GNU Health, manteniendo el entorno existente de WSL2/Hyper-V en una configuración compatible.

### 2.2 Recursos disponibles

Antes de crear la máquina virtual se verificaron los recursos disponibles del equipo:

* Virtualización por hardware habilitada.
* Windows 11 Pro.
* 8 GB de RAM física.
* Procesador con capacidad de virtualización.
* Espacio disponible suficiente en la unidad D:.

Debido a los recursos disponibles, la máquina virtual se configuró de manera moderada para evitar un consumo excesivo del equipo anfitrión.

### 2.3 Configuración de VirtualBox

Se instaló:

**Oracle VirtualBox 7.2.16**

La máquina virtual se creó con la siguiente configuración:

| Recurso   | Configuración          |
| --------- | ---------------------- |
| Nombre    | `GNUHealth-50`         |
| RAM       | 3 GB                   |
| CPU       | 2                      |
| Ubicación | `D:\VirtualBox VMs`    |
| Sistema   | GNU Health / Debian 12 |

> La ubicación correcta utilizada fue `D:\VirtualBox VMs`.

---

## 3. Descarga y verificación de GNU Health

Se descargó la imagen de GNU Health:

```text
GNUHealth-50-debian12.vdi.gz
```

La imagen fue almacenada fuera del repositorio del proyecto.

### 3.1 Verificación de integridad

Se verificó la integridad de la imagen mediante MD5.

Resultado obtenido:

```text
A756AC5AFE0B93AE705E933E74CBB1C0
```

La comprobación permitió verificar que la imagen descargada coincidía con el valor esperado.

---

# Fase 2 — Verificación del entorno GNU Health

Una vez creada e iniciada la máquina virtual se realizaron las verificaciones necesarias para confirmar que el entorno proporcionado por GNU Health funcionaba correctamente.

## 4. Sistema operativo

Se verificó que la máquina virtual utiliza:

```text
Debian 12.11
```

El sistema operativo funciona como base del entorno GNU Health.

---

## 5. Python

Se verificó la versión de Python utilizada por el entorno GNU Health:

```text
Python 3.11
```

GNU Health dispone de su propio entorno virtual de Python.

La ruta observada durante la exploración fue:

```text
/opt/gnuhealth/his-50/venv/
```

Dentro de este entorno se encuentra instalada la infraestructura utilizada por GNU Health y Tryton.

---

## 6. PostgreSQL

Se verificó la instalación y funcionamiento de PostgreSQL.

La base de datos utilizada por GNU Health es:

```text
health50
```

El rol de PostgreSQL utilizado por GNU Health es:

```text
gnuhealth
```

La versión verificada durante esta etapa inicial fue:

```text
PostgreSQL 15.3
```

> Las credenciales no se almacenan en este repositorio.

---

## 7. Servicio GNU Health

Se verificó la existencia y funcionamiento del servicio:

```text
gnuhealth.service
```

El servicio permite comprobar que la instalación de GNU Health se encuentra correctamente configurada y disponible dentro de la máquina virtual.

---

## 8. Primer acceso a GNU Health

Se realizó exitosamente el primer acceso al cliente de GNU Health utilizando las credenciales iniciales proporcionadas por la instalación:

```text
Usuario: admin
```

La contraseña inicial no se documenta en el repositorio.

El acceso permitió comprobar que GNU Health se encontraba operativo y que la instalación proporcionada por la máquina virtual podía utilizarse correctamente.

---

## 9. Cambio de credenciales

Como parte de la configuración inicial de seguridad se modificaron las credenciales predeterminadas correspondientes a:

* Usuario `gnuhealth` de PostgreSQL.
* Usuario `root` del sistema operativo.

Las nuevas contraseñas se almacenan únicamente fuera del repositorio.

### Regla de seguridad

No se deben almacenar contraseñas, tokens ni otras credenciales reales en:

* archivos `.md`;
* scripts;
* archivos de configuración versionados;
* commits de Git;
* repositorios públicos.

---

## 10. Estado de la Fase 1 y Fase 2

Al finalizar estas etapas se confirmó que el laboratorio dispone de:

* VirtualBox 7.2.16 instalado.
* Máquina virtual `GNUHealth-50` creada.
* 3 GB de RAM asignados.
* 2 CPU asignadas.
* Imagen GNU Health verificada mediante MD5.
* Debian 12.11 funcionando.
* Python 3.11 disponible.
* PostgreSQL instalado y operativo.
* Base de datos `health50`.
* Usuario PostgreSQL `gnuhealth`.
* Servicio `gnuhealth.service`.
* Primer acceso exitoso al cliente GNU Health.
* Credenciales iniciales modificadas.

Las configuraciones de red y el acceso desde Windows se documentan por separado en:

```text
docs/arquitectura-red.md
```

---

## 11. Próxima etapa

La siguiente etapa consiste en configurar el acceso externo desde Windows hacia la máquina virtual.

Se documentarán:

* SSH.
* Port Forwarding.
* Configuración de PostgreSQL.
* `listen_addresses`.
* `pg_hba.conf`.
* Acceso externo a la base `health50`.
* DBeaver.

Esta información se encuentra separada de la instalación base para mantener diferenciadas la configuración del sistema y la arquitectura de red.
