

```
print(x.antelopes)  # 10!
```

请记住，当你调用函数时，实际上是在将实参赋值给形参名，因此两者指向的是同一个对象。也就是说，在上面的代码中，`o` 与 `x` 指向同一个对象，就像我们执行了 `o = x` 赋值一样。

## 11.11 对象与 None

我们已经看到，变量可以指向值 `None` 来表示“什么都没有”。

这在对象中经常用于表示某种“未找到”或错误状态。

例如，假设我们有一个对象列表，以及一个按名称搜索对象的函数。该函数应返回一个 `name` 属性与传入函数的 `name` 参数匹配的对象。

但此时自然会浮现一个问题！如果列表中不存在该名称的对象怎么办？函数应该返回什么？`None` 是不二之选。

```
class Person:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return self.name

def get_person_by_name(person_list, name):
    """Return a person object with this name, or None if not found"""
    for p in person_list:
        if p.name == name:
            # If we found them, return the object
            return p

    # If we got here, we didn't find anyone by that name
    return None

person_list = [
    Person("Annie"),
    Person("Beej"),
    Person("Chris")
]

p = get_person_by_name(person_list, "Chris")

print(p)  # "Chris"

p = get_person_by_name(person_list, "Dave")

if p is None:
    print("Dave's not here.")
```

## 11.12 测试属性

有时在运行时，你想知道对象是否具有某个属性。或者你以字符串形式拥有属性名，并想在对象上获取或设置该属性。

有三个内置函数可以帮助实现这一点：

- `hasattr()` 用于测试对象上是否存在某属性。
- `getattr()` 返回属性的值，如果属性不存在，还可以返回默认值。
- `setattr()` 设置属性的值，如果属性不存在则创建它。

这为编写对象提供了更大的灵活性，因为你可以让对象拥有可选属性。

让我们演示一下！

```
class Foo:
    pass

f = Foo()
f.bar = 12

print(hasattr(f, "bar"))    # True
print(hasattr(f, "frotz"))  # False

print(getattr(f, "bar"))            # 12
print(getattr(f, "frotz", None))    # None, since attr frotz doesn't exist

setattr(f, "frotz", 99)  # Just like saying "f.frotz = 99"

print(f.frotz)  # 99
```

我不会说这些函数在日常使用中非常频繁，但它们是你工具库中的有力补充。

## 11.13 章节项目

如果你忘记了，请回顾本章开头给出的章节项目规格说明。

### 解决问题步骤：理解问题。

看起来我们需要存储多家影院的信息，以及多部电影的信息。

而且一部电影可能会同时在多家影院上映。

### 解决问题步骤：制定计划。

有很多方法可以存储这些数据。但既然本章的主题是类和对象，我们何不采用它们呢？

看起来我们应该有一个 `Theater` 类来处理每家影院的信息。

以及一个 `Movie` 类来处理每部电影的信息。

而一家影院可以同时上映多部电影，因此我们可以给它一个属性，用来存放当前上映的电影列表。

我们还会保留一个包含所有影院的列表，以及一个包含所有电影的列表。

### 解决问题步骤：执行计划。

这是一个影院类。我们将名称传递给构造函数，但将 `movies` 初始化为空列表。我们可以在之后填充它们。

```
class Theater:
    """Holds all the information about a specific theater."""
    def __init__(self, name):
        self.name = name
        self.movies = []
```

以及一个电影类：

```
class Movie:
    """Holds all the information about a specific movie."""
    def __init__(self, name, duration, genre):
        self.name = name
        self.duration = duration
        self.genre = genre
```

到目前为止一切顺利。

现在我们需要实例化一批电影，以便将它们添加到影院的 `.movies` 列表中。

我们可以做几件事。

我们可以为每部电影使用一个变量，但这有点笨拙。让我们使用某种集合，比如列表！我们将为所有电影和所有影院各建一个列表。你可以随意添加自己喜欢的。

```
movies = [
    Movie("Star Wars", 125, "scifi"),
    Movie("Shaun of the Dead", 100, "romzomcom"),
    Movie("Citizen Kane", 119, "drama")
]

theaters = [
    Theater("McMenamin's Old St. Francis Theater"),
    Theater("Tin Pan Theater"),
    Theater("Tower Theater")
]
```

看看这里我们做了什么。请注意，`movies` 是一个列表，而在列表内部，我们初始化列表的同时，正在构造新的 `Movie` 对象。

我们对 `theaters` 也是同样的做法。它是一个由新构造的 `Theater` 对象组成的列表。

接下来，我们需要将这些电影与放映它们的影院关联起来。

请记住，每个 `Theater` 对象的 `.movies` 属性是一个电影列表。因此我们需要将电影追加到该列表中。

接下来的部分有点晦涩，所以请务必仔细理解：

```
# McMenamin's is showing Star Wars and Shaun of the Dead
theaters[0].movies.append(movies[0])
theaters[0].movies.append(movies[1])
```

这是什么意思？

好吧，我们一次看一点，每一行从左到右看。

`theaters[0]` 是什么？

如果我们查看 `theaters` 列表，会发现那是 McMenamin’s。

然后我们通过 `theaters[0].movies` 获取它的电影列表。

它的 `movies` 列表是一个列表，所以我们可以使用列表的 `.append()` 方法向其中添加电影。但要追加哪部电影呢？

我们追加 `movies[0]`……如果我们查看 `movies` 列表，会发现那是《星球大战》。

所以 `theaters[0]` 是 McMenamin’s，而 `movies[0]` 是《星球大战》。

这意味着上面的第一行是在说：“将《星球大战》追加到 McMenamin’s 的当前上映电影列表中。”

而下面那一行则是在说：“将《僵尸肖恩》追加到 McMenamin’s 的当前上映电影列表中。”

让我们再做几行。这些行各自做了什么？

```
# Tin Pan is showing Shaun of the Dead and Fastest Indian
theaters[1].movies.append(movies[1])
theaters[1].movies.append(movies[2])

# Tower is showing all three
theaters[2].movies.append(movies[0])
theaters[2].movies.append(movies[1])
theaters[2].movies.append(movies[2])
```

实际上，我们在这里所做的是将所有电影对象与其对应的影院关联起来。

请注意，电影是如何出现在多家影院中的。例如，`movies[0]`（《星球大战》）既在 `theaters[0]`（McMenamin’s）中，也在 `theaters[2]`（Tower）中。

这是否意味着《星球大战》电影对象有两个副本？因为它出现在两家影院？

请仔细想想！

不，只有一个！就是我们在上文创建的那个对象！由于它是一个对象，通过赋值（或使用 `.append()`）进行“复制”只是创建了对同一个对象的另一个引用。它只有一个，但被两个 `Theater` 对象引用。同时也被 `movies` 列表引用。这么多引用指向同一个对象，节省了大量内存。

现在，我们想要打印所有影院及其放映时间。我将在这里创建一个辅助函数来打印单个影院的数据。我们将传入对影院对象的引用，打印其名称，然后打印其 `.movies` 列表中所有电影的数据。

```
def print_theater(theater):
    """Print all the information about a theater."""
    print(f'{theater.name} is showing:')
    for m in theater.movies:
        print(f'    {m.name} ({m.genre}, {m.duration} minutes)')
```

最后，我们要做的就是为 `theaters` 列表中的所有影院调用 `print_theater()`：

```
# Main code
for t in theaters:
    print_theater(t)
```

大功告成！（解决方案⁶）

### 解决问题步骤：回顾。

看看我们是如何看待问题描述的（基本上就是说“影院放映电影，而一部电影可能同时出现在多家影院”），并将其映射为两个类来分别保存每家影院和每部电影的信息的。

请注意，这些类是如何将所有关于一家影院或一部电影的信息封装在独立的单个对象中的。

简洁而干净，而且如果另一个函数想使用某个对象，也很容易传递对该对象的引用。

有哪些不足之处？

那些将电影添加到影院的代码行可读性较差。它们引用的是 `movies[0]` 这样的形式，而不是按名称引用。

