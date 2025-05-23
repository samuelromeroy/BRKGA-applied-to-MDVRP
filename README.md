# BRKGA para MDVRP

## 📌 Descripción del Proyecto

Este proyecto implementa una variante del algoritmo BRKGA (Biased Random-Key Genetic Algorithm) para resolver el problema del Enrutamiento de Vehículos con Múltiples Depósitos (MDVRP). El MDVRP es una extensión del VRP clásico en el que varios depósitos pueden despachar vehículos para satisfacer la demanda de clientes, respetando restricciones de capacidad y duración.

## ✨ Características Clave

- Lectura estructurada de instancias MDVRP desde archivos de texto.
- Visualización de clientes y depósitos con información opcional sobre demanda y ventanas de tiempo.
- Aplicación de un algoritmo basado en representación de claves aleatorias para buscar soluciones factibles.

## ⚙️ Instalación

1. Clona este repositorio:
   ```bash
   git clone https://github.com/samuelromeroy/BRKGA-applied-to-MDVRP
   ```

2. Instala las dependencias necesarias:
   ```bash
   pip install numpy matplotlib
   ```

## 🚀 Uso Rápido

1. Coloca el archivo de instancia (`.txt`) en el directorio raíz.
2. Ejecuta el notebook `BRKGA.ipynb`.
3. Ajusta el parámetro `file_path` con el nombre de tu archivo de instancia.
4. Corre las celdas para cargar datos, visualizar la instancia y ejecutar el algoritmo.

## 🧱 Estructura del Proyecto

```
.
├── BRKGA.ipynb              # Notebook principal con implementación y visualización
├── data/                    # (Opcional) Carpeta para almacenar archivos de instancia
├── README.md                # Este archivo
└── requirements.txt         # Lista de dependencias
```

## 🛠️ Configuración Avanzada

Puedes modificar el comportamiento del algoritmo ajustando:
- Tamaño de población
- Porcentaje de élite y mutantes
- Criterios de parada
- Métricas de evaluación

Estas configuraciones se encuentran en el cuerpo del notebook.

## ⚙️ Hiperparámetros

Los principales hiperparámetros del BRKGA incluyen:
- `population_size`: tamaño de la población
- `elite_fraction`: fracción de la población considerada élite
- `mutant_fraction`: fracción de mutantes por generación
- `inheritance_prob`: probabilidad de herencia del padre élite
- `max_generations`: número máximo de generaciones

## ✅ Validación

El algoritmo se valida gráficamente mediante visualización de los clientes y rutas, y cuantitativamente a través del valor de la función objetivo. También se puede comparar el desempeño en diferentes instancias.

## 📊 Resultados

Se observan rutas generadas a partir de las soluciones halladas. Las soluciones se evalúan en términos de distancia total recorrida y cumplimiento de restricciones.

## 🔗 Referencias

- Prins, C. (2004). A simple and effective evolutionary algorithm for the vehicle routing problem. *Computers & Operations Research*.
- Montané, F. A. T., & Galvão, R. D. (2006). A tabu search algorithm for the vehicle routing problem with simultaneous pick-up and delivery service. *Computers & Operations Research*.

## 📝 Licencia

Este proyecto se distribuye bajo la Licencia MIT. Consulta el archivo `LICENSE` para más información.
