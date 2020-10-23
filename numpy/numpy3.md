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

```
a. order：'C' -- 按行，'F' -- 按列，'A' -- 原顺序，'k' -- 元素在内存中的出现顺序。(简记)
b. order：{'C / F，'A，K}，可选使用此索引顺序读取a的元素。'C'意味着以行大的C风格顺序对元素进行索引，最后一个轴索引会更改F表示以列大的Fortran样式顺序索引元素，其中第一个索引变化最快，最后一个索引变化最快。请注意，'C'和'F'选项不考虑基础数组的内存布局，仅引用轴索引的顺序.A'表示如果a为Fortran，则以类似Fortran的索引顺序读取元素在内存中连续，否则类似C的顺序。“ K”表示按照步序在内存中的顺序读取元素，但步幅为负时反转数据除外。默认情况下，使用Cindex顺序。
```

`flatten()` 函数返回的是拷贝。

`numpy.ravel(a, order='C')` Return a contiguous flattened array.

`numpy.reshape(a, newshape[, order='C'])` 在不更改数据的情况下为数组赋予新的形状。

- 数组转置

`numpy.transpose(a, axes=None)` Permute the dimensions of an array.

`numpy.ndarray.T` Same as `self.transpose()` , except that self is returned if self.ndim < 2 .

- 更改维度

`numpy.newaxis = None` None 的别名，对索引数组很有用。

```
numpy.squeeze(a, axis=None) 从数组的形状中删除单维度条目，即把shape中为1的维度去掉。
a. a 表示输入的数组；
b. axis 用于指定需要删除的维度，但是指定的维度必须为单维度，否则将会报错；
```

- 数组组合

- 数组拆分
- 数组平铺
- 添加和删除元素

### 向量化和广播

