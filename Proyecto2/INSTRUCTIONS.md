# Instrucciones:

## Convenciones:
- Grupo: `24`
- Y: `7`  (20220112[8] + 20220763[9] = 1[7])

# CUNDECH:

## Red:

- Id de red: 192.168.24.0/24
- Método de segmentación: VLSM

### VLANS:

| VLAN          | ID de VLAN | Equipos  |
|---------------|------------|----------|
| Estudiantes   | 17         | 50       |
| Docentes      | 27         | 20       |
| Seguridad     | 37         | 5        |
| Biblioteca    | 47         | 100      |

## Switches:

`SW7` es el server:
- Dominio: `Grupo24`
- Password: usac2025

# CUNOROC:

## Red:

- Id de red: 192.148.24.0/24
- Método de segmentación: VLSM

### VLANS:

| VLAN          | ID de VLAN | Equipos  |
|---------------|------------|----------|
| Estudiantes   | 17         | 45       |
| Docentes      | 27         | 25       |
| Seguridad     | 37         | 10       |
| Biblioteca    | 47         | 75       |

## Switches:

`SW3` es el server:
- Dominio: `Grupo24`
- Password: usac2025

# CUNOC:

## Red:

- Id de red: 172.16.24.0/24
- Método de segmentación: VLSM

### VLANS:

| VLAN          | ID de VLAN | Equipos  |
|---------------|------------|----------|
| Estudiantes   | 17         | 60       |
| Docentes      | 27         | 35       |
| Seguridad     | 37         | 5        |
| Biblioteca    | 47         | 50       |

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

### VLANS:

| VLAN          | ID de VLAN | Equipos  |
|---------------|------------|----------|
| Estudiantes   | 17         | 45       |
| Docentes      | 27         | 25       |
| Seguridad     | 37         | 10       |
| Biblioteca    | 47         | 75       |