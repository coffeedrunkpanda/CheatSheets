# Numpy CheatSheet

- [Numpy CheatSheet](#numpy-cheatsheet)
  - [Importing](#importing)
  - [Creating Arrays \& Tensors](#creating-arrays--tensors)
  - [Array Properties](#array-properties)
  - [Indexing \& Slicing](#indexing--slicing)
  - [Basic Operations (element-wise)](#basic-operations-element-wise)
  - [Linear Algebra](#linear-algebra)
  - [Reshaping](#reshaping)
  - [Aggregate Functions](#aggregate-functions)
  - [Useful Functions](#useful-functions)

## Importing

```python
import numpy as np
```

## Creating Arrays & Tensors

```python
arr = np.array([1, 2, 3])                    # From list
arr = np.zeros((3, 3))                       # All zeros
arr = np.ones((2, 5, 10), dtype=int)         # All ones with dtype
arr = np.arange(0, 10, 2)                    # Range [start, end) with step 
arr = np.linspace(0, 1, 5)                   # 5 evenly spaced values
arr = np.random.random(3, 3)                 # Random uniform distribution [0, 1)
arr = np.random.randn(3, 3)                  # Random normal distribution (mean = 0, std = 1) 
arr = np.random.randint( 20, size=(3, 4, 5)) # Random int of specified size
```

## Array Properties

```python
arr.shape                               # Dimensions (blocks, rows, columns)
arr.dtype                               # Data type
arr.size                                # Total number of elements
arr.ndim                                # Number of dimensions
arr.nbytes                              # Memory usage
```

## Indexing & Slicing
```python
arr[0]                                  # First element
arr[1:3]                                # Elements 1-2
arr[:, 0]                               # All elements of the first column
arr[-1]                                 # Last element
arr[arr > 5]                            # Boolean indexing
arr[arr != 5]                           # Boolean indexing
```

## Basic Operations (element-wise)
```python
arr + 5                                 # Add scalar 
arr * 2                                 # Multiply
arr ** 2                                # Power
np.sqrt(arr)                            # Square root
np.exp(arr)                             # Exponential
```

## Linear Algebra

```python
arr_1 * arr_2                           # Element-wise multiplication (NxM)*(NxM)
np.multiply(arr1, arr2)                 # Element-wise multiplication (NxM)*(NxM)
np.divide(arr1, arr2)                   # Element-wise multiplication (NxM)*(NxM)
np.dot(arr1, arr2)                      # Matrix multiplication (NxM)*(MxN)
np.transpose(arr)                       # Transpose
np.transpose(arr_3d, (1,2,0))           # Transpose
np.linalg.inv(arr)                      # Matrix inverse
np.linalg.det(arr)                      # Determinant
np.linalg.eig(arr)                      # Eigenvalues/vectors
np.eye(7)                               # Identity matrix
```

## Reshaping
```python
arr.reshape(2, 5)                       # Change shape
arr.flatten()                           # 1D array
np.concatenate([arr1, arr2])            # Combine arrays
np.stack([arr1, arr2])                  # Stack arrays
```
## Aggregate Functions
```python
np.sum(arr)                             # Sum
np.mean(arr)                            # Average
np.std(arr)                             # Standard deviation
np.min(arr), np.max(arr)                # Min/Max
np.argmin(arr), np.argmax(arr)          # Index of min/max
```

## Useful Functions

```python
arr.to_list()                           # Convert array to python list    
np.round(arr, 2)                        # Round to 2 decimal points
np.sort(arr)                            # Sort
np.unique(arr)                          # Unique elements
np.where(arr > 5, arr, 0)               # Conditional values
np.clip(arr, 0, 10)                     # Limit values to range

```
