# Three Body Problem Simulation
The Three Body Problem refers to the lack of a general closed-form solution for 3 bodies acting on each other through Newton's Law of Gravitation. It also happens to be the name of the show that inspired me to create this simulation. :)

### Calculations
Trajectories of objects were calculated using Newton's Universal Law of Gravitation $F = G \dfrac{M_1 M_2}{r^2}$. Simplifying for acceleration and including a directional term returns:

$$
\mathbf{a}_1 = \frac{G M_2 \, \hat{\mathbf{r}}}{d^3}
$$

Where $\hat{\mathbf{r}}$ is the distance vector defined by $\langle x_2, y_2 \rangle - \langle x_1, y_1 \rangle$, and $d^3$ is the scalar distance cubed. 
Using the vector sum of the two accelerations acting upon an object, we can update the velocity in the x and y directions, which then updates position, in turn updating distance between bodies. 

The following GIFs show the performance of the simulations using Forward Euler's method or Runge-Kutta 2. (note: the actual simulation on RStudio runs much smoother) 

## Forward Euler's method trajectories at set.seed(1)
![Screen Recording 2025-12-30 at 11 06 45 AM](https://github.com/user-attachments/assets/8c75ec65-0415-4cb2-b75c-f676b2376405)

## Runge-Kutta 2 method trajectories at set.seed(1)
![Screen Recording 2025-12-30 at 11 11 32 AM](https://github.com/user-attachments/assets/07d9541a-8393-48c9-b831-f31c16f2db33)

Qualitative differences in trajectories can be seen across the two GIFs, leading me to quantify the performance of each method using relative energy drift calculations.

### Relative Energy Drift

Relative energy drift can be intuitively thought of as the deviation of energy in a system compared to its initial value. It is defined by:

$$
\frac{E_{\text{step}} - E_{\text{initial}}}{\lvert E_{\text{initial}} \rvert}
$$

and can be used as a validation tool for our simulation. Numerical methods like Forward Euler's or RK2 can not perfectly model dynamic systems like planetary orbit. Over time, accumulations in error in state parameters lead to unrealistic simulation behavior, such as extremely high speeds. By choosing a quantity that should have internal consistency -- like total mechanical energy, which should remain constant throughout the simulation due to conservation of energy -- and measuring the drift from the initial state, we can determine which numerical method does a better job of approximating real-world behavior. 

Relative energy drift plotted over number of steps of the simulation should ideally return a horizontal flat line at 0, indicating no deviation from the initial energy of the system. The following image is the graphs of relative energy drift for Forward Euler's method and RK2. 

<img width="893" height="824" alt="Screenshot 2025-12-30 at 12 36 24 PM" src="https://github.com/user-attachments/assets/d1d7b9d6-8fb6-4038-807b-2c0065f4e170" />

As seen, Forward Euler's method leads to oscillatory behavior around 0 that is steadily increasing, while RK2 is an almost-flat line centered at 0. Though not perfect, RK2 more closely mimics the real-world behavior of planetary systems than Forward Euler's method. It should also be noted that energy drift can be affected by other factors, like step size, which were kept constant among the two simulations.


