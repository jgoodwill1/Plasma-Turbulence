```python
import sys

base = '/pscratch/sd/g/goodwill/'

dirs = '/pscratch/sd/g/goodwill/'

sys.path.insert(0, base)

from Analysis import *

  

times = np.array(get_times(dirs))

vpic_info = get_vpic_info(dirs)
```