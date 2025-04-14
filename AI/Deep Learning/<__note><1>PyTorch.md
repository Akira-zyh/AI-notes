# Foundation of PyTorch

## Tensor

> *tensor* is the extension of *vector* and *matrix*

| dimension of *sensor* | representation                                            |
| --------------------- | --------------------------------------------------------- |
| 0-dim sensor          | *scalar* (number)                                         |
| 1-dim sensor          | *vector*                                                  |
| 2-dim sensor          | *matrix*                                                  |
| 3-dim sensor          | a *RGB* image, text data, stock price, *time series data* |
*Sensor* is the foundation of modern Machine Learning. 
The core of *sensor* is a **data container** which can be imagined as a bucket filled with numbers.

Some types *sensors* which storages common datasets 
- **3-dim**: time series
- **4-dim**: images
- **5-dim**: videos

For example, a single RGB image can be represented as follows:
```Python
(width, height, channel) = 3D
```
While, in actual work, we always need to process a set of images which can be represented as follows:
```Python
(batch_size, width, height, channel) = 4D
```

In *PyTorch*, `torch.Tensor` is a fundamental tool to storage and transform data.
`torch.Tensor` is very similar with `ndarray` in *NumPy*.

However, compared with `ndarray`, `torch.Tensor` provides more powerful abilities(computing on GPUs and automatic solve gradient .etc) which make `Tensor` more fit for Deep Learning.

### Create *tensor*
1. created **randomly initialized matrices** by using `torch.rand()`: 
```Python
import torch
x = torch.rand(4,3)
print(x)
```
![[randcode.png]]

2. create **zero matrices** by using `torch.zeros()` and **set data type** by using parameter `dtype` :
```Python
import torch
x = torch.zeros(4, 3, dtype=torch.long)
```
> we can also convert non-zero matrices into zero matrices by using `torch.zero_()` or `torch.zeros_like()`

3. create **tensors from data** by using `torch.tensor()`:
```Python
import torch
x = torch.tensor([5.5, 3]) # 1-dim tensor
```

4. create **tensors based on tensor already exists**:
```Python
x = x.new_ones(4, 3, dtype=torch.double)
# new tensor has the same torch.dtype and torch.device
x = torch.randn_like(x, dtype=torch.float)
```

#### Common methods of creating tensors:

| Function               | Ability                                                                               |
| ---------------------- | ------------------------------------------------------------------------------------- |
| `Tensor(sizes)`        | basic constructor function                                                            |
| `tensor(data)`         | similar with `np.array`                                                               |
| `ones(size)`           | all elements are `1`                                                                  |
| `zeros(size)`          | all elements are `0`                                                                  |
| `eye(sizes)`           | 对角为1， 其余为0                                                                            |
| `arange(s, e, step)`   | from `s` to `e`, with `step`                                                          |
| `linspace(s, e, steps` | from `s` to `e`, divided into `steps` parts                                           |
| `rand / randn(sizes)`  | `rand`: **uniform** distribution $(0, 1)$. `randn`: **normal** distribution $N(0,1)$. |
| `normal(mean, std)`    | normal distribution whose $mean$ is `mean` and $std$ is `std`                         |
| `randperm(m)`          | random arrangements                                                                   |
