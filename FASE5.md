"""
Programa para calcular y clasificar las horas trabajadas por semana de un equipo.

Este programa procesa los datos de horas trabajadas de 4 recursos durante la semana,
calcula el total de horas y clasifica la jornada como "Sobretiempo" o "Horario Estándar"
según un umbral configurable.
"""

# Umbral de horas estándar configurable
UMBRAL_HORAS = 40

# Matriz de datos: 4 recursos con horas trabajadas de lunes a viernes
EQUIPO = [
    ["Carlos", 8, 9, 8, 7, 8],
    ["Ana", 9, 9, 8, 10, 8],
    ["Luis", 7, 8, 8, 8, 7],
    ["María", 10, 9, 9, 8, 9],
]

# Función para calcular el total de horas de un recurso
def calcular_total_horas(recurso):
    """
    Calcula el total de horas trabajadas en la semana para un recurso.
    Args:
        recurso (list): Lista con nombre y horas de lunes a viernes
    Returns:
        int: Total de horas semanales
    """
    _, *horas = recurso
    return sum(horas)

# Función para clasificar la jornada laboral
def clasificar_jornada(total_horas, umbral=UMBRAL_HORAS):
    """
    Clasifica la jornada laboral según el total de horas.
    Args:
        total_horas (int): Total de horas trabajadas
        umbral (int): Límite de horas estándar
    Returns:
        str: "Sobretiempo" si excede el umbral, "Horario Estándar" si no
    """
    return "Sobretiempo" if total_horas > umbral else "Horario Estándar"

# Función que procesa todos los recursos
def procesar_recursos(equipo, umbral=UMBRAL_HORAS):
    """
    Calcula total de horas y clasificación para cada recurso.
    Args:
        equipo (list): Lista de recursos y sus horas
        umbral (int): Umbral de horas estándar
    Returns:
        list of tuples: (nombre, total_horas, clasificacion)
    """
    resultados = []
    for recurso in equipo:
        nombre = recurso[0]
        total = calcular_total_horas(recurso)
        clasificacion = clasificar_jornada(total, umbral)
        resultados.append((nombre, total, clasificacion))
    return resultados
#modifique nombres
# Función para imprimir los resultados en tabla alineada
def imprimir_reporte(resultados):
    """
    Imprime los resultados en formato de tabla.
    Args:
        resultados (list of tuples): Lista de (nombre, total, clasificacion)
    """
    encabezados = ["Recurso", "Total de Horas", "Clasificación"]
    ancho_nombre = max(len(r[0]) for r in resultados + [("Recurso",)])
    ancho_total = len("Total de Horas")
    ancho_clase = len("Clasificación")
    formato = f"{{:<{ancho_nombre}}} | {{:>{ancho_total}}} | {{:<{ancho_clase}}}"
    print(formato.format(*encabezados))
    print("-" * (ancho_nombre + ancho_total + ancho_clase + 6))
    for nombre, total, clasificacion in resultados:
        print(formato.format(nombre, total, clasificacion))

# Función principal
def main():
    resultados = procesar_recursos(EQUIPO)
    imprimir_reporte(resultados)

# Ejecutar programa
if __name__ == "__main__":
    main()

