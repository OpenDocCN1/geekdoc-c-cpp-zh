![](bbox=[0.12, 0.09, 0.66, 0.47])

# FIGURE 25-2

This brings up the second key enabling technology: the ease with which you can now import and export data and behavior to the Office client applications via VSTO. In fact, even with SharePoint it is the VSTO piece that truly enables you to integrate your custom business application into the Office client tools. VSTO enables you to retrieve data from a database via ADO.NET or LINQ or to communicate with XML Web Services and WCF. Once you have the data, you can enable your users to leverage their experience with the Office user interface to manipulate that data. As you’ll see in this chapter, VSTO allows you to interface your LOB processes and data into every one of the Microsoft Office client applications.

This should give you a better idea of what an OBA is and how it provides an architectural pattern that you can use to create a business application using VSTO. In addition to the URL provided at the start of this section, you can also find more information at the Microsoft-sponsored site www.obacentral.com.

Finally, to see an example of an OBA consider TFS, and what was known as Team System. The Team Explorer install not only provides a set of add-ins for Visual Studio, but also provides support for a set of custom VSTO document applications. Every time you create a new Team Foundation Server (TFS) project, a new SharePoint project site is created. The site will contain several VSTO-based documents for Word and Excel. These illustrate one example of how to use VSTO and the OBA model for your custom applications.

Of course, VSTO wasn’t the original — or even now the only — way to create custom logic within an Office client application. Since the early days of COM, both Microsoft Word and Microsoft Excel have supported Visual Basic for Applications (VBA). Fortunately, ongoing improvements occurring within VSTO can be integrated with existing VBA.

# WORKING WITH BOTH VBA AND VSTO

The VBA model for Office document customization was limited at best. For starters, it is only available in Word and Excel. However, the VBA application model is not yet retired. That bears repeating: VBA is still a viable and supported set of tools for customizing the Microsoft Office experience. As with all such changes