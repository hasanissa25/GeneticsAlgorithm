# GeneticsAlgorithm
This is a Genetics Algorithm, tailored towards solving a person-task assignment problem.

A genetic algorithm is a heuristic method for finding approximate solutions to optimization problems. It maintains a population of solutions at all times, not just a single solution. The individuals in these populations change over time, and at termination the algorithm returns the best solution that it has seen in any population since the beginning.  Genetic algorithms use ideas from evolutionary theory, including survival of the fittest, combining characteristics from parents to create children, and mutation, to create successive generations of individuals that evolve to better solutions.

# The Algorithm steps:

  ## Step 0: Choose the Parameters.
	•	Population size : n
	•	Mutation rate: In %
	•	Stoping conditions :
	⁃	Whichever comes first:
	⁃	Limit on number of generations has been reached
	⁃	No change in the worst solution value for an X amount of generations


  ## Step 1.0: Initial Population Generation

  ### Specified Random Initial Population:

    1-Randomly select a person, randomly assign that person to a task
    2-Select the best unassigned person and assign them to a task.
    3-Repeat step(2) until you have assigned all people

    OR

    1-Randomly choose a task and assign the best person to that task.
    2-Randomly choose an unassigned task and assign the best person to that task
    3-Repeat step(2) until there are no more tasks needing a person. 


  ### Absolutely Random Initial Population:
    1-Generate a random number between 1-10, as the position of the letters.
    2-Current Person gets the index letter of that random number. I.E number 4 means the Current Person gets job 4.
    3- Repeat step(1-2) until you have assigned all people a task.
 

  ### Step 1.1: Incumbent Solution “Best value of the fitness function”

    1-Evaluate each “string”/combination in the initial population, and assign it a value
    2-Set the incumbent solution as the one with the best value 

  ## Step 2.1: Reproduction Operator “Virtual weighted roulette wheel”
    1-Sum the initial population fitness function values, to get a fitness total
    2-Divide each fitness value, by the fitness total, to get fitness as % of total, for each string solution.
    3-Generate a uniformly distributed random number between 0 and 100(Depends on the mutation% parameter set by the user). 
    4-The result of the random number, is the initial solution string to reproduce a copy of, based on the range it falls in.
    5-Repeat steps (3-5) n times. (Equal to the population number) to create a “Mating pool”

  ## Step 3.1: Crossover Operator
    1-Randomly select two strings from the mating pool created in Step 3.1. 
    2-Select two specific Crossover points, in each solution string.
	    -(In our case, 10 People are assigned, so between index 3 and 4, and between index 6 and 8)
    	-ABC \ DEF \ GHIJ , 
    	-CDE \ FGH \ IJKL
    3-Swap the Middle of the two parent strings, to create two new child strings.
    	-ABC \ FGH\ GHIJ , 
    	-CDE \ DEF \ IJKL
    4-Swap the duplicated elements of each string, with the corresponding crossed over element.
    	-F<->D
    	-G<->E
    	-H<->F
    5-Therefore the final result would be:
      -ABC \ FGH\ EFIJ , 
    	-CFG \ DEF \ IJKL
    6-Repeat steps(1-5) until all the population has been crossedover.
      -Repeat it n/2 times. As it creates 2 children 

    7- Update incumbent solution


  ## Step 4.1: Mutation Operator
    1-For each string, For each position, generate a random integer between 1 and 100
    2-If the random generated number is 1, then that position of the string is swapped to a random value in that same string 
    3-Calculate the fitness values for each solution string, and update incumbent solution if there is a better solution in this population.



  ## Step 5.1: Stopping Condition
    1-If the stopping conditions are met, exit and return the incumbent solution 
    2-Else, repeat from step 2.
