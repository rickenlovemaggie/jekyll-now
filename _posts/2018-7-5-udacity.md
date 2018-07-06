---
layout: post
title: Udacity 人工智能基础
---

# Udacity 人工智能编程基础

## 第一章 Python 入门

### Class 2  数据类型和运算符


#### list

##### join 方法
```
name = "-".join(["García", "O'Kelly"])
```
##### append 方法
```
letters = ['a', 'b', 'c', 'd']
letters.append('z')
```

#### tuple

```
dimensions = (52, 40, 100)
dimensions = 52, 40, 100
length, width, height = dimensions
print("The dimensions are {} x {} x {}".format(length, width, height))
```

#### set

```
numbers = [1, 2, 6, 3, 1, 1, 6]
unique_nums = set(numbers)
print(unique_nums)
```

```
fruit = {"apple", "banana", "orange", "grapefruit"}  # define a set

print("watermelon" in fruit)  # check for element

fruit.add("watermelon")  # add an element
print(fruit)

print(fruit.pop())  # remove a random element
print(fruit)
```

#### map

```
elements = {"hydrogen": 1, "helium": 2, "carbon": 6}
```

### Class 3 控制流

#### if

#### for

```
# iterable of cities
cities = ['new york city', 'mountain view', 'chicago', 'los angeles']

# for loop that iterates over the cities list
for city in cities:
    print(city.title())
    
for index in range(len(cities)):
    cities[index] = cities[index].title()    
```

#### while

#### zip 和 enumerate

```
letters = ['a', 'b', 'c']
nums = [1, 2, 3]

for letter, num in zip(letters, nums):
    print("{}: {}".format(letter, num))
```

```
some_list = [('a', 1), ('b', 2), ('c', 3)]
letters, nums = zip(*some_list)
```

```
letters = ['a', 'b', 'c', 'd', 'e']
for i, letter in enumerate(letters):
    print(i, letter)
    
result:
0 a
1 b
2 c
3 d
4 e    
```

#### 列表生成式

```
capitalized_cities = []
for city in cities:
    capitalized_cities.append(city.title())
```
可以简写为：

```
capitalized_cities = [city.title() for city in cities]
```
你还可以向列表推导式添加条件语句。在可迭代对象之后，你可以使用关键字 if 检查每次迭代中的条件。

```
squares = [x**2 for x in range(9) if x % 2 == 0]
```
上述代码将 squares 设为等于列表 [0, 4, 16, 36, 64]，因为仅在 x 为偶数时才评估 x 的 2 次幂。如果你想添加 else，将遇到语法错误。

```
squares = [x**2 for x in range(9) if x % 2 == 0 else x + 3]
```
如果你要添加 else，则需要将条件语句移到列表推导式的开头，直接放在表达式后面，如下所示。

```
squares = [x**2 if x % 2 == 0 else x + 3 for x in range(9)]
```

### Class 4 函数

#### 作用域

```
egg_count = 0

def buy_eggs():
    egg_count += 12 # purchase a dozen eggs

buy_eggs()
```

Python 不允许函数修改不在函数作用域内的变量，所以上述代码报错，可以修改为：

```
egg_count = 0

def buy_eggs(count):
    return count + 12  # purchase a dozen eggs

egg_count = buy_eggs(egg_count)
```

但是列表、字典、集合、类中可以在子程序中（子函数）通过修改局部变量达到修改全局变量的目的。


#### 文档

文档使代码更容易理解和使用。函数尤其容易理解，因为它们通常使用文档字符串，简称 docstrings。文档字符串是一种注释，用于解释函数的作用以及使用方式。下面是一个包含文档字符串的人口密度函数。

```
def population_density(population, land_area):
    """Calculate the population density of an area. """
    return population / land_area
```

文档字符串用三个引号引起来，第一行简要解释了函数的作用。如果你觉得信息已经足够了，可以在文档字符串中只提供这么多的信息；一行文档字符串完全可接受，如上述示例所示。

```
def population_density(population, land_area):
    """Calculate the population density of an area.

    INPUT:
    population: int. The population of that area
    land_area: int or float. This function is unit-agnostic, if you pass in values in terms
    of square km or square miles the function will return a density in those units.

    OUTPUT: 
    population_density: population / land_area. The population density of a particular area.
    """
    return population / land_area
```

如果你觉得需要更长的句子来解释函数，可以在一行摘要后面添加更多信息。在上述示例中，可以看出我们对函数的参数进行了解释，描述了每个参数的作用和类型。我们经常还会对函数输出进行说明。

文档字符串的每个部分都是可选的。但是，提供文档字符串是一个良好的编程习惯。你可以在此处详细了解文档字符串惯例。

#### Lambda 表达式

你可以使用 Lambda 表达式创建匿名函数，即没有名称的函数。lambda 表达式非常适合快速创建在代码中以后不会用到的函数。尤其对高阶函数或将其他函数作为参数的函数来说，非常实用。

我们可以使用 lambda 表达式将以下函数

```
def multiply(x, y):
    return x * y
```

简写为：

```
double = lambda x, y: x * y
```

Lambda 函数的组成部分
关键字 lambda 表示这是一个 lambda 表达式。
lambda 之后是该匿名函数的一个或多个参数（用英文逗号分隔），然后是一个英文冒号 :。和函数相似，lambda 表达式中的参数名称是随意的。
最后一部分是被评估并在该函数中返回的表达式，和你可能会在函数中看到的 return 语句很像。
鉴于这种结构，lambda 表达式不太适合复杂的函数，但是非常适合简短的函数。


#### map 函数

```
numbers = [
              [34, 63, 88, 71, 29],
              [90, 78, 51, 27, 45],
              [63, 37, 85, 46, 22],
              [51, 22, 34, 11, 18]
           ]

def mean(num_list):
    return sum(num_list) / len(num_list)

averages = list(map(mean, numbers))
print(averages)
```

#### filter 函数

```
cities = ["New York City", "Los Angeles", "Chicago", "Mountain View", "Denver", "Boston"]

def is_short(name):
    return len(name) < 10

short_cities = list(filter(is_short, cities))
print(short_cities)
```

#### 迭代器和生成器

迭代器是每次可以返回一个对象元素的对象，例如返回一个列表。我们到目前为止使用的很多内置函数（例如 enumerate）都会返回一个迭代器。

迭代器是一种表示数据流的对象。这与列表不同，列表是可迭代对象，但不是迭代器，因为它不是数据流。

生成器是使用函数创建迭代器的简单方式。也可以使用类定义迭代器，更多详情请参阅此处。

下面是一个叫做 my_range 的生成器函数，它会生成一个从 0 到 (x - 1) 的数字流。

```
def my_range(x):
    i = 0
    while i < x:
        yield i
        i += 1
```

注意，该函数使用了 yield 而不是关键字 return。这样使函数能够一次返回一个值，并且每次被调用时都从停下的位置继续。关键字 yield 是将生成器与普通函数区分开来的依据。

注意，因为这段代码会返回一个迭代器，因此我们可以将其转换为列表或用 for 循环遍历它，以查看其内容。例如，下面的代码：

```
for x in my_range(5):
    print(x)
输出：

0
1
2
3
4
```

### Class 5 脚本编写

#### 输入

我们可以使用内置函数 input 获取用户的原始输入，该函数接受一个可选字符串参数，用于指定在要求用户输入时向用户显示的消息。

```
name = input("Enter your name: ")
print("Hello there, {}!".format(name.title()))
```

这段代码提示用户输入姓名，然后在问候语中使用该输入。input 函数获取用户输入的任何内容并将其存储为字符串。如果你想将输入解析为字符串之外的其他类型，例如整数（如以下示例所示），需要用新的类型封装结果并从字符串转换为该类型。

```
num = int(input("Enter an integer"))
print("hello" * num)
```

我们还可以使用内置函数 eval 将用户输入解析为 Python 表达式。该函数会将字符串评估为一行 Python 代码。

```
result = eval(input("Enter an expression: "))
print(result)
```

如果用户输入 2 * 3，输出为 6。


#### 异常

我们实际上可以指定要在 except 块中处理哪个错误，如下所示：

```
try:
    # some code
except ValueError:
    # some code
```

现在它会捕获 ValueError 异常，但是不会捕获其他异常。如果我们希望该处理程序处理多种异常，我们可以在 except 后面添加异常元组。

```
try:
    # some code
except (ValueError, KeyboardInterrupt):
    # some code
```

或者，如果我们希望根据异常执行不同的代码块，可以添加多个 except 块。

```
try:
    # some code
except ValueError:
    # some code
except KeyboardInterrupt:
    # some code
```

```
def create_groups(items, num_groups):
    try:
        size = len(items) // num_groups
    except ZeroDivisionError as e:
    	 print("ZeroDivisionError occurred: {}".format(e))
        print("WARNING: Returning empty list. Please use a nonzero number.")
        return []
    else:
        groups = []
        for i in range(0, len(items), size):
            groups.append(items[i:i + size])
        return groups
    finally:
        print("{} groups returned.".format(num_groups))

print("Creating 6 groups...")
for group in create_groups(range(32), 6):
    print(list(group))

print("\nCreating 0 groups...")
for group in create_groups(range(32), 0):
    print(list(group))
```

#### 读写文件

##### 读取文件

```
f = open('my_path/my_file.txt', 'r')
file_data = f.read()
f.close()
```

首先使用内置函数 open 打开文件。需要文件路径字符串。open 函数会返回文件对象，它是一个 Python 对象，Python 通过该对象与文件本身交互。在此示例中，我们将此对象赋值给变量 f。
你可以在 open 函数中指定可选参数。参数之一是打开文件时采用的模式。在此示例中，我们使用 r，即只读模式。这实际上是模式参数的默认值。
使用 read 访问文件对象的内容。该 read 方法会接受文件中包含的文本并放入字符串中。在此示例中，我们将该方法返回的字符串赋值给变量 file_data。
当我们处理完文件后，使用 close 方法释放该文件占用的系统资源。

##### 写入文件

```
f = open('my_path/my_file.txt', 'w')
f.write("Hello there!")
f.close()
```

以写入 ('w') 模式打开文件。如果文件不存在，Python 将为你创建一个文件。如果以写入模式打开现有文件，该文件中之前包含的所有内容将被删除。如果你打算向现有文件添加内容，但是不删除其中的内容，可以使用附加 ('a') 模式，而不是写入模式。
使用 write 方法向文件中添加文本。
操作完毕后，关闭文件。


##### With

Python 提供了一个特殊的语法，该语法会在你使用完文件后自动关闭该文件。

```
with open('my_path/my_file.txt', 'r') as f:
    file_data = f.read()
```

该 with 关键字使你能够打开文件，对文件执行操作，并在缩进代码（在此示例中是读取文件）执行之后自动关闭文件。现在，我们不需要调用 f.close() 了！你只能在此缩进块中访问文件对象 f。

##### readline 和 for line in f 语法

使用 readline() 方法可以读取文件的一行，但是 python 支持更简单的写法：

```
camelot_lines = []
with open("camelot.txt") as f:
    for line in f:
        camelot_lines.append(line.strip())

print(camelot_lines)
```

#### 导入脚本

##### import 本地同目录脚本

如果你要导入的 Python 脚本与当前脚本位于同一个目录下，只需输入 import，然后是文件名，无需扩展名 .py。

```
import useful_functions
```

Import 语句写在 Python 脚本的顶部，每个导入语句各占一行。该 import 语句会创建一个模块对象，叫做 useful_functions。模块是包含定义和语句的 Python 文件。要访问导入模块中的对象，需要使用点记法。

```
import useful_functions
useful_functions.add_five([1, 2, 3, 4])
```

我们可以为导入模块添加别名，以使用不同的名称引用它。

```
import useful_functions as uf
uf.add_five([1, 2, 3, 4])
```

##### 从模块中导入函数或者类

```
from module_name import object_name1, object_name2
```

这样可以直接使用，而不再需要点记法来引用：

```
from random import randint

randint(0, 10)
```

##### 使用 if main 块
为了避免运行从其他脚本中作为模块导入的脚本中的可执行语句，将这些行包含在 if __name__ == "__main__" 块中。或者，将它们包含在函数 main() 中并在 if main 块中调用该函数。

每当我们运行此类脚本时，Python 实际上会为所有模块设置一个特殊的内置变量 __name__。当我们运行脚本时，Python 会将此模块识别为主程序，并将此模块的 __name__ 变量设为字符串 "__main__"。对于该脚本中导入的任何模块，这个内置 __name__ 变量会设为该模块的名称。因此，条件 if __name__ == "__main__"会检查该模块是否为主程序。


#### Python 标准库

[Python 标准库](https://docs.python.org/3/library/index.html)

##### 常用的模块

Python 标准库包含大量模块！为了帮助你熟悉那些实用的模块，我们在下面筛选了一些我们推荐的 Python 标准库模块并解释为何我们喜欢使用它们！

- csv：对于读取 csv 文件来说非常便利
- collections：常见数据类型的实用扩展，包括 OrderedDict、defaultdict 和 namedtuple
- random：生成假随机数字，随机打乱序列并选择随机项
- string：关于字符串的更多函数。此模块还包括实用的字母集合，例如 string.digits（包含所有字符都是有效数字的字符串）。
- re：通过正则表达式在字符串中进行模式匹配
- math：一些标准数学函数
- os：与操作系统交互
- os.path：os 的子模块，用于操纵路径名称
- sys：直接使用 Python 解释器
- json：适用于读写 json 文件（面向网络开发）

#### Python 第三方库


独立开发者编写了成千上万的第三方库！你可以使用 pip 安装这些库。pip 是在 Python 3 中包含的软件包管理器，它是标准 Python 软件包管理器，但并不是唯一的管理器。另一个热门的管理器是 Anaconda，该管理器专门针对数据科学。

要使用 pip 安装软件包，在命令行中输入“pip install”，然后是软件包名称，如下所示：pip install package_name。该命令会下载并安装该软件包，以便导入你的程序中。安装完毕后，你可以使用从标准库中导入模块时用到的相同语法导入第三方软件包。

##### 使用 requirements.txt 文件
大型 Python 程序可能依赖于十几个第三方软件包。为了更轻松地分享这些程序，程序员经常会在叫做 requirements.txt 的文件中列出项目的依赖项。下面是一个 requirements.txt 文件示例。

```
beautifulsoup4==4.5.1
bs4==0.0.1
pytz==2016.7
requests==2.11.1
```

该文件的每行包含软件包名称和版本号。版本号是可选项，但是通常都会包含。不同版本的库之间可能变化不大，可能截然不同，因此有必要使用程序作者在写程序时用到的库版本。

你可以使用 pip 一次性安装项目的所有依赖项，方法是在命令行中输入 `pip install -r requirements.txt`。


##### 实用的第三方软件包

能够安装并导入第三方库很有用，但是要成为优秀的程序员，还需要知道有哪些库可以使用。大家通常通过在线推荐或同事介绍了解实用的新库。如果你是一名 Python 编程新手，可能没有很多同事，因此为了帮助你了解入门信息，下面是优达学城工程师很喜欢使用的软件包列表。（可能部分网站在国内网络中无法打开）

- IPython - 更好的交互式 Python 解释器
- requests - 提供易于使用的方法来发出网络请求。适用于访问网络 API。
- Flask - 一个小型框架，用于构建网络应用和 API。
- Django - 一个功能更丰富的网络应用构建框架。Django 尤其适合设计复杂、内容丰富的网络应用。
- Beautiful Soup - 用于解析 HTML 并从中提取信息。适合网页数据抽取。
- pytest - 扩展了 Python 的内置断言，并且是最具单元性的模块。
- PyYAML - 用于读写 YAML 文件。
- NumPy - 用于使用 Python 进行科学计算的最基本软件包。它包含一个强大的 N 维数组对象和实用的线性代数功能等。
- pandas - 包含高性能、数据结构和数据分析工具的库。尤其是，pandas 提供 dataframe！
- matplotlib - 二维绘制库，会生成达到发布标准的高品质图片，并且采用各种硬拷贝格式和交互式环境。
- ggplot - 另一种二维绘制库，基于 R's ggplot2 库。
- Pillow - Python 图片库可以向你的 Python 解释器添加图片处理功能。
- pyglet - 专门面向游戏开发的跨平台应用框架。
- Pygame - 用于编写游戏的一系列 Python 模块。
- pytz - Python 的世界时区定义。


#### Python 在线资源

虽然有很多关于编程的在线资源，但是并非所有资源都是同等水平的。下面的资源列表按照大致的可靠性顺序排序。

- [Python 教程](https://docs.python.org/3/tutorial/) - 这部分官方文档给出了 Python 的语法和标准库。它会举例讲解，并且采用的语言比主要文档的要浅显易懂。确保阅读该文档的 Python 3 版本！
- [Python 语言和库参考资料](https://docs.python.org/3/index.html) - 语言参考资料和库参考资料比教程更具技术性，但肯定是可靠的信息来源。当你越来越熟悉 Python 时，应该更频繁地使用这些资源。
- 第三方库文档 - 第三方库会在自己的网站上发布文档，通常发布于 https://readthedocs.org/ 。你可以根据文档质量判断第三方库的质量。如果开发者没有时间编写好的文档，很可能也没时间完善库。
- 非常专业的网站和博客 - 前面的资源都是主要资源，他们是编写相应代码的同一作者编写的文档。主要资源是最可靠的资源。次要资源也是非常宝贵的资源。次要资源比较麻烦的是需要判断资源的可信度。Doug Hellmann 等作者和 Eli Bendersky 等开发者的网站很棒。不出名作者的博客可能很棒，也可能很糟糕。
- StackOverflow - 这个问答网站有很多用户访问，因此很有可能有人之前提过相关的问题，并且有人回答了！但是，答案是大家自愿提供的，质量参差不齐。在将解决方案应用到你的程序中之前，始终先理解解决方案。如果答案只有一行，没有解释，则值得怀疑。你可以在此网站上查找关于你的问题的更多信息，或发现替代性搜索字词。
- Bug 跟踪器 - 有时候，你可能会遇到非常罕见的问题或者非常新的问题，没有人在 StackOverflow 上提过。例如，你可能会在 GitHub 上的 bug 报告中找到关于你的错误的信息。这些 bug 报告很有用，但是你可能需要自己开展一些工程方面的研究，才能解决问题。
- 随机网络论坛 - 有时候，搜索结果可能会生成一些自 2004 年左右就不再活跃的论坛。如果这些资源是唯一解决你的问题的资源，那么你应该重新思考下寻找解决方案的方式。

### Class 6 Anaconda

#### Anaconda 是什么

Anaconda 实际上是一个软件发行版，它附带了 conda、Python 和 150 多个科学包及其依赖项。应用程序 conda 是包和环境管理器。Anaconda 的下载文件比较大（约 500 MB），因为它附带了 Python 中最常用的数据科学包。如果只需要某些包，或者需要节省带宽或存储空间，也可以使用 Miniconda 这个较小的发行版（仅包含 conda 和 Python）。但你仍可以使用 conda 来安装任何可用的包，它只是自身没有附带这些包而已。

包管理器用于在计算机上安装库和其他软件。你可能已经熟悉 pip，它是 Python 库的默认包管理器。conda 与 pip 相似，不同之处是可用的包以数据科学包为主，而 pip 适合一般用途。与此同时，conda 并非 像 pip 那样专门适用于 Python，它也可以安装非 Python 的包。它是支持 任何 软件的包管理器。也就是说，虽然并非所有的 Python 库都能通过 Anaconda 发行版和 conda 获得，但同时它也支持非 Python 库的获得。在使用 conda 的同时，你仍可以使用 pip 来安装包。

除了管理包之外，conda 还是虚拟环境管理器。它类似于另外两个很流行的环境管理器，即 virtualenv 和 pyenv。

环境能让你分隔用于不同项目的包。你常常要使用依赖于某个库的不同版本的代码。例如，你的代码可能使用了 Numpy 中的新功能，或者使用了已删除的旧功能。实际上，不可能同时安装两个 Numpy 版本。你要做的应该是，为每个 Numpy 版本创建一个环境，然后项目的对应环境中工作。

在应对 Python 2 和 Python 3 时，此问题也会常常发生。你可能会使用在 Python 3 中不能运行的旧代码，以及在 Python 2 中不能运行的新代码。同时安装两个版本可能会造成许多混乱和错误，而创建独立的环境会好很多。

你也可以将环境中的包列表导出为文件，然后将该文件与代码包括在一起。这能让其他人轻松加载代码的所有依赖项。pip 提供了类似的功能，即 pip freeze > requirements.txt。

#### 管理包

```
conda install numpy scipy pandas  # 安装包
conda remove numpy  # 卸载包
conda update numpy  # 更新包
conda update --all  # 更新环境中所有的包
conda list  # 列出所有安装的包
conda search beautifulsoup  # 搜索包
```

#### 管理环境

##### 创建环境

如前所述，你可以使用 conda 创建环境以隔离项目。要创建环境，请在终端中使用

```
conda create -n env_name list of packages
```
在这里，-n env_name 设置环境的名称（-n 是指名称），而 list of packages 是要安装在环境中的包的列表。例如，要创建名为 my_env 的环境并在其中安装 numpy，python，并指定 python 的版本为 python3 请键入： 

```
conda create -n my_env numpy python=3 
```

##### 进入环境

创建了环境后，在 OSX/Linux 上使用 

```
source activate my_env 
```
进入环境。在 Windows 上，请使用 

```
activate my_env
```
##### 保存和加载环境

将当前环境中所有的包保存到 environment.yaml 文件中。

```
conda env export > environment.yaml
```
通过保存的 environment.yaml 文件创建新的环境：

```
conda env create -f environment.yaml
```

##### 列出环境

如果忘记了环境的名称（我有时会这样），可以使用 

```
conda env list
```
列出你创建的所有环境。你会看到环境的列表，而且你当前所在环境的旁边会有一个星号。默认的环境（即当你不在选定环境中时使用的环境）名为 root。

##### 删除环境

如果你不再使用某些环境，可以使用 

```
conda env remove -n env_name 
```
删除指定的环境（在这里名为 env_name）。


### Class 7 Jupyter Notebooks

#### 启动 notebook 服务器

终端输入：

```
jupyter notebook
```

#### markdown

[markdown 语法速查](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

##### 数学表达式

$$
y = \frac{a}{b+c}
$$

[LaTeX](http://data-blog.udacity.com/posts/2016/10/latex-primer/)

#### Magic 命令

Magic 命令的前面带有一个或两个百分号（% 或 %%），分别对应行 Magic 命令和单元格 Magic 命令。行 Magic 命令仅应用于编写 Magic 命令时所在的行，而单元格 Magic 命令应用于整个单元格。


##### 代码计时

计算单个函数的耗时：

```
%timeit fibol(20)
```

计算整个单元格的耗时：

```
%%timeit
fibol(20)
fibol(21)
```

##### notebook 中嵌入可视化内容

```
%matplotlib inline
%config InlineBackend.figure_format = 'retina'

import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 1, 300)
for w in range(2, 6, 2):
    plt.plot(x, np.sin(np.pi*x)*np.sin(2*w*np.pi*x))
```

##### 在 notebook 中进行调试

对于 Python 内核，可以使用 Magic 命令 `%pdb` 开启交互式调试器。出错时，你能检查当前命名空间中的变量。

##### 其他命令

[其他命令](http://ipython.readthedocs.io/en/stable/interactive/magics.html)

#### 转换 notebook

Notebook 只是扩展名为 .ipynb 的大型 JSON 文件。由于 notebook 是 JSON 文件，因此，可以轻松将其转换为其他格式。Jupyter 附带了一个名为 nbconvert 的实用程序，可将 notebook 转换为 HTML、Markdown、幻灯片等格式。

例如，要将 notebook 转换为 HTML 文件，请在终端中使用:

```
jupyter nbconvert --to html notebook.ipynb
```

[nbconvert](https://nbconvert.readthedocs.io/en/latest/usage.html)

#### 创建幻灯片



