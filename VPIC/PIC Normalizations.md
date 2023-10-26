[PIC Normalizations](https://gkeyll.readthedocs.io/en/latest/dev/vlasov-normalizations.html)
Vlasov Maxwell Equations in SI units:
$$
\partial_t f + v \cdot \nabla_x f + \frac{q}{m}(E + v \times B)\cdot\nabla_vf =0
$$$$
\partial_t B + \nabla_x \times E = 0 \qquad \nabla_x \cdot B = 0
$$
$$
\epsilon_0 \mu_0 \partial_t - \nabla_x \times B = - \mu_0 J \qquad \nabla_x \cdot E = \frac{\rho}{\epsilon_0}
$$
$$
\rho = \sum q \int_{-\infty}^\infty f dv \qquad J = \sum q \int_{-\infty}^{\infty} vfdv
$$
With these equations, we set the normalizations to be around the electron length and time scales such that:
$$
t = \omega_{pe} \tau \quad x = d_e \chi \quad v = c \nu
$$
$$
q = e \tilde q \quad m = m_e \tilde m \quad n = n_0 \tilde n 
$$
$$
 E = \frac{e n_0 d_e}{\epsilon_0} \tilde E \quad B = \frac{e n_0}{\epsilon_0 \omega_{pe}} \tilde B 
$$
where 
$$
c = \frac{1}{\sqrt{\mu_0 \epsilon_0}} \quad \omega_{pe} = \sqrt{\frac{e^2 n_0}{m_e \epsilon}}
$$