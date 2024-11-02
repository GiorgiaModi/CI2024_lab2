# CI2024_lab2

In this lab, I experimented with two different algorithms to solve the Traveling Salesman Problem (TSP): a greedy algorithm and a genetic algorithm.

The greedy algorithm aims to find a suboptimal but efficient solution by selecting the nearest unvisited city at each step. This process continues until all cities are visited, forming a complete cycle. To determine the closest city, I used a distance matrix, which stores the distances between all pairs of cities. While this approach does not guarantee the optimal solution, it provides a fast approximation with minimal computational complexity.

The genetic algorithm, in contrast, seeks an improved solution by simulating natural selection processes. It initializes the population with either random routes or by using slight mutations of a precomputed greedy solution. When no initial solution is provided, the algorithm starts with completely random routes. 

In each generation, the algorithm follows a structured process:

- **Elitism:** The top-performing routes, or "elites," are preserved directly in the new population to retain quality solutions. I chose this approach as it improves solution quality and speeds up convergence.
- **Selection and Crossover:** The rest of the population is generated by selecting parent routes probabilistically and combining them through crossover. I experimented with three crossover methods:
    - **“Classic” Crossover**
    - **Partially Matched Crossover (PMX)**
    - **Inver-Over Crossover**
    
    From my experiments, I obtained the best results with the Inver-Over Crossover, which consistently yielded shorter routes and higher-quality solutions.
    
- **Mutation:** Each offspring route is subjected to a mutation, introducing small changes to ensure diversity.

I conducted two main trials with the genetic algorithm:

1. **Random Initialization:** The initial population was entirely random.
2. **Greedy-Based Initialization:** The initial population was derived from mutations of the greedy solution.

Both approaches achieved similar final results. However, the greedy-based initialization required fewer generations (1,500 vs. 2,500) to reach the optimal route. This demonstrates that starting with a relatively good solution can accelerate convergence, even if the algorithm explores other solutions through crossover and mutation.

The solutions obtained with the genetic algorithm tend to be closer to the global optimum compared to the greedy algorithm. However, this improved accuracy comes at the cost of significantly longer execution times.

Additionally, I implemented features that allow the user to customize the problem setup in the notebook. Specifically, the user can choose the country (i.e., the dataset) by uncommenting the desired line in the second cell, which loads the corresponding CSV file. Moreover, the user can select a specific starting city by specifying it in the third cell. Naturally, the results depend on the chosen starting city. In the "plots" folder, I have included the results obtained for different countries, with starting cities selected at my discretion.