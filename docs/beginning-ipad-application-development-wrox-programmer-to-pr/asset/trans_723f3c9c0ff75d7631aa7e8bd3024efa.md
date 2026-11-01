

```
@synthesize browser;
@synthesize services;

//---设置 TableView 的行数---
- (NSInteger)tableView:(UITableView *)tableView
numberOfRowsInSection:(NSInteger)section {
    return [services count];
}

//---在 TableView 中显示每一行---
- (UITableViewCell *)tableView:(UITableView *)tableView
cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    static NSString *CellIdentifier = @"Cell";

    UITableViewCell *cell = [tableView
        dequeueReusableCellWithIdentifier:CellIdentifier];
    if (cell == nil) {
        cell = [[[UITableViewCell alloc]
            initWithStyle:UITableViewCellStyleDefault
            reuseIdentifier:CellIdentifier] autorelease];
    }

    //---显示每个服务的主机名---
    cell.textLabel.text = [[services objectAtIndex:indexPath.row] hostName];

    return cell;
}

//---浏览服务---
- (void) browseServices {
    services = [NSMutableArray new];
    self.browser = [[NSNetServiceBrowser new] autorelease];
    self.browser.delegate = self;
    [self.browser searchForServicesOfType:@"_MyService._tcp." inDomain:@""];
}

- (void)viewDidLoad {
    debug.text = @"";
    [self browseServices];
    [super viewDidLoad];
}

//---找到服务---
- (void)netServiceBrowser:(NSNetServiceBrowser *)aBrowser
    didFindService:(NSNetService *)aService
    moreComing:(BOOL)more {

    [services addObject:aService];
    debug.text = [debug.text stringByAppendingString:
        @"Found service. Resolving address...\n"];
    [self resolveIPAddress:aService];
}
```

```
//---服务从网络中被移除---
-(void)netServiceBrowser:(NSNetServiceBrowser *)aBrowser
    didRemoveService:(NSNetService *)aService moreComing:(BOOL)more {
    [services removeObject:aService];
    debug.text = [debug.text stringByAppendingFormat:@"Removed: %@\n",
        [aService hostName]];
    [self.tbView reloadData];
}

//---解析服务的 IP 地址---
-(void) resolveIPAddress:(NSNetService *)service {
    NSNetService *remoteService = service;
    remoteService.delegate = self;
    [remoteService resolveWithTimeout:0];
}

//---解析成功---
-(void)netServiceDidResolveAddress:(NSNetService *)service {
    NSString    *name = nil;
    NSData      *address = nil;
    struct sockaddr_in *socketAddress = nil;
    NSString    *ipString = nil;
    int         port;

    //---获取服务的 IP 地址---
    for(int i=0; i < [[service addresses] count]; i++) {
        name = [service name];
        address = [[service addresses] objectAtIndex: i];
        socketAddress = (struct sockaddr_in *) [address bytes];
        ipString = [NSString stringWithFormat: @"%s",
            inet_ntoa(socketAddress->sin_addr)];
        port = socketAddress->sin_port;
        debug.text = [debug.text stringByAppendingFormat:
            @"Resolved: %@-->%s:%hu\n", [service hostName], ipString, port];
    }
    [self.tbView reloadData];
}

//---解析失败---
-(void)netService:(NSNetService *)service
    didNotResolve:(NSDictionary *)errorDict {

    debug.text = [debug.text stringByAppendingFormat:
        @"Could not resolve: %@\n", errorDict];
}

- (void)dealloc {
    [tbView release];
    [debug release];
    [browser release];
    [services release];

    [super dealloc];
}

@end
```

3. 就这样！将应用程序部署到至少两台设备上（一台在 iPhone 模拟器上，一台在真机上）。当应用程序运行时，它会搜索在同一网络上发布的所有服务。当发现服务时，它们的名称会出现在表视图中。图 16-3 显示了表视图，其中列出了已发现设备的主机名。在这个例子中：

- “Wei-Meng-Lees-iMac.local” 指的是正在运行该应用程序的 iPhone 模拟器。
- “Wei-Meng-Lees-iPod.local” 指的是正在运行该应用程序的我的 iPod touch。
- “Wei-Meng-Lees-iPhone.local” 指的是正在运行该应用程序的我的 iPhone。

![](img/744c5ec15e15ca7891c98be71dc25d13_448_0.png)

图 16-3

## 工作原理

这里涉及的代码量相当大，所以让我们更详细地看一看。

首先，你定义了 `browseServices` 方法，它使用 `NSNetServiceBrowser` 类在默认域中搜索名为 “_MyService._tcp.” 的服务：

```
services = [NSMutableArray new];
self.browser = [[NSNetServiceBrowser new] autorelease];
self.browser.delegate = self;
[self.browser searchForServicesOfType:@"_MyService._tcp." inDomain:@""];
```

当发现服务时，会调用 `netServiceBrowser:didFindService:moreComing:` 方法。在此方法中，你将所有发现的服务添加到 `services` 可变数组中：

```
-(void)netServiceBrowser:(NSNetServiceBrowser *)aBrowser
 didFindService:(NSNetService *)aService
 moreComing:(BOOL)more {
    [services addObject:aService];
    debug.text = [debug.text stringByAppendingString:
        @"Found service. Resolving address...\n"];
    [self resolveIPAddress:aService];
}
```

你还会调用将要定义的 `resolveIPAddress:` 方法，尝试解析所发现服务的 IP 地址。

`resolveIPAddress:` 方法使用 `NSNetService` 实例（代表所发现的服务）的 `resolveWithTimeout:` 方法来获取其 IP 地址：

```
-(void) resolveIPAddress:(NSNetService *)service {
    NSNetService *remoteService = service;
    remoteService.delegate = self;
    [remoteService resolveWithTimeout:0];
}
```

如果成功解析了服务的 IP 地址，就会调用 `netServiceDidResolveAddress:` 方法。如果未能解析 IP 地址，则会调用 `netService:didNotResolve:` 方法。

在 `netServiceDidResolveAddress:` 方法中，你提取服务的所有可用 IP 地址并显示在 TextView 上，然后尝试使用 `UITableView` 类的 `reloadData` 方法重新加载表视图。

```
-(void)netServiceDidResolveAddress:(NSNetService *)service {
    NSString *name = nil;
    NSData *address = nil;
    struct sockaddr_in *socketAddress = nil;
    NSString *ipString = nil;
    int port;
    for(int i=0;i < [[service addresses] count]; i++) {
        name = [service name];
        address = [[service addresses] objectAtIndex: i];
        socketAddress = (struct sockaddr_in *) [address bytes];
        ipString = [NSString stringWithFormat:@"%s", inet_ntoa(socketAddress->sin_addr)];
        port = socketAddress->sin_port;
        debug.text = [debug.text stringByAppendingFormat:
            @"Resolved: %@->%s:%hu\n", [service hostName], ipString, port];
    }
    [self.tbView reloadData];
}
```

当服务从网络中被移除时，会调用 netServiceBrowser:didRemoveService: 方法，因此在该方法中，你将把该服务从 services 可变数组中移除：

```
-(void)netServiceBrowser:(NSNetServiceBrowser *)aBrowser
didRemoveService:(NSNetService *)aService moreComing:(BOOL)more {
[services removeObject:aService];
debug.text = [debug.text stringByAppendingFormat:@"Removed: %@\n", [aService hostName]];
[self.tbView reloadData];
}
```

其余代码涉及用已发现服务的主机名加载表视图。具体来说，你在表视图中显示每个服务的主机名：

```
//---在 TableView 中显示每一行---
- (UITableViewCell *)tableView:(UITableView *)tableView
cellForRowAtIndexPath:(NSIndexPath *)indexPath {

static NSString *CellIdentifier = @"Cell";

UITableViewCell *cell = [tableView
dequeueReusableCellWithIdentifier:CellIdentifier];
if (cell == nil) {
    cell = [[[UITableViewCell alloc]
        initWithStyle:UITableViewCellStyleDefault
        reuseIdentifier:CellIdentifier] autorelease];
}

//---显示每个服务的主机名---
cell.textLabel.text = [[services objectAtIndex:indexPath.row] hostName];

return cell;
}
```

在发现网络上的对等端之后，接下来你能做什么？你可以使用 TCP/IP 与网络上的对等端连接并向它们发送消息。使用 TCP/IP 进行网络编程超出了本书的范围。不过，感兴趣的读者可以从作者的网站 —— http://www.learn2develop.net —— 下载一个可运行的应用程序，它演示了如何使用 Bonjour 构建聊天应用程序。

