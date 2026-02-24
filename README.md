import xml.etree.ElementTree as ET

def mostrar_vuelos(root):
    """Muestra todos los vuelos"""
    for vuelo in root.findall("vuelo"):
        imprimir_vuelo(vuelo)

def buscar_por_campo(root, campo, valor):
    """Busca vuelos por origen o destino"""
    encontrado = False
    for vuelo in root.findall("vuelo"):
        dato = vuelo.find(campo).text
        if dato.lower() == valor.lower():
            imprimir_vuelo(vuelo)
            encontrado = True
    if not encontrado:
        print(f"No se encontraron vuelos con {campo} = {valor}")

def imprimir_vuelo(vuelo):
    """Imprime los datos de un vuelo"""
    print("Código:", vuelo.find("codigo").text)
    print("Origen:", vuelo.find("origen").text)
    print("Destino:", vuelo.find("destino").text)
    print("Duración:", vuelo.find("duracion").text, "horas")
    print("Aerolínea:", vuelo.find("aerolinea").text)
    print("-------------------------")

def menu(root):
    """Menú interactivo para el usuario"""
    while True:
        print("\n=== Menú de Vuelos ===")
        print("1. Mostrar todos los vuelos")
        print("2. Buscar vuelos por origen")
        print("3. Buscar vuelos por destino")
        print("4. Salir")

        opcion = input("Seleccione una opción: ")

        if opcion == "1":
            mostrar_vuelos(root)
        elif opcion == "2":
            origen = input("Ingrese origen: ")
            buscar_por_campo(root, "origen", origen)
        elif opcion == "3":
            destino = input("Ingrese destino: ")
            buscar_por_campo(root, "destino", destino)
        elif opcion == "4":
            print("Saliendo...")
            break
        else:
            print("Opción inválida, intente de nuevo.")

if __name__ == "__main__":
    # Abrir archivo XML con ruta completa
    tree = ET.parse("C:/Users/kevin/PyCharmMiscProject/vuelos.xml")
    root = tree.getroot()
    menu(root)

