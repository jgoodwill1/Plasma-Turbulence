The Kelvin-Helmholtz instability is different layers of a heterogenous fluid are in relative motion.
Let the density of any point be $\rho + \delta \rho$ and the change in pressure be $\delta p$, and the velocity components are $U + u, v, w$. Thus the governing equations of the perturbation are then
$$
\begin{align}
	\rho \partial_t u + \rho U \partial_x u + \rho w d_zU &= - \partial_x \delta p\\
	\rho \partial_tv + \rho U \partial_xv &= - \partial_y \delta p \\
	\rho \partial_t w + \rho U \partial_x w &= -\partial_z \delta p - g\delta\rho + \sum_s T_s [\partial_x^2 + \partial_y^2] \delta z_s \delta(z- z_s)\\
	\partial_t \delta \rho + U \partial_x \delta \rho &= - w d_z \rho\\
	\partial_t \delta z_s + U_s \partial_x \delta z_s = w(z_s)\\
	\partial_x u + \partial_y v + \partial_z w = 0
\end{align}
$$
where $z_s$ refers to the discontinuity. The streaming is assumed to take place in the x-direction, with the discontinuity occurring in the z-plane. We seek for disturbances in normal modes by assuming a solution:
$$
	e^{i(k_x x + k_y y + nt)}
$$
With this solution, we find that
$$
	\partial_x = ik_x; \partial_y = ik_y; \partial_t = in
$$
Thus, the perturbation equations become
$$
\begin{align}
	i \rho(n + k_x U)u + \rho(d_z U)w &= -ik_x \delta p\\
	i \rho(n + k_x U)v &= -ik_y \delta p\\
	i \rho(n + k_x U)w &= -d_z \delta p - g \delta \rho - k^2 \sum_s T_s \delta z_s \delta(z-z_s)\\
	i(n + k_x U)\delta \rho &= - w d_z \rho\\
	i(n + k_x U_s)\delta z_s &= w_s\\
	i(k_x u + k_y v) &= -d_z w
\end{align}
$$
Multiplying the 1st equation by $-ik_x$ and the 2nd equation by $ik_y$, and adding them together, we get
$$
i\rho(n + k_x U )Dw - i\rho k_x(d_z U)w = -k^2 \delta \rho
$$
Using the 3rd equation and inserting the 4th and 5th equation, we get
$$
i \rho (n+k_x U)w = -d_z \delta p - ig(d_z\rho)\frac{w}{n+k_x U} + ik^2 \sum_s T_s\left(\frac{w}{n+k_x U}\right)_s \delta(z-z_s)
$$
Now we can eliminate $\delta p$ between these equations
$$
d_z[\rho(n+k_x U)d_z w - \rho k_x (d_z U)w]-k^2 \rho(n+k_xU) w= gk^2[(d_z rho) -\frac{k^2}{g}\sum_s T_s \delta(z-z_s)]\frac{w}{n+k_xU}
$$
The boundary conditions of this equation mean that $w=0$ at $z=0$ and $z=d$.
