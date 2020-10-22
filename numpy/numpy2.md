#### 索引与切片

数组索引机制指的是用方括号（[]）加序号的形式引用单个数组元素，它的用处很多，比如抽取元素，选取数组的几个元素，甚至为其赋一个新值。

- 整数索引 
- 切片索引

切片操作是指抽取数组的一部分元素生成新数组。对 python 列表进行切片操作得到的数组是原数组的副本，而对 Numpy 数据进行切片操作得到的数组则是指向相同缓冲区的视图。`[start:stop:step]`

- dots索引

NumPy 允许使用... 表示足够多的冒号来构建完整的索引列表。

```python
1. x[1,2,...] 等于 x[1,2,:,:,:]
2. x[...,3] 等于 x[:,:,:,:,3]
3. x[4,...,5,:] 等于 x[4,:,:,5,:]
```

- 整数数组索引

方括号内传入多个索引值，可以同时选择多个元素。

`numpy. take(a, indices, axis=None, out=None, mode='raise')`

- 布尔索引 n

#### 数组迭代

`apply_along_axis(func1d, axis, arr)` Apply a function to 1-D slices along the given axis. 

axis = 0列 竖着

axis = 1行 横着

```python
def my_func(x):
return (x[0] + x[-1]) * 0.5
y = np.apply_along_axis(my_func, 0, x)
print(y) # [21. 22. 23. 24. 25.]
y = np.apply_along_axis(my_func, 1, x)
print(y) # [13. 18. 23. 28. 33.]
```

