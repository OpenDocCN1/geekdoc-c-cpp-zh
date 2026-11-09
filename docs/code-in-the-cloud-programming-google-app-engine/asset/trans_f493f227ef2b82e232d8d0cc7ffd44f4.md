
在新的资源模型中，我们为 children 加入了一个属性，它是一个由 DirectoryEntry 对象的键组成的列表。我们不使用对条目的引用；在列表属性中我们无法这样做。而且，从概念上说，我们希望这些条目被包含在资源对象中，这意味着我们只会在资源类的方法内部存储或获取它们。引用的意义在于，它让实际获取发生的时机变得透明。这样你就可以像传递真实对象一样传递引用，而不必担心在真正需要其值时如何获取它。但是，这些值只会在一个地方被获取，因此引用的开销根本没有意义。

现在我们有了一种有趣的设置。我们的资源类型包含一个目录条目列表，这些条目通过键访问，而目录条目是引用。我们如何用它来实现目录呢？首先，让我们看看需要如何修改 GetAttribute 和 SetAttribute 方法才能与目录条目配合工作。然后我们会看使用这些文件系统对象的代码，了解它们实际如何使用这些引用。

```python
def GetAttribute(self, name):
    if name == "children":
        return [ DirectoryEntry.get(key) for key in self.children ]
    else:
        for attr_key in self.attributes:
            attr = ResourceAttributeModel.get(attr_key)
            if attr.name == name:
                return attr.value
        return None

def SetAttribute(self, name, value):
    if name == "children":
        self.children = [ de.key() for de in value ]
        self.put()
    else:
        for attr_key in self.attributes:
            attr = ResourceAttributeModel.get(attr_key)
            if attr.name == name:
                attr.value = value
                attr.put()
                return
        newAttr = ResourceAttributeModel(name=name, value=value)
        newAttr.put()
        self.attributes.append(newAttr.key())
        self.put()
def IsDir(self):
    return (self.children is not [])
```

-   在 GetAttribute 中，我们首先检查属性名是否为 children。这有点丑陋，但由于我们面临的限制，这里无法避免。children 属性是一个特殊情况，所以我们需要显式检查它。如果要获取的是它，我们就使用特殊代码来获取资源的子项；否则，我们就落入与之前完全相同的代码。如果获取的是 children 属性，那么我们用列表推导式遍历 DirectoryEntry 键的列表，获取实际的 DirectoryEntry 对象，然后返回该列表。因此，对于文件系统的客户端来说，当他们调用 file.GetAttribute("children") 时，结果是一个目录条目列表。但其中隐藏着一点巧妙之处：正如我们稍后将看到的，对于这段代码的客户端来说，目录条目表现得就像它们真的包含子资源一样，但实际上它们只包含引用。

-   在 SetAttribute 中，我们做与 GetAttribute 相反的操作。我们以完全相同的方式开始，检查要设置的是哪个属性。如果是 children，那么我们期望值是一个 DirectoryEntry 对象列表，因此我们用列表推导式做与获取完全相反的事：把目录条目替换为键，得到一个键的列表，然后把它存入资源的特殊 children 属性。由于这会修改资源，我们需要用 put 调用保存它。

一旦引用属性设置好，我们如何使用它？数据存储会完成所有工作。如果你只是获取数据存储实例中某个引用属性的值，数据存储会完全透明地自动为你获取它。因此，例如，我们可以遍历一个目录的子项，用下面的函数打印每个子项是否为目录：

[下载 filesystem/persistent_filesystem.py](filesystem/persistent_filesystem.py)

```python
def RenderChildren(dir):
    children = dir.GetAttribute("children")
    for c in children:
        # c is a DirectoryEntry
        if c.resource.IsDir():
            print("Child %s is a directory" % c.name)
        else:
            print("Child %s is not a directory" % c.name)
```

在这个函数中，我们遍历 directory 的 children 属性中的 DirectoryEntry 值。对于每个值，我们通过调用 DirectoryEntry 的 resource 字段上的 IsDir 方法来访问它引用的资源。这个字段不是资源；它是一个引用。但每当我们试图访问该引用的任何字段或方法时——比如这里调用它的 IsDir 方法——数据存储都会自动获取被引用的对象。

到目前为止，这看起来非常简单——几乎太简单了。持久化要做到正确可能极其复杂，但我们目前看到的内容在隐藏这种复杂性方面做得相当出色。然而，底层复杂性仍然存在。

这会以几种方式影响你。最直接的是，数据存储在我们使用引用时自动为我们获取引用，这很好，但在幕后，它仍然是一次对数据存储的往返调用。从持久存储系统中获取内容并非没有代价。它并不特别昂贵，而且远比执行查询便宜。但它不是免费的，而且这样做的成本会累积起来，变得相当可观。把获取操作对我们隐藏起来非常方便，但这也让我们很容易意外地做出会让代码变得极慢的事情。

例如，在上面的目录打印器中，当我们以那种方式遍历目录时会发生什么？它会获取目录每个子项的资源对象。而这样做意味着要获取目录中每个成员的每个子项的每个 DirectoryEntry 的键。如果我们使用这些键，最终会获取对其他资源对象的引用。编写一个遍历目录层次结构的例程很容易，但最终会执行大量获取，每次获取都作为引用访问的一部分独立进行。在这种情况下，我们最好只用一次查询就获取所有对象。不加小心地使用引用，意味着你可能会在不知不觉中写出极其低效的代码，如果你不习惯云风格的分布式编程，这种低效可能并不明显。

下面这个例子可以让你感受潜在影响。在我职业生涯早期，我做过一些 C++ 持久化系统方面的工作。在那个系统中，我们做了很多类似这种自动引用获取的事情。有一次，我在为客户编写一些示例代码，发现它的性能完全说不通。我只是在一个循环中迭代，但时间成本巨大。它不是大致与列表大小成正比，而是与列表大小的平方成正比。问题几乎正是我上面描述的那样：每当有人访问列表的一个成员时，它都会自动获取该成员的子项列表，并为它们构造代理（我们这里的引用形式）。所以访问一个列表元素实际上最终创建了一个列表代理。看起来无害的一行代码实际上很昂贵，因为系统在我背后做了那些巧妙的事情。

在数据存储中，你需要了解实际发生了什么，才能理解成本。当你访问一个引用参数时，你实际上是在调用数据存储：db.get(key)。这可能会引发一次非常昂贵的获取操作。

有时这确实是个问题，但你可以通过显式使用键来避免它。当你使用键时，就像我们处理 DirectoryEntry 对象那样，你让获取操作变得显式。在你的代码中，你会非常清楚自己做了多少次获取，因为它们不再对你隐藏。这类编程中有一种微妙的平衡——在像引用这样的简单性和像键这样的显式性之间做选择。一般来说，如果你会有很多对象，我建议使用显式键。这更费力，但它能让你保持诚实。

构建文件系统的下一个主要问题是：我们应该如何处理内容？在我们最初的模型中，我们把内容存储在文本属性中。这不错，但不算很好。文本对象可以变得相当大，但它们基本上仍然只是字符串。这并不完全正确：文件系统中的文件内容可以任意大，而且内容可以是任意字节序列。

但还有另一个问题。每次我们获取一个文件对象时，都会获取整个文件对象。如果内容有 20 MB，而我们只想检查该文件是否为目录，就像我们之前写的 render 函数那样，那会怎样？那会极其低效。记住：在云中，你是要为资源付费的。加载你并不使用的文件内容所花的时间并不是免费的。我们真正想做的是为内容创建另一种对象类型，这样我们就可以使用引用。

（本节的）最终对象模型如下：

```python
class ContentModel(db.Model):
    data = db.BlobProperty()

class DirectoryEntry(db.Model):
    name = db.StringProperty()
    resource = db.ReferenceProperty(PersistentResourceModel)
```
