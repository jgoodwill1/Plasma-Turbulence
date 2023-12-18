Method: Radial average over bins
```python
def EbSpec2D(dbx, dby):
    nx = dbx.shape[0]
    ny = dbx.shape[1]
    
    fdbx = np.fft.fftshift(np.fft.fftn(dbx))/(nx * ny)
    fdbx = np.abs(fdbx)**2/2
    fdbx = fdbx.flatten()
    
    fdby = np.fft.fftshift(np.fft.fftn(dby))/(nx * ny)
    fdby = np.abs(fdby)**2/2
    fdby = fdbx.flatten()

    kfreqx = np.fft.fftshift(np.fft.fftfreq(nx) * nx)
    kfreqy = np.fft.fftshift(np.fft.fftfreq(ny) * ny)
    kfreq2D = np.meshgrid(kfreqx, kfreqy)
    knrm = np.sqrt(kfreq2D[0]**2 + kfreq2D[1]**2)
    knrm = knrm.flatten()
    
    kbins = np.linspace(0, int(np.max(knrm)), int(np.max(knrm)))
    fdbx_av = np.zeros(len(kbins))
    fdby_av = np.zeros(len(kbins))
    for k in np.arange(0,len(kbins)-1):
        index = np.where((knrm > kbins[k]) & (knrm <= kbins[k+1]))[0]
        if (len(index) == 0):
            fdbx_av[k] = 0
            fdby_av[k] = 0
        else:
            # print(fdbx[index])
            fdbx_in = fdbx[index]
            fdby_in = fdby[index]
            # print(fdbx_in)
            fdbx_av[k] = np.sum(fdbx_in)
            fdby_av[k] = np.sum(fdby_in)
            fdb_av = fdbx_av + fdby_av
    return kbins, fdb_av
```
![[Yan_Spectrum.jpeg]]

![[149p6_spectrum.jpg]]
![[magSpec_filt.jpg]]
