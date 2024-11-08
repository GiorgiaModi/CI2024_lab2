# CI2024_lab2

In this lab, I experimented with two different algorithms to solve the Traveling Salesman Problem (TSP): a greedy algorithm and a genetic algorithm.

I implemented features that allow the user to customize the problem setup in the notebook. Specifically, the user can choose the country (i.e., the dataset) by uncommenting the desired line in the second cell, which loads the corresponding CSV file. Moreover, the user can select a specific starting city by specifying it in the third cell. 

### Solution 1: Greedy algorithm 

The greedy algorithm aims to find a suboptimal but efficient solution by selecting the nearest unvisited city at each step. This process continues until all cities are visited, forming a complete cycle. To determine the closest city, I used a distance matrix, which stores the distances between all pairs of cities. While this approach does not guarantee the optimal solution, it provides a fast approximation with minimal computational complexity.


### Solution 2: Genetic algorithm 
The genetic algorithm, in contrast, seeks an improved solution by simulating natural selection processes. It initializes the population with either random routes or by using slight mutations of a precomputed greedy solution. When no initial solution is provided, the algorithm starts with completely random routes. 

In each generation, the algorithm follows a structured process:

- **Elitism:** The top-performing routes, or "elites," are preserved directly in the new population to retain quality solutions. I chose this approach as it improves solution quality and speeds up convergence.
- **Selection and Crossover:** The rest of the population is generated by selecting parent routes probabilistically and combining them through crossover. I experimented with three crossover methods:
    - **“Classic” Crossover**
    - **Partially Matched Crossover (PMX)**
    - **Inver-Over Crossover**
    
    From my experiments, I obtained the best results with the Inver-Over Crossover, which consistently yielded shorter routes and higher-quality solutions.
    
- **Mutation:** Each offspring route is subjected to a mutation, introducing small changes to ensure diversity.

### Observations

I conducted two main trials with the genetic algorithm:

1. **Random Initialization:** The initial population was entirely random. I decided to set number of generations equal to 2,500 in this case.
2. **Greedy-Based Initialization:** The initial population was derived from mutations of the greedy solution. I decided to set number of generations equal to 1,500 in this case.

Both approaches achieved similar final results when the number of cities was low. However, when the number of cities increased, starting from a random solution and running only 2,500 generations did not yield results comparable to those obtained with the greedy algorithm (for example, with the China dataset, the result of the genetic algorithm starting from a random solution yields poor results due to the large size of the dataset). In contrast, beginning with a greedy solution consistently led to improvements in all cases, requiring fewer generations (1,500 vs. 2,500) to reach the optimal route. This demonstrates that starting with a relatively good solution can accelerate convergence, even if the algorithm explores other solutions through crossover and mutation.
Observation: in larger datasets, more than 1500 generations would have been necessary to find an optimal solution even starting from the greedy solution and not from a random one. However, due to time constraints, I set this limit for all cases.

The solutions obtained with the genetic algorithm tend to be closer to the global optimum compared to the greedy algorithm. However, this improved accuracy comes at the cost of significantly longer execution times.

In conclusion, I believe that the best approach is to utilize a genetic algorithm that allows for better results while starting from a greedy solution rather than a random one. This strategy aims to optimize execution times while still providing effective solutions.

### Results
Naturally, the results depend on the chosen starting city. In the "plots" folder, I have included the results obtained for different countries, with starting cities selected at my discretion.

In the table below, I have summarized all the obtained results.

Note again that for large datasets, the results are not optimal and additional generations would have been necessary to achieve better outcomes.

| Dataset    | Start City | Approach                        | Final Cost (km) | Number of Steps/Generations | Time         |
|------------|------------|---------------------------------|-----------------|-----------------------------|--------------|
| **Italy**  | Trento     | Greedy                         | 5172.82         | 46                          | 0.2s         |
|            |            | Genetic (random start)         | 4181.63         | 2500                        | 7m 28.6s     |
|            |            | Genetic (greedy start)         | 4175.24         | 1500                        | 4m 31.1s     |
| **Vanuatu**| Sola       | Greedy                         | 1519.35         | 8                           | 0.1s         |
|            |            | Genetic (random start)         | 1345.54         | 2500                        | 1m 41.8s     |
|            |            | Genetic (greedy start)         | 1345.54         | 1500                        | 55.2s        |
| **US**     | Tacoma     | Greedy                         | 48810.9         | 326                         | 0.5s         |
|            |            | Genetic (random start)         | 133710.9        | 2500                        | 54m 4.4s     |
|            |            | Genetic (greedy start)         | 47000.24        | 1500                        | 33m 39.3s    |
| **Russia** | Armavir    | Greedy                         | 43953.66        | 167                         | 0.3s         |
|            |            | Genetic (random start)         | 55768.75        | 2500                        | 26m 44.6s    |
|            |            | Genetic (greedy start)         | 39870.89        | 1500                        | 15m 52.8s    |
| **China**  | Guiyang    | Greedy                         | 65605.44        | 725                         | 2.0s         |
|            |            | Genetic (random start)         | 377135.14       | 2500                        | 128m 2.8s    |
|            |            | Genetic (greedy start)         | 64869.18        | 1500                        | 81m 45.3s    |
