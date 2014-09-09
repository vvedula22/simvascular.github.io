
## Introduction

This document describes how to use the SimVascular/Solver software for three-dimensional blood flow numerical simulations. SimVascular/Solver solves the three-dimensional Navier-Stokes equations in an arbitrary domain that in general is represented by a vascular model reconstructed from image data. This is a complex subject due to the many aspects involved in it, and therefore this document will focus mainly on the practical sides of the various steps of the analysis. In the rest of this document, we will refer to this software as the “Solver”.

From a historical standpoint, the Solver has evolved from the academic finite element code PHASTA (this stands for Parallel, Hierarchical, Adaptive, Stabilized, Transient Analysis), developed mainly at RPI (Rensselaer Polytechnic Institute, Troy, NY) by Professor Kenneth Jansen. This code is in turned inspired by the Stabilized Finite Element theory developed by Professor Thomas J.R. Hughes during his Stanford years [SUPG paper]. As pointed above, the main features of the original PHASTA code are: 

- **Parallel**: using the MPI communication protocol (Message Passing Interface), the code is able to run analysis on multiple processors, either on Shared-Memory supercomputers, computer clusters, workstations, or regular PC desktops. The scalability of the code (i.e., the ability to make use of a large number of processors without significant losses in efficiency) has been proven up to several thousand processors.

- **Hierarchical basis**: the code has the ability of using variable k-order finite element meshes that allows  for independent assignment of polynomial orders over the finite elements. It must be noted though that, for cardiovascular simulations, we have always considered linear tetrahedral elements (k=1)

- **Adaptive**: the code has mesh-adaptivity capabilities that make possible to generate highly anisotropic finite element meshes based on an error field computed from the finite element solution. Having mesh adaptation tools is a really important feature, since it helps to improve the quality of the numerical solution while keeping the finite element mesh size “under control”.

- **Stabilized**: as we mentioned before, the code uses a Stabilized finite element formulation (more  specifically, a SUPG formulation: Streamline-Upwind Petrov-Galerkin) that allows for equal-order  interpolation of the pressure and velocity fields, while maintaining numerical stability in both the diffusive and advective-dominated limits. This point is the subject of very intense research and debate in the fluid mechanics community. While some people think that having equal-order interpolating functions for pressure and velocity is a very nice feature that makes the overall structure of the finite element code simpler (but needs this “stabilization terms” for the aforementioned diffusive and advective limits), others think that pressure and velocity fields appear in very different ways in the incompressible Navier-Stokes equations, and therefore they call for different interpolation strategies. A good reference to learn more about these topics is [GRESHO and SANI]

- **Transient**: the code uses a time integration algorithm based on the α - method. This is an implicit, second-order accurate, unconditionally stable (for linear systems) algorithm with user-defined level of desired numerical dissipation. On top of these features originally present in the Phasta code, Professor Charles Taylor’s group at Stanford University developed a number of important additions to the Solver in the areas of Boundary Conditions (Irene’s and Jin’s papers) and Fluid-Solid Interaction (Alberto’s papers). These additions are crucial to represent with a high level of realism the way blood flows in arteries, since this flow –which can be reasonably assumed to be incompressible-, is highly dependent on the characteristics of the vascular trees that are downstream of our three-dimensional model (these characteristics can be taken into account by means of adequate boundary conditions), and the compliance of the three-dimensional vascular tree (which is taken into account by the Fluid-Solid Interaction formulation implemented in the Solver).

This document will teach you the fundamentals of:

1. Preparing the necessary input files for the Solver (**PRE-PROCESSING** stage)
2. Running a flow analysis (**SOLVER** stage)
3. Looking and providing interpretation to the results generated by the code (**POST-PROCESSING** stage)

In addition, this tutorial will show you how to use some of the adaptivity tools, and will also show you a number of good practices that are important to observe during the simulation process. We will do this considering very simple geometries (a straight cylinder, an idealized bifurcation, and an idealized aneurysm) to illustrate different points in a simple way. 

### Theory and Implementation

The theory and implementation details are not covered in this document. For more information about those details, please refer to the following theses:

- Figueroa C.A., _“A Coupled-Momentum Method to Model Blood Flow and Vessel Deformation in Human Arteries: Applications in Disease Research and Simulation-Based Medical Planning”_, Department of Mechanical Engineering, Stanford University, 2006.

- Vignon-Clementel I.E., _“A Coupled Multidomain Method for Computational Modeling of Blood Flow”_,  Department of Mechanical Engineering, Stanford University, 2006.

- Whiting C.H., _“Stabilized Finite Element Methods for Fluid Dynamics using a Hierarchical Basis”_, Department of Mechanical Engineering, Rensselaer Polytechnic Institute, 1999.

### Using this Manual

Some conventions that will be helpful for you to know:

1. Text in italics represents things that you type into the command window.
2. Buttons, window names, and other labels in a window in the SimVascular program will be in quotes.
3. Pull-down menu selections will be indicated with an arrow ->.
