# luis david sanchez castillo
# grupo 213022A_2201
# fundamentos de programacion
# Código Fuente: autoría propia
menu = [
    ["Empanadas de carne", "Entrada", 12000],
    ["Patacones con Hogao", "Entrada", 15000],
    ["Arepa de Chócolo", "Entrada", 10000],
    ["Bandeja Paisa", "Plato Fuerte", 35000],    
    ["Ajiaco ", "Plato Fuerte", 32000],  
    ["Arroz con Pollo", "Plato Fuerte", 25000],    
    ["Jugo", "Bebida", 8000],
    ["Limonada de Coco", "Bebida", 12000],
    ["Cerveza Nacional", "Bebida", 15000]
]

def calcular_precio_final(precio_base, categoria_producto, categoria_objetivo, umbral_precio):

    if categoria_producto == categoria_objetivo and precio_base > umbral_precio:
        descuento = precio_base * 0.15
        return precio_base - descuento
    return precio_base


categoria_promo = "Plato Fuerte"
umbral_promo = 30000

print("\n" + "=" * 60)
print("BIENVENIDO AL RESTAURANTE LA SAZON DE LA TIA")
print(f"PROMOCIÓN: 15% en los {categoria_promo} con valor mayor a ${umbral_promo:,}")
print("=" * 60)

print(f"\nNº | {'Producto':<22} | {'Categoría':<15} | {'Precio'}")
print("-" * 60)

for i in range(len(menu)):
    nombre = menu[i][0]
    categoria = menu[i][1]
    precio_base = menu[i][2]
    
    precio_final = calcular_precio_final(precio_base, categoria, categoria_promo, umbral_promo)
    
    print(f"{i+1:2} | {nombre:<22} | {categoria:<15} | ${int(precio_base):,}")

print("-" * 60)

orden_cliente = []
ordenando = True

while ordenando:
    try:
        seleccion = int(input("\nIngrese el número del producto que desea pedir (1-9): "))
        
        if 1 <= seleccion <= len(menu):
            indice_producto = seleccion - 1
            producto_elegido = menu[indice_producto]
            
            orden_cliente.append(producto_elegido)
            print(f"¡{producto_elegido[0]} agregado a su cuenta!")
            
        else:
            print("Número inválido. Por favor elija un producto del 1 al 9.")
            continue
            
        respuesta = input("¿Desea pedir otro producto? (s/n): ").strip().lower()
        if respuesta != 's':
            ordenando = False
            
    except ValueError:
        print("Por favor, ingrese únicamente números.")

print("\n" + "=" * 50)
print("RESUMEN DE SU CUENTA")
print("=" * 50)

total_cuenta = 0
ahorro_total = 0

for item in orden_cliente:
    nombre = item[0]
    categoria = item[1]
    precio_base = item[2]
    
    precio_final = calcular_precio_final(precio_base, categoria, categoria_promo, umbral_promo)
    
    if precio_final < precio_base:
        print(f"• {nombre:<20} : ${int(precio_final):,} (Descuento aplicado)")
        ahorro_total += (precio_base - precio_final)
    else:
        print(f"• {nombre:<20} : ${int(precio_base):,}")
        
    total_cuenta += precio_final

print("-" * 50)
print(f"TOTAL A PAGAR: ${int(total_cuenta):,}")
if ahorro_total > 0:
    print(f"¡Usted ahorró ${int(ahorro_total):,} gracias a nuestra promoción!")
print("=" * 50)
print("¡Gracias por su visita!\n")
