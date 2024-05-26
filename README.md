# BVP_Project_Amir_Gholizad.ipynb - Colab

This project tackles the task of solving a Boundary Value Problem (BVP) adaptively. The focus is on mesh points near the steep front and continuously adapt to keep up with the front's movement over time. This kind of flexible mesh is referred to as an adaptive moving mesh. The method used is based on the equidistribution principle, which aims to evenly distribute an error density function among all mesh elements.

The project uses Newton's Method, which is an iterative numerical method for finding the roots of a function. It starts with an initial guess for the root and then uses the derivative of the function to refine the estimate.

## Instructions

1. **Import necessary packages**: This includes `numpy`, `scipy.sparse`, `pandas`, and `matplotlib.pyplot`.

2. **Define the required constants**: This includes number of total nodes, start and stop points of $X_i$, initial value of $X$, boundary value of $X$, and spacing between the $X_i$ nodes.

3. **Define the $M(X, C)$ function**: This function takes $X_i$ (or $X$) and $C$ (boundary layer) and provides $M$ and $\frac{dM}{dx} in every node.

4. **Define the $G$ function**: This function is essentially the ODE of function $M$. It will be used in Newton's Method.

5. **Define the Jacobian matrix**: This matrix will be used in Newton's Method.

6. **Define the iterative Newton's algorithm**: This algorithm is used for solving ODEs.

7. **Create $X$ vs $X_i$ and $dX$ vs $X_i$ graphs**: This function creates graphs for different values of $C$ (boundary layer).

**Author**: Amir Gholizad, M.Sc. Physics, Memorial University of Newfoundland. The project was designed for CMSC 6920, Feb. 2023.

**Note**: Due to the stored data in memory, it is necessary to execute the entire project to see the results. For this purpose, it is recommended to do `Restart` and `run all`.
