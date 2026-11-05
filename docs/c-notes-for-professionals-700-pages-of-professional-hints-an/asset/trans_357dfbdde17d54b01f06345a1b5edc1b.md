
```csharp
public static void Main(string[] args)
{
    FieldRepository f = new FieldRepository();
    IField grass = f.GetField(FieldType.GRASS);
    grass = f.GetField(FieldType.ROCK);
    grass = f.GetField(FieldType.GRASS);
}
```

控制台中的结果应为：

> > Created a new instance of Grass
> > Created a new instance of Rock

但为什么草只出现一次，如果我们想获取它两次呢？那是因为第一次调用 GetField 时，草实例在我们的存储库中不存在，所以它被创建了，但下一次我们需要草时它已经存在，所以我们只返回它。

## 第 137 章：System.Management.Automation

### 第 137.1 节：调用简单同步管道

获取当前日期和时间。

```csharp
public class Program
{
    static void Main()
    {
        // create empty pipeline
        PowerShell ps = PowerShell.Create();

        // add command
        ps.AddCommand("Get-Date");

        // run command(s)
        Console.WriteLine("Date: {0}", ps.Invoke().First());

        Console.ReadLine();
    }
}
```

![](img/5da9b5c72747b887ec63f57c832400bf_703_0.png)

## 第 138 章：System.DirectoryServices.Protocols.LdapConnection

### 第 138.1 节：经过身份验证的 SSL LDAP 连接，SSL 证书与反向 DNS 不匹配

设置服务器和身份验证信息的某些常量。假设使用 LDAPv3，但更改起来很容易。

```csharp
// Authentication, and the name of the server.
private const string LDAPUser = "cn=example:app:mygroup:accts,ou=Applications,dc=example,dc=com";
private readonly char[] password = { 'p', 'a', 's', 's', 'w', 'o', 'r', 'd' };
private const string TargetServer = "ldap.example.com";

// Specific to your company. Might start "cn=manager" instead of "ou=people", for example.
private const string CompanyDN = "ou=people,dc=example,dc=com";
```

实际上使用三部分创建连接：LdapDirectoryIdentifier（服务器）和 NetworkCredentials。

```csharp
// Configure server and port. LDAP w/ SSL, aka LDAPS, uses port 636.
// If you don't have SSL, don't give it the SSL port.
LdapDirectoryIdentifier identifier = new LdapDirectoryIdentifier(TargetServer, 636);

// Configure network credentials (userid and password)
var secureString = new SecureString();
foreach (var character in password)
{
    secureString.AppendChar(character);
}
NetworkCredential creds = new NetworkCredential(LDAPUser, secureString);

// Actually create the connection
LdapConnection connection = new LdapConnection(identifier, creds)
{
    AuthType = AuthType.Basic,
    SessionOptions =
    {
        ProtocolVersion = 3,
        SecureSocketLayer = true
    };
};

// Override SChannel reverse DNS lookup.
// This gets us past the "The LDAP server is unavailable." exception
// Could be
// connection.SessionOptions.VerifyServerCertificate += { return true; };
// but some certificate validation is probably good.
connection.SessionOptions.VerifyServerCertificate +=
(sender, certificate) => certificate.Subject.Contains(string.Format("CN={0},", TargetServer));
```

使用 LDAP 服务器，例如通过 userid 搜索所有 objectClass 值的人员。objectClass 的存在是为了演示复合搜索：与号是两个查询子句的布尔“与”运算符。

```csharp
SearchRequest searchRequest = new SearchRequest(
    CompanyDN,
    string.Format("(&(objectClass=*)(uid={0}))", uid),
    SearchScope.Subtree,
    null
);

// Look at your results
foreach (SearchResultEntry entry in searchResponse.Entries) {
    // do something
}
```

### 第 138.2 节：超级简单的匿名 LDAP

假设使用 LDAPv3，但更改起来很容易。这是匿名、未加密的 LDAPv3 LdapConnection 创建。

```csharp
private const string TargetServer = "ldap.example.com";
```

实际上使用三部分创建连接：LdapDirectoryIdentifier（服务器）和 NetworkCredentials。

```csharp
// Configure server and credentials
LdapDirectoryIdentifier identifier = new LdapDirectoryIdentifier(TargetServer);
NetworkCredential creds = new NetworkCredential();
LdapConnection connection = new LdapConnection(identifier, creds)
{
    AuthType=AuthType.Anonymous,
    SessionOptions =
    {
        ProtocolVersion = 3
    }
};
```

要使用连接，像这样就可以获取姓氏为 Smith 的人员

```csharp
SearchRequest searchRequest = new SearchRequest("dn=example,dn=com", "(sn=Smith)",
SearchScope.Subtree,null);
```

## 第 139 章：C# Authentication handler

### 第 139.1 节：身份验证处理程序

```csharp
public class AuthenticationHandler : DelegatingHandler
{
    /// <summary>
    /// Holds request's header name which will contains token.
    /// </summary>
    private const string securityToken = "__RequestAuthToken";

    /// <summary>
    /// Default overridden method which performs authentication.
    /// </summary>
    /// <param name="request">Http request message.</param>
    /// <param name="cancellationToken">Cancellation token.</param>
    /// <returns>Returns http response message of type <see cref="HttpResponseMessage"/> class asynchronously.</returns>
    protected override Task<HttpResponseMessage> SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        if (request.Headers.Contains(securityToken))
        {
            bool authorized = Authorize(request);
            if (!authorized)
            {
                return ApiHttpUtility.FromResult(request, false, HttpStatusCode.Unauthorized, MessageTypes.Error, Resource.UnAuthenticatedUser);
            }
            else
            {
                return ApiHttpUtility.FromResult(request, false, HttpStatusCode.BadRequest, MessageTypes.Error, Resource.UnAuthenticatedUser);
            }
        }

        return base.SendAsync(request, cancellationToken);
    }

    /// <summary>
    /// Authorize user by validating token.
    /// </summary>
    /// <param name="requestMessage">Authorization context.</param>
    /// <returns>Returns a value indicating whether current request is authenticated or not.</returns>
    private bool Authorize(HttpRequestMessage requestMessage)
    {
        try
        {
            HttpRequest request = HttpContext.Current.Request;
            string token = request.Headers[securityToken];
            return SecurityUtility.IsTokenValid(token, request.UserAgent, HttpContext.Current.Server.MapPath("~/Content/"), requestMessage);
        }
        catch (Exception)
        {
            return false;
        }
    }
}
```

## 第 140 章：Pointers

### 第 140.1 节：用于数组访问的指针

此示例演示了指针如何用于对 C# 数组进行类似 C 的访问。

```csharp
unsafe
{
    var buffer = new int[1024];
    fixed (int* p = &buffer[0])
    {
        for (var i = 0; i < buffer.Length; i++)
        {
            *(p + i) = i;
        }
    }
}
```

需要 unsafe 关键字，因为指针访问不会发出在常规方式访问 C# 数组时通常发出的任何边界检查。

fixed 关键字告诉 C# 编译器发出指令以异常安全的方式固定对象。固定是必需的，以确保垃圾收集器不会在内存中移动数组，否则会使指向数组内的任何指针失效。

### 第 140.2 节：指针算术

指针中的加法和减法与整数的工作方式不同。当指针递增或递减时，它指向的地址会根据引用类型的大小而增加或减少。

例如，类型 int（System.Int32 的别名）大小为 4。如果 int 可以存储在地址 0，则后续 int 可以存储在地址 4，以此类推。在代码中：

```csharp
var ptr = (int*)IntPtr.Zero;
Console.WriteLine(new IntPtr(ptr)); // prints 0
ptr++;
Console.WriteLine(new IntPtr(ptr)); // prints 4
ptr++;
Console.WriteLine(new IntPtr(ptr)); // prints 8
```

类似地，类型 long（System.Int64 的别名）大小为 8。如果 long 可以存储在地址 0，则后续 long 可以存储在地址 8，以此类推。在代码中：

```csharp
var ptr = (long*)IntPtr.Zero;
Console.WriteLine(new IntPtr(ptr)); // prints 0
ptr++;
Console.WriteLine(new IntPtr(ptr)); // prints 8
ptr++;
Console.WriteLine(new IntPtr(ptr)); // prints 16
```

void 类型是特殊的，void 指针也是特殊的，它们用作万能指针，当类型未知或无关紧要时使用。由于其与大小无关的特性，void 指针不能递增或递减：

```csharp
var ptr = (void*)IntPtr.Zero;
```
