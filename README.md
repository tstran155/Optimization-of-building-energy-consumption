# Optimization of building energy consumption

Building energy consumption has steadily increased over the past decades worldwide, and heating, ventilation and air conditioning (HVAC) account for most of the energy use in the buildings. By optimizing the design parameters with the aim of minimizing the heating and cooling loads, it is possible to minimize the total energy consumption of a building. 

This optimization process can be done using simulation tools that are capable of predicting the heating and cooling loads based on a set of design parameters, as well as using optimization algorithms that can search for the optimal set of parameters that minimize the heating and cooling loads. However, it is time-consuming and computational expensive to run batch simulations for the said purposes.

In this project, machine learning models were trained on the available dataset of design parameters and corresponding energy consumption. Once the models were trained, they can be used as the surrogate models in the optimization process. The optimization algorithm will update the models and use them to predict the energy consumption and for different sets of design parameters, and select the next set of parameters to evaluate based on the estimated performance of the models. 

It is worth noting that I employed two different approaches to evaluate energy consumption: separate energy consumption calculations for heating and cooling systems, and the total energy consumption which sums up the heating and cooling loads over a given period, such as a day, a week, or a year. The latter approach provides a comprehensive view of energy use and can identify opportunities for reducing consumption, such as through measures such as improved insulation, efficient lighting, or the use of renewable energy sources for the entire facility.

The dataset was created by Angeliki Xifara and was processed by Athanasios Tsanas (Oxford Centre for Industrial and Applied Mathematics, University of Oxford, UK) [1]. Please access the UCI Machine Learning Repository to download the dataset.

https://archive.ics.uci.edu/ml/datasets/energy+efficiency

The dataset contains eight attributes (or features, denoted by X1...X8) and two responses (or outcomes, denoted by y1 and y2). Below are underlying assumptions used in the simulations to generate the dataset. 

-	12 building forms were generated using Ecotect
-	All the buildings have the same volume of 771.75 m3
-	All elements used the same material which was not heat insulated
-	Building characteristics (the associated U-values appear in parenthesis): walls (1.780), floors (0.860), roofs (0.500), windows (2.260).
-	Building locations are in Athens, Greece, residential with seven persons, and sedentary activity (70 W).
-	The internal design conditions were set as follows: clothing: 0.6 clo, humidity: 60%, air speed: 0.30 m/s, lighting level: 300 Lux.
-	The internal gains were set to sensible (5) and latent (2 W/m2), while the infiltration rate was set to 0.5 for air change rate with wind sensitivity 0.25 air changer per hour.
-	Mixed mode thermal properties with 95% efficiency, thermostat range 19–24 ◦C, with 15–20 h of operation on weekdays and 10–20 h on weekends.
-	Three types of glazing areas, which are expressed as percentages of the floor area: 10%, 25%, and 40%.
-	Five different distribution scenarios for each glazing area were simulated:
(1) uniform: with 25% glazing on each side, 
(2) north: 55% on the north side and 15% on each of the other sides, 
(3) east: 55% on the east side and 15% on each of the other sides, 
(4) south: 55% on the south side and 15% on each of the other sides, 
(5) west: 55% on the west side and 15% on each of the other sides,

Deterministic optimization and probabilistic optimization are two different approaches to solving optimization problems in the search space. There are some hybrid approaches that combine deterministic and probabilistic elements such as Genetic algorithms with local search. I will examine all optimization approaches on the building energy optimization dataset in this repository. There are six (06) notebooks in this repository and their structures are similar, except for Sections #4 and 5.

- Notebook 1 & 1B: Univariate (total energy consumption) and multivariate (heating and cooling loads) regresssion of the input data to build surrogate or proxy models

- Notebook 2: Single objective optimization using a probabilistic method (Bayesian framework)

- Notebook 3: Single objective optimization using a deterministic method (Pyomo with Ipopt and Gurobi solvers)

- Notebook 4: Single objective optimization using a hybrid approach (Genetic algorithm with local search using a stochastic algorithm)

- Notebook 5: Multi-objective optimization of heating and cooling loads (Pymoo with NSGA-II algorithm)

**<ins>Notebook 1 & 1B</ins>**

1. Prepare Problem

a) Load libraries

b) Load dataset

2. Exploratory Data Analysis

a) Descriptive statistics

b) Data visualizations

3. Prepare Data

a) Data cleaning

b) Split data into train and validation sets

c) Data transforms or Feature engineering (Sobol sensitivity analysis) 

4. Evaluate Algorithms

a) Spot check algorithms (cross-validation technique)
   
   - Notebook 1: machine learning (Linear Regression, Random Forest, and XGBoost) and neural network (Keras Sequential) models
   
   - Notebook 1B: machine learning (Linear Regression, Random Forest, KNN, and Support Vector Machine) and neural network (Keras Sequential) models

b) Compare algorithms

5. Finalize Model

a) Predictions on validation dataset

b) Save the model for later use

6. Conclusions


**<ins>Notebook 2</ins>**

4. Optimization process using Bayesian framework

a)	Load the surrogate model created in Notebook 1

b)	Define objective, acquisition, and optimization functions

c)	Optimization process

5. Conclusions

**<ins>Notebook 3</ins>**

4. Optimization process using Pyomo

a) Create model and define constraints

b) Define objective function

c) Optimization process using IPOPT and Gurobi solvers

5. Conclusions

**<ins>Notebook 4</ins>**

4. Optimization process using GA with local search

a) Define the objective function using the pretrained surrogate model

b) Define the search space and the genetic algorithm parameters

c) Define the local search operator using a stochastic algorithm

d) Optimization using GA with local search 

5. Conclusions

**<ins>Notebook 5</ins>**

4. Multi-objective optimization using Pymoo

a) Define the evaluate function using the pretrained surrogate model

b) Define the problem and search space 

c) Define NSGA-II algorithm parameters

d) Run optimization using NSGA-II algorithm 

5. Conclusions

-------------------------------------------------------------------------------------------------------------------------------------
Reference

[1]	Tsanas, A. and Xifara, A. 2012. Accurate quantitative estimation of energy performance of residential buildings using statistical machine learning tools. Energy and Buildings 49: 560–567. https://doi.org/10.1016/j.enbuild.2012.03.003 

