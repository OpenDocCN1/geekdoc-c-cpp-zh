
## 6.4.1 Conceptual Overview

Within SAP HCP, you can create content repositories using the Document Service. In this section, we'll take a brief look at the Document Service and some of the core features it has to offer.

Within SAP HCP, the Document Service plays the role of content repository. It can be used to store and retrieve unstructured or semistructured data. Internally, this unstructured data can be enriched with various properties that help to classify the data and make it easier to mine later on.

Conceptually speaking, content within the Document Service is organized in much the same way that content is organized within a file system. You can organize files into a hierarchical folder structure that implicitly defines a content taxonomy. How you choose to organize this content is up to you; the Document Service doesn't really care one way or another.

### Creating a Mock File System Using the Document Service

Although the Document Service is primarily intended for use as a full-scale content repository, it can actually be used as a mock file system whenever you have application scenarios that absolutely require the use of a file system. Such scenarios often crop up whenever you attempt to install third-party or legacy Java applications onto SAP HCP. Indeed, as you may recall from Chapter 4, the Cloud Jenkins project uses the Document Service to provide Jenkins with a file system that can be used to store configuration files and so on. Therefore, though widespread use of the Document Service in this capacity is probably not ideal, it's certainly possible.

In keeping with the openness of SAP HCP, the functionality of the Document Service is exposed using the industry standard Content Management Interoperability Services (CMIS) protocol defined by the OASIS consortium. Rather than building a protocol handler from scratch, SAP also standardized around the open-source OpenCMIS library provided by the Apache Chemistry Project. (For more information about the Apache Chemistry Project, check out http://chemistry.apache.org.) This library is automatically included in the classpath for SAP HCP applications, so there's nothing we have to do up front to install it. In addition to being easy to work with, the use of OpenCMIS makes it possible to reuse libraries and frameworks that can be used to synchronize content and so on.

## 6.4.2 Working with the OpenCMIS API

In order to understand how to tap into the functionality of the Document Service, it's helpful to take a look at how you can interact with it using the OpenCMIS API. Therefore, in this section, we'll show you how this API can be used to connect to a repository, add and remove content, and search for content after the fact. Once you grasp these concepts, it will be much easier to see how to exploit some of the value-add features of the Document Service within your application scenarios.

To guide this discussion, we would recommend that you open the AttachmentProcessorBean.java file contained within this chapter's source code bundle in the com.sappress.hcbook.chp06.document package (downloadable from www.sap-press.com/3638). This session EJB is used within the incident management application to process attachments that are uploaded for particular incidents (see Figure 6.44). As such, it provides a fairly typical example of how the Document Service is used from an application perspective.

![](img/cf7012644082c115a2181376d9b7486d_283_0.png)

### Establishing a CMIS Session

Before you can begin doing anything useful with the Document Service, you first need to establish a CMIS session. This session essentially connects you with the application-specific content repository that you wish to interact with.

The code excerpt contained in Listing 6.20 demonstrates how you can create a CMIS session using the OpenCMIS library. The code begins by looking up the core com.sap.ecm.api.EcmService service façade provided by the Document Service via the JNDI context. Although this service is managed by the Document Service, you do have to create a resource reference to it in the application's web.xml file.

```
import org.apache.chemistry.opencmis.client.api.*;

@Stateless
@LocalBean
public class AttachmentProcessorBean
{
    private static final String UNIQUE_NAME = "IncidentRepository";
    private static final String SECRET_KEY = "IncidentAttachments";

    private Session getCmisSession()
    {
        EcmService ecmService = null;

        try
        {
            InitialContext ctx = new InitialContext();
            ecmService = (EcmService)
            ctx.lookup("java:comp/env/EcmService");
            return ecmService.connect(UNIQUE_NAME, SECRET_KEY);
        }
        catch (NamingException ne)
        {
            throw new CmisRuntimeException(ne.getMessage(), ne);
        }
        catch (CmisObjectNotFoundException confe)
        {
            RepositoryOptions options = new RepositoryOptions();
            options.setUniqueName(UNIQUE_NAME);
            options.setRepositoryKey(SECRET_KEY);
            options.setVisibility(Visibility.PROTECTED);
            ecmService.createRepository(options);

            return ecmService.connect(UNIQUE_NAME, SECRET_KEY);
        }
    }
}
```

### Listing 6.20 Establishing a CMIS Session within a Session Bean

Once you obtain a reference to the EcmService handle, you can use its connect() method to connect to the target repository, which is keyed by two string tokens described within the API as the unique name and secret key, respectively. Because this call will fail the first time due to the fact that the repository in question does not yet exist, the code is designed to catch exceptions of type CmisObjectNotFoundException so that you can create the repository on the fly as needed.

### Creating and Removing Content within a Repository

Whenever a repository is initially created, it comes preassigned with a root-level folder. From this root-level folder, you can branch out by defining subfolders and filling them with documents. These operations are carried out using methods provided by the org.apache.chemistry.opencmis.client.api.Folder interface.

Listing 6.21 demonstrates how you can use the createFolder() method to create a new subfolder underneath the root folder called MyFolder. As you can see, the details of the folder itself are captured within a java.util.Map object that maps a series of property names to unique property values. Conceptually, you can think of these properties as tags that are assigned to the folder as it is stored within the repository. These same tags can be used in queries to locate specific pieces of content and so on.

```
Session session = getCmisSession();
Folder rootFolder = session.getRootFolder();

Map<String, String> folderProps =
new HashMap<String, String>();
folderProps.put(PropertyIds.OBJECT_TYPE_ID, "cmis:folder");
folderProps.put(PropertyIds.NAME, "MyFolder");

Folder folder = rootFolder.createFolder(folderProps);
```

### Listing 6.21 Creating a Folder within a CMIS Repository

To create new files, use the createDocument() method of the Folder interface. This overloaded method defines three main parameters:

- Much like the createFolder() method, you must pass a java.util.Map collection object to define the file's properties.
- The content of the file being created is passed in the form of an org.apache.chemistry.opencmis.commons.data.ContentStream object. This object surrounds a java.io.InputStream with additional file metadata, such as the file name, MIME type, and byte count.
- Because documents can exist in versions, you must specify the versioning state of the document at the outset. If desired, you also have the option of turning off versioning for the file.

Once the repository is filled with documents and folders, you can use the methods of the org.apache.chemistry.opencmis.client.api.Session interface to traverse through the repository and search for content. Here, if you happen to know the ID of the object you're looking for, you can use the getObject() method to fetch the object directly. Otherwise, you can search for the content in one of two ways:

- You can use the Session interface's query() method to search for the content using a SQL-like query language called CMISQL. This query language allows you to search for documents based on their assigned properties (e.g., cmis:name, cmis:createdBy, etc).
- If you don't know exactly what you're looking for, then you can recursively search through the folder structure using the Folder interface's getChildren() method.

Regardless of how you get our hands on the content, you can then manipulate it using methods provided by the Folder and Document interfaces. Within these interfaces, you'll find a number of overloaded methods that make it easy to update and remove content, create copies of files, work with version control, and more.

For more information about the kinds of operations that can be performed, we would highly recommend that you read through the help documentation provided online at http://chemistry.apache.org. Suffice to say that there's functionality here to perform just about any content management operation imaginable.

## 6.4.3 Consuming the Document Service Externally

Most of the time, the content stored within the Document Service is intended to be consumed directly by SAP HCP applications. However, that being said, there could be times when this content needs to be consumed externally. For example, it could be that you need to implement some form of content syndication between a cloud-based repository and a repository hosted on-premise, or, if you're building standalone HTML5 applications (which we'll cover in Chapter 7), then you might want to proxy document access to those applications.

Although you could build your own application to expose this content externally, it turns out that SAP has already provided a (mostly) fully functional Servlet class in the SAP HCP SDK for this purpose. The name of this class is com.sap.ecm.api.AbstractCmisProxyServlet. As the name suggests, this class provides a proxy (or bridge) between the CMIS provider (i.e., the Document Service) and CMIS
