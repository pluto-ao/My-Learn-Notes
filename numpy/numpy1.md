#### 什么是numpy？

```
NumPy是Python中科学计算的基础包。
它是一个Python库，提供多维数组对象，各种派生对象（如掩码数组和矩阵），以及用于数组快速操作的各种例程，包括数学，逻辑，形状操作，排序，选择，I / O离散傅立叶变换，基本线性代数，基本统计运算，随机模拟等等。
```

#### 	1.常量

- ##### 空值 numpy.nan

`nan = NaN = NAN`

两个`numpy.nan `是不相等的。

`numpy.isnan(x, *args, **kwargs)  ` 判断是否空值

```python
import numpy as np
x = np.array([1, 1, 8, np.nan, 10])
print(x)
# [ 1. 1. 8. nan 10.]
y = np.isnan(x)
print(y)
# [False False False True False]
z = np.count_nonzero(y)
print(z) # 1
```

- ##### 无穷大 **numpy.inf**

  `Inf = inf = infty = Infinity = PINF`  

- ##### 圆周率 numpy.pi

- ##### 自然常数 numpy.e

#### 2.数据类型

- ##### 常见numpy数据类型

  ![image-20201020100004805](C:\Users\Pluto\AppData\Roaming\Typora\typora-user-images\image-20201020100004805.png)

- ##### 创建数据类型

  numpy 的数值类型实际上是 dtype 对象的实例。

  ![image-20201020095924772](C:\Users\Pluto\AppData\Roaming\Typora\typora-user-images\image-20201020095924772.png)

- 数据类型信息

  numpy整数具有限制,不能像python一样自动扩充

#### 3.时间datatime64


- 单位

![image-20201020103620621](C:\Users\Pluto\AppData\Roaming\Typora\typora-user-images\image-20201020103620621.png)

numpy 会根据字符串自动选择对应的单位。

```python
a = np.datetime64('2020-03-01')
print(a, a.dtype) # 2020-03-01 datetime64[D]
```

可以强制指定使用的单位

```python
print(a, a.dtype) # 2020-03-01 datetime64[D]
```

可从大单位转化为小单位 取01,若单位不统一则自动为最小的单位

arange()，用于生成日期范围

`a = np.arange('2020-08-01', '2020-08-10', dtype=np.datetime64)`

- timedelta表示两个 datetime64 之间的差。和的类型不变

生成 timedelta64时，要注意年（'Y'）和月（'M'）这两个单位无法和其它单位进行运算

- 类型转换

```python
dt64 = np.datetime64(dt, 's')
print(dt64, dt64.dtype)
# 2020-06-01T20:05:30 datetime64[s]
dt2 = dt64.astype(datetime.datetime)
print(dt2, type(dt2))
# 2020-06-01 20:05:30 <class 'datetime.datetime'>
```

- ##### numpy.busday_offset

工作日计算

#### 4.数组的创建

- 通过array()函数创建 np.array([])

- 通过asarray()函数进行创建

```
array() 和asarray() 都可以将结构数据转化为 ndarray，但是array() 和asarray() 主要区别就是当数据源是ndarray 时， array() 仍然会 copy 出一个副本，占用新的内存，但不改变 dtype 时 asarray() 不会。
```

- 通过fromfunction()函数进行创建

  `def fromfunction(function,  shape, **kwargs):`

- 依据 ones 和 zeros 填充方式

   0数组

```python
1. zeros() 函数：返回给定形状和类型的零数组。
2. zeros_like() 函数：返回与给定数组形状和类型相同的零数组。
def zeros(shape, dtype=None, order='C'):
def zeros_like(a, dtype=None, order='K', subok=True, shape=None):
```

​		1数组

```python
1. ones() 函数：返回给定形状和类型的1数组。
2. ones_like() 函数：返回与给定数组形状和类型相同的1数组。
def ones(shape, dtype=None, order='C'):
def ones_like(a, dtype=None, order='K', subok=True, shape=None):
```

​		空数组

```python
1. empty() 函数：返回一个空数组，数组元素为随机数。
2. empty_like 函数：返回与给定数组具有相同形状和类型的新数组。
def empty(shape, dtype=None, order='C'):
def empty_like(prototype, dtype=None, order='K', subok=True, shape=None):
```

​		单位数组

```python
1. eye() 函数：返回一个对角线上为1，其它地方为零的单位数组。
2. identity() 函数：返回一个方的单位数组。
def eye(N, M=None, k=0, dtype=float, order='C'):
def identity(n, dtype=None):
```

​		对角数组

```python
1. diag() 函数：提取对角线或构造对角数组。
def diag(v, k=0):
```

​		常数数组

```python
1. full() 函数：返回一个常数数组。
2. full_like() 函数：返回与给定数组具有相同形状和类型的常数数组。
def full(shape, fill_value, dtype=None, order='C'):
def full_like(a, fill_value, dtype=None, order='K', subok=True, shape=None):
```

- 利用数值范围来创建ndarray

```python
1. arange() 函数：返回给定间隔内的均匀间隔的值。
2. linspace() 函数：返回指定间隔内的等间隔数字。
3. logspace() 函数：返回数以对数刻度均匀分布。
4. numpy.random.rand() 返回一个由[0,1)内的随机数组成的数组。
def arange([start,] stop[, step,], dtype=None):
def linspace(start, stop, num=50, endpoint=True, retstep=False,
dtype=None, axis=0):
def logspace(start, stop, num=50, endpoint=True, base=10.0,
dtype=None, axis=0):
def rand(d0, d1, ..., dn):                             
```

- 结构数组的创建

  `结构数组，首先需要定义结构，然后利用np.array() 来创建数组，其参数dtype 为定义的结构。`

  - 利用字典来定义结构

  ```python
  import numpy as np
  personType = np.dtype({
  	'names': ['name', 'age', 'weight'],
  	'formats': ['U30', 'i8', 'f8']})
  a = np.array([('Liming', 24, 63.9), ('Mike', 15, 67.), ('Jan', 34, 45.8)],dtype=personType)
  print(a, type(a))
  # [('Liming', 24, 63.9) ('Mike', 15, 67. ) ('Jan', 34, 45.8)]
  # <class 'numpy.ndarray'>
  ```

  - 利用包含多个元组的列表来定义结构

  ```python
  import numpy as np
  personType = np.dtype([('name', 'U30'), ('age', 'i8'), ('weight', 'f8')])
  a = np.array([('Liming', 24, 63.9), ('Mike', 15, 67.), ('Jan', 34, 45.8)],
  dtype=personType)
  print(a, type(a))
  # [('Liming', 24, 63.9) ('Mike', 15, 67. ) ('Jan', 34, 45.8)]
  # <class 'numpy.ndarray'>
  # 结构数组的取值方式和一般数组差不多，可以通过下标取得元素：
  print(a[0])
  # ('Liming', 24, 63.9)
  print(a[-2:])
  # [('Mike', 15, 67. ) ('Jan', 34, 45.8)]
  # 我们可以使用字段名作为下标获取对应的值
  print(a['name'])
  # ['Liming' 'Mike' 'Jan']
  print(a['age'])
  # [24 15 34]
  print(a['weight'])
  # [63.9 67. 45.8]
  ```

#### 5.数组的属性

```python
1. numpy.ndarray.ndim 用于返回数组的维数（轴的个数）也称为秩，一维数组的秩为 1，二维数组的秩为 2，以此类推。
2. numpy.ndarray.shape 表示数组的维度，返回一个元组，这个元组的长度就是维度的数目，即 ndim 属性(秩)。
3. numpy.ndarray.size 数组中所有元素的总量，相当于数组的shape 中所有元素的乘积，例如矩阵的元素总量为行与列的乘积。
4. numpy.ndarray.dtype ndarray 对象的元素类型。
5. numpy.ndarray.itemsize 以字节的形式返回数组中每一个元素的大小。
class ndarray(object):
    shape = property(lambda self: object(), lambda self, v: None, lambda self: None)
    dtype = property(lambda self: object(), lambda self, v: None, lambda self: None)
    size = property(lambda self: object(), lambda self, v: None, lambda self: None)
    ndim = property(lambda self: object(), lambda self, v: None, lambda self: None)
    itemsize = property(lambda self: object(), lambda self, v: None, lambda self: None)
```

在ndarray 中所有元素必须是同一类型，否则会自动向下转换， **int->float->str 。**

#### 6.副本与视图

在 Numpy 中，尤其是在做数组运算或数组操作时，返回结果不是数组的 **副本** 就是 **视图**。所有赋值运算*不会*为数组和数组中的任何元素*创建副本*。

```
1. numpy.ndarray.copy() 函数创建一个副本。 对副本数据进行修改，不会影响到原始数据，它们物理内存不在同一位置。
```

数组切片操作返回的对象只是原数组的视图。

`不创建副本即会影响原数组`