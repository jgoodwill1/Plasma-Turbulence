- Takes in an 1D array and outputs wavenumber k and magnetic energy
```python
import numpy.fft as nf
import errno
import math
import os
import sys
import re
import pickle
import h5py as h5
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import csv
from scipy.stats import norm
import statistics
def Spec1D(ar):
    if len(ar) == 0:
      print('No Array')
      return
    ar=ar-np.mean(ar)
    nx=len(ar)
    k= np.abs(nf.fftfreq(nx)* nx)
    far = nf.fft(ar)/(nx); 
    ffteb=0.5*np.abs(far)**2
    return k, ffteb
```
![[1Dspectrum_example.png]]
