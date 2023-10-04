# Coding Concept 编程导论

程序员常说代码逻辑(Logic)、算法(Algorithm)，这两概念其实是一回事，都是解决数学问题的数理逻辑。所有代码都是这种逻辑的实现(Implementation)。无论使用何种类型的编程语言，变化的是语法，不变的是算法。本文基于语法简洁的Python语言和伪代码进行论述。

本文仅论述算法，为保障通俗性，<strong>概念定义非常不严谨，有不少自创概念，故请不要去严格死记定义和分类等，理解概念即可。</strong>

## 1. Some Concepts 一些概念

开始之前，我们需要先知道一些概念和数据结构。

### 1.1 Function 函数

函数是编程中的最重要和基础概念。有些人会觉得这个概念非常的抽象和难以理解。可以从这几方面去理解。

- 从数学上理解函数，是Y=f(x,y,z,...)，也即有多个变量的输入，得到某一个变量的输出。x和Y可以是数字，也可以是向量(list/vector)。
- 从生活上理解函数，这就是一个黑盒子，像快餐店的Drive Thru一样。外面的人看不到里面，但是所有人都知道只要你按照规则在标定的位置提交order和pay，那么等你到给定output的位置等待时，就可以拿到你想要的物品。而这个黑盒子里面也完全不在意外界，他只知道每次有新的信息提交进来，那么他就按照给定的行动指南处理，最后在output的位置把东西给出去。
- 在代码中，函数的形式就是F(x1,x2,...)，其中F是函数的名称，而x1,x2等是函数接收的参数，函数若是有有返回，则在调用时使用Y=F(...)，使用变量Y接收函数的结果。函数内部与外界完全隔绝，只专注于对传入数据进行处理，使用return T将完成的最终结果T交给外部。

### 1.2 Class&OOP 类与面向对象

类(Class)是面向对象(OOP,Object-Orientation Programming)的产物。类这个概念，来源于“归类”一词，也即将一群具有相同特征的物质进行抽象化，得到一个可以概括这群物质的模板，依据这个模板可以找到更多同类的物质，这个模板就叫做类。

类是一个抽象概念，可以用来指代所有具有相同特征的实例。而这个特征可以是任意特征。比如我们常说A和B是一类人，可能是同时具有某种性格，也可能是来自于同一个地方，或是同一个种族之类的。类与类有<strong>继承(Inherit)</strong>关系。存在父类(Parent)、邻类(Sibling)、衍生类(Derived)等关系。

举个例子，我们假设A和B都是外向的人，那么他们对应的类就可以叫做“外向人”类，而A和B自己则叫做“外向人”类的<strong>实例(Instance)</strong>。与此同时，若是他们同时又都来自于东亚，那么他们又同属于类“东亚人”。那么会有人问，为什么不直接弄一个叫做“外向的东亚人”的类呢？当然可以，而且他们同时属于这三个类。由于“外向的东亚人”类的前提条件是拥有“外向人”的全部特征，因此我们又可以说“外向的东亚人”类继承于“外向人”类，其中“外向人”是父类，而“外向的东亚人”是子类/衍生类。“东亚人”类同理。

### 1.3 常见的数据结构

数据结构大多对应着实际生活中的问题，或是解决的工具。

1. 列表List：又叫向量，连续且有序。超市的储物柜就是典型列表，有编号，并且编号连续，可以在常数时间内找到任何编号的格子。
2. 链表Linked List：有序但不连续，只能按顺序查找，没有序号，打开一个看了内容才知道下一个在哪。
3. 队列Queue：先进先出(FIFO), 和排队一样，先到先得。
4. 栈Stack：后进先出(LIFO)，和箱子一样，东西只能放在最上面，拿也只能从最顶上开始拿。
5. 哈希表Hashmap：Python里叫做字典Dict。类似于列表，但编号不局限于纯数字，而是可以使用任意类型但唯一的Key。查找效率和列表相当。（至于为什么叫Hashmap，是因为他内部有一个Hash哈希函数将任意类型的key值转换为一个编号数字，然后在内部用编号直接获取value）

## 2. About Algorithm 关于算法

代码世界中算法很多种，本文自作主张称之为入门算法、基础算法及高阶算法。

### 2.1 入门算法

算法有很多，但算法入门逻辑并不多。大多数的算法都有基础算法组合或延申而来。就如同数学中无论多么复杂的计算，最终都离不开最基本的+/-/x/÷四则运算，这是人类可以大脑可以进行的运算。而算法中的入门逻辑也同样来源于电脑CPU可以进行的运算类型。

算法中可用的运算类型有几种：

- 四则运算如+/-/x/÷/mod(取余)
- 逻辑运算如 and/or/not/xor(异或, 不同为真)
- (类似于乘除2的倍数，了解即可) 左移/右移

基于这些运算类型入门级的算法有求最值、求平均、求和、乘方以及其他数学表达式，我们从解决数学问题的角度详细讲其中几个算法，以便更好地理解算法和编程的本质。

#### 2.1.1 求最值

我们先来看这样一个数学题目。在钢材厂有一大堆钢材，每一块钢板上面都贴了一张带参数的标签。由于生产质量不稳定，钢板重量不一。厂长心血来潮想要看看这批材料中最轻的产品质量，请使用算法找出结果。

对于这个题目，大家都会说，“那直接把钢材全翻一遍，然后不就知道最小了吗”。没错，但是这个说法只能叫做题目的解法思路，是一个指导逻辑，也就是常说的“先这样，在那样，就出来了”。而题目的算法(Algorithm)是什么？算法是更加具体的过程。我们需要切实的把自己带入那个寻找的过程，一步一步的进行。

比如这道题的算法，我们首先查看第一个钢板的重量，然后把这个数字记在脑中，接着开始一个重复的过程，也即查看一个钢板的重量，如果大于之前所记住的那个值，则记住这个新的值，否则忽略这个钢板，就当作没看过。对每一个钢板都这么干，最后把脑子里最终记住的那个数值拿出来作为结果。这个详细的就是题目的算法。

这个算法也可以写成伪代码:
```pseudocode
# 假设有N块钢板, 我们创建一个处理过程(也就是大家说的函数)
function find_min:
    remember_num = above_plate's weight   # 先记住面上这块钢板的值，记为remember_num。名称是为了防止把记住的东西弄混，需要用的时候能够知道把谁拿出来用。
    for i from 1->N:    # 假设当前查找第i个板，i从1开始一直到N结束
        if plate_i's weight<remember_num:  # 如果当前板的重量小于记忆中的最小值
            remember_num = plate_i's weight     # 更新记忆
        end if
    end for   # 循环结束
    return remember_num    # 结束处理过程，把得到的结果交出去，任务结束。
```

而伪代码转换成Python之前需要提一下遍历的概念。钢板存放是有顺序的，按顺序查找永远比胡乱找快。就算你像计算机一样可以记住所有查找过的钢板编号，你也需要在不同的位置跑来跑去并回想确认这里是否查找过。乱序查找永远是没有效率的。<strong>对于所有有顺序的数据结构，比如列表之类，从头到尾按顺序将所有内容进行查看的过程叫做遍历(Iterate/Iteration)</strong>。我们查看钢材中所有钢板的过程叫做遍历钢材。

基于伪代码，我们可以写出对应的Python代码
```python
def find_min(plates: List[Plate]):
    remember_num = plates[0].weight
    for plate in plates:           # Python可以使用in关键字直接遍历，而不需要用下标i进行位置指代
        if (plate.weight < remember_num):
            remember_num = plate.weight
    return remember_num
```

#### 2.1.2 乘方

有些朋友会觉得“乘方还不简单？几次方就是乘几次”，那我们来看看这个循环嵌套循环的问题。 写一个程序，仅使用+/-计算a的b次方。

看到仅使用+-，有些人就懵了。乘方不是乘法的问题吗？对，但是乘法同时也是由加减而来。这道题就可以在数学上被分解为先解决a*b，再解决a^b。这样的话逻辑就很清晰了。

我们先写一个计算a*b的算法伪代码：
```pseudocode
function multiply(a, b):
    value = 0     # 加法从0开始累计，什么都不加的时候是0
    for i from 1->b:
        value += a    # 每次加a，一共b次
    end for
    return value      # value作为结果提交出去
```

现在有了乘法，再做乘方：
```pseudocode
function power(a, b):
    value = 1     # 乘方从1开始乘，什么都不乘的0次方是1
    for i from 1->b:
        value = multiply(value,a)    # 每次进行value乘a，然后将结果赋值给新的value，一共进行b次。
    end for
    return value
```
上面的逻辑考虑到multiply函数内循环次数的问题，由于value往往远大于a，故使用multiply(value,a)而非multiply(a,value)进行计算，可以减少计算的次数。比如2x50的逻辑，2*50=0+2+2+2+...(50个2)，而50*2=0+50+50。你肯定更愿意算后一个，计算机也是。

以上的两个计算逻辑可以写在一起，<strong>把使用乘法函数的地方更换成乘法函数的函数体。这个过程叫做内联</strong>。内联后仅剩下一个函数，增加执行连贯性，少量提升效率。可以和上文的定义进行比较，观察内联变化。算法具体如下：

```pseudocode
function power(a, b):
    value = 1
    for i=1->b：
        ### 以下过程是value = multiply(value, a)的内联
        multi_value = 0        # 使用不同于先前的名称以区分
        for i from 1->a:          # 一共有a个value待乘
            multi_value += value    # 每次加value，一共b次
        end for
        value = multi_value    # 将新的乘法结果赋给value，一次乘法完成。
    end for
    return value
```


对应Python代码:
```python
def power(a, b):
    value = 1
    for i in range(b):
        # 乘法过程：
        multi_val = 0
        for i in range(a):
            multi_val += value
        value = multi_val
    return val
```

熟练后可以做到在编写代码时做到一步直接内联。

### 2.2 Basic Algorithm 基础算法

#### 2.2.1 Time Complexity 时间复杂度

为了衡量代码执行效率，我们有时间复杂度的概念。常用O表示。

按照输入参数的长度N，计算函数的时间复杂度。

常见复杂度：
- O(1), 执行时间与参数长度无关。 Constant Time
- O(log(n)), 对数复杂度 Logarithmic Time
- O(n), 线性复杂度 Linear Time
- O(n^p), polynomial time complexity
- O(2^n), power time complexity‘

具体计算理解请跟随后面的算法。

#### 2.2.1 Sort 排序算法

##### 2.2.1.1 冒泡排序

给定一个列表进行从小到大排序，最简单的排序算法莫过于将列表里所有的元素进行两两对比，若是位于前面的元素大于位于后面的元素，则将这两元素进行调换。这样的算法叫做<strong>冒泡排序（Bubble Sort）</strong>。

时间复杂度分析：对于冒泡排序，一个长度为N的列表，进行这样的排序则需要将每一个元素都和其他N-1个元素进行比较，总的比较次数为N(N-1)/2, 也即当N较大时，忽略低次项，执行所花费的时间近似和N^2线性相关，时间复杂度在O(N^2)等级。也就是说随着列表长度N的增长，排序时间以N^2的速度增长。

##### 2.2.1.2 快速排序

那么是否有速度更加快速的排序方式？答案是有。目前主流的排序方式，除去桶排序，最快的排序方式复杂度为O(n*log(n)).
本文介绍常用的算法<strong>快速排序(Quick Sort)</strong>. 该算法的时间复杂度为O(nlogn).

#### 2.2.2 Recursion 递归

### 2.3 Excercise 一些练习

以下题目可以使用伪代码完成（没有固定语法，逻辑对即可）。答案在Answer.md中。

1. 对于1.1.1 如果要求的并不是最值，而是均值，他的算法逻辑应该是怎么样的？ 他的Python代码是什么样的？(可选)


## 3 Python语言

### 3.1 基本语法

Python语言是OOP面向对象的狂热支持者，完全以面向对象的思路进行设计。在Python中万物皆对象。

Python的语法和逻辑表达相比而言最贴近自然语言。其大多数的关键字也是从英语而来。

#### 3.1.1 Function 函数

一个典型的带注释和提示的函数F(x)定义和调用如下：
```python
# x: list是x的类型提示， ->int 是函数返回类型提示。 类型提示只是一个参考，不会被执行。
# F 可以换成任何喜欢的名字
def F(x: list) -> int:
    """Calculate the Average of list x, return the average."""
    # 上面这一行字符串注释是函数的功能介绍
    _sum = 0
    for i in x:
        _sum += i
    return _sum/len(x)

# 函数调用：
_list_a = [1,2,3,4,5]
Y = F(_list_a)  # val = 2.5
```

可以看到函数定义是非常典型的F(x)->Y的形式。 def是define的缩写。函数也是对象，是一个可以调用(Callable)的函数类的实例。而在Python中所有对象是平等的，可以放入大多数的数据结构，也可以作为参数传递。因此偶尔有些喜欢整活的程序员会搞出很多花活， 比如这个把函数存在变量里的操作：

```python
def add(a, b):
    return a+b

def add1(a):
    return a+1

# 一个接受函数对象作为参数的函数
def run(func, a, b):
    val = func(a, b)   # 使用正确的参数Call function, 只有函数可以被Call
    return val

function = add             # 将函数对象赋值给function，此时function和add相等。add是一个变量，function也是一个变量，但同时他俩也有函数用法。
val = function(1,2)        # val = 3
val = run(function, 1, 2)  # val = 3  正确，根据run的定义，传入的func需接受两个参数
val = run(add1, 1, 2)      # Error位于run的定义：func(a, b)。 传入的add1接受一个参数，却塞给他两个。  解决办法：传入一个接受两个参数的函数
val = run(add, 1, 2)       # val = add(1,2) = 3

```

在Python中，函数还有另外一种形式，即匿名函数。与实名函数截然不同的是，匿名函数没有函数名称，往往在使用的时候才进行定义。在Python中，使用lambda 关键字进行匿名函数定义：

```python
#正常函数
def add(a, b):
    return a+b

func = add  # 赋值
func(1,2) == add(1,2)   # True: 3==3

#匿名函数
func = lambda x,y: (x+y)   # 定义时没有函数名称，若不使用其他变量储存，那就是一次性的，定义完就没了。
func(1,2)  # 函数调用 return 3
```

可以看到，匿名函数的定义由两部分组成， 前半部分`lambda x, y :`对应正常函数的`def F(x, y)`，冒号后的部分`(...)`对应`return (...)`。括号可以省略。 我们可以看到，因为匿名函数最初是用来处理临时简短函数的，因此其函数体很短，由冒号开始，只能够写单个语句一步求值返回。

其最常见的用法是在数据处理中，有很多接受函数作为参数来处理数据的方法， 由于数据处理中这类函数用的特别多，但往往每个又只用一次，因此lambda显得十分重要。一个常见的例子是在Series和DataFrame中处理数据：

```python
# 假设我们需要处理一个数据表中的单个feature
df = DataFrame([[...], [...], ...])
sr = df[colume1]  # 取一个sr = Series([1,2,3,4,5,6,7,8,9,10,11,...])
#此时我们如果需要把这组数据 按照标准正态进行Normalization，怎么操作？
#首先使用Series的方法取mean和dev
mean = sr.mean()
std = sr.std()
# 随后便是用武之地，对每个值都进行 (x-mean)/std
# 你会希望有一个函数，能够自动对每一个值进行你所标定的处理。
# 刚好Series这里就有一个叫做apply的函数，这个函数接受一个函数作为参数，然后将每个值都使用函数处理
normalized = sr.apply(lambda x: (x-mean)/std)
# 在这里，这个匿名函数接受一个参数x，然后进行normalized操作
# Series里每个数值都会依次放进函数，得到返回值，放进新的normalized Series， 最后得到一个新的处理后的Series

#倘若不使用匿名函数，则应当如此写：
def norm(x):
    return (x-mean)/std
normalized = sr.apply(norm)
# 这二种写法这是等价的。且鼓励使用第一种写法。因为没有必要把这个只用一次的函数放在这里。难看又占地方，还把norm变量名占掉了，怎么看怎么亏。
```

#### 3.1.2 Class&Instance 类与实例

类的定义也很简单。比如我想创建一堆学生，那么我就需要先定义学生的特征。然后再使用这个模板去创建学生。典型代码如下:

```python
# 创建一个学生类
class Student:
    # 这些是学生的attribute，每个学生都有这些东西
    name: str
    age: int
    gender: bool/int/str # bool是二元的，string是self-describe的, int是枚举的, 选一个用。
    level: int
    school: str
    GPA_scale: int
    GPA: float
    ...

    # 构造函数，在创建新的对象时会被自动调用。构造函数永远没有返回值
    # 每一次函数调用都会隐式的 将实例本身作为第一个参数传入
    # 因此函数首位需要有一个self变量。self的名字是约定俗成，不建议换。
    # self用来访问对应实例的attribute。
    def __init__(self, name: str, age: int, gender) -> None:
        # self 关键字
        self.name = name
        self.age = age
        self.gender = gender
        # default for rest
        self.level = 1
        self.school = "Unknown"
        ...
        #所有attribute必须初始化

    # 成员函数，这个类的每一个实例都有这些方法
    def make_angry(self) -> None:
        print("你瞅啥？")

    def introduce(self) -> None:
        print(f"我叫{self.name}，今年{self.age}岁")

#创建实例
a1 = Student("小明", 18, gender="non binary") #参数与__init__函数一致，gender=...的语法是指定参数，用于改变参数顺序，此处若删去并无任何不同。
a2 = Student("小红", 19, "female")
# 调用函数 （详见代码后解析
a1.introduce()  # 我叫小明，今年18岁
a2.introduce()  # 我叫小红，今年19岁
Student.introduce(a1)  # 我叫小明，今年18岁
#访问和修改attribute
tmp = a1.age    # tmp = 18
a1.age += 20
a1.introduce()  # 我叫小明，今年38岁
```

成员函数的self可能有些不好理解。要记住这点，类class只是一个模板，每一个它的实例都有自己的attribute，但是成员方法是所有实例所共享的。为了访问某一个特定的实例的attribute，需要将该实例传入函数，并在函数中访问传入实例对应的attribute， 而这个参数就叫self。

而在调用函数时，若是直接对实例调用，则Python会自动使用实例填补self参数，就如同上面所写`a1.introduce()`，a1已经被自动填补给了self参数。而若是使用类名直接调用，则如同`Student.introduce(a1)`，由于没有可自动填补的实例，就必须手动填入a1。

而类的继承则很好理解。即在拥有父类所有attribute和函数的基础上，定义独属于子类的东西。比如我目前要定义一个高中生，那么只需要继承与学生，然后定义高中生特有的内容。

```python

# 定义的括号内是继承关系，括号内填写父类。Python所有类定义均有继承关系
# 不写括号默认继承于Object类，Object是Python中物质的本源，所有东西哪怕是数字和字符串等也是由Object继承而来，拥有Object的类型方法。
class HighSchoolStudent(Student):
    class_type: bool   # 文/理
    rank: int          # 联考排名
    province: str      # 高考所属生源地

    def __init__(self, name, age, class_type):
        self.name = name
        self.age = age
        self.class_type = class_type
        self.rank = -1
        self.province = "Unknown"

# 构造
a1 = HighSchoolStudent("小刚", 16, 0)
a2 = HighSchoolStudent("小红", 15, 0)

# 调用继承而来的函数
a1.introduce()   # 我叫小刚，今年16岁
a1.rank = 1000   # OK， 将排名设置到1000
rank = a1.rank   # rank = 1000
rank = a2.rank   # rank = -1

```

### 3.2 Pandas简单介绍


