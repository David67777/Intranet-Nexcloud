# 🌐 Intranet Corporativa con Nextcloud

## 📖 Descripción del Proyecto

El proyecto consiste en la creación de una **intranet corporativa** utilizando **Nextcloud** como plataforma principal, desplegada en un entorno virtualizado con **Proxmox VE**.  
El objetivo es ofrecer un espacio centralizado para el **almacenamiento de archivos, comunicación interna, calendario compartido y gestión de usuarios mediante LDAP**, garantizando la seguridad, disponibilidad y facilidad de administración.

Además, el sistema incluirá **integración de chat corporativo (Rocket.Chat o Mattermost)**, **copias de seguridad automáticas** y **monitorización del rendimiento** mediante herramientas como Grafana o Zabbix.

---

## 🎯 Justificación del Proyecto

En muchas empresas, los empleados utilizan múltiples servicios dispersos para almacenar archivos, comunicarse o compartir información. Esto genera **ineficiencia, falta de control y riesgos de seguridad**.  

Este proyecto pretende **unificar todos esos servicios** en un único entorno corporativo autogestionado, privado y escalable.  
Frente a soluciones comerciales como Google Workspace o Microsoft 365, **Nextcloud** ofrece una alternativa **de código abierto**, **autohospedada** y **totalmente personalizable**, lo que permite mayor control sobre los datos y ahorro de costes.

---

## ⚙️ Objetivos Principales

- Implementar una **infraestructura virtualizada** con **Proxmox**.  
- Desplegar un servidor **Nextcloud** funcional y seguro.  
- Integrar **autenticación centralizada con LDAP**.  
- Añadir **servicios colaborativos**: correo, chat interno y calendario.  
- Configurar **copias de seguridad automáticas** del sistema.  
- Incorporar **monitorización de rendimiento y disponibilidad**.  
- Documentar cada fase del desarrollo para facilitar mantenimiento futuro.

---

## 🧰 Lenguajes y Tecnologías Utilizadas

| Tecnología / Lenguaje | Uso en el proyecto |
|------------------------|--------------------|
| **Nextcloud** | Plataforma principal de la intranet (archivos, calendario, usuarios). |
| **OpenLDAP** | Autenticación centralizada de usuarios. |
| **Rocket.Chat / Mattermost** | Chat corporativo y comunicación interna. |
| **Grafana / Zabbix** | Monitorización de servicios y recursos del sistema. |
| **Bash** | Automatización de tareas y configuración de servicios. |
| **Ubuntu Server / Debian** | Sistema operativo base de los servidores. |
| **Figma** | Diseño del prototipo de interfaz. |
| **Trello** | Planificación y seguimiento del proyecto. |

---

## 🧠 Módulos Relacionados (ASIR)

- **Implantación de Sistemas Operativos** → Instalación y configuración de servidores.  
- **Servicios de Red e Internet** → Configuración de red, DNS y servicios asociados.  
- **Administración de Sistemas Gestores de Bases de Datos** → Configuración de base de datos para Nextcloud.  
- **Seguridad y Alta Disponibilidad** → Copias de seguridad, monitorización y control de accesos.  
- **Administración de Sistemas Operativos** → Gestión de servicios y mantenimiento del entorno.  
- **Proyecto Integrado** → Coordinación, documentación y presentación del proyecto completo.  

---

## 📅 Fases del Proyecto

1. **Planificación inicial** → Definición de objetivos, recursos y estructura del entorno.  
2. **Análisis y diseño** → Preparación de la arquitectura y modelo de red.  
3. **Desarrollo e implementación** → Instalación de Nextcloud, LDAP, chat y monitorización.  
4. **Pruebas y validación** → Verificación de funcionamiento, usuarios y copias de seguridad.  
5. **Despliegue y documentación final** → Entrega y presentación del sistema completamente operativo.  


## 🧩 Requisitos de Hardware y Software

| Tipo | Elemento | Descripción |
|------|-----------|-------------|
| **Hardware** | Servidor físico o máquina host | Equipo donde se instalará Proxmox. |
| | CPU y RAM | Suficiente para alojar varias máquinas virtuales. |
| **Software** | Proxmox VE | Virtualización y gestión del entorno. |
| | Ubuntu Server | Sistema base para los servicios. |
| | Nextcloud | Servidor de intranet principal. |
| | OpenLDAP | Autenticación de usuarios. |
| | Rocket.Chat / Mattermost | Comunicación interna. |
| | Grafana / Zabbix | Monitorización. |
| | Bash | Automatización. |
| | Figma | Diseño de la interfaz. |
| | Trello | Seguimiento del proyecto. |


## 🛠️ Diario de Implementación y Hitos del Proyecto(ACTUALIZACIÓN)

Desde el inicio del despliegue este sábado, se ha trabajado en la integración real de servicios mediante contenedores Docker, logrando los siguientes objetivos técnicos:

### 1. Infraestructura Base (Docker)
* **Contenerización:** Despliegue de un entorno orquestado mediante `docker-compose` que incluye Nextcloud, MariaDB, OpenLDAP (con phpLDAPadmin) y Rocket.Chat.
* **Persistencia:** Configuración de volúmenes para asegurar la integridad de los datos de la intranet y la base de datos de usuarios.

### 2. Configuración de OpenLDAP y phpLDAPadmin
* **Estructura del Directorio:** Creación y configuración del dominio `dc=david,dc=local`.
* **Organización:** Implementación de la Unidad Organizativa `ou=Usuarios` para centralizar las cuentas corporativas.
* **Gestión:** Uso de phpLDAPadmin para la creación de usuarios y gestión de atributos (`posixAccount`).

### 3. Integración Exitosa: Nextcloud + LDAP
* **Estado:** ✅ **FUNCIONAL**.
* **Hito:** Se ha logrado vincular Nextcloud con el servidor LDAP de forma exitosa. Los usuarios creados en el LDAP pueden iniciar sesión correctamente, logrando una autenticación centralizada para la gestión de archivos.

### 4. Integración de Rocket.Chat + LDAP (En depuración)
* **Estado:** ⚠️ **EN PRUEBAS**.
* **Progreso:** Se ha establecido conexión con el servidor LDAP (`192.168.1.10:389`).
* **Desafíos Técnicos:** Se han realizado ajustes manuales en los filtros de búsqueda `(uid=%username%)` y en el DN base. Actualmente se trabaja en la resolución de conflictos de sincronización para que la lista de usuarios sea plenamente visible.

---

## 📊 Direccionamiento y Puertos
| Servicio | IP Interna | Puerto | Estado de Integración |
| :--- | :--- | :--- | :--- |
| **OpenLDAP** | `192.168.1.10` | `389` | Servidor Maestro |
| **Nextcloud** | `192.168.1.10` | `8080` | **Integrado con LDAP** |
| **Rocket.Chat** | `192.168.1.10` | `3000` | En fase de sincronización |

## 👤 Autor
**Nombre:** David  
**Centro:** IES TRIANA  
**Ciclo:** Administración de Sistemas Informáticos en Red (ASIR)  
**Año:** 2025  


