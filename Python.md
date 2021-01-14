Syntax Error：语法错误
Indentation Error：错误缩进

#### 数

对于很大的数，Python允许在数字中间以_分隔，因此，`10_000_000_000`和`10000000000`是完全一样的。十六进制数也可以写成`0xa1b2_c3d4`。

#### 转义字符

`\`可以转义很多字符，比如`\n`表示换行，`\t`表示制表符
但是如果就想输出`\n`，除了常见的多加一个`\`，还可以使用`r' '`表示` ' ' `内部的字符串默认不转义

```python
print('\\n')  #输出 \n
print(r'\n')  #输出 \n
```

用\n写在一行里不好阅读，为了简化，Python允许用'''...'''的格式表示多行内容

```python
print('''aaa
bbb
ccc''')

输出
aaa
bbb
ccc
```

#### 变量
在Python中，同一个变量可以反复赋值，而且可以是不同类型的变量。

#### 除法
在Python中，有两种除法，一种除法是`/`：
``` Python
>>> 10 / 3
3.3333333333333335

# 除法计算结果是浮点数，即使是两个整数恰好整除，结果也是浮点数：
>>> 9 / 3
3.0
```
还有一种除法是`//`，称为**地板除**，两个整数的除法仍然是整数：
```python
>>> 10 // 3
3
```

#### 编码

Python对bytes类型的数据用带b前缀的单引号或双引号表示：`x = b'ABC'`。要注意区分`'ABC' `和` b'ABC' `，前者是str，后者虽然内容显示得和前者一样，但bytes的每个字符都只占用一个字节。
```python
>>> 'ABC'.encode('ascii')
b'ABC'

>>> b'ABC'.decode('ascii')
'ABC'
```
<br>
由于Python源代码也是一个文本文件，所以，当你的源代码中包含中文的时候，在保存源代码时，就需要务必指定保存为UTF-8编码。当Python解释器读取源代码时，为了让它按UTF-8编码读取，我们通常在文件开头写上这两行：
```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```
第一行注释是为了告诉Linux/OS X系统，这是一个Python可执行程序，Windows系统会忽略这个注释；
第二行注释是为了告诉Python解释器，按照UTF-8编码读取源代码，否则，你在源代码中写的中文输出可能会有乱码。

#### 格式化
##### %
在Python中，采用的格式化方式和C语言是一致的，用`%`实现，举例如下：
``` Python
>>> 'Hello, %s' % 'world'  # 如果只有一个`%`，括号可以省略。
'Hello, world'
>>> 'Hi, %s, you have $%d.' % ('Michael', 1000000)
'Hi, Michael, you have $1000000.'
>>> print(' your grade increases %d%% ' %20) #如果要把 % 转义，则使用 %% ，而不是 \%
your grade increases 20%
```
常见的占位符有：
| 占位符 | 替换内容     |
| ------ | ------------ |
| %d     | 整数         |
| %f     | 浮点数       |
| %s     | 字符串       |
| %x     | 十六进制整数 |

##### format()
另一种格式化字符串的方法是使用字符串的format()方法，它会用传入的参数依次替换字符串内的占位符{0}、{1}……，不过这种方式写起来比%要麻烦得多：
```Python
>>> 'Hello, {0}, 成绩提升了 {1:.1f}%'.format('小明', 17.125)  #第二个大括号里面是  1然后一个冒号 类似数组下标
'Hello, 小明, 成绩提升了 17.1%'
```

##### f-string
它和普通字符串不同之处在于，字符串如果包含{xxx}，就会以对应的变量替换：
```Python
>>> r = 2.5
>>> s = 3.14 * r ** 2
>>> print(f'The area of a circle with radius {r} is {s:.2f}')
The area of a circle with radius 2.5 is 19.62
```

####  列表
##### list
-1、-2...可以表示倒数第1、2...个数据
```python
>>> classmates = ['Michael', 'Bob', 'Tracy']
>>> classmates[-1]
'Tracy'
```
list里面的元素的数据类型也可以不同
list元素也可以是另一个list
##### tuple
和`list`一样，只不过`tuple`是写死的
```python
>>> t = (1, 2)
>>> t
(1, 2)
```
但是注意，只有1个元素的`tuple`需要这样定义：
```python
>>> t = (1,)
>>> t
(1,)
```
如果不加那个逗号，则会被识别为一个数字，而不是一个`tuple`
Python在显示只有1个元素的tuple时，也会加一个逗号,，以免被误解成数学计算意义上的括号。

#### 判断

`elif `是`else if`缩写

```python
if <条件判断1>:
    <执行1>
elif <条件判断2>:
    <执行2>
elif <条件判断3>:
    <执行3>
else:
    <执行4>
```

#### [dict （Map）、Set](https://www.liaoxuefeng.com/wiki/1016959663602400/1017104324028448)

![](https://i.loli.net/2020/12/09/JA7gwNOCrHzlmMb.png)

#### 不可变对象

![](https://i.loli.net/2020/12/09/X4R7EPMzkx5K2Bu.png)

#### 函数

##### 定义函数

``` python
def my_abs(x):
    if x >= 0:
        return x
    else:
        return -x
```

##### 空函数

如果想定义一个什么事也不做的空函数，可以用`pass`语句：

```python
def nop():
    pass
```

`pass`语句什么都不做，那有什么用？实际上`pass`可以用来作为占位符，比如现在还没想好怎么写函数的代码，就可以先放一个`pass`，让代码能运行起来。

##### [参数检查](https://www.liaoxuefeng.com/wiki/1016959663602400/1017106984190464)

```python
def my_abs(x):
    if not isinstance(x, (int, float)):
        raise TypeError('bad operand type')
    if x >= 0:
        return x
    else:
        return -x
```

添加了参数检查后，如果传入错误的参数类型，函数就可以抛出一个错误：

```python
>>> my_abs('A')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 3, in my_abs
TypeError: bad operand type
```

##### 返回多个值

函数可以返回多个值吗？答案是肯定的。

比如在游戏中经常需要从一个点移动到另一个点，给出坐标、位移和角度，就可以计算出新的坐标：

```python
import math

def move(x, y, step, angle=0):
    nx = x + step * math.cos(angle)
    ny = y - step * math.sin(angle)
    return nx, ny
```

`import math`语句表示导入`math`包，并允许后续代码引用`math`包里的`sin`、`cos`等函数。

然后，我们就可以同时获得返回值：

```python
>>> x, y = move(100, 100, 60, math.pi / 6)
>>> print(x, y)
151.96152422706632 70.0
```

但其实这只是一种假象，Python函数返回的仍然是单一值：

```python
>>> r = move(100, 100, 60, math.pi / 6)
>>> print(r)
(151.96152422706632, 70.0)
```

原来返回值是一个tuple！但是，在语法上，返回一个tuple可以省略括号，而多个变量可以同时接收一个tuple，按位置赋给对应的值，所以，Python的函数返回多值其实就是返回一个tuple，但写起来更方便。

##### 默认参数

举个例子，我们写个一年级小学生注册的函数，我们可以把年龄和城市设为默认参数：

```python
def enroll(name, gender, age=6, city='Beijing'):
    print('name:', name)
    print('gender:', gender)
    print('age:', age)
    print('city:', city)
```

默认参数可以按顺序缺省：`enroll('Bob', 'M', 7)`；也可以不按顺序，当不按顺序提供部分默认参数时，需要把参数名写上。比如调用`enroll('Adam', 'M', city='Tianjin')`

⚠️：[默认参数在定义的时候，内存空间就有了对应的默认参数的值用于缺省的时候调用使用，因此**默认参数必须指向不变对象**](https://www.liaoxuefeng.com/wiki/1016959663602400/1017261630425888)

##### [可变参数](https://www.liaoxuefeng.com/wiki/1016959663602400/1017261630425888)

不论是函数的定义还是调用，在数组前面加`*`表示将数组拆开，传入里面的数据（不好总结，直接看文章）

##### 关键字参数

`**`表示将 Map 传入作为参数

```python
def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
```

函数`person`除了必选参数`name`和`age`外，还接受关键字参数`kw`。在调用该函数时，可以只传入必选参数：

```python
>>> person('Michael', 30)
name: Michael age: 30 other: {}
```

也可以传入任意个数的关键字参数：

```python
>>> person('Bob', 35, city='Beijing')
name: Bob age: 35 other: {'city': 'Beijing'}
>>> person('Adam', 45, gender='M', job='Engineer')
name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}
```

关键字参数有什么用？它可以**扩展函数的功能**。比如，在`person`函数里，我们保证能接收到`name`和`age`这两个参数，但是，如果调用者愿意提供更多的参数，我们也能收到。试想你正在做一个用户注册的功能，除了用户名和年龄是必填项外，其他都是可选项，利用关键字参数来定义这个函数就能满足注册的需求。

和可变参数类似，也可以先组装出一个dict，然后，把该dict转换为关键字参数传进去：

```python
>>> extra = {'city': 'Beijing', 'job': 'Engineer'}
>>> person('Jack', 24, **extra)
name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}
```

`**extra`表示把`extra`这个dict的所有key-value用关键字参数传入到函数的`**kw`参数，`kw`将获得一个dict，注意`kw`获得的dict是`extra`的一份**拷贝**，对`kw`的改动不会影响到函数外的`extra`。

> ```python
> dct1 = {'kw1': 0, 'kw2': 2}
> dct2 = {'n': 3, 'kw3': 5, 'kw4': 6}
> 
> def func_8(a, b, c, /, m, n, *, kw1, kw2, kw3, **kwargs):
>     pass
> 
> func_8(1, 2, 3, 4, **dct1, **dct2)
> ```
>
> 则形成了
>
> ```python
> a = 1
> b = 2
> c = 3
> m = 4
> n = dct2['n']
> kw1 = dct1['kw1']
> kw2 = dct1['kw2']
> kw3 = dct2['kw3']
> kwargs = {'kw4': dct2['kw4']}
> ```
>
> 注意，调用`func_8`的时候，想像成把`**dct1`、`**dct2`键值对拆碎了放进去，所以里面的输出`n`时，因为被拆开的一堆键值对里面有`n : 3`，所以输出的是`3`；别想像成顺序放，把`n`弄成了`dct1['kw1']`

##### 递归函数

尾递归调用时，如果做了优化，栈就不会增长，因此，无论多少次调用也不会导致栈溢出。

```python
function story() {
  从前有座山，山上有座庙，庙里有个老和尚，一天老和尚对小和尚讲故事：story() 
  // 尾递归，进入下一个函数不再需要上一个函数的环境了，得出结果以后直接返回。
}
```

```python
function story() {
  从前有座山，山上有座庙，庙里有个老和尚，一天老和尚对小和尚讲故事：story()，小和尚听了，找了块豆腐撞死了 
  // 非尾递归，下一个函数结束以后此函数还有后续，所以必须保存本身的环境以供处理返回值。
}
```



#### 高级特性

