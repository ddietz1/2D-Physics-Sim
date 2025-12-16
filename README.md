# 2D-Physics-Sim
2D physics simulator showing a four arm jack inside a four sided box.

## Overview
This physics simulation displays a four armed jack inside of a four sided box falling under the influence of gravity.
The physics of the impacts between the box and jack are calculated using Euler-Lagrange equations.

## Transformations
The program works by defining 13 reference frames; a fixed frame for the 'World', a frame at the center of the Box, another at the center of the Box rotated by an angle $\theta_{b}$, a frame at the center of the Jack,another frame at the center of the Jack rotated by an angle $\theta_{j}$, and eight additional frames at the center of each link of the Box and the end of each arm of the Jack. A state vector 

A 4x4 transformation matrix in the Special Euclidean group(SE3) is defined at each frame and calculated using a helper function defined at the top of the program. Using matrix multiplication one can then find the overall transformation between any two frames, for instance from World to Box.

The variables $X_{b}(t)$, $Y_{b}(t)$, $X_{j}(t)$, and $Y_{j}(t)$ are the positions of the center of the box and jack relative to the world frame. They are part of the state vector q = ($X_{b}(t)$, $Y_{b}(t)$, $\theta_{b}$(t), $X_{j}(t)$, $Y_{j}(t)$, $\theta_{j}$(t)) which defines the overall state of the system. This state vector is important for solving the Euler-Lagrange equations.

## Dynamics and Impacts
The dynamics of the system are governed by the Euler-Lagrange equations
d/dt(∂L/∂q̇) − ∂L/∂q = τ ∈ ℝⁿ
where the Lagrangian is the difference between the Kinetic and Potential energy for the whole system. 
L = KE - PE
$\tau$ is the generalized force vector acting on the system.
The state vector q is defined above.

The impacts are determined using more matrix multiplication by first definining 16 constraints on the system. Those being that none of the arms of the jack can pass through any of the sides of the circle. Two additional constraints on the system are that the total energy of the system(Hamiltonian) and the generalized momentum must remain constant prior to and after impact. With these constraints we create the impact update equations that are solved numerically via sympy substitution at the moment of impact to determine the velocity and accelerations post impact.

## Simulation
Below is a full video of the running simulation. The system contains several assumptions to make the simulation easier to visualize and understand. The mass of the jack is considered to be concentrated at its center and the inertia values for all four arms of the box and the jack are hardcoded to make tuning the simulation easier. The generalized force vector acting on the system contains a value to counteract the force of gravity thus keeping the system in frame. A small torque is also added to slowly rotate the box, thus displaying more impacts in a shorter time frame.

The simulation successfully demonstrates the total energy and momentum of the system remaining constant, with the momentum of the jack being transferred to the box at the moment of impact.




