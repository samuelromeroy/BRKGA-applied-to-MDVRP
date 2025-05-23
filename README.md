================================================================================
MDVRP SOLVER WITH BRKGA - DOCUMENTACIÓN COMPLETA
================================================================================

1. DESCRIPCIÓN DEL PROYECTO
--------------------------------------------------------------------------------
Implementación de un solucionador para el Problema de Ruteo de Vehículos con 
Múltiples Depósitos (MDVRP) utilizando un Algoritmo Genético con Claves Aleatorias
Sesgadas (BRKGA). El proyecto incluye:

- Parser para archivos de instancia MDVRP estándar
- Visualización avanzada de problemas y soluciones
- Algoritmo de optimización BRKGA altamente configurable
- Sistema de validación de soluciones
- Herramientas para ajuste de hiperparámetros
- Soporte para ejecución batch en múltiples instancias

2. ESTRUCTURA DE ARCHIVOS DE INSTANCIA
--------------------------------------------------------------------------------
Formato estándar para archivos .txt:

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
- Combinaciones de visita permiten múltiples patrones de servicio

3. COMPONENTES PRINCIPALES DEL CÓDIGO
--------------------------------------------------------------------------------
3.1 Parser MDVRP (parse_mdvrp_file)
-----------------------------------
Función: Convierte archivos .txt en estructura de datos Python
Entrada: Ruta de archivo .txt
Salida: Diccionario estructurado con:
- Metadatos del problema
- Lista de depósitos con coordenadas
- Lista de clientes con 15 atributos detallados
- Especificaciones técnicas de vehículos

3.2 Sistema de Visualización
----------------------------
Funciones principales:
- plot_mdvrp_instance: Mapa 2D interactivo con:
  * Depósitos como cuadrados rojos
  * Clientes escalados por demanda
  * Etiquetas de ventanas de tiempo
  * Sistema de coordenadas ajustable

- visualize_routes: Visualización avanzada de soluciones:
  * Rutas multicolor con números de orden
  * Información flotante por ruta
  * Leyenda interactiva
  * Resumen de métricas globales

3.3 Implementación BRKGA (BRKGA_MDVRP)
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

3.4 Validador de Soluciones (debug_solution)
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

4. LIBRERÍAS Y DEPENDENCIAS
--------------------------------------------------------------------------------
Requisitos mínimos:
- Python 3.7+
- Numpy 1.21+ (Manejo de matrices y operaciones vectorizadas)
- Matplotlib 3.5+ (Visualización 2D avanzada)

Requisitos opcionales:
- tqdm (Para barras de progreso en ejecuciones largas)
- pandas (Análisis de resultados y métricas)

Instalación completa:
pip install numpy matplotlib tqdm pandas

5. USO BÁSICO
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

6. AJUSTE DE HIPERPARÁMETROS
--------------------------------------------------------------------------------
Sistema incluido para optimización de parámetros:
- Búsqueda grid automatizada
- Comparación de convergencias
- Análisis tiempo-calidad
- Generación de gráficos comparativos

Ejecución:
python hyperparameter_tuning.py

Archivos de configuración:
- hyperparameter_grid.json: Define espacios de búsqueda
- instances.list: Listado de instancias a evaluar

7. EJECUCIÓN EN MÚLTIPLES INSTANCIAS
--------------------------------------------------------------------------------
Script incluido para procesamiento batch:
- Procesa secuencialmente p01.txt a p23.txt
- Genera reporte consolidado en .txt
- Formato de salida:
  
  Instancia  | Depósitos | Clientes | Vehículos | Tiempo(s) | Distancia Total
  --------------------------------------------------------------------------
  p01.txt    |     4     |    50    |     4     |  152.34   |    1256.78

Ejecución:
python batch_processor.py

8. RESULTADOS Y VALIDACIÓN
--------------------------------------------------------------------------------
Archivos de salida generados:
- resultados_instancias_completos.txt: Métricas principales
- convergence_plots/: Gráficos de convergencia por instancia
- solution_logs/: Detalles completos de mejores soluciones
- validation_reports/: Informes de validación detallados

9. LICENCIA Y REFERENCIAS
--------------------------------------------------------------------------------
Licencia MIT - Ver LICENSE para detalles completos

Referencias clave:
- Primer artículo sobre BRKGA: Gonçalves y Resende (2011)
- Instancias MDVRP estándar: Cordeau et al. (1997)
- Modelos de ventanas de tiempo: Solomon (1987)

10. CONTACTO Y SOPORTE
--------------------------------------------------------------------------------
Autores: [Tu Nombre]
Mantenimiento: [Tu Email]
Repositorio: [URL del Repositorio]
Reporte de errores: [Issues URL]



