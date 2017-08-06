# Python Snippets
#### Get Script Absolute Path
```
import os
os.path.dirname(os.path.abspath(__file__))
```
#### Get Current Directory
```
import os
os.getcwd()
```
#### Simple Filter
```
GAIN = 0.5
def simple_filter(new_val, old_val):
    return (new_val * GAIN) + (old_val * (1 - GAIN))
```
#### Moving Average Class
```
class MovingAverage(object):
    def __init__(self, average_size, initial_value=0):
        self._average_size = average_size
        self._values = [initial_value for _ in range(average_size)]
        
    def update(new_value):
        self._values.insert(0, new_value)
        self._values.pop()
        return sum(self._values) / self._average_size
```        
        
