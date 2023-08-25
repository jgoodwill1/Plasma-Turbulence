# Josh Initializations
Natural PIC units:
$$e, m_{e}, c, d_{e},\epsilon_{0}   = 1$$
Size of simulation
$$L_{x} = 6.4 d_{i}; \quad L_{y} = 12.8 d_{i}; \quad \frac{d_i}{d_{e}}= 10; \quad nx = 64; \quad ny = 128$$
Simulation Parameters:
$$\frac{m_{i}}{m_{e}} = 100 \quad L_{V} = 0.1 d_{i} \quad \beta = \frac{n_{0}T}{B_{0}^{2}} = 0.1 \quad v_{the} = 0.2  $$
Shear Layer Parameters:
$$du_y = U_0 \tanh \left( \frac{x- (L_x/2)}{L_V} \right); U_0 = 10 V_A$$
Magnetic and Electric Field:
$$\vec{B} = B_{0} (\sin \theta\hat{y} + \cos \theta \hat{z})\quad \vec{E} = -\left( \frac{B_{0}U_{0}}{c}\right) \tanh \left(\frac{x}{L_v} \right)$$
$$B_{0}= \frac{m_{e}c \omega_{ce}}{e}=0.5; \quad \theta= 2.86 \degree$$
# Karimabadi 2013 Initializations
Size of simulation
$$L_{x} = 50 d_{i}; \quad L_{y} = 100 d_{i}; \quad nx = 8192; \quad ny = 16384; \quad nppc = 150 $$
Simulation Parameters:
$$\frac{m_{i}}{m_{e}} = 100 \quad L_{V} = 4 d_{i} \quad \beta = \frac{ 16 \pi n_{0}T}{B_{0}^{2}} = 0.1 \quad v_{the} = 0.2;\quad  \frac{\omega_{pe}}{\omega_{ce}} = 2  $$
Shear Layer Parameters:
$$du_y = U_0 \tanh \left( \frac{x- (L_x/2)}{L_V} \right); U_0 \approx 10 V_A^*$$
Magnetic and Electric Field:
$$\vec{B} = B_{0} (\sin \theta\hat{y} + \cos \theta \hat{z}); \quad \vec{E} = -\left( \frac{B_{0}U_{0}}{c}\right) \tanh \left(\frac{x}{L_v} \right)$$
$$B_{0}= \frac{m_{e}c \omega_{ce}}{e}; \quad \theta= 2.86 \degree$$