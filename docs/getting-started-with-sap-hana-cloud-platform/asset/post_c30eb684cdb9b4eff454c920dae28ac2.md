
With one of the next releases of SAP HCP, all of the above steps will be incrementally automated for extension accounts and will be triggered during extension application installation. Therefore, you will no longer need to perform any of these steps manually, although it’s of course important to be aware of the underlying mechanics, so that you can troubleshoot potential integration issues.

## 11.4.6 Creating Custom MDF Objects and Consuming Them from SAP HCP

The MDF is an essential part of SuccessFactors’ customization and extensibility. Combined with the flexibility of SAP HCP and the low-touch, easy integration, it forms one of the most flexible offerings for customizing and enriching SaaS solutions on the market.

Custom MDF objects always start their existence in a SuccessFactors system. They are modeled using the Object Definitions tool in SuccessFactors OneAdmin. You can access this tool via ADMIN TOOLS • COMPANY SETTINGS • CONFIGURE OBJECT DEFINITIONS. It’s critical to set the API visibility flag of newly created objects to EDITABLE or Read-ONLY. If it’s set to Not Visible, then this will mean that the object is not exposed via the OData API and is practically out of reach of SAP HCP applications. All custom MDF objects’ names start with cust_ by default. Once you're through with modeling and saving your custom MDF object, don’t forget to make it visible to the outside world using the OData API Metadata Refresh and Export tool in Admin Tools. Prior to triggering the refresh, your object won’t be present in the OData API data model.

On the SAP HCP application side, you’ll work with the custom MDF objects the same way that you work with any other entity in SuccessFactors, by using the sap.hcmcloud.core.odata destination; however, you will query entities starting with cust_ instead.

## 11.4.7 Creating Custom Home Page Tiles Hosted on SAP HCP

When you log in to a SuccessFactors system, regardless of the modules licensed, you’ll be greeted by the SuccessFactors home page (Figure 11.17). The home page enables user-level personalization of the product experience and allows you to collect all the key ingredients in one common screen.

As noted in Section 11.3.8, it's possible to extend the set of visible tiles by registering custom ones. In addition to being a standard feature of the product, tiles are also a great way to incorporate experience and integration with third-party products. SAP HCP extensions make use of that opportunity. Your next question may be: How do I register a tile?

![](img/cf7012644082c115a2181376d9b7486d_498_0.png)

Figure 11.17 SuccessFactors Enterprise Home Page

Once you log in as a company admin, home page tiles configuration is accessible via ADMIN TOOLS • COMPANY SETTINGS • MANAGE V12 HOME PAGE (Figure 11.18).

You will see a comprehensive overview of all tiles delivered as part of the standard product, including some third-party integration tiles. If you want some tiles to be visible to all users in the system, then make sure they are listed in the DEFAULT section. If you want to introduce optional tiles that end users can pull out of a catalog, then have them in the AVAILABLE section. If there are tiles that you want to keep but that are not in use anymore, then move them to the NOT USED section.

![](img/cf7012644082c115a2181376d9b7486d_499_0.png)

Figure 11.18 SuccessFactors Enterprise v12 Home Page Configuration

For each tile, you can specify whether end users should have the freedom to remove it from the home page and the default size it should be rendered in.

The SuccessFactors home page in version v12 supports three tile sizes:

- Medium: 138 pixels wide
- Large: 296 pixels wide
- Extra-large: 612 pixels wide

All of the tile rules apply both to standard and custom tiles. Having a reasonable strategy for managing the system home page gives you a powerful tool for rolling out new initiatives, campaigns, and tools to the whole employee base.

Looking beyond the standard available tiles, you can register a new one by clicking on ADD CUSTOM TILE (Figure 11.19).

![](img/cf7012644082c115a2181376d9b7486d_500_0.png)

Figure 11.19 Custom Tile Creation Wizard

In addition to the standard properties (e.g., Tile NAME, DISPLAY SIZE, TITLE, and DESCRIPTION), you have the opportunity to specify the target audience and the timeframe you plan to target it in.

The SHOW TILE FOR THIS GROUP field gives you the option to narrow down the group of people who will see the custom tile. We strongly recommend not relying on visibility constraints only, but also performing active group membership checking in the backend services consumed by your tile UI.

Another useful feature defined by the SHOW TILE ON THESE DATES field allows you to specify the effective dating of the custom tile. By default, it’s set to ALL DATES. This means that a tile will immediately become visible to the complete targeted population once you click on the SAVE button.

The next aspect of a custom tile to consider is the body it will render. As a rule of thumb, it has to be as informative and as context specific to the current user as possible. Polluting users’ home pages with static tiles is generally suboptimal. Users will simply tick that tile away from their home page, or even worse will keep it there and start complaining.

For managing the content of your custom tile, you have a rich wizard, allowing some predefined standard operations, such as embedding flash components, images, links, or pretty much any piece of HTML code. Therefore, you can embed any page that you’re serving out as an SAP HCP application in a SuccessFactors custom home page tile. One sample HTML snippet to use is as follows:

```
<iframe border="0" frameborder="0" src="//sf-idp-init/sso/customWidgetLaunch?parameter1=value&amp;parameter2=value" style="width: 100%;height:235px">
```

If you look closely at the snippet, you’ll notice that there is no pointer to any SAP HCP-specific URL. We could instead have a direct URL to your SAP HCP application, but then you’ll see all the CORS issues described in Section 11.3.8. Therefore, we’ve defined a particular custom SP mapping key, which in turn is used for IdP-initiated SSO, embedding the referenced application content in the defined iFrame. Any parameters you pass to the SuccessFactors IdP URL will be transparently passed along to the target URL. In that way, you can achieve a much more tailored personal experience in your integration.

## 11.4.8 Managing Custom Navigation Entries

Another key aspect of making your SuccessFactors extension reachable for users is to register it in the different navigation systems inside SuccessFactors, such as the top-level navigation or the personal profile menus. This is done via ADMIN TOOLS • COMPANY SETTINGS • CONFIGURE CUSTOM NAVIGATION (Figure 11.20).

![](img/cf7012644082c115a2181376d9b7486d_501_0.png)

Figure 11.20 SuccessFactors Custom Navigation Management Tool

This management tool allows you to plug any arbitrary link into the navigation menus, specifying certain conditions. One aspect to configure via the Link Type field is how the navigation should behave. Should it open the link in the same window, effectively handing over the control, or should it open the link in a new window, retaining the control in the original one? For SAP HCP extensions using SAP HANA Cloud Portal as the frontend, EXTERNAL LINK—SAME Browser should be selected. At first, it looks as if we’re navigating away from SuccessFactors. Although technically correct, this is misleading, because the newly opened SAP HANA Cloud Portal site delivers the same header and footer as any other page inside SuccessFactors. Therefore, there should be no visible difference between an extension page and another page inside SuccessFactors.

Another field to consider is the PERMISSIONS field, which lists all existing permissions in the system, thus providing fine-grained access control to navigation. The general philosophy here is that if a user is not allowed to perform some operation, then it should not show up in the menus for that user. Ideally, we should never see an Access Denied error when simply browsing around.

## 11.4.9 Troubleshooting SuccessFactors Extension Applications

Once you’re done with development and moving toward real business, it’s essential to be aware of the different tools offered by the SuccessFactors stack. These tools enable you to develop and troubleshoot applications in the most efficient manner.

We learned about the two different layers of administration in SuccessFactors in Section 11.4.1. We’ll leave the SuccessFactors Provisioning environment aside for now, as customers typically don’t have access to it. Instead, we’ll focus on the tools accessible to customer key users and developers.

As a developer, some burning questions may include the following: Where do I see the results of my API calls? Are they successful? Did they fail? What is the response code returned? For administrators, a reasonable concern might revolve around auditing what data is exposed from the system via APIs and how to keep track of that.

In general, when you’re looking for a particular SuccessFactors administration tool, you can always start from the search bar in the OneAdmin view (Figure 11.21).
