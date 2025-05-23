# 🚚 MDVRP Solver con BRKGA ![Python](https://img.shields.io/badge/Python-3.7%2B-blue) [![Licencia: MIT](https://img.shields.io/badge/Licencia-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

![Visualización de Rutas MDVRP](docs/route_visualization.png)

## 📦 Tabla de Contenidos
1. [Descripción del Proyecto](#-descripción-del-proyecto)  
2. [Características Clave](#-características-clave)  
3. [Instalación](#-instalación)  
4. [Uso Rápido](#-uso-rápido)  
5. [Estructura del Proyecto](#-estructura-del-proyecto)  
6. [Configuración Avanzada](#-configuración-avanzada)  
7. [Hiperparámetros](#-hiperparámetros)  
8. [Validación](#-validación)  
9. [Resultados](#-resultados)  

<a name="descripción"></a>
## Descripción del Proyecto

Solución evolutiva para el **Problema de Ruteo de Vehículos con Múltiples Depósitos** que combina:
- Algoritmo Genético con Claves Aleatorias Sesgadas (BRKGA)
- Sistema de visualización 
- Parser para instancias MDVRP
- Módulo de validación
- Búsqueda de hipérparametros

## Instalación 

git clone [https://github.com/tu_usuario/mdvrp-solver.git](https://github.com/samuelromeroy/BRKGA-applied-to-MDVRP/edit/main/README.md)
cd mdvrp-solver 

Dependencias: 

NumPy	1.21+
Matplotlib	3.5+	

## Uso Rápido 

from mdvrp_solver import (
    parse_mdvrp_file,
    BRKGA_MDVRP,
    visualize_routes,
    debug_solution
)

# 1. Cargar instancia
data = parse_mdvrp_file('instances/p01.txt')

# 2. Configurar algoritmo
solver = BRKGA_MDVRP(
    data,
    population_size=1500,
    elite_percent=0.3,
    mutants_percent=0.1,
    p_bias=0.7
)

# 3. Ejecutar optimización
solution, distance, history = solver.solve(
    generations=500,
    verbose=True
)

# 4. Visualizar resultados
visualize_routes(
    data, 
    solution,
    show_demand=True,
    save_path='results/p01_solution.png'
)

# 5. Validar solución
is_valid, violations = debug_solution(data, solution)

## Estructura del proyecto 

mdvrp-solver/
├── instances/          # Archivos de entrada (.txt)
├── src/                # Código fuente
│   ├── core/           # Lógica principal
│   ├── utils/          # Herramientas auxiliares
│   └── visualization/  # Módulos gráficos
├── results/            # Salidas generadas
│   ├── convergence/    # Gráficas de convergencia
│   └── solutions/      # Archivos de solución
├── experiments/        # Scripts de experimentación
├── docs/               # Documentación técnica
└── tests/              # Casos de prueba

## Configuración avanzada

brkga:
  population_size: 1200
  elite_percent: 0.25
  mutants_percent: 0.15
  p_bias: 0.65
  
visualization:
  node_size: 150
  route_width: 2.5
  show_time_windows: true
  
output:
  save_plots: true
  plot_format: png
  report_format: txt

  ## Hipérparametros 
  
Parámetro	Valor Óptimo	Rango Recomendado	Efecto Principal
Tamaño Población	1500	500-2000	Diversidad genética
Porcentaje Élite	30%	20%-40%	Explotación de soluciones
Tasa de Mutación	10%	5%-15%	Exploración del espacio
Generaciones	500	100-1000	Balance tiempo-calidad
p_bias	0.7	0.6-0.8	Herencia de padres élite

## Validación 

validation_checks = {
    'capacity': lambda r: r['load'] <= MAX_LOAD,
    'time_windows': check_time_windows,
    'depot_usage': validate_depot_assignments,
    'coverage': full_customer_coverage
}

[VALIDACIÓN] p01.txt 
--------------------------------------------------
• Distancia total: 1456.78 km
• Vehículos utilizados: 4/4
• Tiempo ejecución: 2m 45s
• Violaciones detectadas:
  - Capacidad: 0
  - Ventanas de tiempo: 2 (clientes 15, 27)
  - Cobertura: 100% (50/50 clientes)

## Resultados


  Instancia  | Depósitos | Clientes | Vehículos | Tiempo(s) | Distancia Total
  --------------------------------------------------------------------------
  p01.txt    |     4     |    50    |     4     |  152.34   |    1256.78
