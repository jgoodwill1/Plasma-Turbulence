# Josh Initializations

Size of simulation:
$$L_{x} = 6.4 d_{i}; \quad L_{y} = 12.8 d_{i}; \quad \frac{d_i}{d_{e}}= 10; \quad nx = 256; \quad ny = 512$$
Simulation Parameters:
$$\frac{m_{i}}{m_{e}} = 100 \quad L_{V} = 0.01 d_{i} \quad \beta = \frac{2n_{0}T}{B_{0}^{2}} = 0.1 \quad v_{the} = 0.2  $$
Shear Layer Parameters:
$$du_y = U_0 \tanh \left( \frac{x}{L_V} \right); U_0 = 10 V_A$$
Magnetic and Electric Field:
$$\vec{B} = B_{0} (\sin \theta\hat{y} + \cos \theta \hat{z})\quad \vec{E} = -\left( \frac{B_{z}U_{0}}{c}\right) \tanh \left(\frac{x}{L_v} \right) \hat{x}$$
$$B_{0}= \frac{m_{e}c \omega_{ce}}{e}=0.5; \quad \theta= 2.86 \degree$$
Charge Separation:
$$\partial_x E_x = - \frac{e n_e(x)}{\epsilon_{0}}$$
Excess Charge: 
$$n_e(x) = \left( \frac{B_{z}U_{0}}{e {L_{v}}}\right) \epsilon_{0}  sech^2 \left( \frac{x}{L_v} \right)$$









# Karimabadi 2013 Initializations
Size of simulation
$$L_{x} = 50 d_{i}; \quad L_{y} = 100 d_{i}; \quad nx = 8192; \quad ny = 16384; \quad nppc = 150 $$
Simulation Parameters:
$$\frac{m_{i}}{m_{e}} = 100 \quad L_{V} = 4 d_{i} \quad \beta = \frac{ 16 \pi n_{0}T}{B_{0}^{2}} = 0.1 \quad v_{the} = 0.2;\quad  \frac{\omega_{pe}}{\omega_{ce}} = 2  $$
Shear Layer Parameters:
$$du_y = U_0 \tanh \left( \frac{x- (L_x}{2)}{L_V} \right); U_0 \approx 10 V_{A}^{*} \quad \mathbf{U} = U_{0}\tanh \left(\frac{x}{L_{v}} \right) \hat y$$
Magnetic and Electric Field:
$$\vec{B} = B_{0} (\sin \theta\hat{y} + \cos \theta \hat{z}); \quad \vec{E} = -\left( \frac{B_{0}U_{0}}{c}\right) \tanh \left(\frac{x}{L_v} \right)$$
$$B_{0}= \frac{m_{e}c \omega_{ce}}{e}; \quad \theta= 2.86 \degree$$
Excess Electrons:
$$n_{e}= - \frac{\partial_{x} E_{x}}{4 \pi e} $$

