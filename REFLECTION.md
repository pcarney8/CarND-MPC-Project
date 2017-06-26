## The Model
I used the MPC model and a 3-order polynomial to fit the waypoints. I passed a state vector, containing `x,y,psi,v,cte,epsi` into the `MPC.Solve()` method. From there I constructed upper and lower bounds on my variables and constraints, then using the `ipopt` solver I constructed a cost equation with various weights on the actuators (incl. smoothing), cte & epsi errors, and velocity. Then, using our Vehicle Model equations, I constructed our constraints (which were set equal to zero), and had `ipopt` solve it.

## Timestep Length and Elapsed Duration
At first, I tried what we had in our quiz, N = 25 and dt = 0.05, and right off the bat that was giving me trouble. But I was also having some trouble with my model. After doing some research through the forums and having a look at the walkthrough. I corrected several bugs and decided to try N = 10, dt = 0.1. This definitely smoothed things out a bit and didn't have as much jerky reaction as the N = 25, dt = 0.05 values. I stuck with N = 10, and dt = 0.1 because tuning my cost function relied on these being the same, I noticed that if I switched to the previous N & dt, those cost function weights weren't very good anymore.

## Polynomial fitting and MPC preprocessing
I shifted x and y to make sure their coordinates were in the correct space before I fit my polynomial for the waypoints. I fit the waypoints to a third order polynomial, knowing that this would allow for almost any type of curvature. 

## MPC with Latency
I added a little bit of latency to the velocity calculation, but overall I handled latency by changing the weights of my cost functions and running the simulation mutltiple times to figure out what worked best.

## Video
https://youtu.be/UdJyWaVB_44
