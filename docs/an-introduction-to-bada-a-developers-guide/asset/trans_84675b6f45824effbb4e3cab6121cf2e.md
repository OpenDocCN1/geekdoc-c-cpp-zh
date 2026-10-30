
// 逐个获取 IpAddress
IpAddress* pIpAddress = static_cast<IpAddress*>(
    (addressList->GetAt(index));
)
    strTemp += pIpAddress->ToString() + L"\n";
}

// 获取域名的别名列表。
IList* aliasList = ipHostEntry->GetAliasList();

if (aliasList != null)
{
    // 获取别名列表中 IpAddress 对象的数量
    int count = aliasList->GetCount();
    strTemp += L"ALIAS:\n";
    for (int index = 0; index < count; index++)
    {
        // 逐个获取别名
        String* alias = static_cast<String*>(
            (aliasList->GetAt(index));
        strTemp += (*alias) + L"\n";
    }
    if (pLabelHostDetails)
    {
        pLabelHostDetails->SetText(strTemp);
        pLabelHostDetails->Draw();
        pLabelHostDetails->Show();
    }
    delete ipHostEntry;
}
else
{
    AppLog(GetErrorMessage(r));
}

此回调函数的第一个参数是 IpHostEntry。该参数将 DNS 主机名与别名列表和匹配的 IP 地址列表关联起来。要获取 IP 地址列表，需要调用 GetAddressList() 函数；要获取别名列表请调用 GetAliasList() 函数。
我们在 Form 的 OnInitializing 方法中创建 Dns 对象，并将表单添加为监听器。

// 创建 Dns 对象
pDns = new Dns();
// 注册 Dns 事件监听器
pDns->Construct(*this);

要按名称获取主机，请调用 Dns 类的 GetHostByName() 函数。此函数以 String 作为参数。
要按 IP 获取主机，请调用 Dns 类的 GetHostByAddress() 函数。此函数以 IpAddress 作为参数。

下面的代码展示了如何调用这些函数来获取主机信息。

```
void
FormDns::DnsRequestIP(String hostName)
{
    result r = pDns->GetHostByName(hostName);
    if (IsFailed(r))
    {
        AppLog("GetHostByName Failed.");
    }
}
void
FormDns::DnsRequestHostName(Ip4Address& ipAddress)
{
    result r = pDns->GetHostByAddress(ipAddress);
    if (IsFailed(r))
    {
        AppLog("GetHostByAddress Failed.");
    }
}
```

最后，为了清理，在 OnTerminating() 函数中删除 Dns 实例。

```
delete pDns;
pDns = null;
```

## Maps and Location

## 6.1 Get Geographic Data from a Provider and Show a Map

### Problem Description

你想获取地理信息并以地图形式在 bada 设备上显示。

### The Recipe

需要以下配置。

使用的命名空间：
Osp::Locations::Services, Osp::Locations::Controls, Osp::Graphics

需要 #include 的头文件：
FLocations.h

所需库：
FLocations, LocationControls

所需权限级别：
Normal

所需权限组：
LOCATION, LOCATION_SERVICE

命名空间 Osp::Locations::Services 提供了开发人员可以利用的许多有用服务。我们将介绍的一个基本服务是封装在 IMapServiceProvider 接口中的服务。

本配方中使用的另一个命名空间是 Osp::Locations::Controls，它允许用户平移、缩放并按通常预期与地图交互。

我们简单展示如何在屏幕上显示地图。我们的示例代码展示了 C++ 源文件及其对应头文件的片段，我们将其命名为 MapVisualisation.cpp（涵盖将地理数据作为地图呈现的代码）。

为了能够显示地图，我们需要访问地理数据提供者。对于此示例，我们使用 deCarta 作为地图提供者。你可以在 deCarta 网站（developer.decar ta.com）注册并免费申请一个密钥。

获得密钥后，你可以通过创建地图提供者对象将你的 deCarta 账户链接到应用程序中。我们在 MapVisualisation 类中执行此操作。

// 为提供者定义一个名称
String providerName = L"deCarta";

// 为 deCarta 设置地图密钥（将 XXX/YYY 替换为你的用户名/密码）
static const String extraInfo = L"ClientName=XXX;ClientPassword=YYY;"
"HostUrl=http://developer.kr.dz.decarta.com:80/openls/openls";

// 创建地图提供者
IMapServiceProvider* pProvider = static_cast<IMapServiceProvider*>(
ProviderManager::ConnectToServiceProviderN(L"deCarta",
LOC_SVC_PROVIDER_TYPE_MAP, extraInfo));

## 6.2 React to Location Changes

### Problem Description

你想对位置变化做出反应，并在该地图上显示用户当前位置。本配方与配方“从提供者获取地理数据并显示地图”相关。

### The Recipe

需要以下配置。

使用的命名空间：
Osp::Locations, Osp::Graphics, Osp::Locations::Services

需要 #include 的头文件：
FLocations.h

所需库：
FLocations

所需权限级别：
Normal

所需权限组：
LOCATION, LOCATION_SERVICE

命名空间 Osp::Locations 包含其他类，其中包括 LocationProvider 和 Location，我们将在配方中使用它们。使用 LocationProvider 类可以定义你希望从何处获取位置（例如来自 GPS 传感器）。该类还实现了 ILocationListener 接口，可提供位置更新信息。表示位置信息的类 Location 是 LocationProvider 的一部分。我们展示如何显示地图，并在其上叠加显示用户当前位置。

除了来自配方“从提供者获取地理数据并显示地图”的 MapVisualisation.cpp 之外，我们的示例代码还展示了另一个 C++ 源文件的片段，我们将其命名为 MapInteraction.cpp

一旦我们建立了对 deCarta 等地理信息提供者的访问并初始化了地图，我们就可以开始从设备获取位置信息。为此，我们切换到 MapInteraction 类。我们创建

并通过添加位置源来构造一个 LocationProvider。我们使用 GPS 接收器。在此你还可以配置更新速率，我们在 RequestLocationUpdate() 方法中将其设置为 5 秒。

// 创建一个 LocationProvider
LocationProvider *locProvider = new LocationProvider();

// 通过使用 GPS 和 WPS（Wi-Fi 定位系统）作为定位机制来构造 LocationProvider
locProvider->Construct(LOC_METHOD_HYBRID);

// 配置更新的时间间隔
locProvider->RequestLocationUpdates(*this, 5, false);

要接收位置更新，你需要重写 OnLocationUpdated() 方法，该方法在 ILocationListener 接口中声明。

// 当接收到位置事件时被调用
void
MapInteraction::OnLocationUpdated(Location& location)
{
    if(location.GetQualifiedCoordinates() != null)
    {
        const QualifiedCoordinates *q = location.GetQualifiedCoordinates();

        // 经纬度值
        double longitude = q->GetLongitude();
        double latitude = q->GetLatitude();

        // 将地图居中于这些新值
        pFormMap->SetCenter(latitude, longitude, true);

        // 重新绘制并显示地图
        pFormMap->Draw();
        pFormMap->Show();
    }
}

### Hints, Pitfalls, and Related Topics

一旦你的代码编译无误，你就可以在模拟器中运行它。bada 模拟器非常方便的一个功能是事件注入器工具。要获取它，请右键单击模拟器屏幕，选择事件注入器，然后选择位置选项卡。你可以在地图上拖放指针，或直接输入经纬度值，如图 R6.1 所示。这些值随后将作为事件发送到在 bada 模拟器上运行的应用程序。此工具对于测试非常有用。

![](img/a257d5fd53a79a244a20e587cd2f08f6_439_0.png)

图 R6.1 IDE 中正在运行的事件注入器。

## 7.1 Create Content on the bada Server

### Problem Description

你想为 bada 服务器创建内容并将其传输到 Amazon S3 工作区。

### The Recipe

本配方需要以下配置：

使用的命名空间：
Osp::Content

需要 #include 的头文件：
FContent.h

所需库：
FContent.lib

所需权限级别：
System

所需权限组：
REMOTE_CONTENT, CONTENT_TRANSFER

