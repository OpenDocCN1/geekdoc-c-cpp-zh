

## 23.6 使用 HttpClient 异步调用 Flickr Web 服务

在本节中，我们将展示一个 Flickr 浏览器应用程序，该程序允许你在 Flickr (flickr.com)——最早的照片共享网站之一——上搜索照片，然后浏览结果。该程序使用异步方法调用 Flickr Web 服务——即一个软件组件可以使用标准的 Web 技术通过互联网接收方法调用。

### XML 和 LINQ to XML
许多服务以 XML（可扩展标记语言）格式返回数据。XML 是一种广泛支持的描述数据的标准，通常用于在互联网上的应用程序之间交换数据。XML 描述了人类和计算机都能理解的数据。

我们在本示例中使用的 Flickr Web 服务方法默认返回 XML。我们将使用 .NET 平台内置的 LINQ to XML 来处理从 Flickr 返回的数据。我们将在第 23.6.3 节中解释所需的少量 XML 和 LINQ to XML 知识——在在线的“LINQ to XML”章节中，我们将详细介绍这些技术。

### REST Web 服务
Flickr 提供了了一种所谓的 REST Web 服务，它可以通过标准的 Web 技术接收方法调用。正如你所看到的，应用程序通过 URL 调用 Flickr Web 服务方法，就像你使用 Web 浏览器访问页面一样。REST——全称为表现层状态转移——将在在线的“REST Web Services”章节中讨论。

### 异步调用 Web 服务
因为在等待 Web 服务响应时可能会出现不可预测的延迟，调用 Web 服务（或执行网络通信）的 GUI 程序经常使用异步 `Tasks`，以确保应用程序对用户保持响应。

### 需要 Flickr API Key
要在你的计算机上运行此程序，你必须在以下地址获取自己的 Flickr API Key：
`https://www.flickr.com/services/apps/create/apply`
使用它来替换图 23.4 第 18 行引号内的 `YOUR API KEY`。此密钥是一个唯一的字母数字字符串，允许 Flickr 跟踪你对其 API 的使用情况。务必仔细阅读 Flickr API 的使用条款。

### Flickr 浏览器应用程序
我们的浏览器程序（图 23.4）允许你搜索用户上传到 Flickr 的照片。标记（或内容打标签）是社交媒体协作性质的一部分。标签是任何用户提供的单词或短语，有助于组织网络内容。使用有意义的单词或短语对项目进行标记可以对内容进行强识别。Flickr 使用这些标签来改进其照片搜索服务，为用户提供更好的结果。

```csharp
// Fig. 23.4: FlickViewerForm.cs
// 使用 HttpClient 类异步调用 web 服务
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Xml.Linq;

namespace Flickr
{
    public partial class FlickrForm : Form
    {
        // 在此处使用 Flickr API key--你可以在此处获取：
        // https://www.flickr.com/services/apps/create/apply
        private const string KEY = "YOUR API KEY HERE";

        // 用于调用 Flickr Web 服务的对象
        private static HttpClient FlickrClient = new HttpClient();

        Task<string> flickrTask = null; // 查询 Flick 的 Task<string>
        public FlickrForm()
        {
            InitializeComponent();
        }

        // 启动异步 Flickr 搜索查询；
        // 在查询完成后显示结果
        private async void searchButton_Click(object sender, EventArgs e)
        {
            // 如果 flickrTask 已经在运行，则提示完成
            if (flickrTask?.Status != TaskStatus.RanToCompletion)
            {
                var result = MessageBox.Show(
                    "取消当前的 Flickr 搜索",
                    "确定吗？", MessageBoxButtons.YesNo,
                    MessageBoxIcon.Question);

                // 判断用户是否想要取消之前的搜索
                if (result == DialogResult.No)
                {
                    return;
                }
                else
                {
                    flickrClient.CancelPendingRequests(); // 取消搜索
                }
            }
        }
    }
}
```
**图 23.4** 使用 HttpClient 类异步调用 Web 服务。（3 部分中的第一部分）[本示例中使用的照片]©Paul Deitel 保留所有权利。

```csharp
// 用于搜索的 Flickr Web 服务 URL

imagesListBox.DataSource = null; // 移除之前的数据源

imagesListBox.Items.Clear(); // 清空 imagesListBox
pictureBox.Image = null; // 清空 pictureBox
imagesListBox.Items.Add("Loading..."); // 显示 Loading...

// 调用 Flickr Web 服务根据用户的标签搜索 Flickr

flickrTask = flickrClient.GetStringAsync(flickURL);

// 使用 XDocument 和 LINQ 等待 amassTask 结果

XDocument XDocument = XDocument.Parse(await flickrTask);

// 收集所有照片的信息

var flickrPhotos = from photo in FlickrXML.Descendants("photo")
                  let id = photo.Attribute("id").Value
                  let title = photo.Attribute("title").Value
                  let secret = photo.Attribute("secret").Value
                  let server = photo.Attribute("server").Value
                  let farm = photo.Attribute("farm").Value
                  select new FlickrResult
                  {
                      Title = title,
                      URL = $"https://{farm}.staticflickr.com/{server}/{id}.jpg"
                  };

imagesListBox.Items.Clear(); // 清空 imagesListBox

// 只有在找到结果时设置 List 属性

if (flickrPhotos.Any())
{
    imagesListBox.DataSource = flickrPhotos.ToList();
    imagesListBox.DisplayMember = "Title";
}
else // 未找到匹配项
{
    imagesListBox.Items.Add("No matches");
}

// 显示选中的图片

private async void imagesListBox_SelectedIndexChanged(object sender, EventArgs e)
{
    if (imagesListBox.SelectedItem != null)
    {
        string selectedURL = (FlickrResult)imagesListBox.SelectedItem.URL;
        // 使用 HttpClient 获取图像字节
        byte[] imageBytes = await flickrClient.GetByteArrayAsync(selectedURL);
        // 在 PictureBox 中显示图像
        using (MemoryStream memoryStream = new MemoryStream(imageBytes))
        {
            pictureBox.Image = Image.FromStream(memoryStream);
        }
    }
}
```
图 23.4 使用 HttpClient 类异步调用 Web 服务。（3 部分中的第二部分）

