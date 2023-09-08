Method: Radial average over bins
```python
def Eb2Dspec(dbx, dby):
    nx = dbx.shape[0]
    ny = dbx.shape[1]
    
    fdbx = np.fft.fftshift(np.fft.fftn(dbx))
    fdbx = np.abs(fdbx)**2
    fdbx = fdbx.flatten()
    
    fdby = np.fft.fftshift(np.fft.fftn(dby))
    fdby = np.abs(fdby)**2
    fdby = fdbx.flatten()

    kfreqx = np.fft.fftshift(np.fft.fftfreq(nx) * nx)
    kfreqy = np.fft.fftshift(np.fft.fftfreq(ny) * ny)
    kfreq2D = np.meshgrid(kfreqx, kfreqy)
    knrm = np.sqrt(kfreq2D[0]**2 + kfreq2D[1]**2)
    knrm = knrm.flatten()

    kvals = np.linspace(0, int(np.max(knrm)), len(knrm))
    kbins = np.linspace(0, int(np.max(knrm)), int(np.max(knrm)))
    fdbx_av = np.zeros(len(kbins))
    fdby_av = np.zeros(len(kbins))
    print(len(kbins))
    for k in np.arange(0, int(np.max(knrm))-1):
        index = np.where((knrm > kbins[k]) & (knrm < kbins[k+1]))[0]
        if len(index) == 0:
            fdbx_av[k] = 0
            fdby_av[k] = 0
        else:
            fdbx_av[k+1] = 2 * np.pi * (k+1) * np.mean(fdbx[index])/(nx * ny)
            fdby_av[k+1] = 2 * np.pi * (k+1) * np.mean(fdby[index])/(nx * ny)
            fdb_av = fdbx_av + fdby_av 
    return kbins, fdb_av
```