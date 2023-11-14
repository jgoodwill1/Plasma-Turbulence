```python
def pth_calc(dirs, timestep, species, kfilt = 100):
    cbx, cby, cbz, ex, ey, ez, jx, jy, jz, ke, px, py, pz, rho, txx, txy, tyy, tyz, tzx, tzz =load_vars(dirs,timestep,species)
    vpic_info = get_vpic_info(dirs)
    if species == 'ion':
        particle_mass = mi_me
    if species == 'electron':
        particle_mass = 1
    dx = vpic_info['dx/de'] * vpic_info['di']
    dy = vpic_info['dy/de'] * vpic_info['di']
    
    pxx = kfilter(np.array(txx - (jx/rho)*px), kfilt)
    pyy = kfilter(np.array(tyy - (jy/rho)*py), kfilt)
    pzz = kfilter(np.array(tzz - (jz/rho)*pz), kfilt)
    p = (1/3)*(pxx + pyy + pzz)
    
    ux = kfilter(px/rho/particle_mass, kfilt)
    uy = kfilter(py/rho/particle_mass, kfilt)

    
    dux_dx = (np.roll(ux,-1,axis=0)-np.roll(ux,1,axis=0))/(2 * dx)
    duy_dy = (np.roll(uy,-1,axis=1)-np.roll(uy,1,axis=1))/(2 * dy)
    
    theta = np.array(dux_dx + duy_dy)
    ptheta = -p * theta

    pth_rms = np.sqrt(np.mean(ptheta**2))
    ptheta = ptheta/pth_rms
    return ptheta
```