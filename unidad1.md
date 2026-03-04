1. Dirección IP v4: Descripción, clases, máscaras y funcionamiento
1.1 ¿Qué es una dirección IPv4?

Una dirección IPv4 es un identificador numérico único asignado a cada dispositivo dentro de una red que utiliza el protocolo Internet Protocol version 4.

Su función principal es identificar y localizar dispositivos dentro de una red para que los datos puedan enviarse correctamente entre ellos.

Características principales:

Longitud: 32 bits

Representación: 4 octetos

Cada octeto tiene valores entre 0 y 255

Se escribe en notación decimal separada por puntos

Ejemplo:

192.168.1.10

En binario:

11000000.10101000.00000001.00001010
1.2 Estructura de una dirección IP

Una dirección IP se divide en dos partes:

Parte	Función
Network ID	Identifica la red
Host ID	Identifica el dispositivo

Ejemplo:

IP: 192.168.1.10
Mascara: 255.255.255.0

Red: 192.168.1

Host: 10

1.3 Clases de direcciones IPv4

Las direcciones IPv4 originalmente se dividían en clases.

Clase	Rango	Máscara	Redes	Hosts
A	1.0.0.0 – 126.x.x.x	255.0.0.0	128	16,777,214
B	128.0.0.0 – 191.x.x.x	255.255.0.0	16,384	65,534
C	192.0.0.0 – 223.x.x.x	255.255.255.0	2,097,152	254
D	224 – 239	Multicast	—	—
E	240 – 255	Experimental	—	—
1.4 Direcciones IP privadas

Existen rangos reservados para redes internas.

Rango	Uso
10.0.0.0 – 10.255.255.255	redes grandes
172.16.0.0 – 172.31.255.255	redes medianas
192.168.0.0 – 192.168.255.255	redes pequeñas

Ejemplo:

192.168.1.15

Usada normalmente en redes domésticas o empresariales.

1.5 Funcionamiento del direccionamiento IP

Cuando un dispositivo envía datos:

El equipo genera un paquete IP

Incluye:

IP origen

IP destino

Los routers analizan la red destino

El paquete se enruta hasta llegar al host final

Ejemplo:

PC1 → Router → Internet → Router → Servidor
2. Máscaras y cantidad de host contenidos en cada red
2.1 ¿Qué es una máscara de red?

La máscara de red determina qué parte de la IP pertenece a la red y cuál al host.

Ejemplo:

IP: 192.168.1.10
Máscara: 255.255.255.0

En binario:

IP
11000000.10101000.00000001.00001010

Mascara
11111111.11111111.11111111.00000000

Los 1 representan la red
Los 0 representan los hosts

2.2 Cantidad de hosts por máscara

Fórmula:

2^n - 2

donde:

n = bits disponibles para hosts

se restan 2 direcciones:

dirección de red

dirección broadcast

Tabla de hosts más comunes
CIDR	Máscara	Hosts
/24	255.255.255.0	254
/25	255.255.255.128	126
/26	255.255.255.192	62
/27	255.255.255.224	30
/28	255.255.255.240	14
/29	255.255.255.248	6
/30	255.255.255.252	2
Ejemplo práctico

Red:

192.168.1.0/26

/26 significa:

11111111.11111111.11111111.11000000

Bits de host:

6 bits

Hosts:

2^6 - 2 = 62 hosts
3. Cálculo de subredes con técnica FLSM

FLSM significa:

Fixed Length Subnet Mask

Todas las subredes tienen el mismo tamaño.

Procedimiento FLSM

Identificar red base

Determinar número de subredes

Pedir bits prestados

Calcular nueva máscara

Obtener rangos de subred

Ejemplo práctico FLSM

Red base:

192.168.1.0/24

Necesitamos 4 subredes

Paso 1: calcular bits prestados
2^n ≥ 4
2^2 = 4

Se toman 2 bits

Paso 2: nueva máscara
/24 + 2 = /26

Máscara:

255.255.255.192
Paso 3: tamaño de bloque
256 - 192 = 64
Subredes resultantes
Subred	Rango de hosts	Broadcast
192.168.1.0/26	1 – 62	63
192.168.1.64/26	65 – 126	127
192.168.1.128/26	129 – 190	191
192.168.1.192/26	193 – 254	255
4. Cálculo de subredes con técnica VLSM

VLSM significa:

Variable Length Subnet Mask

Permite crear subredes de diferente tamaño para optimizar direcciones.

Procedimiento VLSM

Ordenar redes por cantidad de hosts

Asignar primero la red más grande

Continuar con las siguientes

Ajustar máscara según necesidad

Ejemplo práctico VLSM

Red disponible:

192.168.1.0/24

Necesidades:

Red	Hosts
A	100
B	50
C	20
D	10
Paso 1: ordenar
Red	Hosts
A	100
B	50
C	20
D	10
Red A

Hosts necesarios: 100

2^7 -2 = 126

Máscara:

/25

Subred:

192.168.1.0 – 192.168.1.127

Hosts:

192.168.1.1 – 192.168.1.126
Red B

Hosts necesarios: 50

2^6 -2 = 62

Máscara:

/26

Subred:

192.168.1.128 – 192.168.1.191
Red C

Hosts necesarios: 20

2^5 -2 = 30

Máscara:

/27

Subred:

192.168.1.192 – 192.168.1.223
Red D

Hosts necesarios: 10

2^4 -2 = 14

Máscara:

/28

Subred:

192.168.1.224 – 192.168.1.239
Resultado final
Red	Subred	Máscara	Hosts
A	192.168.1.0	/25	126
B	192.168.1.128	/26	62
C	192.168.1.192	/27	30
D	192.168.1.224	/28	14
Diferencia entre FLSM y VLSM
Característica	FLSM	VLSM
Tamaño subred	Igual	Variable
Uso direcciones	Ineficiente	Eficiente
Complejidad	Baja	Media
Uso actual	Poco usado	Muy usado