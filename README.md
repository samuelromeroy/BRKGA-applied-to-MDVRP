# BRKGA for MDVRP

## 📌 Project Description
This project implements a variant of the BRKGA (Biased Random-Key Genetic Algorithm) algorithm to solve the Multi-Depot Vehicle Routing Problem (MDVRP). The MDVRP is an extension of the classic VRP where multiple depots can dispatch vehicles to satisfy customer demand while respecting capacity and duration constraints.

## ✨ Key Features
- Structured reading of MDVRP instances from text files
- Visualization of customers and depots with optional information about demand and time windows
- Application of an algorithm based on random-key representation to search for feasible solutions

## ⚙️ Installation
1. Clone this repository:
   ```bash
   git clone https://github.com/samuelromeroy/BRKGA-applied-to-MDVRP
   ```
2. Install the necessary dependencies:
   ```bash
   pip install numpy matplotlib
   ```

## 🚀 Quick Start
1. Place the instance file (`.txt`) in the root directory
2. Run the notebook `BRKGA.ipynb`
3. Adjust the `file_path` parameter with your instance file name
4. Run the cells to load data, visualize the instance, and execute the algorithm

## 🧱 Project Structure
```
.
├── BRKGA.ipynb              # Main notebook with implementation and visualization
├── data/                    # (Optional) Folder to store instance files
├── README.md                # This file
└── requirements.txt         # Dependencies list
```

## 🛠️ Advanced Configuration
You can modify the algorithm's behavior by adjusting:
- Population size
- Elite and mutant percentages
- Stopping criteria
- Evaluation metrics

These configurations are found in the notebook body.

## ⚙️ Hyperparameters
The main BRKGA hyperparameters include:
- `population_size`: population size
- `elite_fraction`: fraction of population considered elite
- `mutant_fraction`: fraction of mutants per generation
- `inheritance_prob`: probability of inheritance from elite parent
- `max_generations`: maximum number of generations

## ✅ Validation
The algorithm is validated graphically through visualization of customers and routes, and quantitatively through the objective function value. Performance can also be compared across different instances.

## 📊 Results
Routes generated from the found solutions are observed. Solutions are evaluated in terms of total distance traveled and constraint compliance.

## 🔗 References
- Prins, C. (2004). A simple and effective evolutionary algorithm for the vehicle routing problem. *Computers & Operations Research*.
- Montané, F. A. T., & Galvão, R. D. (2006). A tabu search algorithm for the vehicle routing problem with simultaneous pick-up and delivery service. *Computers & Operations Research*.

## 📝 License
This project is distributed under the MIT License. See the `LICENSE` file for more information.
