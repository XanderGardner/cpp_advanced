
[Data Manipulation](#data-manipulation)
[Linear Algebra](#linear-algebra)

- pytorch

## Tensors

- tensors represent n-d arrays
```python
import torch

# create tensor
x = torch.tensor([[1,2],[3,4]])
x = torch.arange(12, dtype=torch.float32) #[0,1,2,...,11]
x = torch.zeros((2,3,4)) # all 0's:  2 by 3 by 4 shape
x = torch.ones((2,3,4))  # all 1's
x = torch.randn(3,4)     # all iid normal:  3 by 4 shape
z = torch.zeros_like(y)  # all 0's with same shape as tensor y
z = torch.clone(y) # create a deep copy of y


# get number of elements and shape
x.numel() # int
x.shape # torch.Size object

# read
x[-1] # select last row (last on axis 0)
x[1:3] # rows 1 and 2


# read to python object
a.item() # only when one element
float(a) # only when one element
int(a)   # only when one element


# write/edit
x[0,2] = 17 # row 0, column 2
x[:2, :] = 12 # for rows 0,1 (and for every column) set to 12
x = x.reshape(3,4) # change shape to 3 rows, 4 columns (read like a book)
a = torch.cat((x, y), dim=0) # concatenate along 0 axis (add rows)
x.unsqueeze(0) # adds dimension [5,6,7] -> [[5,6,7]]
a = torch.cat((x, y.unsqueeze(0)), dim=0) # concatenate to end

```

- tensor operations
```python
# e^x for each element
y = torch.exp(x)


# applies element wise
# make sure shapes are the same (or broadcasting will occur)
x + y
x - y
x * y
x / y
x ** y
x == y  # tensor of bools


# sum (returns a tensor)
x.sum() # tensor of sum of all elements
x.sum(axis=1) # tensor of the sum of elements across columns (row sums)
x.sum(axis=1, keepdims=True) # keep the same shape so that axis has shape 1


# mean
a.mean() # tensor of mean of all elements
a.mean(axis=1) # tensor of the mean of elmeents across columns (row sums)
x.mean(axis=1, keepdims=True) # keep the same shape so that axis has shape 1
x / x.sum(axis=1, keepdims=True) # rows sum up to one (using broadcasting)


# cumulative sum
a.cumsum(axis=0) # row by row cumulative sum as rows increase


# norms
torch.abs(u).sum() # l1 norm
torch.norm(u) # l2 norm


# matrix operations
a = a.T # transpose
z = torch.dot(x, y) # dot product
z = x@y # matrix multiplication
```





