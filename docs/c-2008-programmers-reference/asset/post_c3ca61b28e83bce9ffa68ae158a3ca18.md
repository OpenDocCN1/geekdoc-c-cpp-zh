
## Part II: Application Development Using C#

![](img/a977a875c7c627b45d939729705a252e_605_0.png)

Figure 18-9

These images will be used by the TreeView control to display its content when the tree is expanded or closed. Hence, associate the ImageList control to the TreeView control by setting the ImageList property of the TreeView control to ImageList1.

Add a new Windows Form to the project, and populate it with a WebBrowser and MenuItem control (see Figure 18-10). The WebBrowser control will be used to view the content of a posting.

![](img/a977a875c7c627b45d939729705a252e_605_1.png)

WebBrowser control (webBrowser1)

MenuItem control (mnuBack)

Figure 18-10

Set the Modifiers property of the WebBrowser control to Internal so that the control is accessible from other forms. Specifically, you want to set the content of the control from within Form1.

Switch to the code behind of Form1, and import the following namespaces:

```
using System.IO;
using System.Net;
using System.Xml;
using System.Text.RegularExpressions;
```

Declare the following constants and variable:

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

## Creating the Helper Methods

When RSS feeds are being downloaded, you want to display a message on the screen to notify the user that the application is downloading the feed (see Figure 18-11).

![](img/a977a875c7c627b45d939729705a252e_606_0.png)

Figure 18-11

## Part II: Application Development Using C#

For this purpose, you can improvise with the aid of the Panel and Label controls. Define the CreatePanel() function so that you can dynamically create the message panel using a couple of Panel controls and a Label control:

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

For simplicity, you are hardcoding the location of panel1 (assuming that this application is running on a wide-screen device). Figure 18-12 shows the various controls forming the display panel.

![](img/a977a875c7c627b45d939729705a252e_607_0.png)

Figure 18-12

## Chapter 18: Developing Windows Mobile Applications

Next, define the IsConnected() function to test whether the user is connected to the Internet:

```
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
```

Dns is a static class that provides simple domain name resolution. The GetHostName() method gets the host name of the local computer, which is then passed to the GetHostEntry() method of the Dns class to obtain an IPHostEntry object. IPHostEntry is a container class for Internet host address information. Using this object, you can access its AddressList property to obtain the list of IP addresses associated with it. If the first member of the AddressList property array is not the loopback address (127.0.0.1; represented by IPAddress.Loopback), it is assumed that there is Internet connectivity.

Next, define the DownloadFeed() function, which takes in the URL for the feed you want to download and a title argument (to return the title of the feed). Each post title and its corresponding description is appended to a string and returned to the calling function:

```
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
```

## Chapter 18: Developing Windows Mobile Applications

To download the RSS feed XML documents, you use the WebRequest and WebResponse classes. The document is then read using a StreamReader object and loaded into an XmlDocument object. Each post title and its description are separated by the ASCII character 3, and each posting is separated by the ASCII character 12, like this:

```
Post_Title<3>Post_Description<12>Post_Title<3>Post_Description<12>
Post_Title<3>Post_Description<12>Post_Title<3>Post_Description<12>
Post_Title<3>Post_Description<12>...
```

Notice that after the XML feed for a URL is downloaded, it is saved onto storage. This ensures that the application continues to work in offline mode (when user disconnects from the Internet). The URL of the feed is used as the filename, minus all the special characters within the URL, with the .xml extension appended. For example, if the feed URL is http://www.wrox.com/WileyCDA/feed/RSS_WROX_ALLNEW.xml, then the filename would be httpwww.wroxcomWileyCDAfeedRSSWROXALLNEWxml.xml. To strip off all the special characters in the URL, define the RemoveSpecialChars() function as follows:

```
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
```

You use the Regex (regular expression) class to extract all the alphabets from the URL and append them into a string, which will be returned to the calling function to use as a filename.

Next, define the SubscribeFeed() function to subscribe to a feed, and then add each post to the TreeView control (see Figure 18-13):

```
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
