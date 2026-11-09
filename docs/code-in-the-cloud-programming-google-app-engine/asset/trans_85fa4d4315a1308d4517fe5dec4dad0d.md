
下载 filesystem/datastore-indexes.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<datastore-indexes
    autoGenerate="true">
    <datastore-index kind="ResourceAttribute" ancestor="false">
        <property name="name" direction="asc" />
        <property name="value" direction="desc" />
    </datastore-index>
</datastore-indexes>
```

### 14.2 更灵活的模型

数据存储中还会出现另一个重要问题：模型限制。我们目前构建的模型受到很多限制。一个类型的每个实例都必须具有完全相同的属性。对于标准模型来说，这一点毫无灵活性。但有时这种限制实在太严格了。遇到这种情况时，有两种变通选择：expando 模型和 polymodel。

expando 模型是一种可以随时向模型实例任意添加新属性的模型。它基本上代表了模型灵活性的极致。你可以在任何时候添加任何想要的内容。所有模型实例——也就是你存储的所有对象——都必须是同一个 Python 类的实例。

polymodel 是一种为模型实例定义超类的模型。然后你可以添加该类的子类。执行查询时，它会检索 polymodel 基类的所有实例以及 polymodel 子类的实例。

在使用 expando 或 polymodel 之前，请停下来想一想。根据我的经验，大多数情况下，如果你无法在不使用 polymodel 或 expando 的情况下清晰地定义模型，那就说明你还没有考虑得足够周全。有些情况可能确实需要它们，但当你真正需要时，它们就在那里供你使用。对于 expando 模型尤其如此：expando 模型的极端灵活性有点像流程控制中 goto 的极端灵活性：有些地方使用它们是有意义的，但也有一些地方，它们只是简单的解决方案，而不是正确的解决方案。

对于 polymodel，情况则清晰而简洁。定义模型类的方式与定义标准模型完全相同，只是基类要继承自 polymodel.PolyModel。然后按常规方式定义该 polymodel 的子类。

例如，我们可以把 ResourceAttribute 做成 polymodel，从而为文件系统添加带类型的属性。然后可以为字符串属性、整数属性等添加 ResourceAttribute 的子类：

```python
class ResourceAttribute(polymodel.PolyModel):
    name = db.StringProperty(required=True)

class StringAttribute(ResourceAttribute):
    strVal = db.StringProperty(required=True)

class IntegerAttribute(ResourceAttribute):
    intVal = db.IntegerProperty(required=True)
```

如果你确实必须使用 expando 模型，那也非常简单——让类继承自 google.appengine.ext.db.Expando。在 expando 模型中，你完全不需要定义属性。你可以定义一组固定属性，这些属性会包含在模型的每个实例中。但同时，Python 对象的每个字段都会被隐式地当作无类型属性处理。这样做时，你就会失去数据存储通常为你提供的所有帮助。你不会获得自动引用；也不会获得任何数据验证。它完全灵活，也完全没有结构。你很可能并不想使用它。我还没有见过一个真正需要做成 expando 的 expando 模型示例。我不会给你展示这样的示例，因为我想不出任何真正有意义的场景。

我可以为我们的文件系统定义一个使用 expando 模型的版本。我可以完全去掉 ResourceAttribute，只使用 Python 资源对象的字段来存储属性。但那会是一个糟糕的解决方案。我会失去基于属性定义查询的能力，也会失去大量结构一致性。我能得到什么？坦率地说，并没有多少。我只会获得稍微好一点的属性更新语法，仅此而已。

### 14.3 事务、键和实体组

回到 **10.2 节“在 GWT 中存储持久对象”**（第 **145** 页），我们讨论了事务、事务为何如此重要，以及事务在 Java 中如何自动工作。事实证明，在 Python 中我们也有事务，只是之前没有费心去了解它们。与 App Engine 中 Python 的许多其他功能一样，默认行为被设置为在大多数情况下都是正确的。但和往常一样，总会有一些情况，你想要的不是默认行为，因此你需要理解它实际是如何工作的。

Python 中的事务由一种称为*实体组*（entity group）的东西驱动。你在 Python 中创建的每个持久对象都属于一组对象，这组对象称为实体组。每次从 Python 向数据存储保存更改时，同一实体组内对象的所有更改都会在单个事务中保存。因此，如果你能安排需要存储的所有内容都位于同一个实体组中，就不必担心事务：它会自动正常工作。

实体组通过祖先关系来管理：每个对象都自动与其父对象处于同一实体组中。父关系在创建对象时建立：创建持久 Python 对象时，可以使用名为 `parent` 的参数指定其父对象。如果不指定父对象，那么该对象就是根对象；它会定义自己的实体组。

如果你不需要在一组对象内实现事务行为，那么最好就让它们作为根对象。事务非常有用，但代价并不低。就数据存储和 App Engine 分布式环境而言，一个实体组无法分布式存储。它需要位于同一台服务器上。这意味着当你扩展到大量用户和对象时，把太多内容放入同一个实体组可能会让你的应用性能变得非常糟糕。

例如，在我们的聊天应用中，我们可以把所有聊天消息放入同一个实体组。这样做有一些优点，比如提供非常强的一致性保证。但随着时间推移，我们很容易在数百个聊天室中拥有数万或数十万条聊天消息，而向任何聊天室添加消息时，在其事务进行期间，可能会阻塞其他聊天室用户的更新。

另一方面，我们也不想完全忘记事务。在我们的文件系统中，如果用户更新单个资源的几个属性然后保存，他们期望更新要么成功，要么失败。因此，对于文件系统资源来说，让属性成为其资源的子对象是合理的，这样属性更新就会成为与其父对象同一事务的一部分。为此，我们唯一需要做的更改是在 Resource 的 SetAttribute 方法中：

下载 filesystem/filesystem_servlet.py

```python
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
        newAttr = ResourceAttribute(parent=self, name=name, value=value)
        newAttr.put()
        self.attributes.append(newAttr.key())
        self.put()
```

这与我们之前见过的 `setAttribute` 方法唯一的区别在于创建新 `ResourceAttribute` 对象的调用。在这个新版本中，我们为 `ResourceAttribute` 提供了 `parent` 参数，这会将该属性放入与 `Resource` 对象本身相同的资源组中。

除了事务之外，资源组还会影响对象的*键*（Key）。键编码了资源路径的信息——也就是从根对象到特定对象的规范路径。这可以用于查询：你可以缩小查询范围，只包含以特定对象为祖先的对象。这可以通过查询中的特殊查询子句 `ANCESTOR IS` 来完成。例如，在我们的文件系统中，属性以资源为父对象，我们可以查询某个特定资源的属性值。如果我们想要资源 R 的 length 属性，可以编写如下 GQL 查询：

```python
query = db.GqlQuery("SELECT * FROM ResourceAttribute WHERE "
                    "name = :name AND ANCESTOR IS :parent",
                    name="length", parent=R.key())
```

### 14.4 策略与一致性模型

关于数据存储，我们需要学习的最后一点涉及*策略*（policy）这一概念。策略是一个通用术语，描述定义系统应如何行为的高层选项。在数据存储中，哪些索引会被自动生成，这属于策略问题。有两个主要的策略问题会影响你可以控制的数据存储查询：
