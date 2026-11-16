

Maven 如何实现这一点？与其他构建自动化工具不同，Maven 中的基本配置单元不是构建脚本。相反，Maven 使用一种名为项目对象模型文件（或 POM 文件）的特殊 XML 配置文件。在 POM 文件中，我们的目标是构建项目的概念模型。在此，我们可以指定（除其他外）以下内容：

- 项目的唯一标识符，包含目标版本号
- 关于项目、参与人员等的描述性详细信息
- 对其他项目或库的定义依赖

此处明显缺少的是低级构建详细信息，例如从哪个文件夹复制源代码、编译详细信息等等。

之所以我们可以（通常）避免指定这些详细信息，是因为 Apache Maven 遵循“约定大于配置”的格言。也就是说，它对构建应如何工作相当有主见。例如，Maven 并不强制开发者每次都指定源代码位置，而是按惯例假设源代码位于项目根目录下的 SRC/MAIN 目录中。当然，这些规则并非一成不变；如果你绝对想要，Maven 会允许你覆盖这些设置。然而，我们越配合，Maven 就越能替我们推断构建详细信息。

遵循惯例的另一大优势是，它使我们能够利用社区中开发的大量插件来执行特定任务。除了更明显的编译和归档插件外，我们还可以找到用于生成项目文档、捕获源代码度量和执行单元测试的有用插件。在 SAP HCP 开发领域，SAP 提供了一个 Maven 插件，可用于从帮助构建中调用控制台客户端命令。您可以在 https://help.hana.ondemand.com/mavenSite/index.html 在线查看有关此插件的详细信息。

最终，使用 Maven 有助于项目维护的一致性。项目呈现出相似的外观和感觉，这通常使开发者更容易浏览项目工件并找到所需内容。从管理角度来看，Maven 使项目构建中的许多猜测工作变得多余。管理员不必操作构建脚本、下载共享库或进行任何前期准备工作，因为 Maven 通常能够自行处理这些任务。即使管理员对可能要构建的项目一无所知，他们通常也可以通过在命令提示符下简单输入命令 `mvn install` 在几秒钟内构建它。

## 在 Eclipse 中使用 Maven

虽然 Apache Maven 是一个独立工具，可以下载并从命令行运行，但对于 SAP HCP 开发，我们通常更倾向于在 Eclipse IDE 内与其交互。如果您按照第 2 章中描述的 IDE 安装说明操作，那么您应该会发现 Maven 已包含在您的 Eclipse 安装中。

Eclipse 中的 Maven 插件允许您以两种方式创建 Maven 项目。您可以从头开始创建 Maven 项目，也可以事后将现有项目转换为 Maven 项目。在日常开发中采用哪种方法是个人偏好的问题。然而，由于大多数 SAP HCP 教程都基于 Eclipse 动态 Web 项目的使用，我们认为演示如何转换现有项目更有益，因为这将是更典型的场景。步骤如下：

- 1. 选择要转换的项目，右键单击它，并选择 CONFIGURE • CONVERT TO MAVEN PROJECT 菜单选项，如图 4.42 所示。
- 2. 这将打开图 4.43 所示的创建新 POM 对话框。在此，您必须通过指定组件/工件 ID 和版本号来输入 Maven“项目坐标”。集体而言，这些属性在 Maven 仓库中唯一标识您的项目。这反过来允许其他项目在后续创建对您的项目的定义依赖。除这些关键属性外，您需要指定打包类型并为项目提供有意义的名称。如图 4.43 所示，我们选择了 WAR 打包类型，因为我们正在转换一个动态 Web 项目，该项目最终将生成 WAR 文件。
- 3. 指定所有 POM 详细信息后，单击“完成”按钮以完成项目转换过程。

![](img/cf7012644082c115a2181376d9b7486d_156_0.png)

图 4.42 将 Eclipse 项目转换为 Maven 项目：第 1 部分

![](img/cf7012644082c115a2181376d9b7486d_156_1.png)

图 4.43 将 Eclipse 项目转换为 Maven 项目：第 2 部分

项目转换过程尘埃落定后，您会发现从 Eclipse 角度来看，变化不大。确实，在项目资源管理器视图中唯一真正可见的区别是添加了一个名为 pom.xml 的文件。这不出所料，就是项目的 POM 配置文件。我们将在下一节中更详细地了解此文件的内容和用途。

## 维护 Maven POM 文件

默认情况下，Eclipse 生成的 POM 文件不足以构建项目。确实，如清单 4.9 所示，除了通过 Maven 插件派生的一些特定于构建的详细信息外，那里没有多少内容。

```
<project xmlns=...>
<modelVersion>4.0.0</modelVersion>
<groupId>Example4.0</groupId>
<artifactId>Example4.0</artifactId>
<version>0.0.1-SNAPSHOT</version>
<packaging>war</packaging>
<name>HCP Book :: Chapter 4 :: Example 1</name>
<build>
...
</build>
</project>
```

清单 4.9 生成的 pom.xml 文件摘录

生成的 POM 文件中明显缺少的是项目依赖。例如，在我们的示例中，我们正在构建基于 Java Servlet 和 SLF4J API 的动态 Web 项目。为了构建项目，我们需要告诉 Maven 去哪里找到相应的库。

要将这些依赖项添加到 POM 中，我们可以使用 Dependencies 选项卡上提供的图形编辑器，也可以在 pom.xml 源代码中键入相应的 XML 标记。为了演示目的，我们选择了前一种方法，如图 4.44 所示。在此，在选择依赖项对话框中，只需输入要为其定义依赖项的项目或库的坐标，以指定依赖项的范围（在此情况下为 provided），然后单击“确定”按钮。清单 4.10 显示了我们示例项目的最终产品。

![](img/cf7012644082c115a2181376d9b7486d_158_0.png)

图 4.44 向 POM 添加依赖项

```
<project...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>Example04_01</groupId>
    <artifactId>Example04_01</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    ...
    <dependencies>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>2.1.7</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>com.sap.cloud</groupId>
            <artifactId>neo-javaee6-wp-api</artifactId>
            <version>${sap.cloud.sdk.version}</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.0.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <configuration>
                    <webXml>WebContent\\WEB-INF\\web.xml</webXml>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

清单 4.10 带有依赖项定义的修订版 POM 文件

## 理解 Maven 仓库概念

查看清单 4.10 中包含的 POM 文件时，您可能会想知道我们是如何得出精确的组件/工件 ID 和版本的。不幸的是，这并非一门精确的科学，需要稍作解释。

从历史上看，实现自动化构建的挑战之一是弄清楚如何跟踪库依赖项。开发者传统上不得不想出巧妙的方法将库文件夹附加到他们的项目中，以便在构建时可用。

遵循“约定大于配置”的格言，Maven 以更抽象的术语定义此类依赖项。因为 Maven 中的每个项目都在其 POM 中定义了一个唯一的项目 ID，Maven 可以使用这些坐标在其全局仓库中创建库索引。在构建时，`<dependency>` 元素中指定的组件/工件 ID 和版本为 Maven 提供了一个键，用于从远程仓库获取指定的库并将其无缝合并到构建中。

在配置时，我们可以使用相同的信息扫描 Maven 仓库并搜索我们需要指定项目依赖项的库。用于执行此类搜索的一个有用网站是 www.mvnrepository.com。该网站提供了一个灵活的搜索引擎，允许您使用组件/工件 ID 甚至自由形式的文本描述来搜索库。

为了进一步提高可移植性，您可以调整附加到 Maven 安装的用户设置文件，以包含自定义属性，例如

