# CS 8395 Final Project

_Isaiah Osborne_

## Project Description

_Improving Augmented Reality Pose Redirection Using Potential Functions and Gradient Descent_

As shown throughout this class, augmented reality has the ability to revolutionize remote work and collaboration. However, there are issues 

- Augmented reality has the ability to dramatically improve remote collaboration
- One problem is tracking the position of hands
  - Especially redirecting poses between actual and virtual environments
- Existing solutions focus on adapting BioIK
  - BioIK employs genetic algorithm optimization to solve the initial problem of finding a solution to the placement of the arm
- BioIK works surprisingly well, but struggles to balance the different functions involved
  - Other works have tried to combat this by dynamically weighting the functions
  - (Cite <https://3dvar.com/Ullal2021A.pdf> and <https://dl-acm-org.proxy.library.vanderbilt.edu/doi/pdf/10.1145/3565970.3567681>) 
- I want to explore ways to incorporate another evaluation function directly into the gradient descent portion of BioIK

We can use an idea from inverse kinematics to optimize both of our variables simulataneously. From [^1] and [^2], we can write the derivative of the two functions together like this (rewritten for clarity):

$$
d\theta = J_1^* \dot q_1 + (I_n - J_1^*J_1)(-\gamma \frac{dp}{d\theta})^T
$$

  - Where:
    - $J_1^*$ is the Jacobian psuedo-inverse
    - $\dot q_1$ is a particular solution
  - This allows the algorithm to explore on the gradient for both the main objective ($J_1^* \dot q_1$) and the secondary objective ($(I_n - J_1^*J_1)(-\gamma \frac{dp}{d\theta})^T$)

## Citations

[^1]: "Automatic Supervisory Control of the Configuration and Behavior of Multibody Mechanisms," in _IEEE Transactions on Systems, Man, and Cybernetics_, vol. 7, no. 12, pp. 868-871, Dec. 1977, doi: 10.1109/TSMC.1977.4309644.

[^2]: Yoshihiko Nakamura. _Advanced Robotics Redundancy and Optimization_, Addison-Wesley, 1991.

[^3]: S. Starke, N. Hendrich and J. Zhang, "Memetic Evolution for Generic Full-Body Inverse Kinematics in Robotics and Animation," in _IEEE Transactions on Evolutionary Computation_, vol. 23, no. 3, pp. 406-420, June 2019, doi: 10.1109/TEVC.2018.2867601.
