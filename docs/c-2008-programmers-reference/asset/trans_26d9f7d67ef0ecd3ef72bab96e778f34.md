

## 第 II 部分：使用 C# 进行应用程序开发

![](img/a977a875c7c627b45d939729705a252e_605_0.png)

图 18-9

这些图像将在树展开或关闭时由 TreeView 控件用来显示其内容。因此，通过将 TreeView 控件的 ImageList 属性设置为 ImageList1，将 ImageList 控件关联到 TreeView 控件。

向项目添加一个新的 Windows 窗体，并在其中放置一个 WebBrowser 和 MenuItem 控件（见图 18-10）。WebBrowser 控件将用于查看帖子的内容。

![](img/a977a875c7c627b45d939729705a252e_605_1.png)

WebBrowser 控件 (webBrowser1)

MenuItem 控件 (mnuBack)

图 18-10

将 WebBrowser 控件的 Modifiers 属性设置为 Internal，以便控件可以从其他窗体访问。具体来说，你希望从 Form1 中设置控件的内容。

切换到 Form1 的代码隐藏部分，并导入以下命名空间：

```
using System.IO;
using System.Net;
using System.Xml;
using System.Text.RegularExpressions;
```

声明以下常量和变量：

```
namespace RSSReader
{
    public partial class Form1 : Form
    {
        //---constants for icons---
        const int ICO_OPEN = 0;
        const int ICO_CLOSE = 1;
        const int ICO_POST = 2;

        //---file containing the list of subscribed feeds---
        string feedsList = @"\Feeds.txt";

        //---app's current path---
        string appPath = string.Empty;

        //---the last URL entered (subscribe)---
        string lastURLEntered = string.Empty;

        //---used for displaying a wait message panel---
        Panel displayPanel;

        //---for displaying individual post---
        Form2 frm2 = new Form2();
    }
}
```

## 创建辅助方法

当 RSS 源正在下载时，你希望在屏幕上显示一条消息，通知用户应用程序正在下载源（见图 18-11）。

![](img/a977a875c7c627b45d939729705a252e_606_0.png)

图 18-11

## 第 II 部分：使用 C# 进行应用程序开发

为此，你可以借助 Panel 和 Label 控件进行改进。定义 CreatePanel() 函数，以便使用几个 Panel 控件和一个 Label 控件动态创建消息面板：

```csharp
//---create a Panel control to display a message---
private Panel CreatePanel(string str)
{
    //---background panel---
    Panel panel1 = new Panel()
    {
        BackColor = Color.Black,
        Location = new Point(52, 13),
        Size = new Size(219, 67),
        Visible = false,
    };
    panel1.BringToFront();

    //---foreground panel---
    Panel panel2 = new Panel()
    {
        BackColor = Color.LightYellow,
        Location = new Point(3, 3),
        Size = new Size(panel1.Size.Width - 6, panel1.Size.Height - 6)
    };

    //---add the label to display text---
    Label label = new Label()
    {
        Font = new Font(FontFamily.GenericSansSerif, 12, FontStyle.Bold),
        TextAlign = ContentAlignment.TopCenter,
        Location = new Point(3, 3),
        Size = new Size(panel2.Size.Width - 6, panel2.Size.Height - 6),
        Text = str
    };

    //---adds the label to Panel2---
    panel2.Controls.Add(label);

    //---adds the Panel2 to Panel1---
    panel1.Controls.Add(panel2);
    return panel1;
}
```

为简单起见，你对 panel1 的位置进行了硬编码（假设此应用程序在宽屏设备上运行）。图 18-12 显示了构成显示面板的各个控件。

![](img/a977a875c7c627b45d939729705a252e_607_0.png)

图 18-12

## 第 18 章：开发 Windows Mobile 应用程序

接下来，定义 IsConnected() 函数以测试用户是否已连接到 Internet：

//---check if you are connected to the Internet---
private bool IsConnected()
{
    try
    {
        string hostName = Dns.GetHostName();
        IPHostEntry curHost = Dns.GetHostEntry(hostName);
        return (curHost.AddressList[0].ToString() != IPAddress.Loopback.ToString());
    }
    catch (Exception)
    {
        return false;
    }
}

Dns 是一个提供简单域名解析的静态类。GetHostName() 方法获取本地计算机的主机名，然后将其传递给 Dns 类的 GetHostEntry() 方法以获取 IPHostEntry 对象。IPHostEntry 是用于 Internet 主机地址信息的容器类。使用此对象，你可以访问其 AddressList 属性以获取与其关联的 IP 地址列表。如果 AddressList 属性数组的第一个成员不是回环地址（127.0.0.1；由 IPAddress.Loopback 表示），则假定存在 Internet 连接。

接下来，定义 DownloadFeed() 函数，该函数接收要下载的源的 URL 和一个 title 参数（用于返回源的标题）。每个帖子标题及其对应的描述被附加到一个字符串中并返回给调用函数：

//---download feed and extract Title and Description for each post---
private string DownloadFeed(string feedURL, ref string title)
{
    XmlDocument xml = new XmlDocument();

    //---always load from storage first---
    string FileName =
        appPath + @"\" + RemoveSpecialChars(feedURL) + ".xml";

    if (File.Exists(FileName))
    {
        xml.Load(FileName);
    }
    else
    {
        //---check if there is network connectivity---
        if (IsConnected())
        {
            WebRequest ftpReq = null;
            WebResponse ftpResp = null;
            Stream ftpRespStream = null;
            StreamReader reader = null;
            bool getRSSFeedFailed = false;

            try
            {
                //---download the RSS document---
                ftpReq = WebRequest.Create(feedURL);
                ftpResp = ftpReq.GetResponse();
                ftpRespStream = ftpResp.GetResponseStream();
                reader = new StreamReader(ftpRespStream,
                    System.Text.Encoding.UTF8);

                //---load the RSS document into an XMLDocument object---
                xml.Load(reader);

                //---save a local copy of the feed document---
                xml.Save(FileName);
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
                getRSSFeedFailed = true;
            }
            finally
            {
                if (ftpRespStream != null)
                {
                    ftpRespStream.Dispose();
                    ftpRespStream.Close();
                }
                if (ftpResp != null) ftpResp.Close();
                if (getRSSFeedFailed) return String.Empty;
            }
        }
        else
        {
            return String.Empty;
        }
    }

    //---get the title of the feed---
    XmlNode titleNode = xml.SelectSingleNode("//rss/channel/title");
    title = titleNode.InnerText;

    //---select all <rss><channel><item> elements---
    XmlNodeList nodes = xml.SelectNodes("rss/channel/item");

    string result = String.Empty;
    foreach (XmlNode node in nodes)
    {
        //---select each post's <title> and <description> elements---
        result += node.SelectSingleNode("title").InnerText + ((char)3);
        result += node.SelectSingleNode("description").InnerText +
            ((char)12);
    }
    return result;
}

## 第 18 章：开发 Windows Mobile 应用程序

要下载 RSS 源 XML 文档，你使用 WebRequest 和 WebResponse 类。然后使用 StreamReader 对象读取文档并将其加载到 XmlDocument 对象中。每个帖子标题与其描述由 ASCII 字符 3 分隔，每个帖子由 ASCII 字符 12 分隔，如下所示：

```
Post_Title<3>Post_Description<12>Post_Title<3>Post_Description<12>
Post_Title<3>Post_Description<12>Post_Title<3>Post_Description<12>
Post_Title<3>Post_Description<12>...
```

请注意，在下载 URL 的 XML 源后，它会被保存到存储中。这确保了应用程序在离线模式下继续工作（当用户断开 Internet 连接时）。源的 URL 用作文件名，去掉 URL 中的所有特殊字符，并附加 .xml 扩展名。例如，如果源 URL 为 http://www.wrox.com/WileyCDA/feed/RSS_WROX_ALLNEW.xml，则文件名将为 httpwww.wroxcomWileyCDAfeedRSSWROXALLNEWxml.xml。为了去掉 URL 中的所有特殊字符，按如下方式定义 RemoveSpecialChars() 函数：

//---removes special chars from an URL string---
private string RemoveSpecialChars(string str)
{
    string NewString = String.Empty;
    Regex reg = new Regex("[A-Z]|[a-z]*");
    MatchCollection coll = reg.Matches(str);
    for (int i = 0; i < coll.Count - 1; i++)
        NewString = NewString + coll[i].Value;
    return NewString;
}

你使用 Regex（正则表达式）类从 URL 中提取所有字母并将它们附加到一个字符串中，该字符串将返回给调用函数用作文件名。

接下来，定义 SubscribeFeed() 函数以订阅源，然后将每个帖子添加到 TreeView 控件（见图 18-13）：

//---returns true if subscription is successful---
private bool SubscribeFeed(string URL)
{
    bool succeed = false;
    try
    {
        //---display the wait message panel---
        if (displayPanel == null)
        {
            displayPanel = CreatePanel("Downloading feed...Please wait.");
            this.Controls.Add(displayPanel);
        }
        else
        {
            displayPanel.BringToFront();
            displayPanel.Visible = true;
        }

