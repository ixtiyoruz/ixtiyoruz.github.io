---
layout: post
title: Pytorch einsum operation
date: 2022-02-01 10:20:20 +0900
description: Einstein summation convention
# img: back_1.jpg
tags: [Deep learning, Pytorch]
author: Majidov Ikhtiyor # Add name author (optional)
usemathjax: true
---


U bizga arrayning ustida bir necha turdagi operatsiyalarni bajarishga yordam beradi. Masalan transpose, kopaytirish, elementwise kopaytirish va hokazo.
uning sintaksisi quyidagicha:

```python
torch.einsum(equation_str, *tensors)
```
# Umuman uni examplelar orqli o'rgangan osonroq

```python
import torch
import numpy as np
```


```python
x = torch.rand((2,3))
```


```python
# permutation of tensors
torch.einsum("ij->ji", x).size()
```




    torch.Size([3, 2])




```python
# summation
torch.allclose(torch.einsum("ij->", x), x.sum())
```




    True




```python
# summing all rows, which returns an array with the shape of columns
torch.allclose(torch.einsum('ij->j',x), x.sum(0))
```




    True




```python
# summing all columns, which returns an array with the shape of rows
torch.allclose(torch.einsum('ij->i',x), x.sum(1))
```




    True




```python
# matrix vector multiplication
v = torch.rand((1,3))

print(torch.einsum("ij,kj->ik", x,v))
print('--'*20)
print(x@v.T)
```

    tensor([[0.5172],
            [0.3321]])
    ----------------------------------------
    tensor([[0.5172],
            [0.3321]])



```python
# matrix matrix multiplication

print(torch.einsum("ij,kj->ik", x,x))
print("--"*20)
print(x@x.T)
```

    tensor([[0.6382, 0.4915],
            [0.4915, 0.9763]])
    ----------------------------------------
    tensor([[0.6382, 0.4915],
            [0.4915, 0.9763]])



```python
# dot product of all the rows of the matrix with itself

print(torch.einsum("ij,ij->i", x,x))

```

    tensor([0.6382, 0.9763])



```python
# even the elementwise multiplication

print(torch.einsum("ij,ij->ij", x,x))
print("--"*20)
print(torch.multiply(x,x))
```

    tensor([[0.4260, 0.0994, 0.1127],
            [0.0325, 0.8927, 0.0511]])
    ----------------------------------------
    tensor([[0.4260, 0.0994, 0.1127],
            [0.0325, 0.8927, 0.0511]])



```python
# outer product
x = torch.rand((3))
y = torch.rand((5))

torch.einsum("i,j -> ij", a,b)
```




    tensor([[0.0897, 0.2208, 0.3084, 0.0471, 0.0190],
            [0.0379, 0.0933, 0.1304, 0.0199, 0.0080],
            [0.0608, 0.1495, 0.2088, 0.0319, 0.0128]])




```python
# batch matrix multiplication 

a = torch.rand((3,2,5))
b = torch.rand((3,5,3))

# you can do this with bmm
torch.einsum("ijk, ikl-> ijl", a,b)
```




    tensor([[[1.0678, 1.2429, 1.1200],
             [0.3129, 0.3637, 0.7859]],
    
            [[1.3433, 0.4159, 1.4224],
             [1.9831, 0.8470, 1.6947]],
    
            [[1.4838, 2.1888, 1.6716],
             [0.9673, 1.3760, 0.7142]]])




```python
# matrix diagonal
x = torch.rand((3,3))

torch.einsum("ii->i", x)
```




    tensor([0.9835, 0.6807, 0.7448])




```python
x
```




    tensor([[0.9835, 0.9617, 0.7266],
            [0.2494, 0.6807, 0.9855],
            [0.8947, 0.6352, 0.7448]])




```python

```


```python

```

ref:
1. Man ham Aladdin <a href='https://www.youtube.com/watch?v=pkVwUVEHmfI&ab_channel=AladdinPersson'>Einsum Is All You Need</a> 