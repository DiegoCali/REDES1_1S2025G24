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
| Biblioteca  | 47         | 100     | 192.168.24.0/25   |
| Estudiantes | 17         | 50      | 192.168.24.128/26 |
| Docentes    | 27         | 20      | 192.168.24.192/27 |
| Seguridad   | 37         | 5       | 192.168.24.224/29 |

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
| Biblioteca  | 47         | 75      | 192.148.24.0/25   |
| Estudiantes | 17         | 45      | 192.148.24.128/26 |
| Docentes    | 27         | 25      | 192.148.24.192/27 |
| Seguridad   | 37         | 10      | 192.148.24.224/28 |

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
| Biblioteca | 47         | 50      | 172.16.24.64/26   |
| Docentes   | 27         | 35      | 172.16.24.128/26  |
| Seguridad  | 37         | 5       | 172.16.24.192/29  |

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

> [!NOTE]
> ID de red de central 192.120.0.0/14

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
    vtp password usac2025
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
    vtp password usac2025
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
    vtp password usac2025
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
    ip routing
    hostname MS8    
    interface GigabitEthernet 0/1
        no shutdown
        ip address 10.0.0.70 255.255.255.252
        exit
    interface range FastEthernet 0/1-3
        switchport trunk encapsulation dot1q
        switchport mode trunk
        exit
    interface vlan 17
        ip address 192.168.24.129 255.255.255.192
        exit
    interface vlan 27
        ip address 192.168.24.193 255.255.255.224
        exit
    interface vlan 37
        ip address 192.168.24.225 255.255.255.248
        exit
    interface vlan 47
        ip address 192.168.24.1 255.255.255.128
        exit
    router eigrp 100
        network 192.168.24.0 0.0.0.255
        network 10.0.0.68 0.0.0.3
        exit
    do write
    exit
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
    vtp password usac2025
    interface GigabitEthernet 0/1
        switchport mode trunk
        exit
    interface FastEthernet 0/10
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
    vtp password usac2025
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
> [!NOTE]
> Los routers que indica el documento son los `1941`, los que tienen comunicación WAN es necesarios agregarles el modulo: `HWIC-2T`.

- R0:
```bash
enable
conf t
    hostname R0
    interface GigabitEthernet 0/0
        no shutdown
        exit
    interface GigabitEthernet 0/0.17
        encapsulation dot1Q 17
        ip address 192.148.24.129 255.255.255.192
        no shutdown
        exit
    interface GigabitEthernet 0/0.27
        encapsulation dot1Q 27
        ip address 192.148.24.193 255.255.255.224
        no shutdown
        exit
    interface GigabitEthernet 0/0.37
        encapsulation dot1Q 37
        ip address 192.148.24.225 255.255.255.240
        no shutdown
        exit
    interface GigabitEthernet 0/0.47
        encapsulation dot1Q 47
        ip address 192.148.24.0 255.255.255.128
        no shutdown
        exit
    interface serial 0/0/0
        ip address 10.0.0.14 255.255.255.252
        no shutdown
        exit
    interface serial 0/0/1
        ip address 10.0.0.21 255.255.255.252
        no shutdown
        exit
    router rip
        version 2
        no auto-summary        
        network 10.0.0.12
        network 10.0.0.20
        network 192.148.24.0               
    do write
    exit
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
    vtp password usac2025
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
    vtp password usac2025
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
    vtp password usac2025
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
    vtp password usac2025
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
    hostname MS1
    ip routing
    interface FastEthernet 0/1
        switchport trunk encapsulation dot1q
        switchport mode trunk
        exit  
    interface FastEthernet 0/10
        switchport trunk encapsulation dot1q
        switchport mode trunk
        ip address 10.0.0.1 255.255.255.252        
        exit  
    interface vlan 17
        ip address 172.16.24.2 255.255.255.192
        standby 17 ip 172.16.24.1
        standby 17 priority 110
        standby 17 preempt
        no shutdown
    interface vlan 27
        ip address 172.16.24.130 255.255.255.192
        standby 27 ip 172.16.24.129
        standby 27 priority 110
        standby 27 preempt
        no shutdown
    interface vlan 37
        ip address 172.16.24.194 255.255.255.248
        standby 37 ip 172.16.24.193
        standby 37 priority 110
        standby 37 preempt
        no shutdown
    interface vlan 47
        ip address 172.16.24.66 255.255.255.192
        standby 47 ip 172.16.24.65
        standby 47 priority 110
        standby 47 preempt
        no shutdown
    router rip
        version 2
        no auto-summary
        network 10.0.0.0
        network 172.16.24.0
    do write
    exit
```

- MS2:
```bash
enable
conf t
    hostname MS2
    ip routing
    interface FastEthernet 0/1
        switchport trunk encapsulation dot1q
        switchport mode trunk
        exit  
    interface FastEthernet 0/10
        switchport trunk encapsulation dot1q
        switchport mode trunk
        ip address 10.0.0.5 255.255.255.252
        exit  
    interface vlan 17
        ip address 172.16.24.3 255.255.255.192
        standby 17 ip 172.16.24.1
        standby 17 priority 100
        standby 17 preempt
        no shutdown
    interface vlan 27
        ip address 172.16.24.131 255.255.255.192
        standby 27 ip 172.16.24.129
        standby 27 priority 100
        standby 27 preempt
        no shutdown
    interface vlan 37
        ip address 172.16.24.195 255.255.255.248
        standby 37 ip 172.16.24.193
        standby 37 priority 100
        standby 37 preempt
        no shutdown
    interface vlan 47
        ip address 172.16.24.67 255.255.255.192
        standby 47 ip 172.16.24.65
        standby 47 priority 100
        standby 47 preempt
        no shutdown
    router rip
        version 2
        no auto-summary
        network 10.0.0.4
        network 172.16.24.0        
        exit
    do write
    exit
```

## Central:

- SW0:
```bash
enable
conf t
    hostname SW0
    vlan 57
        name Server0
        exit
    vlan 67
        name Server1
        exit
    vlan 77
        name Server2
        exit
    interface GigabitEthernet 0/10        
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
    interface FastEthernet 0/3
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
    hostname R7
    interface GigabitEthernet 0/0
        no shutdown
        exit
    interface GigabitEthernet 0/1
        no shutdown
        ip address 10.0.0.58 255.255.255.252
        exit
    interface GigabitEthernet 0/0.57
        encapsulation dot1Q 57
        ip address 192.120.24.1 255.255.255.0
        exit
    interface GigabitEthernet 0/0.67
        encapsulation dot1Q 67
        ip address 192.121.24.1 255.255.255.0
        exit
    interface GigabitEthernet 0/0.77
        encapsulation dot1Q 77
        ip address 192.122.24.1 255.255.255.0
        exit
    ip route 10.0.0.32 255.255.255.252 10.0.0.57
    ip route 10.0.0.40 255.255.255.252 10.0.0.57
    do write 
    exit
```

## CUM:

- SW5: 
```bash
enable
conf t 
    hostname SW5
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
    interface GigabitEthernet 0/1
        switchport mode trunk
        no shutdown
        exit
    interface GigabitEthernet 0/2
        switchport mode trunk
        no shutdown
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
    hostname R4
    interface GigabitEthernet 0/0
        no shutdown
        exit
    interface GigabitEthernet 0/0.17
        encapsulation dot1Q 17
        ip address 192.158.24.2 255.255.255.192
        standby 17 ip 192.158.24.1
        standby 17 priority 110
        standby 17 preempt
        no shutdown
        exit
    interface GigabitEthernet 0/0.27
        encapsulation dot1Q 27
        ip address 192.158.24.66 255.255.255.224
        standby 27 ip 192.158.24.65
        standby 27 priority 110
        standby 27 preempt
        no shutdown
        exit
    interface GigabitEthernet 0/0.37
        encapsulation dot1Q 37
        ip address 192.158.24.98 255.255.255.240
        standby 37 ip 192.158.24.97
        standby 37 priority 110
        standby 37 preempt
        no shutdown
        exit
    interface GigabitEthernet 0/0.47
        encapsulation dot1Q 47
        ip address 192.158.24.114 255.255.255.128
        standby 47 ip 192.158.24.113
        standby 47 priority 110
        standby 47 preempt
        no shutdown
        exit
    interface GigabitEthernet 0/1
        no shutdown
        ip address 10.0.0.50 255.255.255.252
        exit
    router ospf 1
        network 192.158.24.0 0.0.0.255 area 0
        network 10.0.0.48 0.0.0.3 area 1
        exit
    do write
    exit
```
- R5:
```bash
enable
conf t
    hostname R5
    interface GigabitEthernet 0/0
        no shutdown
        exit
    interface GigabitEthernet 0/0.17
        encapsulation dot1Q 17
        ip address 192.158.24.3 255.255.255.192
        standby 17 ip 192.158.24.1
        standby 17 priority 100
        standby 17 preempt
        no shutdown
        exit
    interface GigabitEthernet 0/0.27
        encapsulation dot1Q 27
        ip address 192.158.24.67 255.255.255.224
        standby 27 ip 192.158.24.65
        standby 27 priority 100
        standby 27 preempt
        no shutdown
        exit
    interface GigabitEthernet 0/0.37
        encapsulation dot1Q 37
        ip address 192.158.24.99 255.255.255.240
        standby 37 ip 192.158.24.97
        standby 37 priority 100
        standby 37 preempt
        no shutdown
        exit
    interface GigabitEthernet 0/0.47
        encapsulation dot1Q 47
        ip address 192.158.24.115 255.255.255.128
        standby 47 ip 192.158.24.113
        standby 47 priority 100
        standby 47 preempt
        no shutdown
        exit
    interface GigabitEthernet 0/1
        no shutdown
        ip address 10.0.0.54 255.255.255.252
        exit
    router ospf 1
        network 192.158.24.0 0.0.0.255 area 0
        network 10.0.0.52 0.0.0.3 area 1
        exit
    do write
    exit
```

# BackBone:

- ID de red 10.0.0.0/24
- Método de segmentación: FSLM

# RIP: 

> [!NOTE]
> Para la red en RIP se puede poner solo el ID de red general
>  Sin embargo si se tienen problemas se puede especificar las otrass redes.

 De     | a     | ID de red        | Dirección IP |
--------|-------|------------------|--------------|
MS1     | MS0   | 172.16.24.0/24   | ---          |
MS1     | MS3   | 10.0.0.0/30      | 10.0.0.1     |
MS3     | MS1   | 10.0.0.0/30      | 10.0.0.2     |
MS2     | MS3   | 10.0.0.4/30      | 10.0.0.5     |
MS3     | MS2   | 10.0.0.4/30      | 10.0.0.6     |
MS3     | R1    | 10.0.0.8/30      | 10.0.0.9     |
R1      | MS3   | 10.0.0.8/30      | 10.0.0.10    |
R1      | R0    | 10.0.0.12/30     | 10.0.0.13    |
R0      | R1    | 10.0.0.12/30     | 10.0.0.14    |
R1      | R2    | 10.0.0.16/30     | 10.0.0.17    |
R2      | R1    | 10.0.0.16/30     | 10.0.0.18    |
R0      | SW2   | 192.148.24.0/24  | ---          |
R0      | R2    | 10.0.0.20/30     | 10.0.0.21    |
R2      | R0    | 10.0.0.20/30     | 10.0.0.22    |

- MS3:
```bash
enable 
conf t
    hostname MS3
    ip routing
    interface FastEthernet 0/1
        switchport trunk encapsulation dot1q
        switchport mode trunk
        ip address 10.0.0.2 255.255.255.252
        exit
    interface FastEthernet 0/2
        switchport trunk encapsulation dot1q
        switchport mode trunk
        ip address 10.0.0.5 255.255.255.252
        exit
    interface GigabitEthernet 0/1
        switchport trunk encapsulation dot1q
        switchport mode trunk
        ip address 10.0.0.9 255.255.255.252
        exit
    router rip
        version 2
        no auto-summary
        network 10.0.0.0
        network 10.0.0.4
        network 10.0.0.8
        exit
    do write
    exit
```
- R1:
```bash
enable
conf t
    hostname R1
    interface GigabitEthernet 0/0
        no shutdown
        ip address 10.0.0.10 255.255.255.252
        exit
    interface serial 0/0/0
        ip address 10.0.0.13 255.255.255.252
        no shutdown
        exit
    interface serial 0/0/1
        ip address 10.0.0.17 255.255.255.252
        no shutdown
        exit
    router rip 
        version 2
        no auto-summary
        network 10.0.0.8
        network 10.0.0.12
        network 10.0.0.16
        exit
    do write
    exit
```
- R2:
```bash
enable
conf t
    hostname R2
    interface GigabitEthernet 0/0
        no shutdown
        ip address 10.0.0.25 255.255.255.252
        exit
    interface serial 0/0/0 
        ip address 10.0.0.18 255.255.255.252
        no shutdown
        exit
    interface serial 0/0/1
        ip address 10.0.0.22 255.255.255.252
        no shutdown
        exit
    router rip 
        version 2
        no auto-summary        
        network 10.0.0.16
        network 10.0.0.20        
        redistribute
        exit
    router ospf 1
        network 10.0.0.24 0.0.0.3 area 0
        exit
    router rip
        redistribute ospf metric 2
        exit
    router ospf 1
        redistribute rip subnets
        exit
    do write
    exit
```

# OSPF

> [!NOTE]
> Tener en cuenta de MS4 a MS7 existen EtherChannels.

 De     | a     | ID de red        | Dirección IP |
--------|-------|------------------|--------------|
R2      | R3    | 10.0.0.24/30     | 10.0.0.25    |
R3      | R2    | 10.0.0.24/30     | 10.0.0.26    |
R3      | MS4   | 10.0.0.28/30     | 10.0.0.29    |
MS4     | R3    | 10.0.0.28/30     | 10.0.0.30    |
MS4     | MS5   | 10.0.0.32/30     | 10.0.0.33    |
MS5     | MS4   | 10.0.0.32/30     | 10.0.0.34    |
MS4     | MS6   | 10.0.0.36/30     | 10.0.0.37    |
MS6     | MS4   | 10.0.0.36/30     | 10.0.0.38    |
MS5     | R7    | 10.0.0.56/30     | 10.0.0.57    |
R7      | MS5   | 10.0.0.56/30     | 10.0.0.58    |
MS5     | MS7   | 10.0.0.40/30     | 10.0.0.41    |
MS7     | MS5   | 10.0.0.40/30     | 10.0.0.42    |
MS6     | MS7   | 10.0.0.44/30     | 10.0.0.45    |
MS7     | MS6   | 10.0.0.44/30     | 10.0.0.46    |
MS6     | R4    | 10.0.0.48/30     | 10.0.0.49    |
R4      | MS6   | 10.0.0.48/30     | 10.0.0.50    |
MS6     | R5    | 10.0.0.52/30     | 10.0.0.53    |
R5      | MS6   | 10.0.0.52/30     | 10.0.0.54    |

- R3:
```bash
enable
conf t
    hostname R3
    interface GigabitEthernet 0/0
        no shutdown
        ip address 10.0.0.26 255.255.255.252
        exit
    interface GigabitEthernet 0/1
        no shutdown
        ip address 10.0.0.29 255.255.255.252
        exit
    router ospf 1
        network 10.0.0.24 0.0.0.3 area 0
        network 10.0.0.28 0.0.0.3 area 1
        exit
    do write
    exit
```
- MS4:
```bash
enable
conf t
    hostname MS4
    ip routing
    interface GigabitEthernet 0/1
        no shutdown
        ip address 10.0.0.30 255.255.255.252
        exit
    interface range FastEthernet 0/1-3
        channel-group 1 mode active
        exit
    interface port-channel 1        
        no switchport
        ip address 10.0.0.33 255.255.255.252
        exit
    interface range FastEthernet 0/4-6
        channel-group 2 mode active
        exit
    interface port-channel 2        
        no switchport
        ip address 10.0.0.37 255.255.255.252
        exit
    router ospf 1
        network 10.0.0.28 0.0.0.3 area 0
        network 10.0.0.32 0.0.0.3 area 1
        network 10.0.0.36 0.0.0.3 area 2
        exit
    do write
    exit
```
- MS5:
```bash
enable
conf t
    hostname MS5
    ip routing
    interface GigabitEthernet 0/1
        no shutdown        
        ip address 10.0.0.57 255.255.255.252
        exit
    interface range FastEthernet 0/1-3
        channel-group 1 mode passive
        exit
    interface port-channel 1
        no switchport
        ip address 10.0.0.34 255.255.255.252
        exit
    interface range FastEthernet 0/4-6
        channel-group 2 mode active
        exit
    interface port-channel 2
        no switchport
        ip address 10.0.0.41 255.255.255.252
        exit
    ip route 192.120.24.0 255.255.255.0 10.0.0.58
    ip route 192.121.24.0 255.255.255.0 10.0.0.58
    ip route 192.122.24.0 255.255.255.0 10.0.0.58
    router ospf 1 
        network 10.0.0.57 0.0.0.3 area 0
        network 10.0.0.32 0.0.0.3 area 1
        network 10.0.0.40 0.0.0.3 area 2
        redistribute static subnets
        exit
    do write
    exit
```
- MS6:
```bash
enable
conf t
    hostname MS6
    ip routing
    interface GigabitEthernet 0/1
        no shutdown
        ip address 10.0.0.49 255.255.255.252
        exit
    interface GigabitEthernet 0/2
        no shutdown
        ip address 10.0.0.53 255.255.255.252
        exit
    interface range FastEthernet 0/1-3
        channel-group 1 mode passive
        exit
    interface port-channel 1
        no switchport
        ip address 10.0.0.38 255.255.255.252
        exit
    interface range FastEthernet 0/4-6
        channel-group 2 mode active
        exit
    interface port-channel 2
        no switchport
        ip address 10.0.0.45 255.255.255.252
        exit
    router ospf 1
        network 10.0.0.48 0.0.0.3 area 0
        network 10.0.0.52 0.0.0.3 area 1
        network 10.0.0.36 0.0.0.3 area 2
        network 10.0.0.44 0.0.0.3 area 3
        exit
    do write
    exit
```
- MS7:
```bash
enable
conf t
    hostname MS7
    ip routing
    interface GigabitEthernet 0/1
        no shutdown
        ip address 10.0.0.61 255.255.255.252
        exit
    interface range FastEthernet 0/1-3
        channel-group 1 mode passive
        exit
    interface port-channel 1
        no switchport
        ip address 10.0.0.42 255.255.255.252
        exit
    interface range FastEthernet 0/4-6
        channel-group 2 mode passive
        exit
    interface port-channel 2
        no switchport
        ip address 10.0.0.46 255.255.255.252
        exit
    router ospf 1
        network 10.0.0.40 0.0.0.3 area 0
        network 10.0.0.44 0.0.0.3 area 1        
        exit
    router eigrp 100
        no auto-summary
        network 10.0.0.60 0.0.0.3
        exit
    router ospf 1
        redistribute eigrp 100 subnets
        exit
    router eigrp 100
        redistribute ospf 1 metric 10000 100 255 1 1500
        exit
    do write
    exit
```

# EIGRP:

 De     | a     | ID de red        | Dirección IP |
--------|-------|------------------|--------------|
MS7     | R9    | 10.0.0.60/30     | 10.0.0.61    |
R9      | MS7   | 10.0.0.60/30     | 10.0.0.62    |
R9      | R10   | 10.0.0.64/30     | 10.0.0.65    |
R10     | R9    | 10.0.0.64/30     | 10.0.0.66    |
R10     | MS8   | 10.0.0.68/30     | 10.0.0.69    |
MS8     | R10   | 10.0.0.68/30     | 10.0.0.70    |

- R9:
```bash
enable 
conf t
    hostname R9
    interface GigabitEthernet 0/0
        no shutdown
        ip address 10.0.0.62 255.255.255.252
        exit
    interface GigabitEthernet 0/1
        no shutdown
        ip address 10.0.0.65 255.255.255.252
        exit
    router eigrp 100
        no auto-summary
        network 10.0.0.60 0.0.0.3
        network 10.0.0.64 0.0.0.3
        exit
    do write
    exit
```
- R10:
```bash
enable 
conf t
    hostname R10
    interface GigabitEthernet 0/0
        no shutdown
        ip address 10.0.0.66 255.255.255.252
        exit
    interface GigabitEthernet 0/1
        no shutdown
        ip address 10.0.0.69 255.255.255.252
        exit
    router eigrp 100
        no auto-summary
        network 10.0.0.64 0.0.0.3
        network 10.0.0.68 0.0.0.3
        exit
    do write
    exit
```