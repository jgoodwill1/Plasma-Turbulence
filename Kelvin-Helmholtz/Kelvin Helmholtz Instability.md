![[KHI_diagram.jpg]]
$$
\mathbf{n} \cdot \mathbf{u_{int}} = \mathbf{n} \cdot \mathbf{u_{1}} = \mathbf{n} \cdot \mathbf{u_{2}}
$$
$$
	\mathbf{n} = \frac{1}{\sqrt{1 + \left( \frac{\partial \eta}{\partial t} \right)}} \left(- \frac{\partial \eta}{\partial t} , 1\right)
$$
Bernoulli Equation:
$$
P_1 + \frac12 \rho v_1^2 = P_2 + \frac12 \rho v_2^2
$$
$$
q_1 = \nabla \Phi_1 \quad \nabla^2\Phi = 0; \qquad q_2 = \nabla \Phi_2 \quad \nabla^2 \Phi_2 = 0
$$
$$
\frac{\partial \Phi_1}{\partial t} + \frac{(\nabla \Phi_1)^2}{2} + \frac{p_1}{\rho_1} + C_1 \qquad \frac{\partial \Phi_2}{\partial t} + \frac{(\nabla \Phi_2)^2}{2} + \frac{p_1}{\rho_1} + C_2
$$
Kinematic Equations at boundary:
$$
\frac{\partial \eta}{\partial t} + \frac{\partial \Phi_1}{\partial x} \frac{\partial \eta}{\partial x} = \frac{\partial{\Phi_1}}{\partial t}
$$
$$
\frac{\partial \eta}{\partial t} + \frac{\partial \Phi_2}{\partial x} \frac{\partial \eta}{\partial x} = \frac{\partial{\Phi_2}}{\partial t}
$$
If  $\Phi_i=U_i x+\phi_i$ where $\phi_i \ll \Phi_i$, then the kinematic and dynamic condition at the boundary $y=0$ become:
$$
\frac{\partial \eta}{\partial t} + U_i \frac{\partial \eta}{\partial x} = \frac{\partial \phi_i}{\partial y}
$$
$$
\rho_1 \left(\frac{\partial \phi_1}{\partial t} + U_1 \frac{\partial \phi_1}{\partial x} \right) = \rho_2 \left(\frac{\partial \phi_2}{\partial t} + U_2 \frac{\partial \phi_2}{\partial x} \right)
$$
Now, we can assume that $\eta$  goes as a sinusoidal along the boundary
$$
\eta = A e^{i(kx - \omega t)}
$$
$$
\phi_i = \bar \phi_i e^{\pm ky} e^{i(kx - \omega t)}
$$
Substituting the sinusoidal into the kinematic and dynamic condition at the boundary, we get
$$
	(-i \omega + ikU_i)A = \pm k \bar \phi_i  
$$
$$
	\rho_1 (-i \omega + ik U_1)\phi_1 = \rho_2(-i \omega + ik U_2) \phi_2
$$
Writing this system of equations in matrix form, we can find solve the eigenvalue problem  to find the dispersion relation:
$$
\omega = k \frac{\rho_1 U_1 + \rho_2 U_2}{\rho_1 + \rho_2} \pm ik \frac{\sqrt{\rho_1 \rho_2} \left|U_1- U_2\right|}{\rho_1 + \rho_2}
$$
**Note: 1 denotes upper boundary and 2 denotes lower boundary**

