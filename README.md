# Genetic_algorithm_AI
 This proejct is designed to find the optimized solution for any equation using the Genetic Algorithm

## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Algorithm Details](#algorithm-details)
  - [Fitness Function](#fitness-function)
  - [Binary Encoding](#binary-encoding)
  - [Uniform Crossover](#uniform-crossover)
  - [Mutation](#mutation)
- [Results](#results)

## Introduction

This project demonstrates how to use genetic algorithms to solve a quadratic equation. The genetic algorithm evolves a population of binary-encoded individuals over several generations to find the best solution.

## Features

- Binary encoding of individuals
- Uniform crossover to produce offspring
- Mutation to introduce variability
- Roulette wheel selection for choosing parents
- Fitness function based on the quadratic equation `3x^2+10x+7`

## Installation (Google Colaboratary)

To run this project from google collab, follow these steps:

### 1. Clone the repository:
   open any folder in vscode
   ```bash
   git clone https://github.com/emergingravi/Genetic_algorithm_AI.git
   ```

### 2. installation

    open your google drive
    right click
    select more - connect more apps
    search for google Colaboratory
    install
    

### 3. creating a new file:
    right click 
    select more - google colaboratary
        
### 4. connecting to server:

    select dropdown menu of connect
    change runtime
    select your desired hardware accelerator (TPU v2 -recommended)
    save
    click on connect

### 6. Run the genetic algorithm:

   Follow the instructions within the colaboraotry to run the genetic algorithm and view results.

### 7. Shutdown Colaboratory:

   Once finished, you can shutdown teh file by pressing `Ctrl + w` 


## Algorithm Details

### paramters initalization
```bash
popn_size = 100
int_len = 4
frac_len = 6
bit_len = 1 + int_len + frac_len
mut_rate = 0.1
gen = 100
```
### Fitness Function
  The fitness function evaluates how close a given solution is to the actual solution of the quadratic equation:
```bash
def fitness_function(x):
    x_real = decode_binary(x)
    return abs(3*x_real**2 + 10*x_real + 7)
```

### Binary Encoding
  Each individual in the population is represented as a binary string:

```bash
def decode_binary(x):
    sign_bit = int(x[0])
    integer_part = int(x[1:1+int_len], 2)
    fractional_part = int(x[1+int_len:], 2) / 2**frac_len
    x_real = (-1)**sign_bit * (integer_part + fractional_part)
    return x_real
```
### Population initialization
```bash
def initialize_population(population_size):
    population = []
    for _ in range(population_size):
        individual = ''.join(random.choice('01') for _ in range(bit_len))
        population.append(individual)
    return population
```
### Uniform Crossover
  Uniform crossover creates two offspring from two parents by randomly selecting each bit from either parent:

```bash
   def crossover(parent1, parent2):
    child1 = []
    child2 = []
    for p1, p2 in zip(parent1, parent2):
        if random.random() < 0.5:
            child1.append(p1)
            child2.append(p2)
        else:
            child1.append(p2)
            child2.append(p1)
    return ''.join(child1), ''.join(child2)
```
### Mutation
  Mutation introduces random changes to an individual to maintain genetic diversity:

```bash
def mutate(individual):
    mutated_individual = list(individual)
    for i in range(bit_len):
        if random.random() < mut_rate:
            mutated_individual[i] = '0' if individual[i] == '1' else '1'
    return ''.join(mutated_individual)
```

### Results
  After running the genetic algorithm, the best solution found will be printed along with its fitness value:
  
```text
Best individual found: 10001000001
Decoded best solution: x = -1.015625, Fitness = 0.061767578125
```

