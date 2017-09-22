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

#### Kalman Filter
```
import numpy as np
class KalmanFilter(object):
    def __init__(self, F, B, H, Q, R, P, x):
        """
        Based on https://en.wikipedia.org/wiki/Kalman_filter#Predict
        :type F: numpy.matrix
        :type B: numpy.matrix
        :type H: numpy.matrix
        :type Q: numpy.matrix
        :type R: numpy.matrix
        :type P: numpy.matrix
        :type x: numpy.matrix
        """

        assert F.shape == Q.shape
        assert F.shape == P.shape
        assert F.shape[0] == B.shape[0]
        assert F.shape[0] == H.shape[1]
        assert H.shape[0] == R.shape[0]
        assert H.shape[0] == R.shape[1]

        self._F = F
        self._B = B
        self._H = H
        self._Q = Q
        self._R = R
        self._P = P
        self._I = np.identity(self._P.shape[0])
        self._x = x

    def update(self, z, u):
        """
        :type z: numpy.matrix
        :type u: numpy.matrix
        """
        # Predict
        self._x = self._F * self._x + self._B * u
        self._P = self._F * self._P * self._F.T + self._Q

        # Update
        y = z - self._H * self._x
        S = self._R + self._H * self._P * self._H.T
        K = self._P * self._H.T * S.I
        self._x = self._x + K * y
        self._P = (self._I - K * self._H) * self._P
        return self._x
```
        
