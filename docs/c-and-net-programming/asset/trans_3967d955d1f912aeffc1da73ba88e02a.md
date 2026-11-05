
```csharp
[WebMethod]
public int Multiply(int n1, int n2)
{
  return n1 * n2;
}
```

**步骤 3：** 创建 WebService 二进制文件，使用 Visual Studio 命令提示符上的以下命令。

```sh
>CSC /t:library /out:ArithmeticServiceImpl.dll App_code\MathOperationService.cs
```

这将为 Web 服务创建一个 DLL 文件。此 DLL 文件可通过使用 SOAP 协议被任何客户端应用程序使用。

**步骤 4：** 为了测试并查看 Web 服务通过 SOAP 协议的工作情况，可以在浏览器中查看 *service.asmx* 文件，这将显示 Web 服务公开了哪些函数。XML 文件包含服务描述。

![](img/3005a4307e6d8f3bb7e76eea28a92357_782_0.png)

图 23.3.4 测试 Web 服务

![](img/3005a4307e6d8f3bb7e76eea28a92357_783_0.png)

图 23.3.5 测试 Web 服务

![](img/3005a4307e6d8f3bb7e76eea28a92357_783_1.png)

图 23.3.6 测试 Web 服务

![](img/3005a4307e6d8f3bb7e76eea28a92357_784_0.png)

图 23.3.7 Web 服务输出

## 第 II 部分 使用 Web 服务

WebService 可以通过以下 **三种方式** 消费，

1. **使用 HTTP-Post 方法。**

HTTP-Post 方法可以通过直接从客户端调用 `.asmx` 文件来使用。对于此操作，直接从表单的输入字段中使用方法名称和参数名称。

```html
<html>
  <body>
    <form action="http://localhost/.../Service.asmx/Multiply" method="POST">
      <input name="n1"> </input>
      <input name="n2"> </input>

      <input type="submit" value="Enter"> </input>
    </form>
  </body>
</html>
```

通过此表单，将调用 Web 服务的方法。

2. **使用 XMLHttp 调用服务时会使用 SOAP**

此方法使用基于 SOAP 的 XMLHttp 来访问 Web 服务。当希望使用完整的 SOAP 功能集使用 Web 服务时使用此方法。

3. **使用 WSDL 生成的代理类**

此方法为 Web 服务生成代理类并进一步使用该代理类。此方法更具类型安全且出错可能性更小，因为一旦生成代理类，它就会处理所有 SOAP 消息、序列化和确保所有问题在编译时而不是运行时得到处理。要使用此服务，需要执行“添加 Web 引用”并添加 Web 服务引用。或者也可以使用 WSDL.exe 命令行工具来生成代理类并使用这些类。“添加 Web 引用”也是使用相同的 WSDL.exe 来生成代理类。

### 2. 编写代码以使用代理类执行操作，代理类随后将使用 SOAP 与 Web 服务通信并将结果返回给我们。

```csharp
protected void Button1_Click(object sender, EventArgs e)
{
    if (txtn1.Text != string.Empty
    && txtn2.Text != string.Empty)
    {
        try
        {
            int n1 = Convert.ToInt32(txtn1.Text);
            int n2 = Convert.ToInt32(txtn2.Text);

            ArithmeticService.Service service = new ArithmeticService.Service();

            Label1.Text = "Addition " + service.Add(n1, n2).ToString();
            Label2.Text = "Difference " + service.Subtract(n1, n2).ToString();
            Label3.Text = "Multiplication " + service.Multiply(n1, n2).ToString();
        }
        catch(Exception)
        {
            throw;
        }
    }
}
```

### 3. 运行网站

## 23.4 从 Web 服务传递和返回 DataSets

### 23.4.1 ADO.NET DataSets

AU : May-18, Dec.-18

- 使用 .NET，可以轻松将 Web 服务与 .NET 的新数据服务耦合，以提供在 Web 上工作的强大数据交付机制，使得能够构建在没有本地数据存储的情况下易于工作的分布式应用程序。Web 服务和 ADO.NET DataSets 可以结合在一起在客户端和服务器应用程序之间传递数据，以构建真正断开连接的应用程序。.NET Web 服务可以用作数据的传输，允许使用相对较少的代码构建远程数据服务。
- .NET 通过提供 Web 服务传输机制（SOAP 和 HTTP）以及为其提供的所有数据对象提供内置的 XML 形式的序列化服务，使这种功能相对容易实现。ADO.NET DataSets 使此过程变得非常容易，并允许轻松创建完全断开连接的数据库应用程序，这些应用程序可以使用标准 HTTP 通过 Web 访问数据。
- ADO.NET 允许在单个对象中创建多个表或数据源的离线数据视图，该对象包含数据本身以及在 DataSet 中描述数据的元数据。此外，DataSets 可以直接从 XML 输入创建数据表，而无需任何额外的转换例程。ADO.NET 使用 XML 作为其原生数据格式，存储在数据集中的数据在内部表示为 XML。这使得可以轻松地将数据从非 .NET 源传递到 .NET 应用程序，并让 DataSet 在无需手动通过 XMLDOM、SAX 或 XmlTextReader 解析器解析的情况下接受它。DataSets 本身也具有将数据离线的能力。事实上，DataSets 总是离线的。它们是数据的断开连接视图，这意味着可以将数据传递给其他应用程序，对其进行更改，然后使用更改更新原始数据源。DataSet 管理更改并可以根据需要重新同步数据库。这使得 DataSets 可以相当透明地用作远程数据源或离线应用程序。DataSets 可以处理使用请求/响应模型的单记录更新功能，也可以处理完全离线的场景，其中数据作为大块拉下来、工作和修改，然后最终与数据源重新同步。
- 数据集具有双重生活。当在 .NET 应用程序中使用时，它们可以通过 ADO.NET 对象模型访问，其方式与过去使用 ADO 访问记录集类似。但它们也可以持久化为 XML，完整包含关系和自描述元数据，而无需开发人员付出任何努力。ADO.NET 根据给定情况管理数据集在其内存表示和 XML 持久化形式之间的持久化方式。当从 Web 服务返回 DataSet 时，ADO.NET 将 DataSet 序列化为 XML 并将其发送到 Web 服务使用者。

### 23.4.2 通过 Web 服务传递 DataSet

Web 服务为使用断开连接的数据集提供高效的数据交付机制。下面是如何通过 Web 服务传递数据集的过程描述。

**步骤 1：创建数据。**

SQL Server 中有三个数据库表：

1. Affiliate 表，其中包含该计划中所有附属机构的信息
2. Customer 表，跟踪已进行购买的客户，包括与推荐该客户访问该网站的 Affiliate 的外键关系。
3. Purchase 表，其中包含特定客户在该网站上进行的每笔购买的详细信息。

网站所有者可以将此 Web 服务的数据集成到其现有的客户管理应用程序、其会计应用程序或以所选方式集成到其网站中。

**步骤 2：编写 Web 服务并传递数据**

1. 创建一个新的 Visual Basic.NET Web 服务项目并将“service1.asmx”文件重命名为“AffiliateManagement.asmx”。

2. 在 Server Explorer 中，创建到创建了这些表的数据库的数据连接，然后导航到 Purchase 表，并将该表拖放到 Web 服务设计器表面。这将在 Web 服务的设计器表面上创建一个 SQL 连接和一个 SQL 数据适配器。

3. 选择 SQL 数据适配器并选择属性窗口底部“配置数据适配器...”链接。这将打开“数据适配器配置向导”。

4. 使用查询生成器创建一个 SELECT 语句，该语句从 Purchase 表中获取所有购买信息以及来自 Customer 表的一些客户信息，（尤其是 affiliate_id）。SELECT 语句如下所示，

   ```sql
   SELECT purchase.purchase_id, purchase.purchase_date, purchase.purchase_amount,
   purchase.customer_id, purchase.commission_due, purchase.commission_paid_date,
   customer.customer_name, customer.customer_email, customer.customer_id
   FROM purchase
   INNER JOIN customer ON purchase.customer_id = customer.customer_id WHERE
   (customer.affiliate_id = @affiliate)
   ```
