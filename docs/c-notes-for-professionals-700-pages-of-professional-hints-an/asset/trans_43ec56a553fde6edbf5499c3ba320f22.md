
```csharp
// Tell WCF to use JSON encoding rather than default XML
var webBodyFormatMessageProperty = new
WebBodyFormatMessageProperty(WebContentFormat.Json);
fault.Properties.Add(WebBodyFormatMessageProperty.Name, webBodyFormatMessageProperty);

} // end

} // end class

} // end namespace
```

在此示例中，我们将处理程序附加到服务行为。你也可以用类似方式将其附加到 IEndpointBehavior、IContractBehavior 或 IOperationBehavior。

### 附加到服务行为：

```csharp
using System;
using System.Collections.ObjectModel;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Configuration;
using System.ServiceModel.Description;
using System.ServiceModel.Dispatcher;

namespace BehaviorsAndInspectors
{
    public class ErrorHandlerExtension : BehaviorExtensionElement, IServiceBehavior
    {
        public override Type BehaviorType
        {
            get { return GetType(); }
        }

        protected override object CreateBehavior()
        {
            return this;
        }

        private IErrorHandler GetInstance()
        {
            return new ErrorHandler();
        }

        void IServiceBehavior.AddBindingParameters(ServiceDescription serviceDescription,
ServiceHostBase serviceHostBase, Collection<ServiceEndpoint> endpoints, BindingParameterCollection
bindingParameters) { } // end

        void IServiceBehavior.ApplyDispatchBehavior(ServiceDescription serviceDescription,
ServiceHostBase serviceHostBase)
        {
            var errorHandlerInstance = GetInstance();

            foreach (ChannelDispatcher dispatcher in serviceHostBase.ChannelDispatchers)
            {
                dispatcher.ErrorHandlers.Add(errorHandlerInstance);
            }
        }

        void IServiceBehavior.Validate(ServiceDescription serviceDescription, ServiceHostBase
serviceHostBase) { } // end

} // end class

} // end namespace
```

Web.config 中的配置：

```
...
<system.serviceModel>
    <services>
        <service name="WebServices.MyService">
            <endpoint binding="webHttpBinding" contract="WebServices.IMyService" />
        </service>
    </services>
    <extensions>
        <behaviorExtensions>
            <!-- This extension if for the WCF Error Handling-->
            <add name="ErrorHandlerBehavior" type="WebServices.BehaviorsAndInspectors.ErrorHandlerExtensionBehavior, WebServices, Version=1.0.0, Culture=neutral, PublicKeyToken=null" />
        </behaviorExtensions>
    </extensions>
    <behaviors>
        <serviceBehaviors>
            <behavior>
                <serviceMetadata httpGetEnabled="true"/>
                <serviceDebug includeExceptionDetailInFaults="true"/>
                <ErrorHandlerBehavior />
            </behavior>
        </serviceBehaviors>
    </behaviors>
</system.serviceModel>
...
```

以下是几个可能对该主题有帮助的链接：

https://msdn.microsoft.com/en-us/library/system.servicemodel.dispatcher.ierrorhandler(v=vs.100).aspx

http://www.brainthud.com/cards/5218/25441/which-four-behavior-interfaces-exist-for-interacting-with-a-service-or-client-description-what-methods-do-they-implement-and

其他示例：

当 HTTP 状态码为 401 Unauthorized 时，IErrorHandler 返回了错误的消息正文

IErrorHandler 似乎没有在 WCF 中处理我的错误……有什么想法吗？

如何让自定义 WCF 错误处理程序返回带有非 OK HTTP 状态码的 JSON 响应？

如何为 HttpClient 请求设置 Content-Type 标头？

### 第76.11节：使用异常对象

你可以在自己的代码中创建并抛出异常。实例化异常的方式与任何其他 C# 对象相同。

```
Exception ex = new Exception();

// constructor with an overload that takes a message string
Exception ex = new Exception("Error message");
```

然后可以使用 throw 关键字来引发异常：

```
try
{
    throw new Exception("Error");
}
catch (Exception ex)
{
    Console.Write(ex.Message); // Logs 'Error' to the output window
}
```

注意：如果你在 catch 块内抛出新异常，请确保将原始异常作为“内部异常”传入，例如：

```
void DoSomething()
{
    int b=1; int c=5;
    try
    {
        var a = 1;
        b = a - 1;
        c = a / b;
        a = a / c;
    }
    catch (DivideByZeroException dEx) when (b==0)
    {
        // we're throwing the same kind of exception
        throw new DivideByZeroException("Cannot divide by b because it is zero", dEx);
    }
    catch (DivideByZeroException dEx) when (c==0)
    {
        // we're throwing the same kind of exception
        throw new DivideByZeroException("Cannot divide by c because it is zero", dEx);
    }
}

void Main()
{
    try
    {
        DoSomething();
    }
    catch (Exception ex)
    {
        // Logs full error information (incl. inner exception)
        Console.Write(ex.ToString());
    }
}
```

在这种情况下，假定该异常无法被处理，但会在消息中添加一些有用信息（并且外部异常块仍可通过 ex.InnerException 访问原始异常）。

它将显示类似如下内容：

```
System.DivideByZeroException: Cannot divide by b because it is zero ---> System.DivideByZeroException:
Attempted to divide by zero.
 at UserQuery.g__DoSomething0_0() in C:[...]\LINQPadQuery.cs:line 36
--- End of inner exception stack trace ---
 at UserQuery.g__DoSomething0_0() in C:[...]\LINQPadQuery.cs:line 42
 at UserQuery.Main() in C:[...]\LINQPadQuery.cs:line 55
```

如果你在 LinqPad 中尝试此示例，你会注意到行号并不太有意义（它们并不总能帮到你）。但如上所述传入有帮助的错误文本，通常能显著减少定位错误位置所需的时间，在本示例中，错误显然位于以下行

```
c = a / b;
```

在 DoSomething() 函数中。

[在 .NET Fiddle 中试试](https://dotnetfiddle.net)

### 第76.12节：异常的嵌套与 try catch 块

可以将一个异常/try catch 块嵌套在另一个异常/try catch 块中。

这样，你就可以管理小型代码块，使它们能够正常工作而不会破坏整个机制。

```
try
{
//some code here
    try
    {
        //some thing which throws an exception. For Eg : divide by 0
    }
    catch (DivideByZeroException dzEx)
    {
        //handle here only this exception
        //throw from here will be passed on to the parent catch block
    }
    finally
    {
        //any thing to do after it is done.
    }
    //resume from here & proceed as normal;
}
catch(Exception e)
{
    //handle here
}
```

**注意：** 在向父 catch 块抛出异常时，避免吞掉异常

## 第77章：NullReferenceException

### 第77.1节：NullReferenceException 详解

当你尝试访问引用对象的非静态成员（属性、方法、字段或事件）而该对象为 null 时，就会抛出 NullReferenceException。

```
Car myFirstCar = new Car();
Car mySecondCar = null;
Color myFirstColor = myFirstCar.Color; // No problem as myFirstCar exists / is not null
Color mySecondColor = mySecondCar.Color; // Throws a NullReferenceException
// as mySecondCar is null and yet we try to access its color.
```

要调试此类异常相当容易：在抛出异常的那一行，你只需查看每个“.”或“[”之前；少数情况下查看“(”之前。

```
myGarage.CarCollection[currentIndex.Value].Color = theCarInTheStreet.Color;
```

我的异常来自哪里？可能是以下之一：

- myGarage 为 null
- myGarage.CarCollection 为 null
- currentIndex 为 null
- myGarage.CarCollection[currentIndex.Value] 为 null
- theCarInTheStreet 为 null

在调试模式下，你只需将鼠标光标放在这些元素中的每一个上，就能找到空引用。然后，你只需弄清楚它为什么没有值。修正方式完全取决于你的方法的目标。

你是否忘记实例化/初始化它了？

```
myGarage.CarCollection = new Car[10];
```

如果对象为 null，你是否应该做其他事情？

```
if (myGarage == null)
{
    Console.WriteLine("Maybe you should buy a garage first!");
}
```

或者也许有人给了你一个 null 参数，而本不应如此：

```
if (theCarInTheStreet == null)
{
    throw new ArgumentNullException("theCarInTheStreet");
}
```

无论如何，请记住方法绝不应抛出 NullReferenceException。如果抛出了，就意味着你忘记检查某些内容。

