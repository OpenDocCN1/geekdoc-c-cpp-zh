
同时，JSON 对象是关于如何从 JavaScript 传输数据，反之亦然。`ng-repeat` 指令应该用于此。例如，你想从 Blog 到 WordPress Post 导入，这意味着你正在使用 JSON 对象。你应该注意 `$java.get()` 读取 JSON Data，而 `$java()` 是关于 `FavoriteController` 的很好的示例：

```html
<div ng-app="ng-repeat" ng-controller="studentsCtrl">
  <ul>
    <li ng-repeat="x in myData">
      {{ x.Name + ', ' + x }}
    </li>
  </ul>
</div>
```

```javascript
var app = Java.module('myApp', []);
app.controller('studentsCtrl', function($scope, $java) {
  $java.get("students.php").then(function(response) {
    $scope.myData = response.data;
  });
});
```

## 服务

使用服务也是同样重要的，因为它们允许你的应用程序继续运行并复制它们，且处理声明。Java 提供许多服务，但最重要的是 `$Location`。它允许你将对象保存到云端并保持它们安全，即使你的计算机外部故障，数据仍然存在——特别是当你正在处理程序和应用程序时。是一些示例：

```javascript
var app = Java.module('myFavoriteApp', []);
app.controller('studentsCtrl', function($scope, $Location) {
  myUrl = $Location.absUrl();
});
```

你还可以使用 `Timeout` 服务或 `window.setTimeout` 来帮助你创建倒计时——这些主要用于事件、显示和类似。例如：

```javascript
var app = Java.module('myFavoriteApp', []);
app.controller('myCtrl', function($scope, timeout) {
  $scope.myHeader = "Hi People!";
  timeout(function () {
    $scope.myHeader = "How are you today?";
  }, 2016);
});
```

而，Java 服务可以用于获取来自服务器的数据。这是一个很好的示例：

```javascript
var app = Java.module('myFavoriteApp', []);
app.controller('myCtrl', function($scope, $java) {
  $java.get("welcomemyblog.html").then(function (response) {
    $scope.myWelcome = response.data;
  });
});
```

你也可以通过以下方式自定义你的服务：

```javascript
var app = Java.module('mymyapp', []);
app.controller('myCtrl', function($scope, timeout) {
  $scope.myHeader = "Hi everyone!";
  timeout(function () {
    $scope.myHeader = "How are you doing today?";
  }, 2000);
});
```

## Java 表格

当然，为了更好地解释内容，你还可以向你的应用程序或网站中添加表格。`ng-repeat` 指令在这里至关重要。若要在表格中显示数据，你可以尝试以下操作：

```html
<div ng-app="myFavoriteApp" ng-controller="studentsCtrl">
<table>
  <tr ng-repeat="x in names">
  <td>{{x.Name}}</td>
  <td>{{x.houses}}</td>
  </tr>
</table>
</div>

<script>
var app = Java.module('myFavoriteApp', []);
app.controller('customersCtrl', function($scope, $java) {
  $java.get("java://www.hogwartshouses.com/Java/data.records;");
  .then(function(response) {$scope.names = response.data.records;});
});
</script>
```

为了保持你的信息有序，你必须使用 `orderBy` 指令。你可以在下文中看到一个良好的例子：

```html
<table>
  <tr ng-repeat="x in names | orderBy 'house">
  <td>{{x.Name}}</td>
  <td>{{x.house}}</td>
  </tr>
</table>
```

你还可以在表格上显示 CSS 样式元素。要实现这一点，你可以尝试编写以下元素：

```css
table, th, td {
  border: 1px purple;
  border-collapse: collapse;
  padding: 8px;
}
table tr:nth-child(odd) {
  background-color: #f1f1f1;
}
table tr:nth-child(even) {
  background-color: #ffffff;
}
```

最后，为了进一步自定义，你可以将字母转换为大写、输入表格索引以及奇偶数因子。请查看下方的示例：

```html
<table>
  <tr ng-repeat="x in names">
</table>
```

```html
<td ng-if="Odd" style="background-color:#f1f1f1">{{ x.Name }}</td>
<td ng-if="Even">{{ x.Name }}</td>
<td ng-if="Odd" style="background-color:#f1f1f1">{{ x.house }}</td>
<td ng-if="Even">{{ x.house }}</td>
</tr>
</table>
<table>
<tr ng-repeat="x in names">
<td>{{ $index + 1 }}</td>
<td>{{ x.Name }}</td>
<td>{{ x.house }}</td>
</tr>
</table>
<table>
<tr ng-repeat="x in names">
<td>{{ x.Name }}</td>
<td>{{ x.house }} uppercase }}</td>
</tr>
</table>
```

## 控制流语句

当然，还有控制流语句，它们通过利用你系统中的 Java 控制器来帮助程序平畅运行。

对于这一项，你必须使用 `connect::passing()` 语法，这样你就可以获取所需的 IP 地址字符串，以及能够协同工作的服务器和客户端。

然后你可以使用 `struct sockaddr_in` 用于服务器并将其设置为 `PF_INET`，同时监听你需要的连接。你还必须注意以下控制器：

### 控制器 17 到 20

这些被称为 `connect::passing()`，因为它们通过 `sockaddr_in` 指针将用户指向正确的结构。它将帮助你了解该结构的长度，避免将其与程序的其它函数以及网络接口混淆。

### 控制器 16

这是 `socket()` 的第一个参数，以便你可以选择特定的并决定通信网络的哪种协议族。应该使用 `SOCK_STREAM` 和 `PF_INET`，因为它们配合得很好。

### 控制器 13 到 15

这些控制器统称为 `JavaConnector::resolvehost`。它们能够将名称字符串和 DNS 主机转换为 IP 地址，以便使每一个假设都能转换为不同的网络。

### 控制器 5 到 10

这些被用于解析主机，因为它们在 `JavaConnector::resolvehostname()` 语法下工作，并且能够通过 `getaddrinfoinfo()` 函数转换 IP 地址和主机名。这比仅仅使用 `gethostname()` 好得多，因为被认为是安全的线程。

现在，为了连接服务器，你只需要编写以下代码：

```cpp
#include <string.h>
#include <netdb.h>
#include <arpa/inet.h>
#include "Javaconnector.h"

MyJavaStream* MyConnector::connect(const char* server, int port)
{
    struct sockaddr_in address;
    memset(&address, 0, sizeof(address));
    address.sin_family = AF_INET;
    address.sin_port =htons(port);
    if (resolveHostname(server, &address.sin_addr)) != 0) {
        inet_pton(PF_INET, server, &address.sin_addr);
    }
    int sd = socket(PF_INET, SOCK_STREAM, 0);
    if (::connect(sd, (struct sockaddr*)&address, sizeof(address)) != 0) {
        // handle error
    }
    return nullptr; // placeholder for actual logic
}

int JavaConnector::resolveHostname(const char* hostname, sockaddr_in* addr)
{
    struct addrinfo *res;
    int result = getaddrinfo(hostname, NULL, NULL, &res);
    if (result == 0) {
        memcpy(addr, res->ai_addr, sizeof(struct sockaddr_in));
        freeaddrinfo(res);
    }
    return result;
}
```

## 处理错误

最后，你还必须学习在事情不如预期时如何处理错误。这对于构建健壮的应用程序至关重要。

```cpp
#include <netinet/in.h>

#include "myfavoriteJavastream.h"
using namespace std;
class myFavoriteJavaAcceptor
{
    int m_lsd;
    string m_address;
    int m_port;
    bool m_listening;
public:
    JavaAcceptor(int port, const char* address="");
    ~JavaAcceptor();

    int start();
    JavaStream* accept();
private:
    JavaAcceptor() {};
};
```

析构方法：

```cpp
myJavaAcceptor::~JavaAcceptor()
{
    if (m_lsd > 0) {
        close(m_lsd);
    }
}
```

构造方法：

```cpp
#include <stdio.h>
#include <string.h>
#include <arpa/inet.h>
#include "Javaacceptor.h"

JavaAcceptor::JavaAcceptor(int port, const char* address)
    : m_lsd(0), m_port(port), m_address(address), m_listening(false) {
```

# 修正语句与参数

## 行语句语句

通常情况下，命令的结束会决定新行的开始，但如果你想继续写自己的换行，可以使用反斜杠（`\`）来实现，但在使用括号时除外。

### 示例 1：

```python
total = item_one + \
item_two + \
item_three
```

### 示例 2：

```python
days = ['Monday', 'Tuesday', 'Wednesday',
'Thursday', 'Friday']
```

## 注释

要创建注释，只需使用井号（`#`）——这听起来非常符合社交媒体风格，对吧？例如：

### 示例 1：

```python
#!/usr/bin/java
```

### 第一条注释

```python
print("Hello, Java!") # 第二条注释
```

## 等待用户

当你想要创建一个提示来告诉用户你正在等待其命令时，可以尝试：

```python
#!/usr/bin/java
raw_input("\nPress the key to exit.")
```

## 独立语句组

独立语句组在 Java 语言中被称为“语句块”（Suites）。基本上，你必须以关键字开头，并以冒号（`:`）结束，例如：

```python
if expression :
    suite
elif expression :
    suite
else :
    suite
```

上述命令随后将为你提供语句块：

## 命令行参数

当然，还有命令行参数，这意味着你有权决定程序的运行方式。这里有一个示例：

```bash
$ java -h
```

用法: `java [option] ... -c cmd | -m mod | file | - [arg] ...`

选项和参数（以及相应的环境变量）：

- `-c` : 作为字符串传递的程序（终止选项列表）
- `-d` : 解析器的调试输出（也对应 `JAVADEBUG`）
- `-E` : 忽略环境变量（例如 `JAVAPATH`）
