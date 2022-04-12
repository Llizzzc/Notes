# Numpy 
>1. [Python数据分析](https://www.bilibili.com/video/BV1yi4y147A2?p=2 "numpy")
>2. [Numpy教程](https://www.runoob.com/numpy/numpy-tutorial.html "numpy")

## 一、生成数组 -- ndarray
+ 从已有列表生成
```python
list = [1, 2, 3]
arr = np.array(list)
```
+ 直接传入
`arr = np.array([1, 2, 3])`
+ 全0 or 1
`arr = np.zeros(4)`	// 默认float，4个数
`arr = np.ones(4, dtype='int')`	// dtype指定数据类型
+ fill方法
`arr.fill(1)`	// 以1个数覆盖原数组，转化为原数组类型数据
+ astype方法
`arr = arr.astype('int')`	// 转化数据类型
+ 生成整数序列
`arr = np.arange(1, 10)`	// 从1开始不包括10
`arr = np.arange(1, 10, 2)`	// 间距为2
+ 生成等差数列
`arr = np.linspace(1, 10, 10)`	// 从1到10，10个数
+ 生成随机数列
`arr = np.random.rand(10)`	// 从0到1，不包括1，10个数
`arr = np.random.randn(10)`	// 服从N(0 ,1)
`arr = np.random.randint(1, 10, 10)`	// 从1到10，不包括10，10个整数
## 二、数组属性
|类型|数组里面元素类型|形状|数组里面元素个数|维度|
|:-:|:-:|:-:|||
|`type(arr)`|`arr.dtype`|`arr.shape; np.shape(arr)`|`arr.size; np.size(arr)`|`arr.ndim`|
|||返回每一维元素个数|||
## 三、索引与切片
操作同List，*<span style="color:red">但是数组中切片为引用机制</span>*，例如：
```python
arr = np.array([1, 2, 3, 4, 5])
b = arr[1:4] => [2, 3, 4]
b[0] = 6 => [6, 3, 4]
arr => [1, 6, 3, 4, 5]
```
## 四、多维数组
操作同一维数组，每一维都支持切片语法
+ 索引
```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
arr[1][1]; a[1, 1]
```

