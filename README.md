# Spatial Economics Model

A computational spatial equilibrium model that solves for wages, rents, and commuting flows across locations using a fixed-point algorithm.

Based on Dingel and Tintelnot, with a focus on how individuals sort across residence–workplace pairs in granular settings.



## Project Structure

- `model.py`  
  Defines the SpatialModel, including productivity, land, and commuting costs.

- `solver.py`  
  Implements the EquilibriumSolver, which updates wages and rents.

- `analysis.py`  
  Computes outputs such as price index, flows, and summary statistics.

- `main.py`  
  Runs the model and produces results.



## Model Setup

The economy consists of multiple locations. Each individual chooses:
- a residential location (k)  
- a workplace location (n)  

Utility depends on:
- wages in location n  
- rents in location k  
- commuting costs between locations  
- individual-specific preferences  

Because individuals differ in their preferences, commuting patterns are determined probabilistically rather than deterministically.



## Core Mechanisms

### Commuting Choices

Workers are more likely to choose:
- locations with higher wages  
- locations with lower rents  
- shorter or cheaper commutes  

This generates a distribution of commuting flows across all location pairs.



### Price Index

The model includes a CES price index over goods:

P = [sum over n of (w_n / A_n)^(1 - sigma)]^(1 / (1 - sigma))



### Goods Market Clearing

Output in each location is:

Output = A_n × L_n  

Wages adjust so that supply equals demand across locations.


### Land Market Clearing

Each location has a fixed amount of land. Rents adjust so that total land demand equals land supply.



## Equilibrium

The model solves for:
- wages {w_n}  
- rents {r_k}  
- commuting flows {ℓ_kn}  

such that:
- the goods market clears  
- the land market clears  
- individuals are optimally allocated across locations  


## Computational Method

The equilibrium is computed using a fixed-point iteration:

1. Initialize wages and rents  
2. Compute commuting shares  
3. Update wages using goods market clearing  
4. Update rents using land market clearing  
5. Normalize wages  
6. Repeat until convergence  

Damping is used to ensure stability.


## Results

### Equilibrium Outcomes

After convergence, the model produces:

- Equilibrium wages across locations  
- Equilibrium rents across locations  
- A commuting flow matrix ℓ_kn  
- A price index  

These results describe how individuals are distributed across residence–workplace pairs and how economic activity is spatially organized.



### Convergence

The algorithm converges when changes in wages and rents fall below a chosen tolerance level.

Damping plays an important role in preventing instability during iteration.


