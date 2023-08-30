```python
def Spec2D(ar):
    """
      Spec2D(ar,ax=2,lenx=2*np.pi,leny=2*np.pi,lenz=2*np.pi)

      2D spectrum of ar perpendicular to axis ax

    """
    if len(ar) == 0:
      print('No array provided! Exiting!')
      return
    ar=ar-np.mean(ar)
    
    nx=np.shape(ar)[0]
    kx=nf.fftshift(nf.fftfreq(nx))*nx
    ny=np.shape(ar)[1]
    ky=nf.fftshift(nf.fftfreq(ny))*ny
    
    

    far = nf.fftshift(nf.fftn(ar))/(nx*ny); fftea=0.5*np.abs(far)**2
    fftebx=fftea.sum(axis=1)
    ffteby=fftea.sum(axis=0)
    return kx,ky,fftebx, ffteby
```