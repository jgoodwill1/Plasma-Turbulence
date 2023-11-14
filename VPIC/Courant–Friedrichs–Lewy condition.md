Useful for explicit time integration schemes
CFL has the form:
$$C = \frac{u \Delta t}{\Delta x} \leq C_{max}$$
where $C$ is the Courant number, $u$ is the magnitude of velocity, $\Delta t$ is time step, and $\Delta x$ is length interval. $C_{max} =1$ for explicit solvers.  