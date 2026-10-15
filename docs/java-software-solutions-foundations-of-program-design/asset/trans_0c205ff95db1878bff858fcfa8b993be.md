

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_647_0.png)

# 图 13.1 一个链表

> 关键概念
> 动态链表是通过存储和更新对对象的引用来管理的。

对象的 next 引用可以引用第三个 Node 对象，以此类推，形成一个链表。列表中的第一个节点可以使用单独的变量来引用。列表中的最后一个节点的 next 引用为 null，表示列表的结束。图 13.1 描述了这种情况。

在此示例中，每个 Node 类中存储的信息是一个简单的整数，但请记住，我们可以定义一个类来包含任意类型和任意量的信息。

## 一个动态链表

程序清单 13.1 设置了一个 Magazine 对象的列表，然后打印该列表。杂志列表封装在程序清单 13.2 所示的 MagazineList 类中，并作为动态链表维护。

MagazineList 类表示杂志列表。从类的外部来看，我们不关注列表是如何实现的。例如，我们不知道杂志列表是存储在数组中还是链表中。MagazineList 类提供了一组方法，允许用户维护杂志列表。该方法集，特别是 add 和 toString，定义了对 MagazineList ADT 的操作。

MagazineList 类使用一个名为 MagazineNode 的内部类来表示链表中的一个节点。每个节点包含对一本杂志的引用和对列表中下一个节点的引用。因为 MagazineNode 是一个内部类，允许该类中的数据值公开是合理的。因此，MagazineList 类中的代码直接引用这些数据值。

程序清单 13.3 所示的 Magazine 类封装良好，所有数据均声明为 private，并提供方法来完成必要的任何更新。请注意，因为我们使用单独的类来表示列表中的节点，所以 Magazine 类本身不需要包含指向下一个 Magazine 的链接。这使得 Magazine 类可以摆脱其在列表中包含的相关问题。

> VideoNote
> 使用链表的示例。

### 13.2 动态表示

#### LISTING 13.1

```
//**********************************
// MagazineRack.java Author: Lewis/Loftus
// Driver to exercise the MagazineList collection.
//**********************************

public class MagazineRack
{
	//----------------------------------
	// Creates a MagazineList object, adds several magazines to the
	// list, then prints it.
	//----------------------------------
	public static void main (String[] args)
	{
		MagazineList rack = new MagazineList();

		rack.add (new Magazine("Time"));
	rack.add (new Magazine("Woodworking Today"));
	rack.add (new Magazine("Communications of the ACM"));
	rack.add (new Magazine("House and Garden"));
	rack.add (new Magazine("GQ"));

		System.out.println (rack);
	}
	
}
```

#### OUTPUT

- Time
- Woodworking Today
- Communications of the ACM
- House and Garden
- GQ

其他方法也可以包含在 MagazineList ADT 中。例如，除了提供的 add 方法之外，该方法始终将新杂志添加到列表末尾，还可以定义一个名为 insert 的方法，将节点添加到列表的任何位置，以保持其排序。例如。insert 的一个参数可以指示应在之后插入新节点的节点的值。图 13.2 显示了插入新节点时引用的更新方式。

> 插入和删除操作可以通过仔细操作对象引用来实现。

#### LISTING 13.2

```
//********************** MagazineList.java Author: Lewis/Loftus
// Represents a collection of magazines.
//**********************

public class MagazineList
{
private MagazineNode list;

// Sets up an initially empty list of magazines.
//--------------------
public MagazineList()
{
list = null;
}

// Creates a new MagazineNode object and adds it to the end of the linked list.
//--------------------
public void add (Magazine mag)
{
MagazineNode node = new MagazineNode (mag);
MagazineNode current;

if (list == null)
list = node;
else
{
current = list;
while (current.next != null)
current = current.next;
current.next = node;
}
}

// Returns this list of magazines as a string.
//--------------------
public String toString ()
{
// code would go here
}
```

```
{
    String result = "";
    MagazineNode current = list;
    while (current != null)
    {
        result += current.magazine + "\n";
        current = current.next;
    }
    return result;
}

// An inner class that represents a node in the magazine list.
// The public variables are accessed by the MagazineList class.
private class MagazineNode
{
    public Magazine magazine;
    public MagazineNode next;

    // Sets up the node
    public MagazineNode (Magazine mag)
    {
        magazine = mag;
        next = null;
    }
}
```

```
//******************************************************
//  Magazine.java        Author: Lewis/Loftus
//
//  Represents a single magazine.
*******************************************************/

public class Magazine
{
    private String title;

    //--------------------------------------------------
    //  Sets up the new magazine with its title.
    //--------------------------------------------------
    public Magazine (String newTitle)
    {
        title = newTitle;
    }

    //--------------------------------------------------
    //  Returns this magazine as a string.
    //--------------------------------------------------
    public String toString ()
    {
        return title;
    }
}
```

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_651_0.png)

**图 13.2** 在列表中间插入一个节点

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_652_0.png)

# 图 13.3 从列表中删除一个节点

列表 ADT 中另一个有用的操作将是 delete 方法，用于删除特定节点。回顾我们在第 3 章中的讨论，通过删除对对象的所有引用，它就成为垃圾回收的候选对象。图 13.3 显示了从列表中删除节点时引用的更新方式。必须小心以正确的顺序完成对引用的修改，以确保不会丢失其他节点，并且引用继续引用列表中有效、适当的节点。

## 其他动态列表表示

您可以根据正在设计的程序的具体需求使用不同的列表实现。例如，在某些情况下，为了使处理更容易，可以实现双向链表，其中每个节点不仅具有对列表中下一个节点的引用，还有另一个对列表中前一个节点的引用。我们的通用 Node 类可能如下声明：

关键概念
可以定义许多动态链表实现的变体。

```
class Node
{
    int info;
    Node next, prev;
}
```

图 13.4 显示了一个双向链表。请注意，与单向链表一样，最后一个节点的 next 引用为 null。同样，第一个节点的前一个节点为 null，因为在第一个节点之前没有节点。这种结构使得在列表节点之间前后移动变得容易，但设置和修改需要更多的工作。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_652_1.png)

# 图 13.4 一个双向链表

# 图 13.5 一个带有前端和后端引用的列表

另一个链表的实现可以包括列表的头节点，该节点具有对列表前端的引用和另一个对列表后端的引用。后端引用使得向列表末尾添加新节点变得更容易。头节点可以包含其他信息，例如当前列表中节点的计数。头节点的声明类似于以下内容：

```
class ListHeader
{
    int count;
    Node front, rear;
}
```

请注意，头节点与它引用的 Node 类不是同一类。图 13.5 描述了使用头节点实现的链表。

还可以创建其他链表实现。例如，可以将头的使用与双向链表结合起来，或者列表可以按排序顺序维护。实现应满足所需处理的需要。如果它使结构上的常见操作更有效，那么维护更复杂的数据结构所付出的额外努力可能是值得的。

## 自测问题（参见附录 N 中的答案）

- SR 13.4 什么是动态数据结构？
- SR 13.5 描述图 13.2 中插入节点到列表的步骤。存在哪些特殊情况？
- SR 13.6 描述图 13.3 中从列表中删除节点的步骤。存在哪些特殊情况？

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_653_0.png)

