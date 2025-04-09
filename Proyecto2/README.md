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

# Configuraciones:

## CUNDECH:

### Switches:

- SW6: 
```bash
enable
conf t 
    hostname SW6
    vtp version 2
    vtp mode client
    vtp domain Grupo24
    vtp usac2025
    interface FastEthernet 0/10
        switchport mode trunk
        exit
    interface FastEthernet 0/11
        switchport mode trunk
        exit
    interface FastEthernet 0/1
        switchport mode access
        switchport access vlan 37
        exit
    interface FastEthernet 0/2
        switchport mode access
        switchport access vlan 47
        exit
    interface FastEthernet 0/3
        switchport mode access
        switchport access vlan 47
        exit
    do write
    exit
```
- SW7:
```bash
enable
conf t 
    hostname SW7
    vtp version 2
    vtp mode server
    vtp domain Grupo24
    vtp usac2025
    vlan 17
        name Estudiantes
        exit
    vlan 27
        name Docentes
        exit
    vlan 37
        name Seguridad
        exit
    vlan 47
        name Biblioteca
        exit
    interface FastEthernet 0/10
        switchport mode trunk
        exit
    interface FastEthernet 0/11
        switchport mode trunk
        exit
    interface FastEthernet 0/12
        switchport mode trunk
        exit
    interface FastEthernet 0/1
        switchport mode access
        switchport access vlan 17
        exit
    interface FastEthernet 0/2
        switchport mode access
        switchport access vlan 17
        exit
    do write
    exit
```
- SW8:
```bash
enable
conf t 
    hostname SW8
    vtp version 2
    vtp mode client
    vtp domain Grupo24
    vtp usac2025
    interface FastEthernet 0/10
        switchport mode trunk
        exit
    interface FastEthernet 0/11
        switchport mode trunk
        exit
    interface FastEthernet 0/1
        switchport mode access
        switchport access vlan 27
        exit
    interface FastEthernet 0/2
        switchport mode access
        switchport access vlan 27
        exit
    do write
    exit
```
### Router (Switch capa 3):
- MS8:
```bash
enable
conf t
    hostname MS8
```

## CUNOROC:

### Switches:

- SW2: 
```bash
enable
conf t 
    hostname SW2
    vtp version 2
    vtp mode client
    vtp domain Grupo24
    vtp usac2025
    interface FastEthernet 0/10
        switchport mode trunk
        exit
    interface FastEthernet 0/11
        switchport mode trunk
        exit
    interface FastEthernet 0/1
        switchport mode access
        switchport access vlan 27
        exit
    do write
    exit
```
- SW3: 
```bash
enable
conf t 
    hostname SW3
    vtp version 2
    vtp mode server
    vtp domain Grupo24
    vtp usac2025
    vlan 17
        name Estudiantes
        exit
    vlan 27
        name Docentes
        exit
    vlan 37
        name Seguridad
        exit
    vlan 47
        name Biblioteca
        exit
    interface FastEthernet 0/10
        switchport mode trunk
        exit
    interface FastEthernet 0/11
        switchport mode trunk
        exit
    interface FastEthernet 0/1
        switchport mode access
        switchport access vlan 17
        exit
    do write
    exit
```
- SW4: 
```bash
enable
conf t 
    hostname SW4
    vtp version 2
    vtp mode client
    vtp domain Grupo24
    vtp usac2025
    interface FastEthernet 0/10
        switchport mode trunk
        exit    
    interface FastEthernet 0/1
        switchport mode access
        switchport access vlan 37
        exit
    interface FastEthernet 0/2
        switchport mode access
        switchport access vlan 47
        exit
    do write
    exit
```

### Router:
- R0:
```bash
enable
conf t
```

## CUNOC:

### Switches:

- SW10:
```bash
enable
conf t 
    hostname SW10
    vtp version 2
    vtp mode client
    vtp domain Grupo24
    vtp usac2025
    interface FastEthernet 0/10
        switchport mode trunk
        exit    
    interface FastEthernet 0/1
        switchport mode access
        switchport access vlan 27
        exit
    interface FastEthernet 0/2
        switchport mode access
        switchport access vlan 27
        exit
    do write
    exit
```

- SW9:
```bash
enable
conf t 
    hostname SW9
    vtp version 2
    vtp mode client
    vtp domain Grupo24
    vtp usac2025
    interface FastEthernet 0/10
        switchport mode trunk
        exit    
    interface FastEthernet 0/1
        switchport mode access
        switchport access vlan 37
        exit
    do write
    exit
```

- SW1:
```bash
enable
conf t 
    hostname SW1
    vtp version 2
    vtp mode client
    vtp domain Grupo24
    vtp usac2025
    interface FastEthernet 0/10
        switchport mode trunk
        exit    
    interface FastEthernet 0/1
        switchport mode access
        switchport access vlan 17
        exit
    interface FastEthernet 0/2
        switchport mode access
        switchport access vlan 17
        exit
    do write
    exit
```

- MS0:
```bash
enable
conf t 
    hostname MS0
    vtp version 2
    vtp mode server
    vtp domain Grupo24
    vtp usac2025
    vlan 17
        name Estudiantes
        exit
    vlan 27
        name Docentes
        exit
    vlan 37
        name Seguridad
        exit
    vlan 47
        name Biblioteca
        exit
    interface FastEthernet 0/10
        switchport trunk encapsulation dot1q
        switchport mode trunk
        exit 
    interface FastEthernet 0/11
        switchport trunk encapsulation dot1q
        switchport mode trunk
        exit 
    interface FastEthernet 0/12
        switchport trunk encapsulation dot1q
        switchport mode trunk
        exit 
    interface FastEthernet 0/13
        switchport trunk encapsulation dot1q
        switchport mode trunk
        exit 
    interface FastEthernet 0/14
        switchport trunk encapsulation dot1q
        switchport mode trunk
        exit    
    do write
    exit
```

### Router (Switches Capa 3):

- MS1:
```bash
enable
conf t
```

- MS2:
```bash
enable
conf t
```

## Central:

- SW0:
```bash
enable
conf t
    hostname SW0
    vtp version 2
    vtp mode server
    vtp domain Grupo24
    vtp password usac2025
    vlan 57
        name Server0
        exit
    vlan 67
        name Server1
        exit
    vlan 77
        name Server2
        exit
    interface FastEthernet 0/10        
        switchport mode trunk
        exit 
    interface FastEthernet 0/1
        switchport mode access
        switchport access vlan 57
        exit 
    interface FastEthernet 0/2
        switchport mode access
        switchport access vlan 67
        exit
    interface FastEthernet 0/2
        switchport mode access
        switchport access vlan 77
        exit
    do write
    exit
```

- R7:
```bash
enable
conf t
```

## CUM:

- SW5: 
```bash
enable
conf t 
    hostname SW5
    vtp version 2
    vtp mode server
    vtp domain Grupo24
    vtp usac2025
    vlan 17
        name Estudiantes
        exit
    vlan 27
        name Docentes
        exit
    vlan 37
        name Seguridad
        exit
    vlan 47
        name Biblioteca
        exit
    interface FastEthernet 0/10
        switchport mode trunk
        exit
    interface FastEthernet 0/11
        switchport mode trunk
        exit
    interface FastEthernet 0/1
        switchport mode access
        switchport access vlan 17
        exit
    interface FastEthernet 0/2
        switchport mode access
        switchport access vlan 27
        exit
    interface FastEthernet 0/3
        switchport mode access
        switchport access vlan 37
        exit
    interface FastEthernet 0/4
        switchport mode access
        switchport access vlan 47
        exit
    do write
    exit
```

### Routers:
- R4:
```bash
enable
conf t
```
- R5:
```bash
enable
conf t
```

# BackBone: