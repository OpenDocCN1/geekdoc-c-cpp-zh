
```
[theXML release];

[activityIndicator stopAnimating];

[connection release];
[webData release];
}
-(void) dealloc {
    [ipAddress release];
    [activityIndicator release];
    [super dealloc];
}
```

11. 按 Command-R 测试 iPhone 模拟器上的应用程序。在文本字段中输入 IP 地址 34.5.6.7，然后点击查找国家按钮。

12. 在 Xcode 中，按 Shift-Command-R 打开调试器控制台窗口。观察以下内容已发送到 Web 服务：

```
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
<soap:Body>
<FindCountryAsXml xmlns="http://www.ecubic.../webservices/">
<v4IPAddress>34.5.6.7</v4IPAddress>
</FindCountryAsXml>
</soap:Body>
</soap:Envelope>
```

13. Web 服务返回了以下内容：

```
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
<soap:Body>
<FindCountryAsXmlResponse xmlns="http://www.ecubic.../webservices/">
<FindCountryAsXmlResult>
<IPCountryService xmlns="">
<Country>United States</Country>
</IPCountryService>
</FindCountryAsXmlResult>
</FindCountryAsXmlResponse>
</soap:Body>
</soap:Envelope>
```

Web 服务的响应表明你已成功与 Web 服务通信。现在的问题是如何解析 XML 以提取所需的相关结果。在本例中，你想要的结果封装在 <Country> 元素中。在下一节中，你将学习如何解析 XML 响应。

## 使用 HTTP POST 与 Web 服务通信

你也可以使用 HTTP POST 方法与 Web 服务通信。要使用 HTTP POST 与 Web 服务通信，只需修改 buttonClicked: 方法，如下所示：

```
- (IBAction)buttonClicked:(id)sender {
    NSString *postString =
    [NSString stringWithFormat:@"V4IPAddress=%@", ipAddress.text];
    NSLog(postString);
    NSURL *url = [NSURL URLWithString:
    @"http://www.ecubicle.net/ip2country.asmx/FindCountryAsXml"];
    NSMutableURLRequest *req = [NSMutableURLRequest requestWithURL:url];
    NSString *msgLength = [NSString stringWithFormat:@"%d", [postString length]];
    [req addValue:@"application/x-www-form-urlencoded"
     forHTTPHeaderField:@"Content-Type"];
    [req addValue:msgLength forHTTPHeaderField:@"Content-Length"];
    [req setHTTPMethod:@"POST"];
    [req setHTTPBody: [postString dataUsingEncoding:NSUTF8StringEncoding]];
    [activityIndicator startAnimating];
    conn = [[NSURLConnection alloc] initWithRequest:req delegate:self];
    if (conn) {
        webData = [[NSMutableData data] retain];
    }
}
```

基本上，你不再需要形成 SOAP 消息，而只需向 Web 服务发布一个简单的字符串，例如：

```
V4IPAddress=34.5.6.7
```

> **注意** 请注意，要使 HTTP POST 正常工作，Web 服务必须支持 HTTP POST 方法。务必参考 Web 服务的文档（或图 14-2 中显示的测试页面）以确认 Web 服务是否支持 HTTP POST。

Web 服务返回的结果将如下所示：

```
<?xml version="1.0" encoding="utf-8"?>
<IPCountryService>
<Country>United States</Country>
</IPCountryService>
```

NSXMLParser 对象读取 XML 文档并从头到尾扫描它。当它遇到文档中的各种项目（如元素、属性、注释等）时，它会通知其委托，以便采取适当的行动（如提取元素的值等）。

## 试一试 解析 XML 结果

- 1. 使用上一节创建的 WebServices 项目，将以下语句添加到 WebServicesViewController.h 文件中以解析 Web 服务的响应：

```
#import <UIKit/UIKit.h>

@interface WebServicesViewController : UIViewController {
IBOutlet UITextField *ipAddress;
IBOutlet UIActivityIndicatorView *activityIndicator;

NSMutableData *webData;
NSMutableString *soapResults;
NSURLConnection *conn;

NSXMLParser *xmlParser;
BOOL elementFound;
}

@property (nonatomic, retain) UITextField *ipAddress;
@property (nonatomic, retain) UIActivityIndicatorView *activityIndicator;

- (IBAction)buttonClicked:(id)sender;

@end
```

- 2. 在 WebServicesViewController.m 文件中，将以下加粗语句添加到 connectionDidFinishLoading: 方法中：

```
-(void) connectionDidFinishLoading:(NSURLConnection *) connection {

NSLog(@"DONE. Received Bytes: %d", [webData length]);
NSString *theXML = [[NSString alloc]
initWithBytes: [webData mutableBytes]
length:[webData length]
encoding:NSUTF8StringEncoding];

//---shows the XML---
NSLog(@"theXML");
[theXML release];

[activityIndicator stopAnimating];

if (xmlParser) {
[xmlParser release];
}

xmlParser = [[NSXMLParser alloc] initWithData: webData];
[xmlParser setDelegate: self];
```

```
didStartElement:(NSString *) elementName
namespaceURI:(NSString *) namespaceURI
qualifiedName:(NSString *) qName
attributes:(NSDictionary *) attributeDict {
    if ([elementName isEqualToString:@"Country"]) {
        if (![soapResults]) {
            soapResults = [[NSMutableString alloc] init];
        }
        elementFound = YES;
    }
}
```

在这里，你检查标签是否为 <Country>。如果是，你将布尔变量 elementFound 设置为 YES。

parser:foundCharacters: — 在找到元素的文本时触发：

```
-(void)parser:(NSXMLParser *) parser foundCharacters:(NSString *)string {
    if ([elementFound]) {
        [soapResults appendString: string];
    }
}
```

在这里，如果找到 <Country> 标签，你就开始将 Country 元素的值提取到 soapResults 对象中。

parser:didEndElement:namespaceURI:qualifiedName: — 在找到元素的末尾时触发：

```
//---when the end of element is found---
-(void)parser:(NSXMLParser *)parser
    didEndElement:(NSString *)elementName
    namespaceURI:(NSString *)namespaceURI
    qualifiedName:(NSString *)qName {
    if ([elementName isEqualToString:@"Country"]) {
        //---displays the country---
        NSLog(soapResults);
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Country found!"
            message:soapResults
            delegate:self
            cancelButtonTitle:@"OK"
            otherButtonTitles:nil];
        [alert show];
        [alert release];
        [soapResults setString:@""];
        elementFound = FALSE;
    }
}
```

在这里，你只需查找 </Country> 标签，这样你就知道 Country 元素的值已被正确提取。然后你使用 UIAlertView 对象打印出该值。

## 摘要

本章探讨了在你的 iPad 应用程序中消费 Web 服务的各种方式——SOAP、HTTP GET 和 HTTP POST。你还学习了如何从 XML 文档中提取数据。希望你现在对消费 Web 服务所涉及的内容有了一个很好的了解。

## 练习

- 1. 命名在你的 iPad 应用程序中消费 Web 服务的三种方式。
- 2. 命名使用 `NSURLConnection` 类时需要处理的三个关键事件。
- 3. 描述 `NSXMLParser` 类解析 XML 文档内容的步骤。

练习的答案可在附录 A 中找到。

## 本章学到的内容

| 主题 | 关键概念 |
|---|---|
| Web 服务的消费方式 | SOAP 1.1/1.2, HTTP GET, and HTTP POST |
| 制定 URL 请求 | 使用 `NSMutableURLRequest` 类 |
| 建立 URL 连接 | 使用 `NSURLConnection` 类 |
| 存储字节缓冲区的类 | 使用 `NSMutableData` 类 |
| `NSURLConnection` 类触发的事件 | `connection:didReceiveResponse:`<br>`connection:didReceiveData:`<br>`connection:didFailWithError:`<br>`connectionDidFinishLoading:` |
| 解析 XML 内容 | 使用 `NSXMLParser` 类 |
| `NSXMLParser` 类触发的事件 | `parser:didStartElement:namespaceURI:qualifiedName:attributes:`<br>`parser:foundCharacters:`<br>`parser:didEndElement:namespaceURI:qualifiedName:` |

