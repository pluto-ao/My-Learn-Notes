 

### 数学函数

#### 算数运算

- `numpy.add`

- `numpy.subtract`

- `numpy.multiply`

- `numpy.divide`

- `numpy.floor_divide`

- `numpy.power`

`在 numpy 中对以上函数进行了运算符的重载，且运算符为 元素级。也就是说，它们只用于位置相同的元素之间，所得到的运算结果组成一个新的数组。`

- `numpy.sqrt`  平方根

- `numpy.square ` 平方

#### 三角函数

- `numpy.sin`

- `numpy.cos`

- `numpy.tan`

- `numpy.arcsin`

- `numpy.arccos`

- `numpy.arctan`

```
通用函数（universal function）通常叫作ufunc，它对数组中的各个元素逐一进行操作。这表明，通用函数分别处理输入数组的每个元素，生成的结果组成一个新的输出数组。输出数组的大小跟输入数组相同。
```

#### 指数和对数

- `numpy.exp`

- `numpy.log`

- `numpy.exp2`

- `numpy.log2`

- `numpy.log10`

#### 加法函数、乘法函数

- `numpy.sum(a[, axis=None, dtype=None, out=None, …]) Sum of array elements over a given axis.`

```
通过不同的 axis ，numpy 会沿着不同的方向进行操作：如果不设置，那么对所有的元素操作；如果axis=0 ，则沿着纵轴进行操作； axis=1 ，则沿着横轴进行操作。但这只是简单的二位数组，如果是多维的呢？可以总结为一句话：设axis=i ，则 numpy 沿着第i 个下标变化的方向进行操作。
```

- `numpy.cumsum(a, axis=None, dtype=None, out=None) Return the cumulative sum of the elements along a given axis.`

```
聚合函数 是指对一组值（比如一个数组）进行操作，返回一个单一值作为结果的函数。因而，求数组所有元素之和的函数就是聚合函数。ndarray 类实现了多个这样的函数。
```

```python
import numpy as np
x = np.array([[11, 12, 13, 14, 15],
[16, 17, 18, 19, 20],
[21, 22, 23, 24, 25],
[26, 27, 28, 29, 30],
[31, 32, 33, 34, 35]])
y = np.cumsum(x)
print(y)
# [ 11 23 36 50 65 81 98 116 135 155 176 198 221 245 270 296 323 351
# 380 410 441 473 506 540 575]
y = np.cumsum(x, axis=0)
print(y)
# [[ 11 12 13 14 15]
# [ 27 29 31 33 35]
# [ 48 51 54 57 60]
# [ 74 78 82 86 90]
# [105 110 115 120 125]]
y = np.cumsum(x, axis=1)
print(y)
# [[ 11 23 36 50 65]
# [ 16 33 51 70 90]
# [ 21 43 66 90 115]
# [ 26 53 81 110 140]
# [ 31 27 63 96 130 165]]
```

- `numpy.prod乘积 `  返回给定轴上数组元素的乘积。

- `numpy.cumprod累乘 ` 返回给定轴上数组元素的累乘

- `numpy.diff差值 `计算沿给定轴的第n个离散差

`第一个差异由沿着给定轴的out [i] = a [i + 1] -a[i]给出，更高的差异通过递归使用diff计算。`

#### 四舍五入

- `numpy.around舍入`

`numpy.around(a, decimals=0, out=None) Evenly round to the given number of decimals.`

- `numpy.ceil上限`
- `numpy.floor下限`  向上向下取整

#### 杂项

- `numpy.clip裁剪`

`numpy.clip(a, a_min, a_max, out=None, **kwargs): Clip (limit) the values in an array.`

`y = np.clip(x, a_min=20, a_max=30)`

- `numpy.absolute 绝对值`
- `numpy.abs` 简写

- `numpy.sign 返回数字符号的逐元素指示 `  符号返回+1  -1

### 逻辑函数

#### 真值测试

- `numpy.all`
- `numpy.any`

#### 数组内容

- `numpy.isnan`

#### 逻辑运算

`numpy.logical_not`  计算非x元素的真值。

`numpy.logical_and ` 计算x1 AND x2元素的真值。

`numpy.logical_or`   逐元素计算x1 OR x2的真值。

`numpy.logical_xor`  计算x1 XOR x2的真值，按元素计算。

#### 对照

- `numpy.greater` >
- `numpy.greater_equal ` >=
- `numpy.equal `  ==
- `numpy.not_equal`  !=
- `numpy.less`  <
- `numpy.less_equal`  <=
- `numpy.isclose`   

```
numpy.isclose(a, b, rtol=1.e-5, atol=1.e-8, equal_nan=False) 
返回一个布尔数组，其中两个数组在公差范围内在元素方面相等。
numpy.allclose() 等价于 numpy.all(isclose(a, b, rtol=rtol, atol=atol, equal_nan=equal_nan)) 。
```



- `numpy.allclose`

```
numpy.allclose(a, b, rtol=1.e-5, atol=1.e-8, equal_nan=False) 
Returns True if two arrays are element-wise equal within a tolerance.
如果两个数组在公差范围内按元素方式相等，则返回True。
```



`公差值是正的，通常很小。将相对差（rtol * abs（b））和绝对差atol相加在一起，以与a和b之间的绝对差进行比较。`