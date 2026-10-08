| IMAGETYPE VALUE | DESCRIPTION |
| --- | --- |
| EMF | This format produces images with the Enhanced Metadata Format (EMF). This format records the graphical primitives used to draw a picture, and so it is a vector format combined with the capability to store bitmaps. Pictures with this format often have the smallest size, mainly for line charts. However, the same EMF files can be displayed differently, depending on the browser type or other application using the files, unlike other formats. |

If you have situations where it's difficult to choose the appropriate file type, define test scenarios, execute, and evaluate them. Using the default Png format works in most scenarios.

# Using Charts with Legacy Web Sites

Often, you must integrate your web pages into legacy websites. You can embed your charts created with the ASP.NET Chart control in the same way as any other ASP.NET pages. One solution is to use the HTML <iframe> tag that defines an inline frame that contains another document.

The PetChartsSample project has a page named HtmlPageWithIFrame.html that represents a legacy website's page. The source code of the page is simple, as Listing 16-7 shows.

+   LISTING 16-7: HtmlPageWithIFrame.html

![](bbox=[0.095, 0.545, 0.14, 0.575])

```
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Legacy HTML Page using an IFRAME tag&gt;&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;h3&gt;This sample demonstrates how to use the ASP.Net Chart control
within an &lt;amp&gt; tag of an existing Legacy web page.
&lt;/h3&gt;
&lt;iframe style="WIDTH:800px; HEIGHT:400px" marginWidth="0"
marginHeight="0" src="DataBindCrossTable.aspx" frameBorder="YES"
width="800" height="400"
scrolling="no"&gt;
&lt;iframe style="WIDTH:200px; HEIGHT:400px; marginWidth="10"
marginHeight="0" src="LegacyHtml.htm" frameBorder="NO"
width="800" height="400"
scrolling="no"&gt;
&lt;/body&gt;
&lt;/html&gt;
```

Code file [HtmlPageWithIFrame.html] available for download at Wrox.com