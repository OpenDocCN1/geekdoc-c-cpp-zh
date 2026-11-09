

```python
print('\n')

# clear list values
even_nums.clear()
print("Even number list after clearing is: ", even_nums)
print('\n')

# extend the empty list
even_nums.extend(['Tom', 1, 'python'])
print("Even number list after extending is: ", even_nums)
print('\n')

# insert new element at index 0
even_nums.insert(0, 'new')
print("Even number list after inserting at index 0 is: ", even_nums)
print('\n')

# pop list last element
even_nums.pop()
print("Even number list after popping is: ", even_nums)
print('\n')

# find the index of 'Tom' and change it to Nick
index_python = even_nums.index('Tom')
even_nums[index_python] = 'Nick'

print("Even number after replacing Tom is: ", even_nums)
```

**输出：**

even_nums 列表的长度是：6

偶数是：
0
2
4
6
8
10

小于 5 的偶数是：[0, 2, 4]

追加后的偶数列表是：[0, 2, 4, 6, 8, 10, 12]

12 在 even_nums 列表中出现了 1 次

清空后的偶数列表是：[]

扩展后的偶数列表是：['Tom', 1, 'python']

在索引 0 处插入后的偶数列表是：['new', 'Tom', 1, 'python']

弹出后的偶数列表是：['new', 'Tom', 1]

替换 Tom 后的偶数是：['new', 'Nick', 1]

## 元组

元组与列表类似，因为它们也存储一组项目。事实上，元组可以被视为不可变列表。元组是不可变的；一旦赋值，它们就不能更改。这使得它们更高效、更快速。元组使用圆括号定义，而列表使用方括号定义。要创建元组，请将逗号分隔的值放在圆括号中。

```python
my_tuple = (1,3,5)
```

对于单值元组，请在值后面加上逗号。如果没有逗号，Python 会将其视为数字。

```python
my_tuple = (1,)
```

在这个代码片段中，我们创建元组并尝试修改它们的值；然而，Python 会抛出类型错误，因为元组是不可变的。

```python
# create a tuple

# single value tuple
tu1 = (1, )

print("Single value tuple: ", tu1)
# Multi values tuple
tu2 = (1, 'a', 'python')
print("Multi value tuple: ", tu2)
print("tuple type is ", type(tu2))

# try modifying tuple
tu2[2] = 'C++'
```

```text
Single value tuple:  (1,)
Multi value tuple: (1, 'a', 'python')
tuple type is  <class 'tuple'>

--------------------------------------------
Traceback (most recent call last):
  File "<ipython-input-7-a5d65c274c9b>", line 13, in <module>
    11
    12 # try modifying tuple
---> 13 tu2[2] = 'C++'

TypeError: 'tuple' object does not support item assignment
```

### 元组方法

与列表类似，元组支持索引、`len`、切片和 `in` 成员运算符等基本方法。元组还支持 `index` 和 `count` 方法。注意，元组的方法不如列表多，因为元组是不可变的。

### 示例 2：*元组方法*

在本示例中，我们对元组执行基本方法。请注意，这些方法与列表方法相同。

```python
# Basic tuple methods
tu = ('Tom', 'Jane', 'Python', 10, 'Tom')

# len()
print("Tuple length is :", len(tu))

# Element access
print("Last element of tuple is :",tu[-1])

# slicing
print("tu[0:3] is :",tu[0:3])

# index method
print("'Python' is at index:",tu.index('Python'))

# count method
print("'Tom' occurs:",tu.count('Tom'))
```

```text
Tuple length is : 5
Last element of tuple is : Tom
tu[0:3] is : ('Tom', 'Jane', 'Python')
'Python' is at index: 2
'Tom' occurs: 2
```

## 字典

字典是键值对。列表和元组通过位置索引访问，而字典的值通过其对应的键访问。键必须是不可变的，例如字符串、数字甚至元组，但不能是列表，因为列表是可变的。键也是唯一的；不能有两个值具有相同的键。

字典由花括号中逗号分隔的键: 值对定义。

创建空字典：

```python
my_dict = {}
```

或

```python
my_dict = dict()
```

创建基本字典：

```python
num_dict = {'one':1, 'two':2, 'three':3}
```

### 字典基本方法

要访问字典的值，请使用其键。

```python
num_dict = {'one':1, 'two':2, 'three':3}
num_dict['one'] is 1
```

成员资格检查与元组和列表类似，不同之处在于它检查键。

```python
num_dict = {'one':1, 'two':2, 'three':3}
'one' in num_dict returns True
```

要添加新的键值对，请使用赋值运算符。

```python
num_dict = {'one':1, 'two':2, 'three':3}
num_dict['four'] = 4
num_dict now is {'one':1, 'two':2, 'three':3, 'four':4}
```

- `dict.clear` – 清除字典。

    ```python
    num_dict = {'one':1, 'two':2, 'three':3}
    num_dict.clear()
    num_dict now is {}
    ```

- `dict.get(key)` – 通过键检索字典值，如果不存在这样的键则返回 None。

    ```python
    num_dict = {'one':1, 'two':2, 'three':3}
    num_dict.get('one') returns 1
    ```

- `dict.pop(key)` – 删除与 key 对应的键:值对。

    ```python
    num_dict = {'one':1, 'two':2, 'three':3}
    num_dict.pop('three') removes 3
    num_dict now is {'one':1, 'two':2}
    ```

- `dict.items()` – 返回 (key, value) 元组列表。

    ```python
    num_dict = {'one':1, 'two':2, 'three':3}
    num_dict.items() returns [('one', 1), ('two', 2), ('three', 3)]
    ```

- `dict.keys()` – 返回包含所有字典键的 dict_keys 对象。

    ```python
    num_dict = {'one':1, 'two':2, 'three':3}
    num_dict.keys() returns dict_keys(['one', 'two', 'three'])
    ```

- `dict.values()` – 返回字典值的列表。

    ```python
    num_dict = {'one':1, 'two':2, 'three':3}
    num_dict.values() returns [1, 2, 3]
    ```

### 示例 3：*字典方法*

在示例 3 中，我们使用并试验所学的字典方法。

```python
# create a dictionary of shopping items quantity
shopcart = {'chips':2, 'ink cartridge':1, 'paper':1}

# dictionary length counts key-value pairs
print('Shopcart is:', shopcart)
print('Your shopcart distinct items are ', len(shopcart))
print('\n')

# shop cart include a pens ?
pens_in = 'pens' in shopcart

# membership test
print("There is a pen in shopping cart?", pens_in)
print('\n')

# accessing a value
print("The number of chips items is", shopcart['chips'])
print('\n')

# add a pair
shopcart['orange juice'] = 4
print(shopcart)
print('\n')

# get method
print("Quantity of orange juice is", shopcart.get('orange juice'))
print('\n')

# pop method removes element at a key
shopcart.pop('paper')
print(shopcart)
print('\n')

# get items, keys, values
items = shopcart.items()
keys = shopcart.keys()
values = shopcart.values()

print("Shopcart items are:", items)
print("Shopcart keys are:", keys)
print("Shopcart values are:", values)
```

```text
Shopcart is: {'chips': 2, 'ink cartridge': 1, 'paper': 1}
Your shopcart distinct items are 3

There is a pen in shopping cart False

The number of chips items is 2

{'chips': 2, 'ink cartridge': 1, 'paper': 1, 'orange juice': 4}

Quantity of orange juice is 4

{'chips': 2, 'ink cartridge': 1, 'orange juice': 4}

Shopcart items are: dict_items([('chips', 2), ('ink cartridge', 1), ('orange juice', 4)])
Shopcart keys are: dict_keys(['chips', 'ink cartridge', 'orange juice'])
Shopcart values are: dict_values([2, 1, 4])
```

### 示例 4 – 猜世界首都

在本示例中，我们同时使用列表和字典。字典 `capital_dict` 用于创建国家:首都键值对。然后我们使用 `keys()` 方法获取字典的键，并将它们存储在 `countries` 列表中。这是必要的，这样我们就可以使用 `random.choice()` 函数，该函数接收一个列表并从中随机返回一个值。然后在一个无限 `while` 循环中，使用 `input` 函数要求用户输入首都，并将答案与实际首都进行比较。

```python
# World capital game
import random

# World capitals dictionary
capital_dict={
    'spain':'madrid',
    'france':'paris',
    'germany':'berlin',
    'norway':'oslo',
    'india':'new delhi',
    'egypt':'cairo'
}

# get countries and convert them to a list so we can use random function
countries = list(capital_dict.keys())
print ("Let's learn World Capitals. Enter quit to quit the game.")

while True:
    # pick a random country
    country = random.choice(countries)
    capital = capital_dict[country]

    guess = input(f'What is the capital of {country}.')
    # if user types quit, quit
    if guess.lower() == "quit":
        break
    elif guess.lower() == capital:
        print(f'Correct !')
        break
    else:
        print(f'Incorrect. The capital of {country} is {capital}.')
```

