
表19.3列出了ServiceContractAttribute属性的属性：

**表19.3：展示ServiceContractAttribute属性的属性**

| 属性 | 说明 |
|---|---|
| `ConfigurationName` | 定义配置文件中服务配置的名称。 |
| `CallbackContract` | 定义当服务用于双工消息传递时在客户端实现的协定。 |
| `Name` | 定义Web服务描述语言（WSDL）中`<portType>`元素的名称。 |
| `Namespace` | 定义WSDL中`<portType>`元素的XML命名空间。 |
| `SessionMode` | 指定调用服务协定的操作是否需要会话。此属性的可能值为`Allowed`、`NotAllowed`和`Required`。 |
| `ProtectionLevel` | 定义绑定是否保护通信。此属性的可能值为`None`、`Sign`和`EncryptAndSign`。 |

服务协定包括以下两个组件：

- 操作协定
- 数据协定

让我们逐一详细讨论这些内容。

## 操作协定

操作协定定义了应暴露给外部客户端的方法。它提供了OperationContractAttribute属性，用于标记作为服务协定组成部分的每个方法。表19.4描述了OperationContractAttribute属性的属性：

**表19.4：展示OperationContractAttribute属性的属性**

| 属性 | 说明 |
|---|---|
| `Action` | 指定唯一标识操作的操作，并根据操作将请求消息分派到相应的方法。 |
| `ReplyAction` | 设置回复消息的操作名称。 |
| `AsyncPattern` | 指示操作是异步实现的，或者可以使用Begin/End方法对异步调用。 |
| `IsInitiating` | 从一系列操作中启动一个操作。启动操作会开始一个新会话；而…… |
| `IsTerminating` | 从一系列操作中终止一个操作。服务器通过终止操作结束会话。 |
| `IsOneWay` | 允许客户端不等待回复消息。客户端没有直接方法确保请求是否正确发送。 |
| `Name` | 定义操作的名称。 |
| `ProtectionLevel` | 指定消息应签名、加密，还是两者皆需。 |

清单19.2展示了一个定义服务协定的示例，该协定应用了ServiceContractAttribute和OperationContractAttribute属性：

```
清单19.2：展示将ServiceContractAttribute和OperationContractAttribute属性应用于服务协定的代码

[ServiceContract]
public interface IService
{
```

```
// 由于参数和返回类型都是基元类型，因此不需要数据协定。
[OperationContract]
double Area(int area);
// 由于参数和返回类型都标记有SerializableAttribute属性，因此不需要数据协定。
[OperationContract]
System.Drawing.Bitmap GetImage(System.Uri pictureUri);
// MyComplexTypes.ReservationForm 是一个复杂类型，
// 因此需要数据协定。
[OperationContract]
bool ApproveReservationForm(MyComplexTypes.ReservationForm rf);
}
```

## 数据协定

数据协定是客户端与服务之间的一种约定，在概念上描述了要交换的数据。客户端与服务之间的通信不需要相同的类型，但需要相同的数据协定。与服务协定只能处理简单类型不同，数据协定可以处理复杂类型。这意味着数据协定可以处理复杂的服务调用；即具有复杂类型参数并返回复杂类型值的调用。

在WCF中，服务协定通过接口定义，而数据协定通过类定义。这些类以DataContractAttribute属性为前缀，其成员以DataMemberAttribute属性为前缀。

清单19.3展示了如何在应用程序中应用DataContractAttribute和DataMemberAttribute属性来创建MyComplexTypes.ReservationForm类型：

### 清单19.3：展示应用DataContractAttribute和DataMemberAttribute属性的代码

```
namespace MyComplexTypes
{
    [DataContract]
    public class ReservationForm
    {
        private int rfid_value;
        // 将[DataMember]属性应用于该属性。
        [DataMember]
        public int ReservationFormId
        {
            get { return rfid_value; }
            set { rfid_value = value; }
        }
    }
}
```

## 行为

行为用于自定义服务终结点的运行时行为。它们还允许你向服务添加自定义扩展，以检查和验证服务配置，或修改应用程序的运行时行为。你可以通过配置文件或为其提供的属性将行为应用于WCF服务。以下是WCF服务使用的行为列表：

- 服务行为——在服务实现（类）级别标识服务范围的实现行为。你不能在协定（接口）级别应用此属性。
- 协定行为——实现IContractBehavior接口以扩展客户端和服务的运行时。
- 终结点行为——实现IEndpointBehavior接口以修改特定终结点的服务或客户端运行时。
- 操作行为——实现IOperationBehavior接口以扩展客户端和服务对操作的运行时。

## WCF服务的配置

你可以使用配置文件配置WCF服务，这些文件以XML格式包含WCF服务的配置信息。这些文件中的XML元素允许你逐机修改配置细节，例如WCF服务的终结点地址。WCF还包含一些系统定义的元素，使你能够快速选择WCF服务最基本的功能。部署WCF服务时，配置文件为你呈现终结点和服务行为数据提供了灵活性。你可以使用web.config文件或WCF配置编辑器工具更改WCF服务的配置。

## 使用web.config文件

你可以使用web.config或app.config文件来配置WCF服务。选择哪种配置文件（web.config或app.config）来配置WCF服务取决于你为WCF服务选择的主机环境。如果你的主机环境是IIS，则可以使用web.config文件；如果主机环境不是IIS，则使用app.config文件。清单19.4展示了web.config文件的主要元素：

### 清单19.4：展示web.config文件的主要元素

```
<system.serviceModel>
  <services>
    <service>
      <endpoint/>
    </service>
    <service>
      <endpoint/>
    </service>
  </services>
  <bindings>
    <binding>
      <!--系统提供的绑定或自定义绑定-->
    </binding>
    <binding>
      <!--系统提供的绑定或自定义绑定-->
    </binding>
  </bindings>
  <behaviors>
    <behavior>
      <!--系统提供的行为或自定义行为-->
    </behavior>
    <behavior>
      <!--系统提供的行为或自定义行为-->
    </behavior>
  </behaviors>
</system.serviceModel>
```

**注意**

<bindings>和<behaviors>元素是可选的。

WCF的web.config文件包含以下元素：

- <Service>
- <endpoints>
- <binding>
- <behaviors>

让我们详细讨论这些元素。

## <service>元素

<service>元素包含应用程序托管的所有服务的规范。它由以下两个属性组成：

- name——指示提供服务协定实现的类型。它是命名空间和类型名称的组合。
- behaviorConfiguration——指示<behaviors>元素中找到的某个<behavior>元素的名称。

## <endpoint>元素

<endpoint>元素包含以下属性：

- address——指示服务的URI，可以是绝对地址或相对地址。
- Binding——指示系统提供的绑定，例如WSDualHttpBinding，但也可以指定用户定义的绑定。指定的绑定决定使用的传输协议、安全性和编码格式。
- bindingConfiguration——包含一个字符串，表示绑定的绑定名称，在创建终结点实例时使用。
- Contract——通过<service>元素的name属性指示描述协定的接口。

## <bindings>元素

<bindings>元素包含任何服务中定义的终结点可以使用的所有绑定的规范。它包含一个或多个具有name属性的<binding>元素。该属性将绑定与<endpoint>元素的bindingConfiguration属性中指定的终结点关联起来。

## <behaviors>元素

<behaviors>元素充当一个或多个<behavior>元素的容器元素，这些元素描述服务的行为。每个<behavior>元素包含一个name属性，该属性定义系统提供的行为或自定义行为。

## 使用WCF配置编辑器工具

WCF配置编辑器工具名为Microsoft Service Configuration Editor，允许你创建或修改WCF服务的配置设置。它是一个图形工具，可用于管理WCF绑定、行为和服务设置。与手动修改配置文件相比，使用Microsoft Service Configuration Editor修改或设置WCF服务的配置信息可以节省大量时间。Microsoft Service Configuration Editor工具的界面如图19.6所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1009_0.png)

图19.6：展示Microsoft Service Configuration Editor工具

