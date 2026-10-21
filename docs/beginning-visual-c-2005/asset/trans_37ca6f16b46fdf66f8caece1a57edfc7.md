

![](img/2359b0c604600c58fba3539c738a356e_906_0.png)

## Figure 16-23

模态对话框在对话框关闭之前会保留应用程序的焦点。只要模态对话框显示，应用程序中的所有其他窗口都处于非活动状态。

无模式对话框允许焦点在对话框和其他窗口之间切换并返回。无模式对话框如果需要，可以在应用程序执行期间一直显示。

通用控件是一组标准 Windows 控件，由 MFC 和 Developer Studio 的资源编辑功能支持。

尽管控件通常与对话框相关联，但你可以向任何窗口添加控件。

## Exercises

你可以从 http://www.wrox.com 下载本书中示例的源代码以及以下练习的解决方案。

- 1. 使用单选按钮实现比例对话框。
- 2. 使用列表框实现画笔宽度对话框。
- 3. 将画笔宽度对话框实现为组合框，并在属性框的 Styles 选项卡上选择下拉列表类型。 （下拉列表类型允许用户从下拉列表中选择，但不允许在列表中键入替代条目。）

你希望能够将文档保存到文件中，但将类对象写入文件代表着一个问题，因为它与写入整数或字符字符串等基本数据项不同。基本数据项由已知数量的字节组成，因此将其写入文件只需要写入适当数量的字节。相反，如果你知道文件写入了 int 类型的值，要取回它，只需读取适当数量的字节即可。

写入对象则不同。即使你写入了对象的所有数据成员，也不足以取回原始对象。类对象包含函数成员和数据成员，并且所有成员，无论是数据还是函数，都有访问说明符；因此，要将对象记录到外部文件中，写入文件的信息必须包含所涉及的所有类结构的完整规范。读取过程还必须足够智能，能够完全从文件中的数据合成原始对象。MFC 支持一种称为序列化的机制，帮助你以最少的时间和麻烦实现类对象的磁盘输入和输出。

序列化的基本思想是，任何可序列化的类都必须负责存储和检索自身。这意味着要使你的类可序列化——在 Sketcher 应用程序的情况下，这将包括 CElement 类以及从它派生的形状类——它们必须能够将自身写入文件。这意味着要使一个类可序列化，用于声明该类数据成员的所有类类型也必须可序列化。

## Serializing a Document

所有这些听起来相当棘手，但序列化文档的基本功能已在应用程序一开始就由 Application  wizard 构建到应用程序中。File > Save、File > Save As 和 File > Open 菜单项的处理程序都假定你希望为文档实现序列化，并且已经包含支持它的代码。查看 CSketcherDoc 的定义和实现中与使用序列化创建文档相关的部分。

## Serialization in the Document Class Definition

使文档对象可序列化的 CSketcherDoc 定义中的代码在以下片段中以阴影显示：

```
class CSketcherDoc : public CDocument
{
protected: // create from serialization only
    CSketcherDoc();
    DECLARE_DYNCREATE(CSketcherDoc)

// Rest of the class...

// Overrides
public:
    virtual BOOL OnNewDocument();
    virtual void Serialize(CArchive& ar);

// Rest of the class...
};
```

这里有三件事与序列化文档对象相关：

- 1. DECLARE_DYNCREATE() 宏。
- 2. Serialize() 成员函数。
- 3. 默认类构造函数。

DECLARE_DYNCREATE() 是一个宏，使 CSketcherDoc 类的对象能够在序列化输入过程中由应用程序框架动态创建。它与类实现中的一个互补宏 IMPLEMENT_DYNCREATE() 相对应。这些宏仅适用于派生自 CObject 的类，但正如你很快会看到的，它们并不是在此上下文中可用的唯一一对宏。对于任何你想要序列化的类，CObject 必须是直接或间接的基类，因为它添加了使序列化工作成为可能的功 能。这就是为什么 CElement 类派生自 CObject 的原因。几乎所有 MFC 类都派生自 CObject，因此是可序列化的。

> Visual C++ 2005 的 Microsoft Foundation Class Reference 中的层次结构图显示了未派生自 CObject 的类。请注意，CArchive 在此列表中。

类定义还包括对虚拟函数 Serialize() 的声明。每个可序列化的类都必须包含此函数。它用于对类的成员数据执行输入和输出序列化操作。传递给此函数的 CArchive 类型对象的参数决定了要执行的操作是输入还是输出。你将在考虑文档类的序列化实现时更详细地探讨这一点。

请注意，类显式定义了默认构造函数。这对于序列化工作也是必不可少的，因为默认构造函数由框架用于在从文件读取时合成对象，然后合成的对象用文件中的数据填充以设置对象数据成员的值。

## Serialization in the Document Class Implementation

CSketcherDoc 实现的文件中有两个部分与序列化相关。第一个是与 DECLARE_DYNCREATE() 宏互补的宏 IMPLEMENT_DYNCREATE()：

```
// SketcherDoc.cpp : implementation of the CSketcherDoc class
//

#include "stdafx.h"
#include "Sketcher.h"
#include "PenDialog.h"

#include "SketcherDoc.h"

#ifdef _DEBUG
#define new DEBUG_NEW
#endif

// CSketcherDoc

IMPLEMENT_DYNCREATE(CSketcherDoc, CDocument)

// Message maps and the rest of the file...
```

此宏所做的全部工作就是将 CSketcherDoc 的基类定义为 CDocument。这对于 CSketcherDoc 对象的正确动态创建是必需的，包括从基类继承的成员。

## The Serialize() Function

类实现还包括 Serialize() 函数的定义：

```
void CSketcherDoc::Serialize(CArchive& ar)
{
    if (ar.IsStoring())
    {
        // TODO: add storing code here
    }
    else
    {
        // TODO: add loading code here
    }
}
```

此函数序列化类的成员数据。传递给函数的参数是对 CArchive 类对象 ar 的引用。此类对象的 IsStoring() 成员如果操作是要将成员数据存储到文件中则返回 TRUE，如果操作是要从先前存储的文档中读取回成员数据则返回 FALSE。

由于 Application wizard 不知道你的文档包含什么数据，因此写入和读取此信息的过程由你决定，如注释所示。要了解这是如何完成的，请更仔细地查看 CArchive 类。

## The CArchive Class

CArchive 类是驱动序列化机制的引擎。它提供了 MFC 基于的 C++ 流操作的等价物，你在控制台程序示例中使用它从键盘读取和向屏幕写入。一个 MFC CArchive 对象提供了一种机制，将你的对象流式传输到文件，或再次作为输入流恢复，在此过程中自动重建你的类的对象。

CArchive 对象有一个与其关联的 CFile 对象，该对象为二进制文件提供磁盘输入/输出功能，并提供与物理文件的实际连接。在序列化过程中，CFile 对象负责所有文件输入和输出操作的细节，而 CArchive 对象处理要写入的对象数据的结构化逻辑或从读取的信息重建对象。你只需要担心关联的 CFile 对象的细节，如果你正在构建自己的 CArchive 对象。与 Sketcher 中的文档，框架已经处理了它并将它构造的 CArchive 对象 ar 传递给 CSketcherDoc 中的 Serialize() 函数。当你为形状类实现序列化时，你将能够在添加到形状类的每个 Serialize() 函数中使用相同的对象。

CArchive 类重载了提取和插入运算符（>> 和 <<），分别用于派生自 CObject 的类对象以及一系列基本数据类型上的输入和输出操作。这些重载运算符适用于以下对象类型和原始类型：

