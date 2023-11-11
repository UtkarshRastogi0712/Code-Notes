#Python 
Numpy is a library that makes tedious numerical applications and operations like matrix multiplication etc very simple. When used in tandem with [[Pandas]] , it offers a complete suite of data manipulation options for Machine Learning.

```Python
import numpy as np
import math

#create a matrix
m: list = [[1,2],[2,3]]
M: np.ndarray = np.array(m)

#reshaping a matrix
shape: tuple = M.shape
linearM: np.ndarray = M.reshape((1,4))

#Create a matrix from range
N: np.ndarray = np.arrange(4)

#Stack matrix vstack/hstack
S: np.ndarray = np.vstack((M,N))

#Repeat rows/columns
S = np.repeat(S, repeats=[2,2], axis=0)

#apply function to all elements of matrix
def sigmod(x:float)-> float:
	return 1/(1+math.exp(-x))
vecSigmoid: pyfunc = np.vectorize(sigmoid)
sigmoidS = vecSigmoid(S)

```