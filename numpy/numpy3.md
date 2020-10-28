### 数组操作

- 更改形状

`numpy.ndarray.shape` 表示数组的维度，返回一个元组，这个元组的长度就是维度的数目，即 `ndim` 属性(秩)。

```python
x = np.array([1, 2, 9, 4, 5, 6, 7, 8])
print(x.shape) # (8,)
x.shape = [2, 4]
print(x)
# [[1 2 9 4]
# [5 6 7 8]]
```

`numpy.ndarray.flat `将数组转换为一维的迭代器，可以用for访问数组每一个元素。

```python
y = x.flat
print(y)
# <numpy.flatiter object at 0x0000020F9BA10C60>
for i in y:
print(i, end=' ') # 11 12 13 14 15 16 17 18 19 20 21 22 23 24 ...
y[3]=0
```

`numpy.ndarray.flatten([order='C'])` 将数组的副本转换为一维数组，并返回。

`flatten()` 函数返回的是**拷贝**。

```
a. order：'C' -- 按行，'F' -- 按列，'A' -- 原顺序，'k' -- 元素在内存中的出现顺序。(简记)
b. order：{'C / F，'A，K}，可选使用此索引顺序读取a的元素。'C'意味着以行大的C风格顺序对元素进行索引，最后一个轴索引会更改F表示以列大的Fortran样式顺序索引元素，其中第一个索引变化最快，最后一个索引变化最快。请注意，'C'和'F'选项不考虑基础数组的内存布局，仅引用轴索引的顺序.A'表示如果a为Fortran，则以类似Fortran的索引顺序读取元素在内存中连续，否则类似C的顺序。“ K”表示按照步序在内存中的顺序读取元素，但步幅为负时反转数据除外。默认情况下，使用Cindex顺序。
```

`numpy.ravel(a, order='C')` Return a contiguous flattened array.

`numpy.reshape(a, newshape[, order='C'])` 在不更改数据的情况下为数组赋予新的形状。

例`y = np.reshape(x, [3, 4])`，为-1自动确定行列数

当参数`newshape = -1 `时，表示将数组降为一维。

- 数组转置

`numpy.transpose(a, axes=None)` Permute the dimensions of an array.

`numpy.ndarray.T` Same as `self.transpose()` , except that self is returned if self.ndim < 2 .

`y = x.T`or`y = np.transpose(x)`

- 更改维度

`numpy.newaxis = None` None 的别名，对索引数组很有用。

```
numpy.squeeze(a, axis=None) 从数组的形状中删除单维度条目，即把shape中为1的维度去掉。
a. a 表示输入的数组；
b. axis 用于指定需要删除的维度，但是指定的维度必须为单维度，否则将会报错；
```

- 数组组合

`1. numpy.concatenate((a1, a2, ...), axis=0, out=None) Join a sequence of arrays along an existing axis`

`1. numpy.stack(arrays, axis=0, out=None) Join a sequence of arrays along a new axis.`

沿着新的轴加入一系列数组（stack为增加维度的拼接）。

```python
1. numpy.vstack(tup) Stack arrays in sequence vertically (row wise).
2. numpy.hstack(tup) Stack arrays in sequence horizontally (column wise).
```



- 数组拆分

`1. numpy.split(ary, indices_or_sections, axis=0) Split an array into multiple sub-arrays as views into ary.`

`1. numpy.vsplit(ary, indices_or_sections) Split an array into multiple sub-arrays vertically (row-wise).`

`1. numpy.hsplit(ary, indices_or_sections) Split an array into multiple sub-arrays horizontally (column-wise).`

- 数组平铺

`1. numpy.tile(A, reps) Construct an array by repeating A the number of times given by reps.`

```python
1. numpy.repeat(a, repeats, axis=None) Repeat elements of an array.
a. axis=0 ，沿着y轴复制，实际上增加了行数。
b. axis=1 ，沿着x轴复制，实际上增加了列数。
c. repeats ，可以为一个数，也可以为一个矩阵。
d. axis=None 时就会flatten当前矩阵，实际上就是变成了一个行向量。
```

- 添加和删除元素

- ```python
  1. numpy.unique(ar, return_index=False, return_inverse=False,return_counts=False, axis=None) Find the unique elements
  of an array.
  a. return_index：the indices of the input array that give the unique values
  b. return_inverse：the indices of the unique array that reconstruct the input array
  c. return_counts：the number of times each unique value comes up in the input array
  ```

### 向量化和广播

```
有了向量化，编写代码时无需使用显式循环.
广播（Broadcasting）机制描述了 numpy 如何在算术运算期间处理具有不同形状的数组，让较小的数组在较大的数组上“广播”，以便它们具有
兼容的形状。并不是所有的维度都要彼此兼容才符合广播机制的要求，但它们必须满足一定的条件。
若两个数组的各维度兼容，也就是两个数组的每一维等长，或其中一个数组为 一维，那么广播机制就适用。
```

**广播的三个规则**：

```
1. 如果两个数组的维度数dim不相同，那么小维度数组的形状将会在左边补1。
2. 如果shape维度不匹配，但是有维度是1，那么可以扩展维度是1的维度匹配另一个数组；
3. 如果shape维度不匹配，但是没有任何一个维度是1，则匹配引发错误；
```

