# BRKGA Solver for MDVRP (Multi-Depot Vehicle Routing Problem)

## Descripción del Proyecto

Este proyecto implementa un algoritmo BRKGA (Biased Random-Key Genetic Algorithm) para resolver el problema MDVRP, una variante del problema de enrutamiento de vehículos con múltiples depósitos. El sistema incluye funcionalidades para cargar instancias del problema, resolverlas mediante técnicas evolutivas y visualizar los resultados.

## Características principales

1. **Parser MDVRP**: Carga y procesa archivos de instancias en formato estándar
2. **Algoritmo BRKGA**: Implementación completa con operadores genéticos especializados
3. **Visualización**: Herramientas gráficas para analizar soluciones
4. **Validación**: Verificación automática de factibilidad de soluciones

## Requisitos del sistema

- Python 3.8 o superior
- Librerías requeridas (instalables via pip):
  - numpy >= 1.20.0
  - matplotlib >= 3.4.0
  - scipy >= 1.7.0

## Estructura del código

El proyecto puede ejecutarse de dos formas:

1. **Como Jupyter Notebook**:
   - Contiene celdas ejecutables paso a paso
   - Ideal para experimentación y análisis
   - Incluye visualizaciones interactivas

2. **Como script Python**:
   - Ejecución directa desde terminal
   - Opciones configurables por parámetros
   - Genera reportes en formato texto

## Funciones

### Procesamiento de datos
- parse_mdvrp_file(): Carga y estructura datos de instancias MDVRP
- calculate_route_distance(): Calcula distancias euclidianas para rutas

### Algoritmo BRKGA
- Clase BRKGA_MDVRP: Implementa el algoritmo evolutivo completo
  - initialize_population(): Crea población inicial
  - decode(): Transforma cromosomas en soluciones
  - fitness(): Evalúa calidad de soluciones
  - crossover(): Operador de recombinación
  - evolve(): Genera nueva población
  - solve(): Ejecuta el proceso evolutivo

### Visualización
- plot_mdvrp_instance(): Muestra distribución geográfica de clientes/depósitos
- visualize_routes(): Dibuja rutas de solución con información detallada
- Gráficos de convergencia: Muestran mejora del fitness por generación

### Validación
- debug_solution(): Verifica restricciones y detecta violaciones
- chromosome_to_solution(): Convierte cromosomas a estructura legible

## Ejecución del proyecto

Para usar el Jupyter Notebook:
1. Instalar Jupyter: pip install notebook
2. Ejecutar: jupyter notebook BRKGA_MDVRP.ipynb
3. Ejecutar celdas en orden

Para ejecutar como script:
1. Guardar código como BRKGA_MDVRP.py
2. Ejecutar: python BRKGA_MDVRP.py instancia.txt
3. Parámetros opcionales:
   - --popsize: Tamaño de población (default 100)
   - --generations: Número de generaciones (default 50)
   - --elite: Porcentaje élite (default 0.2)

## Formatos de entrada/salida

Entrada:
- Archivos .txt en formato MDVRP estándar
- Primera línea: tipo_problema num_vehiculos num_clientes num_depositos
- Líneas siguientes: especificaciones de vehículos y clientes

Salida:
- Soluciones como listas de rutas con métricas asociadas
- Gráficos de convergencia y visualización geográfica
- Reportes de validación en consola

## Personalización

Los parámetros clave del algoritmo son ajustables:
- Tamaño de población
- Porcentajes de élite/mutantes
- Probabilidad de sesgo en cruce
- Criterios de terminación
- Funciones de penalización

## Limitaciones conocidas

- Diseñado para instancias pequeñas/medianas
- Distancias euclidianas (no incluye matriz de distancias precalculada)
- Ventanas de tiempo implementadas pero no utilizadas en fitness básico

## Referencias 

[1] Christofides, N., Eilon, S.: An algorithm for the vehicle-dispatching problem. Oper. Res. Q. 20(3), 309–318 (1969).

[2] Gillett, B., Johnson, J.: Multi-terminal vehicle-dispatch algorithm. Omega 4(6), 711–718 (1976).

[3] Chao, I., Golden, B., Wasil, E.: A new heuristic for the multi-depot vehicle routing problem that improves upon best-known solutions. Am. J. Math. Manag.Sci. 13(3), 371–406 (1993).

[4] Cordeau, J., Gendreau, M., Laporte, G.: A tabu search heuristic for periodic and multi-depot vehicle routing problems. Networks 30(2), 105–119 (1997).

[5] Cordeau, J., Maischberger, M.: A parallel iterated tabu search heuristic for vehicle routing problems. Comput. Oper. Res. 39(9), 2033–2050 (2012)

[6] Subramanian, A., Uchoa, E., Ochi, L.S.: A hybrid algorithm for a class of vehicle routing problems. Comput. Oper. Res. 40(10), 2519–2531 (2013)

[7] Vidal, T., Crainic, T., Gendreau, M., Lahrichi, N., Rei, W.: A hybrid genetic algorithm for multi-depot and periodic vehicle routing problems. Oper. Res. 60(3), 611–624 (2012).

[8] Escobar, J. W., Linfati, R., Toth, P., & Baldoquin, M. G. (2014). A hybrid granular tabu search algorithm for the multi-depot vehicle routing problem. Journal of Heuristics, 20(5), 483-509.
