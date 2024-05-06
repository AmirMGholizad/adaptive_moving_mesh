# Adaptive Moving Mesh #

To effectively solve a BVP, the mesh points need to be focused near the steep
front and continuously adapted to keep up with the front's movement over time.
This kind of flexible mesh is called an *adaptive moving mesh*.

**Equidistribution**

To adjust the mesh in order to follow the front as it moves we can use a method based on the equidistribution principle, which aims to evenly distribute an error density function among all mesh elements. In one dimension, the equidistribution principle can uniquely determine a mesh for a given mesh density function, along with appropriate boundary conditions.

Equidistribution is a crucial concept in mesh adaptation. It involves creating a mesh that evenly distributes a given continuous function, represented by $M(x_i)$, over a bounded interval $[\alpha, \beta]$. The mesh is defined by a set of $n$ points on the interval, $x_{\alpha} = \alpha, x_0, ..., x_n, x_{\beta} = \beta$, and it is called an equidistributing mesh if the area under the function $M(x_i)$ is the same for every subinterval between the mesh points.
The mathematical form of this principle is
<center>$\int_{x_{\alpha}}^{x_{0}}M(x,u(x))dx=...=\int_{x_{n}}^{x_\beta}M(x,u(x))dx. \: \: (1)$  
</center>

The objective is to determine the optimum mesh for $u(x)$ using $M$ which is the *mesh density function*.The mesh density function is proportional to the density of the mesh when the equidistribution principle is satisfied. It must be non-negative, meaning that it can vanish locally, which may lead to non-unique equidistributing meshes. Therefore, the assumption is made that any mesh density function is strictly positive on the interval $[\alpha, \beta]$.

If we refer to the Fundamental Theorem of Calculus, for the entire interval of $[\alpha, \beta]$ we can say

<center>$ \frac{1}{n} \int_{x_{\alpha}}^{x_\beta}M(x,u(x))dx=\int_{x_{i}}^{x_{i+1}}M(x,u(x))dx. \: \: (2)$  
</center>

Also, if we define $\xi$ as $\xi = \frac{1}{n}$ and consequently for discrete space $\xi_i = \frac{i}{n}$ we will get

<center>$ \xi \int_{x_{\alpha}}^{x_\beta}M(x,u(x))dx=\int_{x_{i}}^{x_{i+1}}M(x,u(x))dx. \: \: (3)$  
</center>

By differentiating both sides of Eq.(2) with respect to $\xi$ we find

<center>$ \int_{x_{\alpha}}^{x_\beta}M(x,u(x))dx = M(x(\xi),u(x))\frac{dx}{d\xi} \: \: (4)$  
</center>

and second differentiation gives us

<center>$ \frac{d}{d\xi}(M(x(\xi),u(x))\frac{dx}{d\xi}) = 0. \: \: (5)$  
</center>

In this project our aim is to solve the Eq.(5) using a uniform grid $\xi$ as our initial guess, a pre-defined mesh density function $M$, the original function $u$ and find the final $x$ as our adaptive mesh for $u$. We will solve this equation using Newton's Method.

**Newton's Method**

Newton's Method is an iterative numerical method for finding the roots of a function. It starts with an initial guess for the root and then uses the derivative of the function to refine the estimate. The general idea is to iteratively improve an initial guess for the root by finding the zero of a linear approximation to the function at that point.

**The Algorithm**

Using a uniform grid like $x_i = \xi_i = \frac{i}{n}$ we can discretize the Eq.(5) and get to
<center>$ \frac{1}{2Δ\xi^2}((M_{i+1} + M_{i})(x_{i+1} - x_i) - (M_{i} + M_{i-1})(x_{i} - x_{i-1})) = 0. \: \: (6)$
</center>

We also asume that $x_{\alpha} = \alpha = 0$ and $x_{\beta} = \beta = 1$.

If we redefine the Eq.(6) as $G_i = 0$, the Newton's method will take the form
<center>
$ \Sigma_{j} J_{ij}.Δx_j = - G_i. \: \: (7)$
</center>

Here's how the algorithm works:

 -  We start with an initial guess $x = \xi = \frac{1}{n}$ for the root of the function $G(\xi)$.

 - We compute the Jacobian matrix of the function $G(\xi)$ at the guess $\xi$.

 - Using Eq.(7), we find the difference between $x$-intercept of the tangent line to the graph of $G(\xi)$ and $\xi$ and add it to $\xi$ to get the next guess for the root, $x$.

 - We repeat steps 2-4 with the new guess $x$ until the desired level of accuracy is achieved.
