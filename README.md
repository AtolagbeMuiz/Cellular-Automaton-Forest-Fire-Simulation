Advanced Computational Science: Simulation of the Spread of Forest Fires, Adopting the Cellular Automaton Model Approach

## Abstract 
The spread of forest fires is a major threat to both humans and animals, and predicting the direction of a fire's spread can be difficult. This report presents a simulation model based on Cellular Automaton that accurately simulates the spread of forest fires. The model considers various stochastic parameters, including the probability of a tree being immune to burning and the probability of lightning. The model was implemented in Python, using the Von Neumann and Moore Neighbourhood principles to determine transition rules for simulating the spread of the fire. Numba and Pool multiprocessing approach was adopted to parallelise the sequential implementation, which allowed us to measure the runtime execution of each implementation. Our results show that the Moore Neighbourhood parallel implementation outperformed the Von Neumann sequential implementation in terms of runtime. This model can help improve fire management strategies and prevent the loss of lives and property to wildfires.
Introduction 
The spread of fire in a forest is a major threat to both humans and animals that are habitat of a forest, and the direction of the spread of a fire is most times unpredictable which has made it a problem to make proper decisions to prevent loss of lives and properties to wildfires. Therefore, scientists have come up with various methodologies to simulate and predict the spread of fires in the forest and this can also help in improving fire management strategies. 
The motivation behind this algorithm is to simulate the spread of fire within a given domain. This model can be simulated using different probabilistic parameter variables for the prediction, such as the probability of a tree being immune to burning, the probability of lightning, etc. 
The objective of this algorithm is to create a model based on the principles of cellular automation, and will take into account various parameters. 

## Aim & Objectives
This coursework aims to present an algorithm for simulating the spread of forest fires using Cellular Automaton, specifically focusing on the implementation of both Sequential and parallel techniques for improving the computational efficiency of the simulation. The report aims to provide a detailed explanation of the model formulation, setup, and implementation, along with the results and evaluation of the algorithm.
The objectives of this coursework implementation are as follows: 
- To implement the sequential spread of the forest fire algorithm using the defined transition rules. 
- Optimise the sequential implementation using the parallelization technique. 
- To present the results and evaluation of the algorithm, including the comparison of runtime execution between sequential and parallel implementations for different grid sizes, and the assessment of the computational efficiency of the algorithm. 
- To recommend further implementation to be done to improve the architecture of the algorithm and also the runtime complexity.

## Methodology 
<b>Setup:</b> The setup of the model implementation was done in a Python environment by writing the Python programming language in a Jupyter notebook and different necessary libraries were used in the course of this model implementation such as numpy, multiprocessing and matplotlib for graphical user interface interaction for the simulation. 

<b>Cellular Automation Method:</b> The cellular automation method adopted for this simulation model is a 2-dimensional model which has the capability of simulating 2D models of any grid size, whereby the cells of this grid are initialised with zeros. The transition of these cell values is determined based on the pre-defined transition rules for simulating the spread of the fire. The transition rules are based on the n * n grid cell values 0, 1, or 2, indicating an empty cell, a cell with a non-burning tree, or a cell with a burning tree, respectively. The status of each cell (Spread of fire) is determined at every iteration by validating against the pre-defined stochastic parameters and depending on the neighbouring cell values with the aid of Vonn Neuman or Moore Neighbourhood principles.

<b>Model Formulation:</b> The "InitializeUniverse" function is the entry point of the algorithm and initialises an array (forest or universe) of n * n size with zeros. This 2-dimensional array (forest) is looped through while randomly assigning trees and setting some of the trees on fire based on the given probabilistic parameters. 

The <i>"ExtendUniverse"</i> function extends the forest grid to include periodic boundary conditions. This was achieved by getting the dimension of the array (forest) to be extended and then extending an empty forest (array initialised with zeros) by 2 extra rows and columns.

![extendUniverse.png](https://github.com/AtolagbeMuiz/Cellular-Automaton-Forest-Fire-Simulation/blob/main/ReportImages/extendUniverse.png)


Then, the burning forest is copied into the empty forest such that its boundaries are bounded by empty rows and columns to the top and bottom, to the right and left.

![extenduniverse2.png](https://github.com/AtolagbeMuiz/Cellular-Automaton-Forest-Fire-Simulation/blob/main/ReportImages/extenduniverse2.png)


Then the periodic boundary conditions were further implemented by copying cell values of the last row into the first row and copying the second row into the last row. The same thing also applies to the columns as well to help us simulate an infinite lattice similar to the topology of a torus.

![extenduniverse3.png](https://github.com/AtolagbeMuiz/Cellular-Automaton-Forest-Fire-Simulation/blob/main/ReportImages/extenduniverse3.png)


The "FireSpread" function simulates the spread of fire by updating the state of each cell according to certain transition rules (Von Neuman Neighbourhood). If a cell is empty or has a non-burning tree, there is a chance that it will catch fire based on the "probBurning" parameter. If a cell is a burning tree, it will become empty. If a non-burning tree is adjacent to a burning tree, there is a chance that it will catch fire based on the "probLightning" parameter.

![vonnneumannalgorithm.png](https://github.com/AtolagbeMuiz/Cellular-Automaton-Forest-Fire-Simulation/blob/main/ReportImages/vonnneumannalgorithm.png)

The screenshot of the algorithm above illustrates the Von Neumann neighborhood principle, which was used as the transition rule for the spread of the forest fire.

The "simulate" function uses the "FireSpread" function to simulate the spread of fire in the forest. This spread of fire is carried out sequentially.

![simulatemethod.png](https://github.com/AtolagbeMuiz/Cellular-Automaton-Forest-Fire-Simulation/blob/main/ReportImages/simulatemethod.png)


The "visualise" function contains implementation to visualise the animated simulated model using the Python library called Matplotlib.

![visualizemethod.png](https://github.com/AtolagbeMuiz/Cellular-Automaton-Forest-Fire-Simulation/blob/main/ReportImages/visualizemethod.png)

## Parallel Implementation
The Parallel implementation uses the Moore Neighbourhood algorithm while the sequential implementation uses the Von Neumann algorithm to determine its transition rule.

The Parallelization of the implementation is done by adopting Numba and pool multiprocessing; Multiprocessing has some overhead when it is compared to Numba as Numba uses multithreading. The comparison is quite complicated as it sometimes requires tradeoffs when deciding the parallelization method to adopt. The overhead of multiprocessing sometimes makes it the best method especially when complex computation is done on a computer with several processors.

As shown below, the Numba parallelisation technique was used when looping through to initialise or populate the forest grid (universe).
NB: The attribute "nopython=True" wasn't used due to the deprecated version of Numba.

![initializeforest.png](https://github.com/AtolagbeMuiz/Cellular-Automaton-Forest-Fire-Simulation/blob/main/ReportImages/initializeforest.png)

The other part of the implementation where parallelisation was applied was on the FireSpread based on the Moore Neighbourhood Algorithm. This parallelisation technique was achieved by applying multiprocessing against the fire spread.

![simulatemethod2.png](https://github.com/AtolagbeMuiz/Cellular-Automaton-Forest-Fire-Simulation/blob/main/ReportImages/simulatemethod2.png)

## Results and evaluation
![ResultEvaluation.png](https://github.com/AtolagbeMuiz/Cellular-Automaton-Forest-Fire-Simulation/blob/main/ReportImages/ResultEvaluation.png)

The Chart below shows the runtime execution between the sequential and parallel implementation, which was calculated using the Python time function. This depicts that the Parallelised algorithm took less runtime compared to the sequential algorithm. This runtime also varies depending on the grid size, as a larger grid size such as 2000x2000 require higher computation time compared to a 100x100 grid size.
Runtime execution between the sequential and parallel algorithms.
![RuntimeExecution.png](https://github.com/AtolagbeMuiz/Cellular-Automaton-Forest-Fire-Simulation/blob/main/ReportImages/RuntimeExecution.png)



![SpreadofFireAnimation.png](https://github.com/AtolagbeMuiz/Cellular-Automaton-Forest-Fire-Simulation/blob/main/ReportImages/SpreadofFireAnimation.png)

A frame from the animated simulation model.

## Conclusion
The Implementation has been able to showcase the runtime complexity of both sequential and parallel algorithms and how parallelisation was achieved using both Numba and Multiprocessing pool to reduce the runtime. Although this algorithm still requires some form of refactoring and optimisation such that each implemented Neighbourhood algorithm can be utilised by any of both parallel and sequential implementations.

## References
- Numba. (n.d.). Deprecation - Numba documentation. Retrieved April 15, 2023, from https://numba.readthedocs.io/en/stable/reference/deprecation.html#recommendations
- Numba. (n.d.). njit.parallel=True or python.multiprocessing for speed up? Retrieved April 15, 2023, from https://numba.discourse.group/t/njit-parallel-true-or-python-multiprocessessing-for-speed-up/130/2
- Shiftlet, A.B. and Shiftlet, G.W. (2014). Introduction to Computational Science: Modelling and Simulation for the Sciences. Princeton, N.J.: Princeton University Press, 2nd ed.
