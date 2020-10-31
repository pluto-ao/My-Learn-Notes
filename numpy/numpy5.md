### 排序，搜索和计数

#### 排序

- `numpy.sort(a, axis=-1, kind='quicksort', order=None)`

```python
np.random.seed(20201028)  
x = np.random.rand(3, 3) * 10
x = np.around(x, 2)
print(x)
# [[3.55 1.02 8.3 ]
#  [5.16 3.54 0.77]
#  [0.86 6.71 5.53]]

y = np.sort(x, axis=0)  # axis=0，按列排序
print(y)
# [[0.86 1.02 0.77]
#  [3.55 3.54 5.53]
#  [5.16 6.71 8.3 ]]

y = np.sort(x, axis=1)  # axis=1，按行排序
print(y)
# [[1.02 3.55 8.3 ]
#  [0.77 3.54 5.16]
#  [0.86 5.53 6.71]]

y = np.sort(x)  # 默认按行排序
print(y)
# [[1.02 3.55 8.3 ]
#  [0.77 3.54 5.16]
#  [0.86 5.53 6.71]]
```

- 参数 order

```python
tp = np.dtype([('name', 'S10'), ('age', np.int)])

a = np.array([("dawang", 21), ("yiyi", 18)], dtype=tp)

b = np.sort(a, order='name')  # 按name排序
print(b)
# [(b'dawang', 21) (b'yiyi', 18)]

b = np.sort(a, order='age')  # 按age排序
print(b)
# [(b'yiyi', 18) (b'dawang', 21)]
```

- `numpy.argsort()`

用元素的索引位置替代排序后的实际结果

- `numpy.lexsort()`

指定排序指标

- `numpy.partition()`

以索引是 kth 的元素为基准，将元素分成两部分，即大于该元素的放在其后面，小于该元素的放在其前面。

#### 搜索

- `numpy.argmax() & numpy.argmin()`

`numpy.argmax()`是返回数组最大值的索引，`numpy.argmin()`与之相反

- `numppy.nonzero()`

返回非零元素的索引值

将布尔数组转换成整数数组

```python
x = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
print(x)
# [[1 2 3]
#  [4 5 6]
#  [7 8 9]]

y = x > 5
print(y)
# [[  False False False]
#  [ False  False  True]
#  [ True  True  True]]

y = np.nonzero(x > 5)
print(y)
# (array([1, 2, 2, 2], dtype=int64), array([2, 0, 1, 2], dtype=int64))

y = x[np.nonzero(x > 5)]
print(y)
# [6 7 8 9]

y = x[x > 3]
print(y)
# [6 7 8 9]
```

- `numpy.where(condition, x, y)`

满足条件`condition`，输出`x`，不满足输出`y`

只有`condition`，没有`x`和`y`，则输出满足条件元素的坐标(等价于`numpy.nonzero`).

- `numpy.searchsorted(a, v, side='left')`

a：一维输入数组。

v：插入`a`数组的值，可以为单个元素，`list`或者`ndarray`。

side：查询方向，当为`left`时，将返回第一个符合条件的元素下标；当为`right`时，将返回最后一个符合条件的元素下标。

#### 计数

- `numpy.count_nonzero()`

返回数组中的非0元素个数。

### 集合操作

#### 构造集合

- `numpy.sunique(ar, return_index=False, return_inverse=False, return_counts=False, axis=None)` Find the unique elements of an array.

  a. return_index=True 表示返回新列表元素在旧列表中的位置。
  b. return_inverse=True 表示返回旧列表元素在新列表中的位置。
  c. return_counts=True 表示返回新列表元素在旧列表中出现的次数。

#### 布尔运算

- `numpy.in1d(ar1, ar2, assume_unique=False, invert=False)`

前面的数组是否包含于后面的数组，返回布尔值。

#### 求两个集合的交集

-  `numpy.intersect1d(ar1, ar2)`

#### 并集

- `numpy.union1d(ar1, ar2)`

#### 差集

- `numpy.setdiff1d(ar1, ar2)`, 集合的差，即元素存在于第一个函数不存在于第二个函数中

#### 异或

- `setxor1d(ar1, ar2)`，异或，即两个数组中各自独自拥有的元素的集合