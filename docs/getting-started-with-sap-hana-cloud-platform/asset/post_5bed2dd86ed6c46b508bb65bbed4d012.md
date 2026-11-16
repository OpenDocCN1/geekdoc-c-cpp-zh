
| Name | Description | Categories | Type | Requires Authentication | URL |
|---|---|---|---|---|---|
| HTML Viewer | A widget used to upload and display HTML files | Delivered with proc | Optional | | https://example.com/... |
| Social Networks Widget | A widget used to display common social networks in | Delivered with proc | Optional | | https://example.com/... |
| Video Player Widget | A widget used to publish video contents to Web page | Delivered with proc | Optional | | https://example.com/... |
| Document Widget | A widget used to display a document | Delivered with proc | Optional | | https://example.com/... |
| Image Widget | A widget used to display an image | Delivered with proc | Optional | | https://example.com/... |
| URL Widget | A widget used to display an external web page | Delivered with proc | Optional | | https://example.com/... |
| List Builder | A widget used to display custom lists or items, will | Delivered with proc | Optional | | https://example.com/... |
| Horizontal Menu | A widget used to display a horizontal site navigation | Delivered with proc | Optional | | https://example.com/... |
| Weather | Weather Widget | | Optional | | https://example.com/... |
| Incident Widget | HCP Book - Chapter 4 - Incident Editor Widget | Auto-discovered | Optional | Yes | https://example.com/... |
| Bootstrap Application | Bootstrap Application | URL | | Yes | https://example.com/... |
| Customer Maintenance Widget | Customer Maintenance Widget | URL | | Yes | https://example.com/... |

Figure 9.40 Creating Widgets for the SAP HANA XS and HTML5 Applications

# Embedding the Application Widgets

With your application widgets in place, you're ready to start building out the content areas of your pages. For the application-based pages, the steps required to drop in your application widgets are as follows:

- 1. Navigate to the page that you want to edit, and open up the CONTENT CATALOG pane via the toolbar button on the right-hand side of the page with the plus (+) icon on it.
- 2. Locate the target widget and drag it onto the page's content area (see Figure 9.41).
- 3. To resize the widget, you have two options: Use the drag handles surrounding the widget (see Figure 9.41) to move and resize the widget, or configure the widget to expand to match the size of the page's content area. In this case, opt for the latter approach by opening up the widget's design panel. This is achieved by selecting the DESIGN... menu option from the widget's menu bar (see Figure 9.42).

![](img/cf7012644082c115a2181376d9b7486d_424_0.png)

Figure 9.41 Adding an Application Widget to a Page: Part 1

![](img/cf7012644082c115a2181376d9b7486d_424_1.png)

Figure 9.42 Adding an Application Widget to a Page: Part 2

- 4. This will open the Design popup window shown in Figure 9.43. To expand the widget size, click on the SET AS FULL PAGE button.

![](img/cf7012644082c115a2181376d9b7486d_425_0.png)

Figure 9.43 Adding an Application Widget to a Page: Part 3

# Playing with Pre-delivered Widget Types

After you embed your application-based widgets, all that's left to configure, content-wise, is the SCRATCH PAD page that we created to demonstrate the capabilities of some of the SAP HANA Cloud Portal's out-of-the-box widgets.

The first widget you'll embed is the List Builder widget. By the name suggests, this widget type is used to create lists. For the purposes of this demo, create a Things to WORK On list that highlights some of the SAP HANA Cloud Portal-related technologies we've covered in the book. Figure 9.44 shows how the editor view looks like for this widget. As you can see, the editor view provides most of the text editing features common to word processing applications like Microsoft Word. Thus, it's a fairly simple task to touch up the list content.

The next widget you'll embed is the Video Player widget. This widget provides a nice container for displaying videos that might have been uploaded to YouTube, Vimeo, and so forth. As you can see in Figure 9.45, the only thing you have to specify when configuring this widget is the URL to the video you wish to display.

![](img/cf7012644082c115a2181376d9b7486d_426_0.png)

Figure 9.44 Adding a List to the Site

![](img/cf7012644082c115a2181376d9b7486d_426_1.png)

Figure 9.45 Adding a Video to the Site

Obviously, this simple demonstration barely scratches the surface of what some of these pre-delivered widget types can do. For more information about the widget types that are available and their specific capabilities, we recommend that you check out the online help documentation.

# 9.4.4 Publishing and Testing the Site

At this point, you've completed your content development and are ready to test out your site definition. Before you can test the site, though, you first have to publish it.

To publish a site, click on the toolbar button with the planet icon on it. This opens the Publishing Options flyout pane shown in Figure 9.46. Here, simply click on the Publish button to publish the site. Also worth noting on the Publishing Options pane are the Revert to Last PUBLISHED Site and Take Offline buttons. As the labels suggest, these buttons can be used to revert inadvertent changes and/or take down a site altogether.

![](img/cf7012644082c115a2181376d9b7486d_427_0.png)

Figure 9.46 Publishing the Demo Site: Part 1

Whenever you click on the PUBLISH button, you'll be presented with the confirmation prompt shown in Figure 9.47. If you choose to proceed (by clicking on the PUBLISH button), then the latest-and-greatest version of the site will be published, and you should eventually arrive at the completion screen shown in Figure 9.48.

![](img/cf7012644082c115a2181376d9b7486d_428_0.png)

Figure 9.47 Publishing the Demo Site: Part 2

![](img/cf7012644082c115a2181376d9b7486d_428_1.png)

Figure 9.48 Publishing the Demo Site: Part 3

After the site is published, you can access it by clicking on the PUBLISHED SITE link in the Publishing Options pane, as shown in Figure 9.49.

This will open the site in a separate browser window or tab, as shown in Figure 9.50. From here, you can click through the various pages and verify that all the content is showing up correctly. It's also a good idea to plug the site URL into other device types (e.g., tablets, phones, etc.) to see what the site looks like there. Because we didn't really tailor our demo site for mobile access, the spoiler alert here is that the site won't look fantastic on a small form factor, but that's a challenge for another day.

![](img/cf7012644082c115a2181376d9b7486d_429_0.png)

Figure 9.49 Launching the Published Site: Part 1

![](img/cf7012644082c115a2181376d9b7486d_429_1.png)

Figure 9.50 Launching the Published Site: Part 2

# 9.5 Next Steps

Despite being positioned as a service within SAP HCP, one could certainly make the argument that SAP HANA Cloud Portal is a product unto itself. Indeed, with so many powerful features, it’s difficult to do SAP HANA Cloud Portal justice in an introductory chapter like this one. Still, we hope that we’ve provided you with a good enough foundation to take the next steps on your journey.

What are these next steps, you might ask? For developers, there’s obviously an emphasis on learning the ins and outs of the OpenSocial standard for widget development, LESS for theming, and so forth. For the foreseeable future, though, it’s also vitally important that developers learn their way around SAP HANA Cloud Portal’s administrative tools. This is because the lines between content developer and content administrator will likely be blurred for a while as SAP HANA Cloud Portal matures.

The day-to-day administrative tasks are described in the online help documentation, under the section titled “SAP HANA Cloud Portal–User Guide.” Within this guide, you can find details about how to configure site security, translate site content, and configure the use of standard-delivered widgets. Even if you never plan on performing an SAP HANA Cloud Portal administrative task, this is good knowledge to have, because it helps you develop with the platform instead of against it.

# 9.6 Summary

In this chapter, we provided you with a whirlwind introduction to SAP HANA Cloud Portal. As we observed, this SAP HCP service provides a rapid development environment for building mashup sites. As such, it’s central to a lot of the extension application development that goes on in SAP HCP.

In the next chapter, we’ll take a look at another useful service offering within SAP HCP: SAP HANA Cloud Integration (SAP HCI). Here, we’ll see how this service can be used to build complex integration scenarios between applications hosted on the cloud and on-premise.
