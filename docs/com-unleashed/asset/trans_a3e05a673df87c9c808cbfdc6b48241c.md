
```cpp
// retrieve catalog collection for transient subscriptions
hr = pAdminCatalog->GetCollection(bstrCatalogName,
                                   (IDispatch**)&pCatalogCollection);

// free bstr
::SysFreeString(bstrCatalogName);

if (SUCCEEDED(hr))
{
    ICatalogObject* pCatalogObject;

    // get new, initialized catalog object (not in catalog yet!)
    hr = pCatalogCollection->Add((IDispatch**)&pCatalogObject);
    if (SUCCEEDED(hr))
    {
        // use the pCatalogObject->put_Value to set the
        // subscription values

        // when finished setting values, release catalog object
        pCatalogObject->Release();

        // save object into COM+ catalog
        LONG lResult;
        hr = pCatalogCollection->SaveChanges(&lResult);

        // check lResult for success
    }
}
pCatalogCollection->Release();
}
```

## 注销临时订阅

既然你已经了解了如何注册临时订阅，接下来我将演示如何注销临时订阅。尽管部分准备工作（例如实例化 COMAdminCatalog 对象和获取 ICatalogCollection 接口）是相同的，但差异足够多，因此有必要查看一段 Visual C++ 代码（清单 26.3），了解如何以编程方式完成此操作。

### 清单 26.3（续）

```cpp
HRESULT hr;
ICOMAdminCatalog* pAdminCatalog;

// retrieve the COM+ catalog object
hr = ::CoCreateInstance(CLSID_COMAdminCatalog, NULL,
                        CLSCTX_SERVER,
                        IID_ICOMAdminCatalog,
                        (void**)&pAdminCatalog);

if (SUCCEEDED(hr))
{
    ICatalogCollection* pCatalogCollection;

    // allocate bstr for catalog name
    BSTR bstrCatalogName = ::SysAllocString(L"TransientSubscriptions");

    // retrieve catalog collection for transient subscriptions
    hr = pAdminCatalog->GetCollection(bstrCatalogName,
                                       (IDispatch**)&pCatalogCollection);

    // free bstr
    ::SysFreeString(bstrCatalogName);

    if (SUCCEEDED(hr))
    {
        // fill out collection
        hr = pCatalogCollection->Populate();

        if (SUCCEEDED(hr))
        {
            IEnumVARIANT* pEnumVariant;
            hr = pCatalogCollection->_get_NewEnum((IUnknown**)&pEnumVariant);

            if (SUCCEEDED(hr))
            {
                VARIANT var;
                VariantInit(&var);
                int nIdx = 0;

                while (S_OK == pEnumVariant->Next(1, &var, NULL))
                {
                    ICatalogObject* pCatalogObject =
                        (ICatalogObject*)var.pdispVal;
                    if (/* compare to name you want to remove */)
                    {
                        hr = pCatalogCollection->Remove(nIdx);
                        if (SUCCEEDED(hr))
                        {
                            long lResult;
                            pCatalogCollection->SaveChanges(&lResult);
                        }
                    }

                    VariantClear(&var);
                    break;
                }
            }
        }
    }
}
```

**图 26.13**  
使用“筛选器组件服务”，可以为给定订阅定义单个筛选器。不过，大多数情况下这并不太实用，因为筛选器通常是动态的。

![](img/112c2326f49d26b8d59aa054e14c5747_741_0.png)

至此，选项已经相当明显。只需为筛选器命名，然后使用一个属性和有效值作为名称/值对来指定所需的筛选器。一个简单示例是希望获取编号为“1234”的 SKU 的库存更新，如下所示：

```
bstrSKU="1234"
```

你可能永远不会想筛选细到单个 SKU 这样的内容。不过，某个特定的“建议购买”组件可能希望按特定类别的 SKU 进行筛选。例如，在汽车零部件分销系统中，你可能会有针对整类零部件的多个订阅，例如“玻璃”、“车身”和“机械”。显然，从这一点来看，如何筛选的具体选择在很大程度上取决于具体应用。但是，请记住，你可以使用标准布尔运算符（列于表 26.2）来帮助定义系统的筛选器字符串。

**表 26.2 筛选器语法**

| 运算符 | 含义 |
|---|---|
| `=`, `==` | 等于 |
| `!=`, `~=`, `<>` | 不等于 |
| `&` | 布尔“AND” |
| `\|` | 布尔“OR” |
| `!`, `~` | 布尔“NOT” |

## 以编程方式创建筛选器字符串

既然你已经了解了如何使用组件服务创建筛选器字符串，接下来我将演示如何使用 Visual C++ 和 COM+ 事件服务管理接口执行同样的任务（见清单 26.4）。该应用程序位于名为 FilterStringVC 的 CD-ROM 文件夹中（Visual Basic 替代版本位于 FilterStringVB 中）。我们再次筛选 SKU 为“1234”的零部件。

### 清单 26.4 以编程方式创建事件筛选器字符串

```cpp
HRESULT hr;
ICOMAdminCatalog* pAdminCatalog;

// retrieve the COM+ catalog object
hr = ::CoCreateInstance(CLSID_COMAdminCatalog, NULL,
                        CLSCTX_SERVER,
                        IID_ICOMAdminCatalog,
                        (void**)&pAdminCatalog);

if (SUCCEEDED(hr))
{
    ICatalogCollection* pCatalogCollection;

    // allocate bstr for catalog name
    BSTR bstrCatalogName = ::SysAllocString(L"TransientSubscriptions");

    // retrieve catalog collection for transient subscriptions
    hr = pAdminCatalog->GetCollection(bstrCatalogName,
                                      (IDispatch**)&pCatalogCollection);

    // free bstr
    ::SysFreeString(bstrCatalogName);

    if (SUCCEEDED(hr))
    {
        BSTR bstrPropName = ::SysAllocString(L"FilterCriteria");

        // notice the handling of the quotes for an embedded string
        BSTR bstrValue = ::SysAllocString(L"bstrSKU=\"1234\"");

        VARIANT var;
        var.vt = VT_BSTR;
        var.bstrVal = bstrValue;

        hr = pCatalogCollection->put_Value(bstrPropName, var);
        // check for success

        ::SysFreeString(bstrValue);
        ::SysFreeString(bstrPropName);
    }
}
```

## 小结

本章中，你了解了 COM+ 如何通过松耦合事件和事件服务解决事件通知问题。在学习事件服务架构中发布者和订阅者组件的角色之后，你看到了一个触发事件的简单应用程序，以及另一个接收该事件触发通知的应用程序。之后，你了解了 COM+ 事件服务的一些更高级问题，例如处理 IEventSubscription 接口，以及使用 COM+ 事件服务管理接口注册和注销临时订阅。最后，你学习了如何以编程方式筛选订阅者传入的事件。至此，你已经学到了不少关于在 COM+ 下使用异步事件处理的知识，希望这些信息能帮助你编写更具动态性、分布式的应用程序。

## 第 27 章：队列组件

### 本章内容

- 队列组件概述 *722*
- 分布式计算与队列组件 *723*
- 队列组件架构 *727*
- 编写队列组件演示应用程序 *731*
- 测试组件和客户端代码 *748*
- 导出 COM+ 应用程序 *749*

本章分为四节，以便更容易学习队列组件，并让读者能够灵活跳转到对自己有意义的章节。第一节概述队列组件的目的；第二节介绍分布式计算的概念及其与队列组件的关系。这一节之所以放在描述队列组件的章节之前，是出于实用性的考虑。就我而言，我无法忍受读了好几页某技术有多棒，结果在列出限制之后才发现我的应用程序并不适合实现它。因此，即使你熟悉分布式计算的概念（特别是关于 MTS 和 MSMQ），我也建议你阅读这一节。

在决定队列组件是否适合你的应用程序之后，第三节将介绍并探讨队列组件架构。最后，在本章的第四节也是最后一节中，你将运用新学到的知识编写服务器端组件和客户端应用程序，对其进行测试，然后导出 COM+ 应用程序以便分发到客户端计算机。

> **注意**
> 
> 许多开发者想尽快进入代码。毕竟，我们工作的主要职责之一就是评估不同的技术和编程技巧，并决定它们是否适用于某个特定应用程序。有时我们根本没有时间阅读某项技术的所有复杂细节，而是想先测试它，再决定是否值得进一步研究其内部工作原理。因此，对于那些手痒难耐的人，我建议先阅读第二节（“分布式计算与队列组件”），然后直接进入第四节的演示应用程序。这样，你可以立即看到使用队列组件实现组件和客户端应用程序是多么容易。完成之后，你可以再回到第三节（“队列组件架构”），确切了解“幕后”发生了什么。

## 队列组件概述

十年前，全职奔波于户外、拜访客户、供应商和供货商的销售人员已经习惯这样一个事实：他们所做的任何工作都必须在回到酒店后“上传”。实际上，那些人还算先进，因为他们至少可以在路上通信。在那个年代，
