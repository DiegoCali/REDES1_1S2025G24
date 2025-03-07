# División de trabajo:

## Diego:
- Área de Administración
- Área de Desarrollo

## Josué:
- Área de Infraestructura
- Área de Gerencia
- Área Central (Backbone)

# Estándares:

## Vlans Generales:
| Departamento | Vlan | ID de red       |
|--------------|------|-----------------|
| Ventas       | 17   | 192.168.17.0/24 |
| Soporte      | 27   | 192.168.27.0/24 |
| Gerencia     | 37   | 192.168.37.0/24 |
| Seguridad    | 47   | 192.168.47.0/24 |

## Otras Vlans:
| Área         | Vlan | ID de red       |
|--------------|------|-----------------|
| Recepción    | 57   | 192.168.57.0/24 |

# Instrucciones:

- Crea un área con los estándares previos
- Guardar los comandos en un script por área y guardarlos en scripts/. ej: script_admin.txt
- Tomar capturas del área y guardarlas en img/. ej: admin.jpg
- Añadir el presupuesto de esa área en el archivo **BUDGET.md**. *(ver ejemplo 1)*
- Añadir las IPs en el archivo **README.md**. *(ver ejemplo 2)*

> [!NOTE]
> El manual del proyecto será el archivo **README.md** ya que es lo primero que aparece.

## Ejemplo 1:
```markdown
| Articulo     | Cantidad | Precio    | Subtotal  |
|--------------|----------|-----------|-----------|
| PC           | 10       | 1,500.00  | 15,000.00 |
<!-- Agregar mas con este formato -->
```

## Ejemplo 2:
```markdown
| Área         | Nombre | Dirección IP    |
|--------------|--------|-----------------|
| Recepción    | PC0    | 192.168.57.1    |
<!-- Agregar mas con este formato -->
```

> [!IMPORTANT]
> Como Packet Tracer no permite trabajar en conjunto, se harán los commits en la misma rama. Informar que dia se trabajará y ese día solo trabajará esa persona.
