# Python函数



## 1. 函数介绍

### 函数初体验

函数：是**组织好的，可重复使用的**，用来实现特定功能的**代码段**。

`len()`是一个Python内置的函数，用来判断字符串的长度，即：

```python
str = "Hello World"
print(len(str))
```

如果我们不用内置的`len()`函数，去完成字符串长度计算：

```python
str = "Hello World"
recode  = 0

for i in str:
  recode += 1
print(recode)
```

可见，函数对我们的开发效率起着至关重要的作用。



## 2. 函数的定义

```python
# 函数的定义
def 函数名(传入参数):
  函数体
  return 返回值

# 函数的调用
函数名(参数)
```

> #### **注意：**
>
> 1. 参数如不需要，可以省略（后续章节讲解） 
>
> 2. 返回值如不需要，可以省略（后续章节讲解）
>
> 3. 函数必须先定义后使用

### 案例

定义一个函数，函数名任意，要求调用函数后可以输出如下欢迎语：

请出示您的健康码以及72小时核酸证明！

```python
def Hello():
  print("请出示您的健康码以及72小时核酸证明！")

Hello()
```





## 3. 函数的参数

传入参数的功能是：在函数进行计算的时候，接受外部（调用时）提供的数据。

我们写写一个`1+2的函数`

```python
def add():
  result = 1 + 2
  print(f"1+2的结果为:{result}")
  
add()
```

函数的功能非常局限，只能计算1+2。

有没有可能实现：每一次使用函数，去计算用户指定的2个数字，而非每次都是1+2呢？

```python
def add(x, y):
  result = x + y
  print(f"{x}+{y}的结果为:{result}")

add(2, 5)
```

- 函数定义中，提供的x和y，称之为：形式参数（形参），表示函数声明将要使用2个参数 
  - **参数之间使用逗号进行分隔**

- 函数调用中，提供的5和6，称之为：实际参数（实参），表示函数执行时真正使用的参数值
  - **传入的时候，按照顺序传入数据，使用逗号分隔**

### 案例

定义一个函数，名称任意，并接受一个参数传入（数字类型，表示体温） 

在函数内进行体温判断（正常范围：小于等于37.5度），并输出如下内容：

```python
def temperature(x):
  if x <= 37.5:
    print("正常")
  else:
    print("异常")
    
temperature(int(input("Your temperature:")))
```



## 4. 函数的返回值

### 4.1 函数返回值的定义

##### 4.1.1 什么是返回值

所谓“返回值〞，就是程序中函数完成事情后，最后给调用者的结果。

###### 案例

```python
def add(x, y):
  result = x + y
  return result

num = add(1, 2)
```

#### 4.2 None类型

如果函数没有使用return语句返回数据，其实这个函数也有返回值。

Python中有一个特殊的字面量：None，其类型是：<class "NoneType“> 无返回值的函数，实际上就是返回了：None这个字面量

```python
def say_hello():
  print("Hello...")
	# return None
  
result = say_hello()
print(result) # None
print(type(result)) # NoneType
```

#### None类型的应用场景

None作为一个特殊的字面量，用于表示：空、无意义，其有非常多的应用场景。

- 用在函数无返回值上
- 用在 if 判断上

  - 在 if 判断中，None等同于False
  - 一般用于在函数中主动返回None，配合 if 判断做相关处理

  ```python
  def check_age(age):
    if age > 18:
      return "SUCCESS"
    else:
    	return None
  
  result = check_age(17)
  if not result:
    print("未成年，禁止进入")
  ```



> ## 函数的说明文档
>
> 函数是纯代码语言，想要理解其含义，就需要一行行的去阅读理解代码，效率比较低。
>
> 我们可以给函数添加说明文档，辅助理解函数的作用。
>
> 语法如下：
>
> ```python
> def func(x,y):
>   """
>   函数说明
>   :param x: 行参x的说明
>   :param y: 行参y的说明
>   :return: 返回值的说明
>   """
>   函数体
>   return 返回值
> ```
>
> 通过多行注释的形式，对函数进行说明解释。
>
> > **注意：**内容应写在函数体之前



## 5. 函数的嵌套调用

所谓函数嵌套调用指的是一个函数里面又调用了另外一个函数。

```python
def func_a():
  print("---2---")
  
def func_b():
	print("---1---")
  def func_a()
  print("---3---")
  
func_b()
```

如果函数A中，调用了另外一个函数B，那么先把函数B中的任务都执行完毕之后才会回到上次函数A热行解位。



## 6. 变量的作用域

变量作用域指的是变量的作用范围（变量在哪里可用，在哪里不可用） 

主要分为两类：局部变量、全局变量

- 局部变量：定义在函数体内部的变量，即只在函数体内部生效。

局部变量的作用：在函数体内部，临时保存数据，即当函数调用完成后，则销毁局部变量。

- 所谓全局变量，指的是在函数体内、外都能生效的变量。

### global关键字

使用 global关键字可以在函数内部声明变量为全局变量。

```python
num = 100

def func_a():
  global num
  num = 200
  print(num)
  
printf(num)
func_a()
```



## 综合案例——ATM案例

```python
name = input("姓名：")
money = 5000000
judge = 0

def query_balance():
    """
    查看余额函数
    :return: 余额
    """
    print("----------------查询余额----------------")
    print(f"{name}，你好，您的余额为{money}元")
    return money

def deposit_money(a):
    """
    存钱函数
    :param a: 存入钱款
    """
    print("------------------存款------------------")
    global money
    money += a
    print(f"{name}，您好，您存款{a}元成功")
    print(f"{name}，你好，您的余额为{money}元")
   
def without_money(b):
    """
    取钱函数
    :param b: 取出钱款
    """
    print("------------------取款------------------")
    global money
    money -= b
    print(f"{name}，您好，您取款{b}元成功")
    print(f"{name}，你好，您的余额为{money}元")
    
def main_menu():
    """
    主菜单函数
    """
    print("-----------------主菜单--------------------")
    print(f"{name}，你好，欢迎来到银行ATM，请选择操作:")
    print("查询余额\t[输入1]")
    print("存款\t\t[输入2]")
    print("取款\t\t[输入3]")
    print("退出\t\t[输入4]")
    global judge
    judge = int(input("请输入您的操作: "))


while True:
    main_menu()
    if judge == 1:
        query_balance()
    elif judge == 2:
        deposit_money(int(input("你想存入的额度为(元): ")))
    elif judge == 3:
        deposit_money(int(input("你想取出的额度为(元): ")))
    elif judge == 4:
        print("退出成功，祝您生活愉快")
        break 
    else:
        print("您的操作无效，请重新尝试。")
```

