# Pi-D

$$\Pi_{ij} = P_{ij} - p \delta_{ij}; \quad p = (p_{xx} + p_{yy} + p_{zz})/3; \quad \theta = \nabla \cdot u
$$
 $$\Pi = \begin{bmatrix} p_{xx} - p & p_{xy} & p_{xz} \\ p_{yx} & p_{yy} - p & p_{yz} \\ p_{zx} & p_{zy} & p_{zz}-p \end{bmatrix}$$ 

$$D_{ij} = \frac12 (\partial_i u_j + \partial_j u_i) - \frac{\theta}{3} \delta_{ij}$$
 $$D = \begin{bmatrix} \partial_x u_x - \frac\theta3 & \frac12(\partial_x u_y + \partial_y u_x) & \frac12 \partial_x u_z\\ \frac12(\partial_y u_x + \partial_x u_y) & \partial_y u_y - \frac\theta3 & \frac12\partial_y u_z\\ \frac12\partial_x u_z & \frac12 \partial_y u_z & -\frac\theta3 \end{bmatrix}
$$ 

$$\Pi_{ij} D_{ij} = \Pi_{xx}D_{xx} + \Pi_{yy} D_{yy} + \Pi_{zz}D_{zz} + \Pi_{xy}D_{xy} + \Pi_{yx}D_{yx} + \Pi_{xz}D_{xz} + \Pi_{zx}D_{zx} + \Pi_{yz}D_{yz} + \Pi_{zy}D_{zy}$$
$$\Pi_{ij} D_{ij} = \Pi_{xx}D_{xx} + \Pi_{yy} D_{yy} + \Pi_{zz}D_{zz} + 2(\Pi_{xy}D_{xy} + \Pi_{xz}D_{xz} + \Pi_{yz}D_{yz})$$
$$
e^{i \pi} = -1
$$
