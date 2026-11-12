

例如，如果你想知道伦敦的人口，你可以从上往下扫描城市名称列，直到找到伦敦。由于城市按字母顺序排列，你也可以模拟二分查找。你可以从列的中间附近开始搜索，确定伦敦位于哪一半，然后对适当的一半递归应用二分查找。如你所知，二分查找比从头开始扫描整个城市名称列要高效得多。

然而，如果你想找出数据集中哪些城市在西班牙，你别无选择，只能扫描整个数据集。城市名称的字母顺序对这个问题完全没有帮助。数据排列有助于查找给定城市，但其他类型的问题需要对数据进行完整扫描。

ADT字典（也称为映射或表）也允许你轻松查找信息，并为此目的提供特殊操作。通常，ADT字典中的项目是包含多个数据项的对象。你可以通过基于指定搜索键进行搜索来促进项目的检索。例如，在城市字典中，如果你经常需要检索关于某个城市的信息，可以将City指定为搜索键。你可以设计字典的实现，以便快速检索搜索键与某个指定值匹配的项目。但是，如果你需要基于不是搜索键的值来检索项目，则必须检查整个字典。因此，搜索键的选择向ADT实现者传达了以下信息：

The ADT dictionary uses a search key to identify its items

ADT字典使用搜索键来标识其项目

Arrange the data to facilitate the search for an item, given the value of its search key.

根据其搜索键的值安排数据，以便于查找项目。

The basic operations that define the ADT dictionary are as follows:

定义ADT字典的基本操作如下：

**Note: ADT dictionary operations**

**注意：ADT字典操作**

- Test whether a dictionary is empty.
- Get the number of items in a dictionary.
- Insert a new item into a dictionary.
- Remove the item with a given search key from a dictionary.
- Remove all items from a dictionary.
- Get the item with a given search key from a dictionary.
- Test whether a dictionary contains an item with a given search key.
- Traverse the items in a dictionary in sorted search-key order.

- 测试字典是否为空。
- 获取字典中的项目数量。
- 将新项目插入字典。
- 从字典中删除具有给定搜索键的项目。
- 从字典中删除所有项目。
- 从字典中获取具有给定搜索键的项目。
- 测试字典是否包含具有给定搜索键的项目。
- 按排序后的搜索键顺序遍历字典中的项目。

For simplicity, we will assume that all items in the dictionary have distinct search keys. This assumption can affect our design in one of several ways:

为简单起见，我们将假设字典中的所有项目都具有不同的搜索键。这一假设可能以多种方式之一影响我们的设计：

- Distinct search keys can be a precondition of the insertion operation
- The insertion operation can deny an attempt to insert a new entry whose search key already exists in the dictionary
- The insertion operation can replace an existing entry whose search key matches the search key of a new entry with the new entry

- 不同的搜索键可以是插入操作的前置条件
- 插入操作可以拒绝尝试插入其搜索键已在字典中存在的新条目
- 插入操作可以用新条目替换其搜索键与新条目的搜索键匹配的现有条目

We will choose the first option.

我们将选择第一个选项。

The following operation contract specifies in more detail an ADT dictionary of items with distinct search keys. Figure 18-2 shows a UML diagram for a class of dictionaries.

以下操作契约更详细地指定了具有不同搜索键的项目的ADT字典。图18-2显示了字典类的UML图。

## ABSTRACT DATA TYPE: DICTIONARY

## 抽象数据类型：字典

### DATA

### 数据

- A finite number of objects, each associated with a search key.

- 有限数量的对象，每个对象关联一个搜索键。

### OPERATIONS

### 操作

| Pseudocode | Description |
| :--- | :--- |
| isEmpty() | Task: Sees whether this dictionary is empty. Input: None. Output: True if the dictionary is empty; otherwise false. |
| getNumberOfItems() | Task: Gets the number of items in this dictionary. Input: None. Output: The number of items in the dictionary. |
| add(searchKey, newItem) | Task: Inserts an item into this dictionary according to the item's search key. Input: newItem is the data item to be inserted; searchKey is the item's associated search key and differs from all search keys presently in the dictionary. Output: True if the insertion is successful, or false if not. |
| remove(searchKey) | Task: Removes the item with the given search key from this dictionary. Input: searchKey is the search key of the item to be removed. Output: True if the removal is successful, or false if not. |
| clear() | Task: Removes all entries from this dictionary. Input: None. Output: None. |
| getItem(searchKey) | Task: Gets an item with a given search key from this dictionary. Input: searchKey is the search key of the item to be retrieved. Output: The item associated with the given search key. |
| contains(searchKey) | Task: Sees whether this dictionary contains an item with a given search key. Input: searchKey is the search key of the desired item. Output: True if the dictionary contains the designated item, or false if not. |
| traverse(visit) | Task: Traverses this dictionary and calls a given client function once for each item. Input: The client function visit, which exists outside of the ADT implementation. Output: visit's action occurs once for each item in the dictionary and possibly alters the item. |

| 伪代码 | 描述 |
| :--- | :--- |
| isEmpty() | 任务：查看此字典是否为空。输入：无。输出：如果字典为空，则为真；否则为假。 |
| getNumberOfItems() | 任务：获取此字典中的项目数量。输入：无。输出：字典中的项目数量。 |
| add(searchKey, newItem) | 任务：根据项目的搜索键将项目插入此字典。输入：newItem是要插入的数据项；searchKey是项目关联的搜索键，且与字典中当前的所有搜索键不同。输出：如果插入成功，则为真；否则为假。 |
| remove(searchKey) | 任务：从此字典中删除具有给定搜索键的项目。输入：searchKey是要删除的项目的搜索键。输出：如果删除成功，则为真；否则为假。 |
| clear() | 任务：从此字典中删除所有条目。输入：无。输出：无。 |
| getItem(searchKey) | 任务：从此字典中获取具有给定搜索键的项目。输入：searchKey是要检索的项目的搜索键。输出：与给定搜索键关联的项目。 |
| contains(searchKey) | 任务：查看此字典是否包含具有给定搜索键的项目。输入：searchKey是所需项目的搜索键。输出：如果字典包含指定项目，则为真；否则为假。 |
| traverse(visit) | 任务：遍历此字典，并为每个项目调用一次给定的客户端函数。输入：客户端函数visit，它存在于ADT实现之外。输出：visit的操作对字典中的每个项目发生一次，并可能更改该项目。 |

Various sets of dictionary operations are possible

可能有多种字典操作集

Our dictionary assumes distinct search keys

我们的字典假设搜索键不同

You should realize that these operations are only one possible set of dictionary operations. The client may require either a subset of these operations or other operations not listed here to fit the application at hand. It may also be convenient to modify the definitions of some of the operations. For example, these operations assume that no two dictionaries have the same search keys. However, in many applications it is quite reasonable to expect duplicate search keys. If this is the case, you must redefine several of the operations to eliminate the ambiguity that would arise from duplicate search keys. For example, which item should getItem return if several items have the specified search key? You should tailor your definition of the ADT dictionary to the problem at hand.

你应该意识到，这些操作只是一种可能的字典操作集。客户端可能需要这些操作的一个子集，或者这里未列出的其他操作，以适应手头的应用程序。修改某些操作的定义也可能很方便。例如，这些操作假设没有两个字典具有相同的搜索键。但是，在许多应用程序中，预期会有重复的搜索键是非常合理的。如果是这种情况，你必须重新定义几个操作，以消除重复搜索键可能产生的歧义。例如，如果有多个项目具有指定的搜索键，getItem应该返回哪个项目？你应该根据手头的问题定制ADT字典的定义。

### FIGURE 18-2 UML diagram for a class of dictionaries

### 图18-2 字典类的UML图

![](img/288a0c22d14d2450c1e772f228f867b0_555_0.png)

Other dictionaries could allow duplicate search keys

其他字典可能允许重复的搜索键

Although just the operations add, remove, and getItem in the previous set of operations are sufficient for some applications, you cannot do several significant things without additional operations. For instance, you cannot display all the dictionary items, because you cannot retrieve a data item unless you know the value of its search key. Thus, you cannot display the entire dictionary until you can traverse the dictionary.

尽管前一组操作中仅add、remove和getItem操作对某些应用程序来说就足够了，但没有额外的操作，你无法完成几件重要的事情。例如，你无法显示所有字典项目，因为除非你知道数据项的搜索键值，否则无法检索数据项。因此，在你能够遍历字典之前，无法显示整个字典。

traverse visits all dictionary items

traverse访问字典中的所有项目

The traverse operation visits each item in the dictionary once. In defining this operation, you must specify the order in which the traversal should visit the items. One common specification is to visit the items in sorted order by search key, but perhaps you do not care about the order in which the items are visited. As you will see, the way you define traverse—if you request it at all—can affect the way you implement the dictionary.

traverse操作访问字典中的每个项目一次。在定义此操作时，你必须指定遍历访问项目的顺序。一种常见的规范是按搜索键的排序顺序访问项目，但也许你不关心访问项目的顺序。如你将看到的，你定义traverse的方式（如果你确实请求它的话）会影响你实现字典的方式。

> **Note: Search keys**
> 
> The concept of a search key for the dictionary items is essential to the implementation of the dictionary. It is important that the value of the search key remain the same as long as the item is stored in the dictionary. Changing the search key of an existing entry in the dictionary could make that entry or other dictionary entries impossible to find. Thus, the client should not be able to modify the value of an entry's search key once that entry is in the dictionary.

> **注意：搜索键**
> 
> 字典项目的搜索键概念对于字典的实现至关重要。重要的是，只要项目存储在字典中，搜索键的值就应保持不变。更改字典中现有条目的搜索键可能会使该条目或其他字典条目无法找到。因此，一旦条目在字典中，客户端就不应该能够修改条目的搜索键值。

Like the traversal operations for the ADT binary tree, traverse has a visit function as its argument. Because visit can do any number of things—including access the dictionary via the ADT operations—traverse is a versatile operation. We illustrate this versatility with three brief examples, in which the dictionary contains the data for the cities listed in Figure 18-1.

与ADT二叉树的遍历操作类似，traverse将visit函数作为其参数。因为visit可以执行任何数量的操作——包括通过ADT操作访问字典——所以traverse是一个多功能操作。我们用三个简短的例子来说明这种多功能性，其中字典包含图18-1中列出的城市的数据。

**Examples:** Each of the following tasks will use the city's name as the search key. The class City contains all the information for a city, including its name, country, and population. The class has accessor and mutator methods for each these pieces of data.

**示例：** 以下每个任务都将使用城市名称作为搜索键。City类包含城市的所有信息，包括其名称、国家和人口。该类为每个数据项都具有访问器和修改器方法。

### Tasks that use the city's name as the search key

### 使用城市名称作为搜索键的任务

- **Display, in alphabetical order, the name of each city and its population.**

- **按字母顺序显示每个城市的名称和人口。**

This task requires you to write the city names in alphabetical order. Since the city names are the search keys, traverse must visit items alphabetically by search key. You pass the method the name of the function displayItem, which appears in pseudocode as follows:

此任务要求你按字母顺序写出城市名称。由于城市名称是搜索键，traverse必须按搜索键的字母顺序访问项目。你将函数displayItem的名称传递给该方法，其伪代码如下：

```
displayItem(anItem: ItemType): void

    Display anItem.getName()
    Display anItem.getPopulation()
```

