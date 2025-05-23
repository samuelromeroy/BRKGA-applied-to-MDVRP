# BRKGA Solver for MDVRP (Multi-Depot Vehicle Routing Problem)

## Descripción del Proyecto

Este proyecto implementa un algoritmo BRKGA (Biased Random-Key Genetic Algorithm) para resolver el problema MDVRP, una variante del problema de enrutamiento de vehículos con múltiples depósitos. El sistema incluye funcionalidades para cargar instancias del problema, resolverlas mediante técnicas evolutivas y visualizar los resultados.

## Características principales

- Parser para archivos de instancia MDVRP. 
- Funciones para visualización de la instancia y solucionador.
- Algoritmo de optimización BRKGA. 
- Sistema de validación de soluciones.
- Grid search de hiperparámetros. 
- Ejecución batch en múltiples instancias

## Estructura de la instancia 

Línea 1: 
<problem_type> <num_vehicles> <num_customers> <num_depots>

Líneas 2-(num_depots+1): 
<max_duration> <max_load> (Especificaciones por vehículo)

Líneas restantes (clientes):
<id> <x> <y> <service_duration> <demand> <frequency> <num_visit_combinations>
<visit_combinations> [time_window_start] [time_window_end]

Ejemplo detallado:
1 4 50 4       # Problema tipo 1, 4 vehículos, 50 clientes, 4 depósitos
200 100        # Vehículo 1: Duración máxima 200, Carga 100
...            # (3 líneas más de especificaciones de vehículos)
5 12 45 30 15 2 3 1 4 2 0 50  # Cliente ID 5 en (12,45), servicio 30u.t., demanda 15
...

Características especiales:
- Los depósitos se identifican por demanda=0 y frecuencia=0
- Las ventanas de tiempo son opcionales
  
## Requisitos del sistema

- Python 3.8 o superior
- Librerías requeridas (instalables via pip):
  - numpy >= 1.20.0
  - matplotlib >= 3.4.0
  - scipy >= 1.7.0

## Componentes principales del código 

Parser MDVRP (parse_mdvrp_file)
-----------------------------------
Función: Convierte archivos .txt en estructura de datos Python
Entrada: Ruta de archivo .txt
Salida: Diccionario estructurado con:
- Metadatos del problema
- Lista de depósitos con coordenadas
- Lista de clientes con 15 atributos detallados
- Especificaciones técnicas de vehículos

Sistema de Visualización
----------------------------
Funciones principales:
- plot_mdvrp_instance: Mapa 2D con:
  * Depósitos como cuadrados rojos
  * Clientes escalados por demanda
  * Etiquetas de ventanas de tiempo
  * Sistema de coordenadas ajustable

- visualize_routes: Visualización avanzada de soluciones:
  * Rutas multicolor con números de orden
  * Información flotante por ruta
  * Leyenda interactiva
  * Resumen de métricas globales

Implementación BRKGA (BRKGA_MDVRP)
---------------------------------------
Clase principal con métodos:
- Constructor: Configura parámetros del algoritmo
- decode: Transforma cromosomas en rutas válidas
- fitness: Función de evaluación con penalizaciones
- evolve: Mecanismo de evolución generacional
- solve: Loop principal de optimización

Parámetros clave del algoritmo:
- Tamaño poblacional: 100-2000 individuos
- Porcentaje de élite: 10-40%
- Tasa de mutación: 5-20%
- Generaciones: 50-1000 iteraciones

Validador de Soluciones (debug_solution)
--------------------------------------------
Sistema de verificación que chequea:
- Cumplimiento de capacidades vehiculares
- Respeto de ventanas de tiempo
- Cobertura completa de clientes
- Uso correcto de depósitos
- Consistencia de datos

Salida detallada:
- Reporte por ruta con métricas
- Detección de violaciones específicas
- Resumen general de validez

## Uso básico
--------------------------------------------------------------------------------
Ejemplo mínimo funcional:

# Carga de datos
from mdvrp_solver import parse_mdvrp_file, BRKGA_MDVRP, visualize_routes

data = parse_mdvrp_file('p01.txt')

# Configuración del solver
solver = BRKGA_MDVRP(
    data,
    population_size=1000,
    elite_percent=0.2,
    mutants_percent=0.1
)

# Optimización
solution, distance, history = solver.solve(generations=100)

# Visualización
visualize_routes(data, solution)

# Validación
debug_solution(data, solution, verbose=True)

## Ajuste de hiperparametros 
--------------------------------------------------------------------------------
Sistema incluido para búsqueda de parámetros:
- Búsqueda grid 
- Comparación de convergencias

## Ejecución en múltiples instancias 
--------------------------------------------------------------------------------
Función incluida para procesamiento batch:
- Procesa secuencialmente p01.txt a p23.txt
- Genera reporte consolidado en .txt
- Formato de salida:
  
  Instancia  | Depósitos | Clientes | Vehículos | Tiempo(s) | Distancia Total
  --------------------------------------------------------------------------
  p01.txt    |     4     |    50    |     4     |  152.34   |    1256.78







