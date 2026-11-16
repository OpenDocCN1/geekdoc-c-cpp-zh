

## 6.4.1 概念概览

在 SAP HCP 中，你可以使用 Document Service 创建内容存储库。在本节中，我们将简要了解 Document Service 及其提供的一些核心功能。

在 SAP HCP 中，Document Service 扮演着内容存储库的角色。它可用于存储和检索非结构化或半结构化数据。在内部，这些非结构化数据可以通过各种属性进行丰富，这些属性有助于对数据进行分类，并使其日后更易于挖掘。

从概念上讲，Document Service 中的内容组织方式与文件系统中的内容组织方式大致相同。你可以将文件组织成层次结构文件夹，这会隐式定义内容分类法。你如何组织这些内容由你决定；Document Service 并不在意具体方式。

### 使用 Document Service 创建模拟文件系统

虽然 Document Service 主要旨在用作全规模内容存储库，但当你有绝对需要使用文件系统的应用场景时，它实际上可以用作模拟文件系统。当你尝试将第三方或旧版 Java 应用程序安装到 SAP HCP 时，此类场景经常出现。确实，如你可能还记得第 4 章中所述，Cloud Jenkins 项目使用 Document Service 为 Jenkins 提供可用于存储配置文件等内容的文件系统。因此，尽管以这种方式广泛使用 Document Service 可能并非理想，但这当然是可行的。

与 SAP HCP 的开放性保持一致，Document Service 的功能是使用 OASIS 联盟定义的行业标准内容管理互操作性服务（CMIS）协议公开的。SAP 并没有从头开始构建协议处理程序，而是围绕 Apache Chemistry 项目提供的开源 OpenCMIS 库进行了标准化。（有关 Apache Chemistry 项目的更多信息，请查看 http://chemistry.apache.org。）该库会自动包含在 SAP HCP 应用程序的类路径中，因此我们无需事先安装它。除了易于使用之外，使用 OpenCMIS 还可以重用可用于同步内容等的库和框架。

## 6.4.2 使用 OpenCMIS API

为了了解如何利用 Document Service 的功能，查看如何使用 OpenCMIS API 与其交互会很有帮助。因此，在本节中，我们将向你展示如何使用此 API 连接到存储库、添加和删除内容，以及事后搜索内容。一旦掌握这些概念，你将更容易了解如何在应用场景中利用 Document Service 的一些增值功能。

为了指导本次讨论，我们建议你打开本章源代码包中 com.sappress.hcbook.chp06.document 包内的 AttachmentProcessorBean.java 文件（可从 www.sap-press.com/3638 下载）。此会话 EJB 在事件管理应用程序中用于处理为特定事件上传的附件（参见图 6.44）。因此，它提供了一个相当典型的示例，说明如何从应用程序角度使用 Document Service。

![](img/cf7012644082c115a2181376d9b7486d_283_0.png)

### 建立 CMIS 会话

在开始使用 Document Service 进行任何有用操作之前，你首先需要建立一个 CMIS 会话。此会话基本上将你与希望交互的应用程序特定内容存储库连接起来。

清单 6.20 中的代码片段演示了如何使用 OpenCMIS 库创建 CMIS 会话。代码首先通过 JNDI 上下文查找 Document Service 提供的核心 com.sap.ecm.api.EcmService 服务门面。尽管此服务由 Document Service 管理，但你确实需要在应用程序的 web.xml 文件中为其创建资源引用。

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

### 清单 6.20 在会话 Bean 中建立 CMIS 会话

一旦获得 EcmService 句柄的引用，你可以使用其 connect() 方法连接到目标存储库，该存储库由 API 中分别描述为唯一名称和密钥的两个字符串标记进行索引。由于第一次调用会失败，因为相关存储库尚不存在，因此代码设计为捕获 CmisObjectNotFoundException 类型的异常，以便你可以根据需要即时创建存储库。

### 在存储库中创建和删除内容

每当最初创建存储库时，它都会预先分配一个根级文件夹。从这个根级文件夹开始，你可以通过定义子文件夹并用文档填充它们来进行扩展。这些操作是使用 org.apache.chemistry.opencmis.client.api.Folder 接口提供的方法执行的。

清单 6.21 演示了如何使用 createFolder() 方法在根文件夹下创建名为 MyFolder 的新子文件夹。如你所见，文件夹本身的详细信息被捕获在一个 java.util.Map 对象中，该对象将一系列属性名称映射到唯一属性值。从概念上讲，你可以将这些属性视为在存储库中存储文件夹时分配给文件夹的标签。这些相同的标签可以用于查询以定位特定内容等等。

```
Session session = getCmisSession();
Folder rootFolder = session.getRootFolder();

Map<String, String> folderProps =
new HashMap<String, String>();
folderProps.put(PropertyIds.OBJECT_TYPE_ID, "cmis:folder");
folderProps.put(PropertyIds.NAME, "MyFolder");

Folder folder = rootFolder.createFolder(folderProps);
```

### 清单 6.21 在 CMIS 存储库中创建文件夹

要创建新文件，请使用 Folder 接口的 createDocument() 方法。此重载方法定义三个主要参数：

- 与 createFolder() 方法类似，你必须传递一个 java.util.Map 集合对象来定义文件的属性。
- 正在创建的文件的内容以 org.apache.chemistry.opencmis.commons.data.ContentStream 对象的形式传递。该对象围绕一个 java.io.InputStream，并带有额外的文件元数据，例如文件名、MIME 类型和字节数。
- 由于文档可以存在版本，你必须在一开始就指定文档的版本状态。如果需要，你还可以选择关闭文件的版本控制。

一旦存储库中填充了文档和文件夹，你可以使用 org.apache.chemistry.opencmis.client.api.Session 接口的方法遍历存储库并搜索内容。这里，如果你碰巧知道要查找的对象的 ID，可以使用 getObject() 方法直接获取该对象。否则，你可以通过两种方式之一搜索内容：

- 你可以使用 Session 接口的 query() 方法，使用一种称为 CMISQL 的类 SQL 查询语言来搜索内容。这种查询语言允许你根据分配的属性（例如 cmis:name、cmis:createdBy 等）搜索文档。
- 如果你不确定要查找什么，则可以使用 Folder 接口的 getChildren() 方法递归搜索文件夹结构。

无论你如何获取内容，随后都可以使用 Folder 和 Document 接口提供的方法对其进行操作。在这些接口中，你会发现许多重载方法，它们使更新和删除内容、创建文件副本、使用版本控制等变得容易。

有关可执行的操作类型的更多信息，我们强烈建议你阅读 http://chemistry.apache.org 上提供的在线帮助文档。可以肯定的是，这里提供了执行几乎任何可想象的内容管理操作的功能。

## 6.4.3 外部使用 Document Service

大多数情况下，存储在 Document Service 中的内容旨在由 SAP HCP 应用程序直接使用。话虽如此，也有可能需要外部使用此内容。例如，你可能需要在基于云的存储库与本地托管的存储库之间实现某种形式的内容分发，或者，如果你正在构建独立的 HTML5 应用程序（我们将在第 7 章中介绍），那么你可能希望为这些应用程序代理文档访问。

虽然你可以构建自己的应用程序来外部公开此内容，但事实证明，SAP 已在 SAP HCP SDK 中为此目的提供了一个（大部分）功能齐全的 Servlet 类。此类的名称是 com.sap.ecm.api.AbstractCmisProxyServlet。正如名称所示，此类在 CMIS 提供程序（即 Document Service）和 CMIS 之间提供了一个代理（或桥接）。

