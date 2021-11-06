---
title: Python 笔记
tags: TeXt
toc:
  selectors: "h1,h2,h3,h4,h5"
image:
    
typora-root-url: ..
---





## python基础知识

​	

```python
for i in (3, 5, 7):
    print(i,end='a\t')
#    3a	5a	7a	

#chr与str函数
print(chr(65)) #return char  	A
print(str(65)) # return string  65
#A
#65

#list tuple dict set 将其他类型转换成列表，元组，字典，集合
print(tuple(range(5)))
print(dict(name='cx', age=22))
print(set('pythomm'))  # out of order

print(eval('[1, 2, 3]')) # change it into list
print(list('[1, 2, 3]'))  #a little different
                        #['[', '1', ',', ' ', '2', ',
                         # ', ' ', '3', ']']
```



#### enumerate

- enumerate(列表):枚举列表元素，返回枚举对象，其中**每个元素为包含下标和值的元组。**该函数对元组、字符串同样有效。

```python
for 循环使用 enumerate
>>>seq = ['one', 'two', 'three']
>>> for i, element in enumerate(seq):
...     print i, element
... 
0 one
1 two
2 three

以下展示了使用 enumerate() 方法的实例：

>>>seasons = ['Spring', 'Summer', 'Fall', 'Winter']
>>> list(enumerate(seasons))
[(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
>>> list(enumerate(seasons, start=1))       # 下标从 1 开始
[(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]


>>> for item in enumerate('abcdef'):
    print(item)

(0, 'a')
(1, 'b')
(2, 'c')
(3, 'd')
(4, 'e')
(5, 'f')


```



### type

type用来查看对象类型

![image-20211008193056162](/Python/image-20211008193056162.png){:.border}

**x+=6可以存在，但++不存在**

字符串和元组均是不可变序列，故无法通过下标来修改元素值



### 基于值的内存管理方式!

#### 什么叫基于值？

为不同的变量赋 **相同的值**时，内存中只会保存一份，多个变量指向同一个值的 **首地址**，

如果某个变量要修改呢？ 只需要改变这个变量的指向值

另：如果多个变量值位于[-5,256] **则共用同一个**，否则之外的值，**在同一个程序或交互模式下共用同一个值的内存空间**，**不同程序和交互不遵循**

**浮点数不遵循**[-5,256]：

![image-20211008194256232](/chenxin.github.io/Python/image-20211008194256232.png){:.border}





同一个语句下，大数也共用

![image-20211008194432056](/chenxin.github.io/Python/image-20211008194432056.png){:.border}

```python
x,z = 200.0, 200.0
print(id(x) == id(z)) //也遵循
```

**非同一语句下：**

![image-20211008194831749](/chenxin.github.io/Python1/image-20211008194831749.png){:.border}



**在交互模式下同值不同名不共用同一个内存空间**， 但是同一个程序下回 **共用**



![image-20211008195149383](/chenxin.github.io/Python/image-20211008195149383.png){:.border}



**数字**可以用 **_** 提高程序**可读性**,但没什么用



## 字符串

### r或R表示原始字符串

不对特殊字符进行转义，但字符串末尾不能有\

```python
ss = r'sss\' #前面这个r表示不转义
print('我是测试r原始字符 \\'+ss)

# ss = r'sss\' #前面这个r表示不转义
```



### // **求整商向下取整**



**x is y** 测试两个对象引用的地址是否一致

![image-20211008202558191](/Python/image-20211008202558191.png){:.border}

### is ，in 与 id的区别

in用来测试一个对象是否是另一个对象的元素

**单位是对象，不是[3]之类**



is**是用来测试两个对象是否相同**

![image-20211008204318330](/Python/image-20211008204318330.png){:.border}

两者单个类型一致

![image-20211008204351876](/Python/image-20211008204351876.png)





### -17%4=？

python中 余数与右侧的运算符号一致即与（-17%4） 中的==4==一致，均为正数

所以等于三，**而不是负一**

### 关系运算符的比较

比较列表的大小

![image-20211008203555563](/Python/image-20211008203555563.png){:.border}

![image-20211008203839847](/Python/image-20211008203839847.png){:.border}

### and or

具有惰性求值的特点，即

- 对于and，如果没有假值，返回的是最后一个真值，**如果有假值，则返回的是第一个假值。** ==惰性求值==
- 对于or	 如果没有真值，返回的是最后一个假值，**如果有真值，则返回的是第一个真值。**

### python不支持++，--

### 内置函数

详情见p17

ord 与chr

![image-20211008210743226](/Python/image-20211008210743226.png){:.border}

str 特点是加‘’

>>> str([1,2,3])
>>> '[1, 2, 3]'
>
>>> str((1,2,3))  
>
>>> '(1, 2, 3)'



```python
>>> eval('[1,2,3]')
[1, 2, 3]  //eval将字符串返回成列表
>>> list('[1,2,3]') //list将字符串里的每一个元素都转换成列表的值
['[', '1', ',', '2', ',', '3', ']']
>>> 
```



### map函数

- 内置函数map()可以将一个函数作用到一个或多个序列或迭代器对象上，返回可迭代的map对象。

```python
>>> print(x)
[1, 2, 1]
>>> list(map(str,x))  #map只关注x里面的元素，不处理[]
['1', '2', '1']  


>>> def add5(v):
    return v+5

>>> list(map(add5,range(10)))
[5, 6, 7, 8, 9, 10, 11, 12, 13, 14]

>>> def add(x, y):
    	return x+y
>>> list(map(add, range(5), range(5)))
[0, 2, 4, 6, 8]

```



### reduce函数

- 可以将一个接受**2个参数的函数**以迭代的方式从左到右依次作用到一个序列或迭代器对象的所有元素上。

```python
>>> from functools import reduce
>>> seq=[1,2,3,4,5,6,7,8,9]
>>> reduce(lambda x,y:x+y, seq)
45
>>> def add(x, y):
    return x + y
>>> reduce(add,range(10))
45
>>> reduce(add,map(str,range(10)))
map() -> '0', '1'....
#'01' 
'0123456789'

```



### sorted函数

***x.sort()函数***是 ==原地排序== 所以他不会返回一个新的列表等，**无法直接print(x.sort())**

sorted函数可以直接输出,因为他返回了一个新的对象？ ==yes,他返回了另一个==

```python
#sorted
x=list(range(11))
random.shuffle(x) #shuffle打乱数字
print(x)      #[5, 8, 7, 6, 10, 3, 1, 9, 4, 0, 2]
print(sorted(x)) #[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
# use  Key to sort
x=['sss', 'ss', 'zz', 'xxx', 'xxx222', '0']
print(sorted(x, key=lambda item: (len(item), item)))  #先按
# 长度排 长度一致在顺序排
print(x)  #sorted 和 print 分开不能work lambda是迭代器
x.sort()
print(x)
#['0', 'ss', 'zz', 'sss', 'xxx', 'xxx222']
#['sss', 'ss', 'zz', 'xxx', 'xxx222', '0']
#['0', 'ss', 'sss', 'xxx', 'xxx222', 'zz']

```



## 2--python序列

### 列表

列表是==有序连续内存空间==，由于存在==自动管理==，所以建议在列表尾部进行**增加**，**删改**。

### 增加

#### +

太慢了

**创建了一个新列表**，并将原列表中的元素和新元素依次复制到新列表的内存空间。由于涉及大量元素的复制，该操作速度较慢，**+**更多**的是用来拼接列表，而且执行效率并不高**

> \>>> aList = aList + [7]
>
> \>>> aList
>
> [3, 4, 5, 7]

#### extend

- 通过extend()方法来增加列表元素也不改变其内存首地址，属于**原地操作**。

> \>>> a.extend([7,8,9])
>
> \>>> a
>
> [5, 2, 4, 7, 8, 9]



- 运算符+=类似于列表的extend()方法。

> \>>> x = []
>
> \>>> x += '1234'
>
> \>>> x
>
> ['1', '2', '3', '4']
>
> \>>> x += range(3)
>
> \>>> x
>
> ['1', '2', '3', '4', 0, 1, 2]

#### insert

- 应**尽量从列表尾部进行元素的增加与删除操作**。
- 列表的insert()可以在列表的任意位置插入元素，但由于**列表的自动内存管理功能，**insert()方法会引起插入位置之后所有元素的移动，这会影响处理速度。
- 类似的还有后面介绍的remove()方法以及使用pop()函数弹出列表非尾部元素和使用del命令删除列表非尾部元素的情况。

#### 乘法 *

n当使用*运算符将包含列表的列表重复并创建新列表时，并不是复制子列表值，而是复制已有元素的引用。因此，当修改其中一个值时，相应的引用也会被修改。

> \>>> x = [[None] * 2] * 3
>
> \>>> x
>
> [[None, None], [None, None], [None, None]]
>
> \>>> x[0][0] = 5
>
> \>>> x
>
> [[5, None], [5, None], [5, None]]

### 删除

（1）使用del命令删除列表中的指定位置上的元素。

（2）使用列表的pop()方法删除并返回*指定位置*（默认为最后一个）上的元素，**如果给定的索引超出了列表的范围则抛出异常**。

（3）使用列表对象的remove()方法删除首次出现的指定元素，如果列表中不存在要删除的元素，则抛出异常。

### 切片操作

1. **切片****返回的是浅复制。****所谓浅复制，是指生成一个新的列表，并且把原列表中所****选****元素的引用都复制到新列表中。**如果原列表中只包含整数、实数、复数等基本类型或元组、字符串这样的不可变类型的数据，一般是没有问题的。



```python
>>> aList = [3, 5, 7]

\>>> bList = aList[::]         #切片，浅复制

\>>> aList == bList          #两个列表的元素完全一样

True

\>>> aList is bList          #但不是同一个对象

False

\>>> id(aList) == id(bList)      #内存地址不一样

False
```

- 如果原列表中包含**列表之类的可变数据类型**，由于浅复制时只是把子列表的引用复制到新列表中，**这样的话修改任何一个都会影响另外一个。**

### 排序

#### reversed

```python
aList = [3, 4, 5, 6, 7, 9, 11, 13, 15, 17]
newList = reversed(aList)         #返回reversed对象
# list(newList)                     #把reversed对象转换成列表
# [17, 15, 13, 11, 9, 7, 6, 5, 4, 3]
for i in newList:
    print(i, end=' ')  
               
print(list(newList))   
    #newlist只能用一次，不能重复用

	#17 15 13 11 9 7 6 5 4 3 []
```



### all()和any()：

测试是否为True，即大于“1”

### sum()

> sum([[1, 2], [3], [4]], [])  #这个操作占用空间较大，慎用
>
> [1, 2, 3, 4]

### zip函数

zip即“拉链,缝合”，生成==元组==

•用于将**可迭代的对象**作为参数，将对象中对应的元素打包成一个个**元组**，然后**返回由这些元组组成的列表**。

### 列表推导式





```python
list(map(list, zip(*matrix)))
#[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]

```





### 元组

1. 元组一旦创建，用任何方法都不可以修改其元素
2. 元组属于不可变序列，元素值不可变，但是如果存在==可变序列==，值就可以变。
3. §使用del可以删除元组对象，不能删除元组中的元素

### 创建

```python
>>> a = (3,)             #包含一个元素的元组，最后必须多写个逗号
(3,)


>>> tuple('abcdefg')                    #把字符串转换为元组
('a', 'b', 'c', 'd', 'e', 'f', 'g')

>>> s = tuple()                         #空元组
>>> s
()

```



### 元组与列表的区别

1. **元组的速度比列表更快**。如果定义了一系列常量值，而所需做的仅是对它进行遍历，那么一般使用元组而不用列表。
2. **元组对不需要改变的数据进行“写保护”**将使得代码更加安全。
3. **元组可用作字典的“键”**，也可以作为集合的元素。列表不能作为字典的“键”，包含列表、字典、集合或其他类型可变对象的元组也不能做字典的“键”。

### 对元组中可变序列进行修改的错误

```python
>>> x
([5, 2, 8], 3)
>>> x[0] = x[0]+[10]  相当于新列表
TypeError: 'tuple' object does not support item assignment
>>> x
([5, 2, 8], 3)
>>> x[0] += [10]   #相当于extend
TypeError: 'tuple' object does not support item assignment
>>> x
([5, 2, 8, 10], 3)

```

### 序列解包

•**序列****封包与序列解包**

•把多个值赋给一个变量时，Python会自动的把多个值封装成**元组**，称为序列封包。

•把一个**序列**（列表、元组、字符串等）直接赋给多个变量，此时会把序列中的各个元素依次赋值给每个变量，但是**元素的个数需要和变量个数相同，这称为序列解包**。

```python
>>> print(*[1, 2, 3], 4, *(5, 6))
1 2 3 4 5 6
>>> *range(4),4
(0, 1, 2, 3, 4)

>>> {'x': 1, **{'y': 2}} #注意顺序，先**，
{'y': 2, 'x': 1}

```

### 生成器推导式

1. 生成器推导式的结果是一个生成器对象。使用生成器对象的元素时，可以根据需要将其转化为列表或元组，也可以使用生成器对象’_---‘next’===_‘()方法或内置函数next()进行遍历，或者直接将其作为迭代器对象来使用。
2. 生成器对象具有惰性求值的特点，只在需要时生成新元素，空间占用非常少，尤其适合大数据处理的场合。
3. **不管用哪种方法访问生成器对象，都无法再次访问已访问过的元素**。



```python

#()叫生成器推导式 []叫列表推导式
>>> g = ((i+2)**2 for i in range(10))  #创建生成器对象
>>> g
<generator object <genexpr> at 0x0000000003095200>
>>> tuple(g)                          
(4, 9, 16, 25, 36, 49, 64, 81, 100, 121)
>>> list(g)             #生成器对象已遍历结束，没有元素了
[] 

#获取元素的两种方式
>>> g = ((i+2)**2 for i in range(10))  
>>> g.__next__()        #使用生成器对象的__next__()方法获取元素
4
>>> g.__next__()        #获取下一个元素
9
>>> next(g)             #使用函数next()获取生成器对象中的元素
16

```





### 字典

1. 字典是**无序**、**可变序列**。
2. 字典中的**键**可以为任意不可变数据，比如整数、实数、复数、字符串、**元组**等等。
3. globals()返回包含**当前作用域内所有全局变量和值**的字典
4. locals()返回包含**当前作用域内所有局部变量和值**的字典。



#### 创建

```python
>>> keys = ['a', 'b', 'c', 'd']
>>> values = [1, 2, 3, 4]
>>> dictionary = dict(zip(keys, values))
>>> dictionary
{'a': 1, 'b': 2, 'c': 3, 'd': 4}

#使用dict根据给定的键、值创建字典

>>> d = dict(name='Dong', age=37)
>>> d
{'name': 'Dong', 'age': 37}

#以给定内容为键，创建值为空的字典

>>> adict = dict.fromkeys(['name', 'age', 'sex'])
>>> adict
{'name': None, 'age': None, 'sex': None}


```



#### 读取



```python

>>> aDict = {'name':'Dong', 'sex':'male', 'age':37}
>>> aDict['name']
'Dong'

#使用字典对象的get()方法获取指定键对应的值，并且可以在键不存在的时候返回指定值。

>>> print(aDict.get('address'))
None
>>> print(aDict.get('address', 'SDIBT'))
SDIBT


print(aDict.items())
print(aDict.keys())
print(aDict.values())
#返回的都是列表,items单个元素是元组tuple
'''dict_items([('name', 'Dong'), ('sex', 'male'), ('age', 37)])
dict_keys(['name', 'sex', 'age'])
dict_values(['Dong', 'male', 37])'''

 #序列解包用法
>>> for key, value in aDict.items():      
    print(key, value)

age 37
name Dong
sex male


```













### 习题

```python
print(int('1'*64,2))
# ‘111111111111111111’ 的2进制，换成10进制
```



## 5--函数设计

### 循环break问题

> while 条件表达式:
>
> 循环体
>
> [else:           **# 如果循环是因为break结束的，就不执行else中的代码**
>
> else子句代码块]





### 形参与实参

在一般情况下如果定义函数内部的**形参值发生改变**， **不会改变实参的结果**

如果传入的形参是可变序列：

- 使用已**下标方式访问**，改变值，会使实参值改变
- 使用原地操作的方法增加序列

**删除和修改也**可以改变外面即实参的值

```python
def delete(list1):
    print('我进入删除函数了我的值时：'+str(list1))
    list1.pop()
    list1[0] = '我被修改了'
    print('我被改变了：'+str(list1))


L = [1, 2, 3, 4]
delete(L)
print('我的实参改变了吗'+str(L))
'''我进入删除函数了我的值时：[1, 2, 3, 4]
我被改变了：['我被修改了', 2, 3]
我的实参改变了吗['我被修改了', 2, 3]'''

#集合形参可以影响实参吗 可以！！！！！
def delete(set1):
    print('我进入删除函数了我的值时：'+str(set1))
    set1.pop()
    
    print('我被改变了：'+str(set1))


L = {1, 2, 3, 4}
delete(L)
print('我的实参改变了吗'+str(L))

'''-------------------
我进入删除函数了我的值时：{1, 2, 3, 4}
我被改变了：{2, 3, 4}
我的实参改变了吗{2, 3, 4}
'''
```

### 参数类型

#### 默认参数类型

#### 什么叫默认参数类型？

**默认类型参数只能位于右侧**



默认类型对于复杂类型如字典，列表等存在的问题

==默认值参数的赋值只会在函数定义时被解释一次。函数的默认值只在函数被加载时调用一次，之后若不传值则一直都会用加载函数时候设置的值，此值不会再改变==,如下：

```python
def demo(newitem, old_list=[]): 
    old_list.append(newitem)
    print("aaa"+str(old_list))
    return old_list


print(demo('4',[1,2,3]))
print(demo('aaaa',['a','b']))
print('-------------------')
print(demo('a'))
print(demo(1))

'''
[1, 2, 3, '4']       
['a', 'b', 'aaaa']   
-------------------  
['a']          如果每次调用该函数时，不为默认参数类型设值（传值，将会使默认类型值被改变，
				如[] 变成['a']
['a', 1]

'''


```



#### 关键字参数

**指使用形式参数的名字来确定输入的参数值**

即==demo(c=8,a=9,b=0)==   

**实参顺序可以和形参顺序不一致**

```python
>>> def demo(a,b,c=5):
    print(a,b,c)


>>> demo(a=7,b=3,c=6)
7 3 6

```



#### 可变成参数

可变长度参数主要有两种形式：在参数名前加**1个星号***或**2个星号**。

parameter用来接收**多个位置实参**并将其放在==元组==中。

parameter接收**多个关键参数**并存放到==字典==中。

```python

#*p的用法

def test1(*p):
    print(p)
test1(1,2,3,4)
#(1, 2, 3, 4)是个元组


def test2(**p):
    for item in p.items():
        print(item)

test2(a=2, y=6, z=1, b=3)
'''('a', 2)
('y', 6)
('z', 1)
('b', 3)'''

```



#### 参数类型混合使用

```python
def func_4(a, b, c=4, *aa, **bb):
    print(a,b,c)
    #1,2,3 我的错误在当形参是3的时候，c=4会被替换
    print(aa)
    (4, 5, 6, 7, 8, 9)
    print(bb)
    {'xx':'1','yy':'2','zz'=3}
	#错误在于未加{}，xx这种str要加''	
func_4(1,2,3,4,5,6,7,8,9,xx='1',yy='2',zz=3)

```



#### 参数传递的序列解包

即拿到里面的值

> dic = {1:'a', 2:'b', 3:'c'}
>
> \>>> demo(*dic)
>
> 6
>
> 
>
> \>>> Set = {1, 2, 3}
>
> \>>> demo(*Set)
>
> 6



如果函数**实参是字典**，可以在前面加**两个星号进行解包**，等价于**关键参数**

```python
dic = {‘a’:1, ‘b’:2, ‘c’:3}#
>>> demo(**dic)
6
>>> demo(a=1, b=2, c=3)
6
>>> demo(*dic.values())
6
```

\#**位置参数**和**序列解包**同时使用



下图很有趣，出错的原因在于**先解包**，所以b的形参以及获得了3，但实参还有一个b=1

导致一个b有多个值

![image-20211012225844995](/Python/image-20211012225844995.png)



### return语句

> return语句用来从一个函数中返回一个值，同时结束函数。
>
> 对于以下情况，Python将认为该函数以return None(空值返回)结束，返回空值：
>
> 1. 函数有return语句但是没有执行到；
> 2. **函数有return也执行到了，但是没有返回任何值。**
> 3. 函数没有return语句；
>
> 



### global关键字

- 如果一个变量在**函数外没有定义**，在函数内部也可以直接将一个变量定义为全局变量，该函数执行后，将增加一个新的全局变量。

- 一个变量**已在函数外定义**，如果在**函数内需要为这个变量赋值**，并要将这个赋值结果==反映到函数外==，可以在函数内使用**global将其声明为全局变量**。

  如：

```python
def demo():
    global x
    x = 3
    y = 4
    print(x,y)

x=5
demo() #3 4 x不等于5
#验证函数外没有定义时，调用global在函数内创建新的一个全局变量
del x
demo()
print(x)
```



•注意：在某个**作用域内**任意位置**只要有为变量赋值的操作**，该变量在**这个作用域内**就是**局部变量**，**除非使用global进行了声明。**

```python
>>> x = 3
>>> def f():
    print(x)           #本意是先输出全局变量x的值，但是不允许这样做
    x = 5              #有赋值操作，因此在整个作用域内x都是局部变量
    print(x)

```

- **globals()** 函数会以字典类型返回当前位置的全部全局变量。

```python
x=3
def f():
    print(globals()['x'])           #先输出全局变量x的值
    x = 5              #有赋值操作，因此在整个作用域内x都是局部变量
    print(x)

f()
```



### nonlocal关键字

没怎么看懂



### lambda表达式

```python
L = [(lambda x: x**2),                   #匿名函数
         (lambda x: x**3),
         (lambda x: x**4)]

print(L[0](2)) #等于给0号位置赋值2


L = [1,2,3,4,5]
>>> print(list(map(lambda x: x+10, L)))      #lambda表达式作为函数参数 
[11, 12, 13, 14, 15]
>>> L #L还是原来的值
[1, 2, 3, 4, 5] 
```



使用lambda表达式时，**要注意作用域带来的问题**

```python
>>> r = []
>>> for x in range(10):
    r.append(lambda: x**2)
	
>>> r[0]()
81
>>> r[1]()
81

>>> r = []
>>> for x in range(10):
    r.append(lambda n=x: n**2)

>>> r[0]()
0
>>> r[1]()
1
>>> r[2]()
4

```





### 修饰器

•修饰器（decorator，包装器）是函数嵌套定义的另一个重要应用。修饰器**本质上也是一个函数**，只不过这个函数==接收其他函数作为参数==并对**其进行一定的改造之后返回新函数**。(函数即对象)

•当你希望在**不修改函数本身的前提下扩展函数的功能**时非常有用,在函数执行之前或者之后修改该函数的行为，**而无需修改函数本身的代码。**

•Python面向对象程序设计中的静态方法、类方法、属性等也都是通过修饰器实现的，Python中还有很多这样的用法。



### 偏函数

如果现在需要一个类似的函数，与上面的函数add3()的区别仅在于参数b固定为一个数字（例如666），这时就可以使用偏函数的技术来复用上面的函数



```python
def add2(a, c):
    return add3(a, 666, c)


print(add2(1, 1))

def add3(a,b, c)
 return a+b+c

#或者使用标准库functools提供的partial()方法创建指定函数的偏函数。

from functools import partial
add2 = partial(add3, b=666)
print(add2(a=1, c=1))

```



### 第五章试题

397、已 知 f = lambda n: len(bin(n)[bin(n).rfind('1')+1:]) ， 那 么 表 达 式 f(6) 的 值 为__________________。（1）

398、已 知 f = lambda n: len(bin(n)[bin(n).rfind('1')+1:]) ， 那 么 表 达 式 f(7) 的 值 为__________________。（0）

print(*[1,2,3]) #1 2 3



## 面向对象程序设计

- 定义了类之后，可以用来实例化对象，并通过“对象名.成员”的方式来访问其中的数据成员或成员方法。

> car = Car()
>
> car.infor()

- nPython提供了一个关键字“pass”，表示空语句，可以用在类和函数的定义中或者选择结构中。当暂时没有确定如何实现功能，或者为以后的软件升级预留空间，或者其他类型功能时，可以使用该关键字来“占位”。

> class A:
>
> pass

### self函数

#### 什么叫实例方法？

```python
class Person(object):

    def __init__(self, name):
        self.__name = name

    def get_name(self):
        return self.__name
get_name(self) 就是一个实例方法，它的第一个参数是self。__init__(self, name)其实也可看做是一个特殊的实例方法。
```





- 类的所有实例方法都必须**至少有一个名为self的参数**，并且必须是**方法的第一个形参**（如果有多个形参的话），s**elf参数代表将来要创建的对象本身，表示的都是实际调用该方法的对象**。
- 在类的实例方法中**访问实例属性时**需要以self为前缀。
- 在外部通过对**象调用对象方法时并不需要传递self这个参数**，如果**在外部通过==类调用对象方法==则需要显式为self参数传值。**

### 类成员和实例成员

1. 类体中、所有函数之外：此范围定义的变量，称为**类属性或类变量**；
2. 类体中，所有函数内部：以“self.变量名”的方式定义的变量，称为**实例属性或实例变量**；
3. 类体中，所有函数内部：以“变量名=变量值”的方式定义的变量，称为**局部变量**。
4. 在实例方法中可以调用该实例的其他方法，也可以访问类属性以及实例属性
5. **在Python中，可以动态地为自定义类和对象增加或删除成员，**
6. 因为类属性为所有实例化对象共有，通过类名修改类属性的值，会影响所有的实例化对象。



只要使用列表自身的原地修改方法或者下标的形式，修改的都是同一个列表。



### 私有变量和成员变量

1. Python并没有对私有成员提供严格的访问保护机制。
   1. 在定义类的成员时，如果成员名以**两个下划线“__”或更多下划线开头**而**不以两个或更多下划线结束**则表示是**私有成员**。
   2. 私有成员在**类的外部不能直接访问**，需要通过**调用对象的公开成员方法来访问**，也可以通过Python**支持的特殊方式来访问。**
2. 公开成员既可以在类的内部进行访问，也可以在外部程序中使用。

3. n在Python中，以下划线开头的变量名和方法名有特殊的含义，尤其是在类的定义中。
   1. _xxx：受保护成员，不能用'from module import *'导入；
   2. ‘     __xxx——  ’：系统定义的特殊成员；
   3. ____xxx：私有成员，只有类对象自己能访问，子类对象不能直接访问到这个成员，但在对象外部可以通过“==对象名._类名xxx==”这样的特殊方式来访问。

注意：Python中不存在严格意义上的私有成员。

n在IDLE交互模式下，一个下划线“_”表示解释器中最后一次显示的内容或最后一次语句正确执行的输出结果。

```
在程序中，可以使用一个下划线来表示不关心该变量的值。

>>> for _ in range(5):
    print(3, end=' ')
	
3 3 3 3 3 

a, _ = divmod(60, 18)          #只关心整商，不关心余数，
                                   #等价于a = 60//18
>>> a
3

```





### 方法

在类中定义的方法可以粗略分为四大类：**公有方法**、**私有方法**、**静态方法和类方法**。

1. 私有方法的名字以==两个下划线“__”开始==，每个对象都有自己的公有方法和私有方法，在这两类方法中可以访问属于类和对象的成员；
2. 公有方法通过对象名直接调用，==私有方法不能通过对象名直接调用==，只能在属于==对象的方法中通过self调用==或在外部通过Python支持的特殊方式来调用。
3. 如果通过类名来调用属于对象的公有方法，**需要显式为该方法的self参数传递一个对象名**，用来明确指定访问哪个对象的数据成员。
4. **采用 @classmethod 修饰的方法为类方法；采用 @staticmethod 修饰的方法为静态方法；不用任何修改的方法为实例方法。**
5. 静态方法和类方法都可以**通过类名和对象名调用**，但**不能直接访问属于对象的成员**，**只能访问属于类的成员。**
6. **静态方法可以没有参数**。
7. Python 类方法和实例方法相似，**它最少也要包含一个参数**，只不过类方法中通常将其命名为 cls，Python 会**自动将类本身绑定给 cls 参数**（注意，绑定的不是类对象）。也就是说，我们在调用类方法时，无需显式为 cls 参数传参。

```python
class Root:
    __total = 0
    def __init__(self, v):    #构造方法，实际也是实例方法
        self.__value = v
        Root.__total += 1

    def show(self):           #普通实例方法
        print('self.__value:', self.__value)
        print('Root.__total:', Root.__total)

    @classmethod              #修饰器，声明类方法
    def classShowTotal(cls):  #类方法
        print(cls.__total)

    @staticmethod             #修饰器，声明静态方法静态方法没有类似 self、cls 这样的特殊参数，因此 Python 解释器不会对它包含的参数做任何类或对象的绑定。也正因为如此，类的静态方法中无法直接调用任何类属性和类方法。
    def staticShowTotal():    #静态方法
        print(Root.__total)



rr = Root(5)
Root.classShowTotal()           #类方法推荐使用类名直接调用，当然也可以使用实例对象来调用（不推荐）

Root.staticShowTotal()          #通过类名调用静态方法



r = Root(3)
r.classShowTotal()            #通过对象来调用类方法

print(r.staticShowTotal())             #通过对象来调用静态方法

# Root.show()  #  #试图通过类名直接调用实例方法，失败
Root.show(rr)   #但是可以通过这种方法来调用方法并访问实例成员
#r指的是前面的实例对象？
```

#### 什么是私有方法

```python
class Student:
    def __init__(self,name):
        self.__name = name

    def __printMessage(self):
        print(self.__name)



stu = Student("陈鑫")

stu._Student__printMessage()

```



### 属性

可读可写属性

```python
可读、可写属性：属性名=property(fget=None, fset=None, fdel=None, doc=None)； fget 参数用于指定获取该属性值的类方法，fset 参数用于指定设置该属性值的方法，fdel 参数用于指定删除该属性值的方法，最后的 doc 是一个文档字符串，用于说明此函数的作用。
>>> class Test:
	    def __init__(self, value):
	        self.__value = value	

	    def __get(self):
        return self.__value

	    def __set(self, v):
        self.__value = v

	    value = property(__get, __set)

	    def show(self):
        print(self.__value)

```



### 内置方法

#### OOP题库

> 定义类时实现了__eq__()方法，该类对象即可支持运算符==。（对）
>
> 
>
> 定义类时实现了__pow__()方法，该类对象即可支持运算符**。（对）
>
> 只可以动态为对象增加数据成员，而不能为对象动态增加成员方法。（错）
>
> 任何包含__call__()方法的类的对象都是可调用的。（对）
>
> 函数和对象方法是一样的，内部实现和外部调用都没有任何区别。（错）
>
> 如果在设计一个类时实现类__len__()方法，那么该类的对象会自动支持 Python 内置函数 len()。（对）
>
> isinstance('4', (int, float, complex)) 的值为_____________。（False）
>
> str???? 是的它是str
>
> 如果在设计一个类时实现了__contains__ ()方法，那么该类的对象会自动支持  _ _in_  _  运算符。（in）
>
> 



## 文件操作

- 文件中数据的组织形式把文件分为**文本文件**和**二进制文件两类。**
  - **文本文件：** 常规字符串以文本，一换行符'\n'结束
  - **二进制文件** 把对象内容**以字符串（bytes）**进行存储



### 文件基本操作

- 文件内容操作三步走：打开、读写、关闭。

1. 文件的应用级操作可以分为以下 3 步，每一步都需要借助对应的函数实现：打开文件：**使用 open() 函数，**该函数会**返回一个文件对象**；
2. 对已打开文件做读/写操作：读取文件内容可使用 **read()、readline() 以及 readlines() 函数；向文件中写入内容，可以使用 write() 函数。**
3. 关闭文件：完成对文件的读/写操作之后，**最后需要关闭文件，可以使用 close() 函数。**

> open(file（**R**, mode='r', buffering=-1, encoding=None, errors=None,newline=None, closefd=True, opener=None)
>
> 2.mode 即打开模式  有a追加， b二进制（可组合， +读写（可组合
>
> buffering参数指定了读写文件的**缓存模式**。0表示不缓存，1表示缓存，如大于1则表示缓冲区的大小。默认值-1表示由系统管理缓存
>
> **encoding参数**指定对文本进行编码和解码的方式，**只适用于文本模式**，可以使用Python支持的任何格式，如GBK、utf8、CP936等等

### 文件打开方式

![image-20211024211800557](/Python/image-20211024211800557.png)



![image-20211024212402399](/Python/image-20211024212402399.png)



![image-20211024212528862](/Python/image-20211024212528862.png)





### 二进制文件

- 所谓序列化，简单地说就是把内存中的数据在不丢失其类型信息的情况下转成对象的二进制形式的过程（**程序的各种类型数据对象 变成 表示该数据对象的 二进制形式**这个过程 称之为 **序列化**）
- 对象序列化后的形式经过**正确的反序列化**过程应该能够准确无误地恢复为原来的对象。
- Python中常用的序列化模块有struct、pickle、marshal和shelve。



#### 使用pickle模块

•[Python](http://c.biancheng.net/python/) 中有个序列化过程叫作 pickle，它能够实现任意对象与文本之间的相互转化，也可以实现任意对象与二进制之间的相互转化。也就是说，pickle 可以实现 Python 对象的存储及恢复。

•pickle 模块提供了以下 4 个函数供我们使用：

- dumps()：将 Python 中的对象序列化成二进制对象，**并返回**；
- loads()：读取给定的二进制对象数据，并**将其转换为 Python 对象**；
- dump()：将 Python 中的对象序列化成二进制对象，**并写入文件**；
- load()：读取指定的序列化数据文件，并**返回对象**。



 以上这 4 个函数可以分成两类，其中 dumps 和 loads 实现基于内存的 Python 对象与二进制互转；dump 和 load 实现基于文件的 Python 对象与二进制互转。

```python
import pickle

i = 13000000
a = 99.056
s = '中国人民123abc'
lst = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
tu = (-5, 10, 8)
coll = {4, 5, 6}
dic = {'a':'apple', 'b':'banana', 'g':'grape', 'o':'orange'}
data = [i, a, s, lst, tu, coll, dic]

with open('sample_pickle.dat', 'wb') as f:
    try:
         pickle.dump(len(data), f) #表示后面将要写入的数据个数
         for item in data:
              pickle.dump(item, f)
    except:
        print('写文件异常!')        
        
例7-9  读取二进制文件。

import pickle

with open('sample_pickle.dat', 'rb') as f:
    n = pickle.load(f)        #读出文件的数据个数
    for i in range(n):
        x = pickle.load(f)
        print(x)

```



#### 文件操作题库



> **文件操作**
>
> 
>
> 对文件进行写入操作之后，_______________方法用来在不关闭文件对象的情况下将缓冲区内容写入文件。（flush()）
>
> Python 内置函数_____________用来打开或创建文件并返回文件对象。（open()）
>
> 使用上下文管理关键字______________可以自动管理文件对象，不论何种原因结束该关键字中的语句块，都能保证文件被正确关闭。（with）
>
> 424、Python 标 准 库 os 中 用 来 列 出 指 定 文 件 夹 中 的 文 件 和 子 文 件 夹 列 表 的 方 式 是__________。listdir()）
>
> Python 标准库 os.path 中用来判断指定文件是否存在的方法是______________。exists()）
>
> 426、Python 标准库 os.path 中用来判断指定路径是否为文件的方法是_______________。（isfile()）
>
> 427、Python 标 准 库 os.path 中 用 来 判 断 指 定 路 径 是 否 为 文 件 夹 的 方 法 是____________。（isdir()）
>
> 428、Python 标准库 os.path 中用来分割指定路径中的文件扩展名的方法是____global______。（splitext()）
>
> 429、Python 扩 展 库 ____openpyxl_________ 支 持 Excel 2007 或 更 高 版 本 文 件 的 读 写 操 作 （openpyxl）
>
> Python 标准库_______hashlib_____中提供了计算 MD5 摘要的方法 md5()。（hashlib）
>
> 已知当前文件夹中有纯英文文本文件 readme.txt，请填空完成功能把 readme.txt 文件 中 的 所 有 内 容 复 制 到 dst.txt 中 ， with open('readme.txt') as src, open('dst.txt',
>
> ____’w’________) as dst:dst.write(src.read())。（'w'）
