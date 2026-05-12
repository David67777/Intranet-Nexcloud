# 🌐 Intranet Corporativa con Nextcloud

## 📖 Descripción del Proyecto

El proyecto consiste en el diseño y despliegue de una **intranet corporativa privada** utilizando **Nextcloud** como eje central, alojada en un entorno de red virtualizado mediante **VirtualBox**. 

El objetivo principal es ofrecer a la empresa un ecosistema centralizado, seguro y autogestionado para el **almacenamiento de archivos, comunicación interna (Chat y Correo), y gestión unificada de usuarios mediante OpenLDAP**. Todo ello respaldado por políticas estrictas de seguridad (cortafuegos UFW), **copias de seguridad automatizadas** y **monitorización proactiva** de recursos con Zabbix.

---

## 🎯 Justificación del Proyecto

En el entorno empresarial actual, el uso de herramientas dispersas para el almacenamiento y la comunicación genera ineficiencia y graves riesgos de privacidad. Este proyecto elimina la dependencia de nubes públicas de terceros (como Google Drive o Microsoft 365), proponiendo una infraestructura **Open Source y autohospedada**. 

Esta solución no solo garantiza el cumplimiento de las normativas de protección de datos al mantener la información dentro del perímetro de la empresa, sino que además supone un importante ahorro de costes en licencias a largo plazo.

---

## ⚙️ Objetivos Alcanzados

- ✅ **Infraestructura de red aislada:** Creación de un entorno de 4 servidores en VirtualBox.
- ✅ **Gestión de Identidades:** Autenticación centralizada (Single Sign-On) mediante **OpenLDAP**.
- ✅ **Nube Privada:** Servidor **Nextcloud** funcional con aplicaciones de productividad (Calendario y Contactos).
- ✅ **Comunicaciones en Docker:** Despliegue contenerizado de **Rocket.Chat** y un **Mailserver**.
- ✅ **Seguridad Perimetral:** Fortificación de servidores mediante políticas estrictas con **UFW**.
- ✅ **Resiliencia:** Scripts en Bash programados (Cron) para realizar copias de seguridad de las bases de datos.
- ✅ **Monitorización Centralizada:** Despliegue de **Zabbix** para vigilar el rendimiento del hardware en tiempo real.

---

## 🧰 Tecnologías Utilizadas

| Tecnología / Lenguaje | Uso en el proyecto |
|------------------------|--------------------|
| **Nextcloud** | Nube privada corporativa (archivos, contactos, calendario). |
| **OpenLDAP** | Directorio activo para autenticación centralizada. |
| **Docker & Compose** | Orquestación de microservicios (Chat y Correo). |
| **Rocket.Chat** | Plataforma de mensajería instantánea empresarial. |
| **Mailserver** | Servidor de correo electrónico corporativo. |
| **Zabbix** | Monitorización de servidores, red y espacio en disco. |
| **Bash & Cron** | Scripts de automatización para tareas de Backup. |
| **UFW** | Cortafuegos para la seguridad perimetral de la red. |
| **Ubuntu Server 22.04/24.04** | Sistema Operativo base de la infraestructura. |

---

## 🏗️ Arquitectura y Nodos de Red

La infraestructura se ha diseñado dividiendo los servicios críticos en cuatro máquinas virtuales independientes conectadas a través de una red interna aislada, garantizando alta disponibilidad y tolerancia a fallos:

| Servidor (Hostname) | IP Interna | Rol Principal | Servicios Activos |
| :--- | :--- | :--- | :--- |
| **srv-ldap** | `192.168.100.10` | Directorio Activo | OpenLDAP (`:389`) |
| **srv-nextcloud** | `192.168.100.20` | Almacenamiento Web | Apache, MariaDB, Nextcloud (`:80/443`) |
| **srv-chat** | `192.168.100.30` | Comunicaciones | Docker: Rocket.Chat (`:3000`), MongoDB, Mailserver |
| **srv-monitor** | `192.168.100.40` | Monitorización | Zabbix Server, Zabbix Web (`:80`), MariaDB |

---

## 🛠️ Hitos Técnicos y Desafíos Superados

Durante la fase de integración, se resolvieron con éxito los siguientes retos de ingeniería de sistemas:

### 1. Unificación de Identidades (Nextcloud + LDAP)
* **Estado:** ✅ **ÉXITO**
* Se logró vincular la base de datos de Nextcloud con el servidor LDAP (`ou=Usuarios,dc=david,dc=local`). Los empleados pueden iniciar sesión en su nube privada de forma transparente usando sus credenciales corporativas unificadas.

### 2. Mensajería Instantánea (Rocket.Chat + LDAP)
* **Estado:** ✅ **ÉXITO**
* Se superaron los problemas de sincronización de atributos. Rocket.Chat extrae periódicamente los usuarios del directorio activo, permitiendo la creación automática de perfiles de chat al dar de alta un nuevo empleado.

### 3. Servidor de Correo Centralizado (Mailserver + LDAP)
* **Estado:** ✅ **ÉXITO** (Desafío principal del proyecto)
* La configuración más compleja consistió en mapear correctamente los atributos y filtros de búsqueda (DN) para que el contenedor del Mailserver validara el inicio de sesión del correo electrónico contra la base de datos de OpenLDAP.

### 4. Automatización y Seguridad (Infraestructura como Código)
* **Estado:** ✅ **ÉXITO**
* Implementación de reglas `deny` por defecto en UFW, permitiendo solo tráfico esencial. Desarrollo de un script Bash que realiza volcados SQL (`.sql`) y los comprime en (`.tar.gz`), eliminando automáticamente históricos de más de 7 días.

---

## 👤 Autor
**Nombre:** David García  
**Centro:** IES TRIANA  
**Ciclo:** Administración de Sistemas Informáticos en Red (ASIR)  
**Año:** 2024 / 2025

