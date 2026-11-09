
You can also set the value of the `VaryByParam` attribute to `*`, which directs the caching engine to check any POST parameter associated with the requests.

## Implementing Output Caching

Output caching is the simplest method of caching available in ASP.NET. To show how to implement output caching in Web pages, let’s create a new Web site by performing the following steps:

- 1. *Open* **Microsoft Visual Studio 2010**.
- 2. *Click* **File > New > Web Site**. The New Web Site dialog box appears.
- 3. *Select* **Visual C#** from the **Installed Templates** pane and the **ASP.NET Web Site** template from the middle pane of the **New Web Site** dialog box and name it as **OutputCache**.
- 4. *Click* the **OK** button.

  The OutputCache application (also available on the CD) has been created.

- 5. *Add* the following code snippet under the **@Page** directive of the **Default.aspx** page:

```aspx
<%@ OutputCache Duration="10" VaryByParam="none" %>
```

- 6. *Select* the **Design** tab to view the design of the Web page.
- 7. *Drag* and drop three **Label** controls on the **Default.aspx** page from the Toolbox.
- 8. *Right-click* each control, select the **Properties** option from the context menu to open the **Properties** window. Set the properties of each control, as listed in Table 9.6.

**Table 9.6: Properties to be Set for the Controls**

| **Control Name** | **Property Name** | **Value** |
|---|---|---|
| Label1 | Text | Output Cache example |
| Label3 | Text | The above displayed time was cached for 10 seconds. Keep refreshing the Web page to see the changes. |

- 9. *Rearrange* the **Label** controls in the **Default.aspx** page, as shown in Fig. ASP-9.1:

![](img/9862a98a1a2d3bb14334137965a1ec60_663_0.png)

Fig. ASP-9.1

- 10. *Double-click* the **Default.aspx.cs** file in the Solution Explorer window to open it (Fig. ASP-9.1). Now, *add* the code, shown in Listing 9.1, in the **Page_Load** event of the **Default.aspx** page:

### Listing 9.1: Showing the Code for the Page_Load Event

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        Label2.Text = DateTime.Now.ToString();
    }
}
```

In Listing 9.1, the Text property of the Label2 control is set to the current date and time.

- 11. Run the application by pressing the F5 key from the keyboard. The output is displayed, as shown in Fig. ASP-9.2.

![](img/9862a98a1a2d3bb14334137965a1ec60_664_0.png)

Fig. ASP-9.2

The time displayed in Fig. ASP-9.2 is cached in the cache memory for 10 seconds.

Now, let's learn about the partial-page output caching.

### Describing Partial-Page Output Caching

Caching of a complete Web page is not always required. Sometimes, you need to implement caching on specific content of a Web page and the remaining content of the Web page needs to be refreshed each time the page is requested. This can be implemented by using **partial caching or fragment caching**. The steps to apply partial caching are as follows:

- 1. Identify the parts of the Web page that require more resources and processing than other parts.
- 2. Create one or many user controls and decide cache policies for them. Cache policies ensure the validity of the cached data on each user request.

You can cache the content of a user control either by using the `@ OutputCache` directive or by using the `PartialCachingAttribute` class in the code-behind file. The following code snippet shows the caching engine to cache a control in the output cache for 500 seconds:

```aspx
<%@ OutputCache Duration="500" VaryByParam="None" %>
```

If you do not want to use the functionality of VaryByParam attribute, set its value to None, as shown in the preceding code snippet.

A parser error occurs if you do not include the `VaryByParam` attribute while using the `@ OutputCache` directive.

If you prefer to use the **PartialCachingAttribute** class, then you need to add the following code snippet in the metadata of your class declaration:

```csharp
[PartialCaching(300)]
```

Now, if you request for a Web page where a user control is used, the user control is stored in the output cache for 500 seconds. During the subsequent request made within 500 seconds, the user control is retrieved from the output cache by the cache engine. The remaining content of the Web page is accessed from the server.

Let’s take another scenario and assume that the user control is cached for 200 seconds and nested in a Web page, which has its output cache enabled for only 100 seconds. In this situation, the user control is cached for 200 seconds, even though the cache for the page is re-generated after 100 seconds. Therefore, the control is retrieved from the cache only after 200 seconds.

Let’s now reverse the case, assuming that the page expires in 200 seconds, and the control expires in 100 seconds. In such a situation, the complete page will be present in the cache for 200 seconds, including the user control.

### Understanding the Disk Output Cache

The **disk output cache** can be used to save cached responses to the disk as well as in memory. To use the disk output cache, you need to first edit the **web.config** file of a Web application to specify the maximum size per application. Next, you need to specify the duration for which the cached responses are saved by the output cache in the **OutputCache** element by using the **Duration** attribute. To enable the disk output cache, you also need to set the **DiskCacheable** attribute to **True**.

Now let’s learn about post-cache substitution and the **Substitution** control.

### Describing Post-Cache Substitution and Substitution Control

The post-cache substitution allows caching by updating some of the content in a Web page dynamically. In some cases, however, you may want to cache a page, but at the same time you may want some of its content to be dynamically available as well. In such a situation, you can use the post-cache substitution feature.

Let’s consider an example to understand how post-cache substitution works. Suppose a Web page contains information on automobiles. This information, being static, can be easily cached. However, if this page contains an **AdRotator** that changes on each page request, making this part of the page dynamic, you can use the post-cache substitution feature to cache the page that contains the static information on automobiles, while leaving the dynamic part containing the **AdRotator**. You can implement post-cache substitution by performing any of the following three tasks:

- Using the **Substitution** control to specify the part of the page that needs to be made dynamic, or is exempted from caching
- Using the Substitution control Application Programming Interface (API) to programmatically create that part of the page that needs to be made dynamic
- Using the AdRotator control (implicitly) to internally provide support for post-cache substitution

The Substitution control can be used to specify the part of a Web page that is exempted from caching. You can drag the Substitution control from the Toolbox and drop it on the page having the dynamic content. The **MethodName** property of the Substitution control can be used to specify the method that the Substitution control calls at runtime. This method, specified by using the **MethodName** property, returns a String value that replaces the content of the Substitution control. When you use the Substitution control, the Web page is cached on the server instead of the client. This allows the method to retrieve the updated content of the Substitution control whenever the request for that Web page is made in future.

Programmatically, you can create dynamic content for a cached page by calling the **WriteSubstitution** method of the Substitution control API in the code. The **WriteSubstitution** method takes the name of the method defined for performing the task of creating dynamic content as a parameter. This method also takes an **HttpContext** parameter and returns a string, which is the content that is substituted at the specified location. The advantage of using the **WriteSubstitution** method instead of the Substitution
