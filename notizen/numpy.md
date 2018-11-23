# NumPy

Arrays of numbers are the fundamental data structure for data analysis.
Python's primitive values have a large overhead. This information is redundant
in lists, because the same type information is stored for every element. NumPy
arrays are much more efficent than Python's lists―especially for big data sets.
Python also offers an array type without redundant type information. However,
this array type doesn't offer the fast and powerful operations of NumPy's
`ndarray` type.

Conventionally, the NumPy library is imported as follows:

```python
import numpy as np
```

## Array Creation

### Arrays of Python Lists

NumPy arrays can be created from Python lists:

```python
ints = np.array([2, 4, 6, 8]) # integer array
floats = np.array([2, 4, 6, 8.1]) # upcast to float because of 8.1
floats = np.array([2, 4, 6, 8], dtype='float') # with explicit type parameter
ints = np.array([1.1, 2.2, 3.3], dtype='int') # with explicit type parameter
```

NumPy arrays can be multi-dimensional:

```python
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])
```

### Arrays from Scratch

Numpy offers various functions to generate arrays from scratch. Where a
dimension is required (`size`), a single number (length), a tuple of two (rows,
columns) or more (1st dimension, 2nd dimension, 3rd dimension, etc.) can be
passed.

- `np.zeros(size, dtype)`: array of zeros
- `np.ones(size, dtype)`: array of ones
- `np.full(size, value)`: array filled with the given value
- `np.arange(start, end, step)`: array with values from start (inclusive) to
  end (exclusive) and given step width; `length=(end-start)/step`
- `np.linspace(from, to, n)`: array with evenly spaced values in interval
  `[from,to]` (both inclusive) of length n
- `np.random.random(size)`: uniformly distributed random values
- `np.random.normal(mean, sd, size)`: normally distributed array with the given
  mean and standard deviation
- `np.random.randint(from, to, size)`: random integers in the interval
  `[from,to)` (inclusive/exclusive)
- `np.eye(n)`: identity matrix with n rows and columns (values at indices with
  equal row/column index are 1)
- `np.empty(size)`: uninitialized array, values from current memory content
  (garbage)

### Data Types

The `dtype` parameter can either be passed as a string literal or using a
pre-defined constant:

1. literal: `dtype='int32'`
2. constant: `dtype=np.int32`

Common numeric types are:

- boolean: `Bool_`
- signed integers: `int8`, `int16`, `int32`, `int64`
    - `int_`: system's default `long`
    - `intc`: system's default `int`
- unsigned integers: `uint8`, `uint16`, `uint32`, `uint64`
- floating point: `float16`, `float32`, `float64` 
    - `float_`: system default
- complex numbers: `complex64`, `complex128`
    - `complex_`: system default

## Array Manipulation

NumPy arrays offer a rich set of attributes and operation for their manipulation. Since NumPy arrays are the foundation of many higher-level libraries, data manipulation in Python is often NumPy array manipulation.

### Attributes

These read-only attributes can be used to retrieve information about an array:

- `ndim`: number of dimensions
- `shape`: size of each dimension
- `size`: total size of the array (the number of elements)
- `dtype`: data type of the array's elements
- `itemsize`: byte size of a single element
- `nbytes`: byte size of the entire array

In general, `nbytes` is equal to `itemsize` multiplied by `size`.

```python
>>> np.random.seed(0) # for reproducable results
>>> arr = np.random.randint(10, 100, (3, 3))
>>> arr
array([[54, 57, 74],
       [77, 77, 19],
       [93, 31, 46])
>>> arr.ndim
2
>>> arr.shape
(3, 3)
>>> arr.size
9
>>> arr.dtype
dtype('int64')
>>> arr.itemsize
8
>>> arr.nbytes
72
>>> arr.itemsize * arr.size
72
```

### Indexing

Values of NumPy arrays can both be retrieved and modified by the means of
indexing.

The indexing of single dimension arrays works with square brackets, just like
indexing of Python lists:

- `arr[0]`: first element
- `arr[n]`: nth element
- `arr[-1]`: last element (first element counted from the end)
- `arr[-3]`: third last element (third element counted from the end)

For multi dimension arrays, a comma separated tuple has to be passed in square
brackets:

- `arr[0, 0]`: first element of the first dimension
- `arr[3, 5]`: fifth element of the third dimension

```python
>>> np.random.seed(0) # for reproducable results
>>> arr = np.random.randint(10, 100, (3, 3))
>>> arr
array([[54, 57, 74],
       [77, 77, 19],
       [93, 31, 46])
>>> arr[0, 0]
54
>>> arr[1, 2]
19
>>> arr[-1, -1]
46
>>> arr[2, 2]
46
```