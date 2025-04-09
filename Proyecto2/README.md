# Proyecto 2 de Redes 1

## Convenciones:
- Grupo: `24`
- Y: `7`  (20220112[8] + 20220763[9] = 1[7])

# CUNDECH:

## Red:

- Id de red: 192.168.24.0/24
- Método de segmentación: VLSM

### CIDR:

| CIDR  | Mascara de Subred | Hosts  | Wildcard  |
|-------|-------------------|--------|-----------|
| /25   | 255.255.255.128   | 128    | 0.0.0.127 |
| /26   | 255.255.255.192   | 64     | 0.0.0.63  |
| /27   | 255.255.255.224   | 32     | 0.0.0.31  |
| /29   | 255.255.255.248   | 8      | 0.0.0.7   |

### VLANS:

| VLAN        | ID de VLAN | Equipos | ID de Red         |
|-------------|------------|---------|-------------------|
| Estudiantes | 17         | 50      | 192.168.24.0/26   |
| Docentes    | 27         | 20      | 192.168.24.64/27  |
| Seguridad   | 37         | 5       | 192.168.24.96/29  |
| Biblioteca  | 47         | 100     | 192.168.24.104/25 |

## Switches:

`SW7` es el server:
- Dominio: `Grupo24`
- Password: usac2025

# CUNOROC:

## Red:

- Id de red: 192.148.24.0/24
- Método de segmentación: VLSM

### CIDR:

| CIDR  | Mascara de Subred | Hosts  | Wildcard  |
|-------|-------------------|--------|-----------|
| /25   | 255.255.255.128   | 128    | 0.0.0.127 |
| /26   | 255.255.255.192   | 64     | 0.0.0.63  |
| /27   | 255.255.255.224   | 32     | 0.0.0.31  |
| /28   | 255.255.255.240   | 16     | 0.0.0.15  |

### VLANS:

| VLAN        | ID de VLAN | Equipos | ID de Red         |
|-------------|------------|---------|-------------------|
| Estudiantes | 17         | 45      | 192.148.24.0/26   |
| Docentes    | 27         | 25      | 192.148.24.64/27  |
| Seguridad   | 37         | 10      | 192.148.24.96/28  |
| Biblioteca  | 47         | 75      | 192.148.24.112/25 |

## Switches:

`SW3` es el server:
- Dominio: `Grupo24`
- Password: usac2025

# CUNOC:

## Red:

- Id de red: 172.16.24.0/24
- Método de segmentación: VLSM

### CIDR:

| CIDR  | Mascara de Subred | Hosts  | Wildcard  |
|-------|-------------------|--------|-----------|
| /26   | 255.255.255.192   | 64     | 0.0.0.63  |
| /29   | 255.255.255.248   | 8      | 0.0.0.7   |

### VLANS:

| VLAN       | ID de VLAN | Equipos | ID de Red         |
|------------|------------|---------|-------------------|
| Estudiantes| 17         | 60      | 172.16.24.0/26    |
| Docentes   | 27         | 35      | 172.16.24.64/26   |
| Seguridad  | 37         | 5       | 172.16.24.128/29  |
| Biblioteca | 47         | 50      | 172.16.24.136/26  |

## Switches:

La salida de la red interna del CUNOC estará a cargo de dos switches multicapa (MS1 y
MS2), configurados para proveer redundancia mediante el protocolo HSRP. Estos
dispositivos ofrecerán direcciones IP virtuales que funcionarán como puertas de enlace
predeterminadas para todas las VLANs de la red

`MS0` es el server:
- Dominio: `Grupo24`
- Password: usac2025

# Central:

## Ids de Red:

| Servidor      | ID de Red       |
|---------------|-----------------|
| Server0       | 192.120.24.0/24 |
| Server1       | 192.121.24.0/24 |
| Server2       | 192.122.24.0/24 |

## VLANS:
| VLAN          | ID de VLAN | Equipos  |
|---------------|------------|----------|
| Server0       | 57         | 60       |
| Server1       | 67         | 35       |
| Server2       | 77         | 5        |

# CUM:

## Red:

- Id de red: 192.158.24.0/24
- Método de segmentación: VLSM

### CIDR:

| CIDR  | Mascara de Subred | Hosts  | Wildcard  |
|-------|-------------------|--------|-----------|
| /25   | 255.255.255.128   | 128    | 0.0.0.127 |
| /26   | 255.255.255.192   | 64     | 0.0.0.63  |
| /27   | 255.255.255.224   | 32     | 0.0.0.31  |
| /28   | 255.255.255.240   | 16     | 0.0.0.15  |

### VLANS:

| VLAN        | ID de VLAN | Equipos | ID de Red         |
|-------------|------------|---------|-------------------|
| Estudiantes | 17         | 45      | 192.158.24.0/26   |
| Docentes    | 27         | 25      | 192.158.24.64/27  |
| Seguridad   | 37         | 10      | 192.158.24.96/28  |
| Biblioteca  | 47         | 75      | 192.158.24.112/25 |