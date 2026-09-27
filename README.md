"""Semana 15: uso de colecciones de datos (diccionarios).

Inventario sencillo para registrar, mostrar, buscar y eliminar productos.
"""

def solicitar_precio():
    """Solicita un precio numerico no negativo."""
    while True:
        try:
            precio = float(input("Ingrese el precio del producto: "))
            if precio >= 0:
                return precio
            print("El precio no puede ser negativo.")
        except ValueError:
            print("Ingrese un precio valido, por ejemplo 12.50.")


def solicitar_cantidad():
    """Solicita una cantidad entera mayor que cero."""
    while True:
        try:
            cantidad = int(input("Ingrese la cantidad disponible: "))
            if cantidad > 0:
                return cantidad
            print("La cantidad debe ser mayor que cero.")
                    except ValueError:
            print("Ingrese una cantidad entera valida.")


def buscar_clave(productos, nombre):
    """Devuelve la clave del producto ignorando mayusculas y minusculas."""
    nombre_buscado = nombre.casefold()
    for clave in productos:
        if clave.casefold() == nombre_buscado:
            return clave
    return None


def agregar_producto(productos):
    """Agrega un producto nuevo al diccionario del inventario."""
    nombre = input("Nombre del producto: ").strip()
    if not nombre:
        print("El nombre no puede estar vacio.")
        return
    if buscar_clave(productos, nombre) is not None:
        print("Ese producto ya esta registrado.")
        return

        precio = solicitar_precio()
    cantidad = solicitar_cantidad()
    productos[nombre] = {"precio": precio, "cantidad": cantidad}
    print(f"Producto '{nombre}' agregado correctamente.")


def mostrar_productos(productos):
    """Recorre y muestra todos los productos registrados."""
    if not productos:
        print("El inventario esta vacio.")
        return

    print("\n--- Inventario de productos ---")
    for nombre, datos in productos.items():
        print(
            f"{nombre}: precio ${datos['precio']:.2f} | "
            f"cantidad: {datos['cantidad']}"
        )


def buscar_producto(productos):
    """Busca un producto y muestra sus datos."""
    nombre = input("Ingrese el nombre que desea buscar: ").strip()
    clave = buscar_clave(productos, nombre)
    if clave is None:
        print("No se encontro ese producto.")
        return

    datos = productos[clave]
    print(
        f"{clave}: precio ${datos['precio']:.2f} | "
        f"cantidad: {datos['cantidad']}"
    )


def eliminar_producto(productos):
    """Elimina del inventario el producto indicado."""
    nombre = input("Ingrese el nombre del producto que desea eliminar: ").strip()
    clave = buscar_clave(productos, nombre)
    if clave is None:
        print("No se encontro ese producto.")
        return

    del productos[clave]
    print(f"Producto '{clave}' eliminado correctamente.")


    def main():
    # El diccionario relaciona el nombre de cada producto con sus datos.
    productos = {}

    # Menu principal: permite agregar, recorrer, buscar y eliminar elementos.
    while True:
        print("\n=== Registro de productos ===")
        print("1. Agregar producto")
        print("2. Mostrar inventario")
        print("3. Buscar producto")
        print("4. Eliminar producto")
        print("5. Salir")

        opcion = input("Seleccione una opcion: ").strip()
        if opcion == "1":
            agregar_producto(productos)
        elif opcion == "2":
            mostrar_productos(productos)
        elif opcion == "3":
            buscar_producto(productos)
        elif opcion == "4":
            eliminar_producto(productos)
        elif opcion == "5":
            print("Gracias por utilizar el registro de productos.")
            break
                    else:
            print("Opcion no valida. Seleccione un numero del 1 al 5.")


if __name__ == "__main__":
    main()
