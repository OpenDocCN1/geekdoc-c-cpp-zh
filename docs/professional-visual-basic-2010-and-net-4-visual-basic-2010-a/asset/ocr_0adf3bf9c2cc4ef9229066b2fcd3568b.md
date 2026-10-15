What we refer to as SharePoint is really a set of products and technologies. These are grouped into a set of services and a set of products built on top of those services. In SharePoint 2003, the services were referred to as Windows SharePoint Services 2.0 and the products were referred to as SharePoint Portal Server 2003. In SharePoint 2007, it was Windows SharePoint Services 3.0 and Microsoft Office SharePoint Server 2007. Now, in SharePoint 2010, we have Microsoft SharePoint Foundation 2010 and Microsoft SharePoint Server 2010.

# SharePoint Foundation 2010

Microsoft SharePoint Foundation 2010 is a free add-on to Windows Server 2008 or Windows Server 2008 R2. It provides the core features (or the foundation) for the SharePoint platform. It implements the provisioning engine that enables end users to create sites, lists, and libraries and the security model to ensure that access to these resources is protected. It also implements the information collaboration and management features mentioned previously. SharePoint Foundation is a powerful piece of software on its own and has enough functionality to meet the needs of many small to mid-size organizations.

# SharePoint Server 2010

SharePoint Server 2010 is a retail product that sits on top of SharePoint Foundation, adding functionality commonly desired by larger organizations. At a high level, the Server product editions are separated into two groups depending on whether you plan to use SharePoint internally on an intranet or externally on the Internet. Enterprise search, Web content management, social networking, InfoPath and Excel services, and access to external applications through Business Connectivity Services are just a few of the features offered by SharePoint Server 2010.

# SharePoint Terminology

You should be familiar with several terms and concepts when working with SharePoint. The most important of these are the architectural concepts: farm, Web application, site collection, site, list, and library.

A SharePoint deployment is called a farm. The farm is made up of one or more front-end Web servers and a SQL Server database used to store configuration information. A simple deployment can be done on a single server using SQL Server 2008 Express.

A farm may contain one or more SharePoint Web applications. A Web application is an IIS website extended for use with SharePoint. In general, you will segregate Web applications by authentication mode. For example, you may have one Web application for internal use that uses integrated Windows authentication, and another that acts as an extranet that uses ASP.NET forms authentication.

A SharePoint Web application is made up of several site collections. These are portions of the application that are isolated from each other in terms of administrative privilege and visibility of data. For example, a company intranet could have site collections for individual departments (Sales, Marketing, HR, and so on). One or more end users can be designated as owners of a site collection, giving them administrative privilege within its boundaries. Within a site collection, the owner can create new sites, pages, lists of data, or libraries of documents, and they can give rights to other users to view or contribute to these resources.

A site collection contains a hierarchy of sites. The root of this hierarchy acts as the entry point for the collection. The root may contain many child sites, and they in turn may have child sites of their own. For example, the site at the root of the Sales site collection may have child sites named North Division and South Division.

Within each site, owners can provision lists, libraries, and pages. The list, which consists of rows and columns of data, is the basic storage mechanism in SharePoint. It is similar to an Excel worksheet or a database table. SharePoint has several built-in list templates, including contacts, announcements, and events. A special form of a list is the library. The library has the same features but it is centralized around a document (Word, Excel, InfoPath, image, etc.). Both lists and libraries have built-in collaboration features, including major and minor versioning, content approval, and check in/out policy.