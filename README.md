# CS 8395 Final Project

_Isaiah Osborne_

# Code is now available here: <https://github.com/VU-RASL/InverseKinematics>

_Why?!?_ Well, Github limits LFS storage on Personal accounts 🫤, so I used my lab's research one instead. If you look at the history (<https://github.com/VU-RASL/InverseKinematics/commits/master/>), all commits are from me, `IMOsbo`.

## Project Description

_Improving Augmented Reality Pose Redirection Using Potential Functions and Gradient Descent_

As shown throughout this class, augmented reality has the ability to revolutionize remote work and collaboration. However, there are issues with collaborating between real and virtual environments, such as transferring poses between the environments [^5]. Pose redirection can be viewed as a multi-objective optimization problem, with the two objectives being to minimize the position error [^5]. It also works to minimize the difference between the ground-truth's pose and the new pose - the model favors new poses that are closer to the existing pose. Previous work for rerouting poses relies on BioIK and its genetic algorithm implementation. In this problem, BioIK employs genetic algorithm optimization to find the solution to the placement of the arm, but it does not do anything to optimize the angles of the individual joints of the arm [^3]. To counteract this problem, some people have tried dynamically weighting the two objectives [^4]. 

For my project, I want to explore other ways to optimize the pose redirection. For example, we can use other ideas from inverse kinematics to optimize both of our variables simulataneously. We can define two different objective functions: one function for the location for the hand, and one function for the difference in joint angles between the two poses, as used in [^4]. From [^1] and [^2], we can write the derivative of the two functions together like this (rewritten for clarity):

$$
d\theta = J_1^* \dot q_1 + (I_n - J_1^*J_1)(-\gamma \frac{dp}{d\theta})^T
$$

- Where:
    - $J_1^*$ is the Jacobian psuedo-inverse
    - $\dot q_1$ is a particular solution

In an engineering setting, this is used to calculate the velocity of the end of the link (usually a manipulator, but in this case a hand). However, this could also be used as part of our gradient descrnt, allowing the algorithm to explore on the gradient for both the main objective ($J_1^* \dot q_1$) and the secondary objective ($(I_n - J_1^*J_1)(-\gamma \frac{dp}{d\theta})^T$). The two objectives will be the ones in [^5]. By replacing the gradient step in BioIK with this expression, I'm hoping to be able to optimize both of the variables concurrently. Depending on time constraints, I will try to refine the weighting metric from [^5], potentially replacing the logistic function with another weighting function.

## Technical Details

I am planning on using Unity and the Microsoft Mixed Reality Toolkit for my project. I am also going to use and modify the BioIK package for the inverse kinematics optimization. My final project will be deployed using either the MRTK simulator or an actual Hololens 2. 

<https://unity.com/>

<https://learn.microsoft.com/en-us/windows/mixed-reality/mrtk-unity/mrtk3-overview/>

<https://learn.microsoft.com/en-us/windows/mixed-reality/mrtk-unity/mrtk3-input/packages/input/input-simulation>

<https://github.com/sebastianstarke/BioIK>

## Citations

[^1]: "Automatic Supervisory Control of the Configuration and Behavior of Multibody Mechanisms," in _IEEE Transactions on Systems, Man, and Cybernetics_, vol. 7, no. 12, pp. 868-871, Dec. 1977, doi: 10.1109/TSMC.1977.4309644.

[^2]: Yoshihiko Nakamura. _Advanced Robotics Redundancy and Optimization_, Addison-Wesley, 1991.

[^3]: S. Starke, N. Hendrich and J. Zhang, "Memetic Evolution for Generic Full-Body Inverse Kinematics in Robotics and Animation," in _IEEE Transactions on Evolutionary Computation_, vol. 23, no. 3, pp. 406-420, June 2019, doi: 10.1109/TEVC.2018.2867601.

[^4]: Ullal A, Watkins C, Sarkar N. "A Dynamically Weighted Multi-Objective Optimization Approach to Positional Interactions in Remote-Local Augmented/Mixed Reality," in _The Institute of Electrical and Electronics Engineers, Inc. (IEEE) Conference Proceedings._ The Institute of Electrical and Electronics Engineers, Inc. (IEEE); 2021. doi:10.1109/AIVR52153.2021.00014

[^5]: Akshith Ullal, Alexandra Watkins, and Nilanjan Sarkar. 2022. A Multi-Objective Optimization Framework for Redirecting Pointing Gestures in Remote-Local Mixed/Augmented Reality. In Proceedings of the 2022 ACM Symposium on Spatial User Interaction (SUI '22). Association for Computing Machinery, New York, NY, USA, Article 9, 1–11. https://doi-org.proxy.library.vanderbilt.edu/10.1145/3565970.3567681
