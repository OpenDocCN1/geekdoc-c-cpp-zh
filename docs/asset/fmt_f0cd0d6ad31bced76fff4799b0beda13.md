
## 限制区域

你还应该理解范围从何时开始，何时结束。这会让你的程序更有连贯性，并帮助你理解需要做什么。这就像了解周围发生了什么，这样你就可以轻松处理它们。除非你在处理大型 DOM 应用，否则这通常不是问题。`ng-repeat` 指令对于这一点至关重要。

为此，你可以遵循以下代码：

```html
<div ng-app="TheFirstApp" ng-controller="myCtrl">
  <ul>
    <li ng-repeat="x in items">{{x}}</li>
  </ul>
</div>
<script>
var app = angular.module('TheFirstApp', []);
app.controller('myCtrl', function($scope) {
  $scope.items = ["Apple", "Banana", "Cherry"];
});
</script>
```

## 方法

在 Java 编程中，范围（Scopes）等同于参数。发生这种情况是因为范围绑定了 JavaScript 和 HTML 元素，这意味着在某些时刻，也会出现某种形式的冲突。

范围具有可用的的方法和能力，并且对控制器和视图都可用。视图描绘 HTML，而控制器是 JavaScript——后者负责控制、编辑或删除数据。

范围也是具有属性（Properties）和方法的模型，供用户使用。这意味着当发生更改时，控制器和视图都会受到影响——并被更新。

## 源代码

编写此代码，请使用以下内容：

```cpp
#include <netinet/in.h>
#include <arpa/inet.h>
#include <string>
#include <iostream>

class JavaStream {
public:
    JavaStream(int sd, struct sockaddr_in* address);
    ~JavaStream();
    std::string getPeerIP();
    int getPeerPort();

private:
    int m_sd;
    std::string m_peerIP;
    int m_peerPort;
};
```

# 第 8 章 封装、继承与多态

Java 元素也有助于确定你的程序如何被编辑，以及在他人看来它是是什么样的。这些元素还涵盖了程序的深度——或者说它的核心。你可以在下方学习更多信息：

## 封装

首先是封装，它利用一些原则来很好执行。**这些原则是：**

1. **健壮性原则。** 这意味着协议必须实现，但发送行为应该是保守的，而接收行为应该是宽容的。这意味着在发送/接收数据报时必须非常小心。这意味着即使某些软件有缺陷，确保你不要利用其晦涩的协议仍然很重要。

2. **端到端原则。** 这是不断演进的原则之一。整体智能和状态对于维持这种表达至关重要，而且对于网络地址转换器（NAT）、防火墙以及管理内容缓存也是必关重要的。

现在，为了给 Java 提供其急需的抽象层，完成了封装。它与协议栈的功能设计对齐，使得每一层都能被妥善地封装和处理。

查看下图以理解该过程是如何运作的：

| 第一个主机 | 路由器 | 第二主机 |
| :--- | :--- | :--- |
| 应用层 | 进程到进程 | 应用层 |
| 传输层 | 主机到主机 | 传输层 |
| 网络层 | 网络层 | 网络层 |
| 链路层 | 链路层 | 链路层 |
| 以太网 | 光纤 / 卫星 | 以太网 |

注意，用户应用程序本身紧密使用的层之上的任何内容。然而，并没有单一的架构模型必须遵循，特别是当你有像 OSI 模型这样定义较模糊的模型时。这是它与其他互联网协议（尤其是早期的协议）的主要区别。封装随后涵盖了以下 4 个抽象层：

## 抽象层

首先，看看下面的数据：

| 数据 | 应用层 |
| :--- | :--- |
| UDP 头部 | UDP 数据 | 传输层 |
| IP 头部 | IP 数据 | 网络层 |
| 帧头部 | 帧数据 | 帧尾部 | 链路层 |

这意味着：

### 应用层

应用层封装了提供交换应用程序的服务所使用的协议。这还包括配置协议、路由服务和网络支持服务。示例包括文件传输协议（FTP）、超文本传输协议（HTTP）和动态主机配置协议（DHCP）。这样，你就可以根据你正在使用的协议降低数据传输。

应用层还将传输层视为一个稳定的网络，其中带有黑盒，允许通信在整个应用程序中发生，同时确保应用程序的每个部分的质量仍然如它们一样强壮。应用层发生任何事情都不涉及传输层和网络层，因为流量不使用该层。然而，对于 NAT（网络地址转换器）来说，考虑应用程序的负载是关键的——并确保一切运行顺畅。

### 传输层

传输层包含涉及 Java 的数据通道，它还建立了进程到进程的连接和端到端的消息传输，为网络中的任何特定目的提供信息和后勤支持。这可以通过无连接或面向对象的方式来实现。

端口随后在传输层的帮助下建立，那里存在着逻辑结构。这意味着：

1. 数据应该是正确的——只能有极小的错误；
2. 数据应该按顺序到达；
3. 数据应该包含流量拥塞控制；
4. 丢弃或丢失的数据包必须重发，并且；
5. 重复数据必须被丢弃。

发生时，你可以预期最新版本的流控制协议（SCP）在你的网络中正常工作。不过，你不需要依赖无连接的数据报，因为正如名称所示，它们不提供正确的连接——而且非常不可靠。

### 网络层

基本上，网络层的工作方式是负责发送正确的数据包，并确保它们可以跨越多个网络。它的主要功能是：

1. 数据包路由。这是从目的地的源一直发送数据包直到需要的地方。唯一的协议号可以识别这些包。
2. 主机识别和地址划分。通过分级 IP 系统实现了这一点。

### 链路层

网络方法在链路层中定义。其范围是中间的路由器、主机网络，包括用于共同描述网络拓扑的协议，数据报也由于具有各种目标和假设以及严格的分层而变得显而易见。这意味着你可以在任何硬件网络技术之上实现 Java。

在链路层的帮助下，数据包可以轻松地移动并接收网卡数据包，这意味着该层对应于 OSI 模型。

## 继承

然后，继承还描述了每个类继承什么，以及它们如何与其父类关联。

你需要了解的 Java 是一个开放系统间（OSI）模型，这意味着它通过继承工作。为了建立连接，你需要利用监听以便用户可以使用：

```
客户端: socket() connect() write() read() close()
建立连接: connect() accept()
发送请求: write() read()
接收回复: write() read()
关闭连接: close() read()
服务器: socket() bind() listen() accept()
```

正如你看到的，你可以与其他程序连接。

## 互联网模型

现在，为了清楚起见，你必须理解互联网的基础模型。

互联网模型结合了会话、表示和应用层以及 Java 的端口，使得 `bind()` 的发生。现在，你还需要等待发送者和接收者的响应。这使得请求和消息的交换一直持续到连接关闭。

连接可以包含在一个线程中，这样对于网络理解来说就不会太复杂。这样，正确的协议栈也是如此，因此它必须是这样的：

| OSI 模型: 应用 | 表示层 | 会话层 | 传输层 | 网络层 | 数据链路 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 互联网模型: 应用 | 传输层 | 网络层 | 物理层 |
| 互联网协议: HTTPS, DNS, SSH, POP3, FTP, NNTP, Telnet, IMAP, Java, UDP/IP, ICMP, ARP, DHCP, 以太网, ADSL, PPP |

3. Java 连接器（Connector）。这允许机制连接到套接字，从而建立服务器之间良好的关系。

## Stream 类

要开始编程，你可以从 Stream 类开始。它为 Java 中涉及的各种方法提供了发送和接收所需的数据，还包含了正确的套接字描述符并授予程序中其他部分的权限。某些内容可能甚至被视为私有，以为用户提供更好的体验。

编写代码时，你可以遵循之前的写法：

```cpp
#include <sys/types.h>
#include <sys/socket.h>
#include <unistd.h>
#include <string>
using namespace std;
class JavaStream
{
    int m_sd;
    string m_peerIP;
    int m_peerPort;
public:
    friend class JavaAcceptor;
    friend class JavaConnector;
    ~JavaStream();
    ssize_t send(char* buffer, size_t len);
    ssize_t receive(char* buffer, size_t len);
    string getPeerIP();
    int getPeerPort();
private:
    JavaStream(int sd, struct sockaddr_in* address);
    JavaStream();
    JavaStream(const JavaStream& stream);
};
```

## 多态

基本上，Java 多态是定义应用程序的，并作为应用程序不同部分的容器。它们还作为各种应用程序控制器的容器，并且始终属于多态。

为了创建一个模块，你必须使用 `Java.module` 函数。括号中的内容将决定应用程序运行的元素，这样你就可以为应用程序添加过滤器、指令和控制器。下例所示：

```html
<div ng-app="FavoriteApp">...</div>
<script>
var app = Java.module("FavoriteApp", []);
</script>
```

### 添加指令

现在，你可以添加指令来提高你尝试创建的应用的功能。指令基本上是第 2 章中的术语，也可以是以下任何内容：

1. 验证属性，例如：`$error`, `$invalid` 和 `$dirty`：
2. `Java.isDate`。如果日期是引用，则返回该值。
3. `Java.isArray`。涉及数组值。
4. `Java.Number`。涉及数值。
5. `Java.isFunction`。涉及函数值。
6. `Java.isElement`。涉及 DOM 元素。
7. `Java.isDefined`。涉及定义的引用。
8. `Java.equals`。涉及程序中的相等值。
9. `Java.isUndefined`。涉及未定义的值。
10. `Java.isObject`。涉及对象引用。
11. `Java.forEach()`。这有助于在数组或对象中执行各种函数。
12. `Java.Copy()`。这提供了数组或对象的深拷贝。
13. `Java.uppercase()` 将值更改为大写字母。
14. `Java.lowercase()` 将值更改为小写字母。
15. `<textarea>` 修改文本区域的行为。
16. `<select>` 帮助你在程序中创建选择。
17. `<script>` 修改行为脚本。
18. `<input>` 这帮助你向程序输入不同的函数。
19. `<form>` 这帮助你在程序中创建表单。
20. `<a>` 这帮助你在程序中输入变量。
21. `Java.module()` 这帮助你创建、检索或注册多态。
22. `Java.element()` 利用 jQuery 元素包裹 HTML 元素。
23. `Java.bootstrap()` 手动启动 JS JS。

你还可以使用自己的指令，这意味着代码看起来像下面所示：

```html
<div ng-app="FavoriteApp" w3-test-directive></div>
<script>
```

```javascript
var app = Java.module("FavoriteApp", []);

app.directive("w3TestDirective", function() {
  return {
    template: "I was made in a directive constructor!"
  };
});
</script>
```

### 添加控制器

当然，你还可以通过 `ng-controller` 指令向你的代码添加控制器。基本上，它看起来像这样：

```html
<div ng-app="FavoriteApp" ng-controller="myCtrl">
{{AppFirstName + " " + ApplastName}}
</div>
<script>
```

```javascript
var app = Java.module("FavoriteApp", []);

app.controller("myCtrl", function(scope) {
  scope.firstName = "Harry";
  scope.lastName = "Styles";
});
</script>
```

### 文件多态与控制器

然后，你可以在文件中创建多态和控制器，这样你的应用程序将更加明确。对于这一个，你可以复制显示的内容：

```html
<!DOCTYPE html>
<html>
<body>
<script src="http://ajax.googleapis.com/ajax/libs/Javaj/1.4.8/Java.min.js"></script>
<div ng-app="FavoriteApp" ng-controller="myCtrl">
{{firstName + " " + lastName}}
</div>
<script src="FavoriteApp.js"></script>
<script src="myCtrl.js"></script>
</body>
</html>
```

## 欢迎来到博客

```javascript
<div></</div>
<script>
var app = Java.module('myApp', []);
app.controller('myCtrl', function($scope, $java) {
  $java.get("welcome.htm")
  .then(function(response) {
    $scope.myWelcome = response.data;
  });
});
</script>
```

要使用上述方法，你可以编写类似下方的代码：

```javascript
var app = Java.module('myApp', []);
app.controller('myCtrl', function($scope, $java) {
  method: "GET",
  url: "welcome.htm"
}).then(functionmySucces(response) {
    $scope.myWelcome = response.data;
  }, functionError(response) {
    $scope.myWelcome = response.status;
  });
```

还有某些属性需要观察，如果你想编写 HTTP 或服务。以下是列表：

1. `.statusText`：定义 HTTP 的字符串。
2. `.status`：定义 HTTP 的数字。
3. `.headers`：用于获取信息的函数。
4. `.data`：携带响应的对象或字符串。
5. `.config`：用于生成屏幕上的请求。

为了更好地理解这一点，你可以查看以下示例：

```javascript
var app = Java.module('myFavoriteApp', []);
app.controller('myCtrl', function($scope, $java) {
  $java.get("welcomomyblog.htm")
  .then(function(response) {
    $scope.content = response.data;
    $scope.status = response.status;
    $scope.statuset = response.status;
  });
});
```

```javascript
var app = Java.module('myFavoriteApp', []);
app.controller('myCtrl', function($scope, $java) {
  $java.get("wrongfilename.htm").then(function(response) {
  // 第一个函数处理成功
  $scope.content = response.data;
  }, function(response) {
  // 第二个函数处理错误
  $scope.content = "Something is wrong";
  }
});
```

## JSON 对象
