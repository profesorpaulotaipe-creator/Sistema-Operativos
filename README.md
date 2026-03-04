La asignatura se enfoca en:

* Direccionamiento TCP/IP y subnetting
* Administración de Windows Server
* Administración de Linux Server
* Seguridad y hardening en ambos entornos

---

# 🔹 UNIDAD I: Direccionamiento de Redes Basado en TCP/IP

## 📌 Modelo TCP/IP

El modelo TCP/IP tiene 4 capas:

1. **Acceso a Red**
2. **Internet**
3. **Transporte**
4. **Aplicación**

Comparación con OSI:

| OSI          | TCP/IP     |
| ------------ | ---------- |
| Aplicación   | Aplicación |
| Presentación | Aplicación |
| Sesión       | Aplicación |
| Transporte   | Transporte |
| Red          | Internet   |
| Enlace       | Acceso     |
| Física       | Acceso     |

---

## 🌐 Dirección IP v4

### 📌 Estructura

Una IPv4 tiene:

* 32 bits
* 4 octetos
* Rango: 0.0.0.0 – 255.255.255.255

Ejemplo:

```
192.168.1.10
```

En binario:

```
11000000.10101000.00000001.00001010
```

---

## 📌 Clases de Direcciones IP

| Clase | Rango                 | Máscara       | Hosts |
| ----- | --------------------- | ------------- | ----- |
| A     | 1.0.0.0 – 126.x.x.x   | 255.0.0.0     | 16M   |
| B     | 128.0.0.0 – 191.x.x.x | 255.255.0.0   | 65k   |
| C     | 192.0.0.0 – 223.x.x.x | 255.255.255.0 | 254   |
| D     | Multicast             | —             | —     |
| E     | Experimental          | —             | —     |

Direcciones privadas:

* 10.0.0.0/8
* 172.16.0.0/12
* 192.168.0.0/16

---

## 📌 Máscaras y Cálculo de Hosts

Fórmula:

```
2^n - 2
```

Donde:

* n = bits disponibles para host
* Se restan 2 (red y broadcast)

Ejemplo:

```
/24 → 255.255.255.0
Bits host = 8
2^8 - 2 = 254 hosts
```

---

## 📌 Subnetting FLSM

FLSM = todas las subredes tienen igual tamaño.

Ejemplo:

Red base:

```
192.168.1.0/24
```

Necesitamos 4 subredes.

Se piden 2 bits prestados:

```
/26
```

Subredes:

| Subred           | Rango       | Hosts |
| ---------------- | ----------- | ----- |
| 192.168.1.0/26   | .1 – .62    | 62    |
| 192.168.1.64/26  | .65 – .126  | 62    |
| 192.168.1.128/26 | .129 – .190 | 62    |
| 192.168.1.192/26 | .193 – .254 | 62    |

---

## 📌 Subnetting VLSM

VLSM permite tamaños variables.

Ejemplo:

Red:

```
192.168.1.0/24
```

Necesitamos:

* 100 hosts
* 50 hosts
* 20 hosts

Se asigna desde mayor a menor:

| Hosts | Máscara | Subred        |
| ----- | ------- | ------------- |
| 100   | /25     | 192.168.1.0   |
| 50    | /26     | 192.168.1.128 |
| 20    | /27     | 192.168.1.192 |

VLSM optimiza uso de direcciones.

---

# 🔹 UNIDAD II: Windows Server

## 🖥 ¿Qué es Windows Server?

Es un sistema operativo empresarial de la empresa Microsoft diseñado para:

* Controladores de dominio
* Servidores de archivos
* Infraestructura de red
* Virtualización

Versiones comunes:

* Windows Server 2016
* Windows Server 2019
* Windows Server 2022

---

## 📌 Instalación y Configuración Básica

Pasos:

1. Configuración BIOS/UEFI
2. Instalación desde ISO
3. Asignación IP estática
4. Configuración de nombre de servidor
5. Activación de roles

Comando para IP estática:

```powershell
New-NetIPAddress
```

---

## 📌 Active Directory (AD)

Active Directory permite:

* Gestión centralizada de usuarios
* Dominios
* Unidades Organizativas (OU)
* Políticas de seguridad

Componentes:

* Dominio
* Árbol
* Bosque
* OU
* Objetos

---

## 📌 GPO (Group Policy Objects)

Permiten aplicar configuraciones como:

* Restricción de USB
* Configuración de escritorio
* Scripts de inicio
* Configuración de firewall

Ruta:

```
gpmc.msc
```

---

## 📌 Servicios de Infraestructura

### 🔹 DNS

Traduce nombre → IP

### 🔹 DHCP

Asigna IP automática

### 🔹 IIS

Internet Information Services

Servidor web de Microsoft.

---

## 🔐 Hardening Windows Server

Medidas:

* Deshabilitar servicios innecesarios
* Activar BitLocker (cifrado)
* Configurar firewall avanzado
* Actualizaciones automáticas
* Antivirus corporativo
* Políticas de auditoría
* NTFS con permisos avanzados

---

# 🔹 UNIDAD III: Linux Server

## 🐧 Historia del Software Libre

Proyecto:
GNU Project

Fundador:
Richard Stallman

Licencia:
GPL (General Public License)

---

## 📌 4 Libertades del Software Libre

1. Usar
2. Estudiar
3. Modificar
4. Redistribuir

Conceptos:

* Copyleft
* Copyright
* Propiedad intelectual

En Chile:
Ley 17.336 sobre propiedad intelectual.

---

## 📌 Sistema Linux

Distribuciones comunes:

* Ubuntu Server
* CentOS
* Rocky Linux

---

## 📌 Estructura de Directorios

| Directorio | Función       |
| ---------- | ------------- |
| /          | raíz          |
| /home      | usuarios      |
| /etc       | configuración |
| /var       | logs          |
| /usr       | aplicaciones  |
| /bin       | binarios      |
| /root      | admin         |

---

## 📌 Usuarios y Comandos

Tipos:

* root
* usuario normal
* usuario sistema

Comandos básicos:

```
whoami
id
useradd
passwd
su
sudo
```

---

## 📌 Permisos

Formato:

```
-rwxr-xr--
```

Valores:

* r = 4
* w = 2
* x = 1

Ejemplo:

```
chmod 755 archivo
```

Permisos especiales:

* SUID
* SGID
* Sticky Bit

Umask:

```
umask 022
```

---

## 📌 Gestión de Paquetes

RPM:

```
rpm -ivh paquete.rpm
```

YUM:

```
yum install nombre
yum update
```

APT (Debian):

```
apt install
```

---

## 🔐 Hardening Linux

Medidas:

* Deshabilitar root remoto
* Configurar SSH seguro
* Firewall (iptables / firewalld)
* Antivirus (ClamAV)
* Antirootkit (chkrootkit)
* Actualizaciones constantes
* SELinux o AppArmor
* Auditoría (auditd)

---

# 📌 Comparación Windows Server vs Linux Server

| Característica | Windows          | Linux              |
| -------------- | ---------------- | ------------------ |
| Licencia       | Comercial        | Libre              |
| GUI            | Fuerte           | Opcional           |
| AD             | Integrado        | Samba              |
| Seguridad      | GPO              | Permisos + SELinux |
| Firewall       | Windows Firewall | iptables           |

---
¿Quieres que lo prepare como material docente listo para presentar?
