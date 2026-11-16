


![](img/cf7012644082c115a2181376d9b7486d_202_0.png)

图 5.30 定义安全角色：第 2 部分

向导完成后，我们将得到一个名为 (role_name).hdbrole 的空文件。清单 5.7 演示了填充角色详细信息所需的语法。在此，角色是通过初始角色子句定义的。{acct} 标记指向目标 SAP HCP 账户，而 package 是用于定义角色的完全限定包名（例如，hcpbook.bookstore.storefront）。在角色定义本身中，我们将在本节中创建的应用程序权限分配给该角色，以及一些对象权限，这些权限将允许用户查询我们书店数据模型中的条目。后者是处理来自 SAPUI5 客户端应用程序的 OData 请求所必需的。

```
role ({acct} :package):display_access {
    application privilege: {acct}.{package}::Basic;
    catalog sql object "_SYS_"
    BIC:"{acct}.{package}.model::Bookstore.Books": SELECT;
    catalog sql object "_SYS_"
    BIC:"{acct}.{package}.model::Bookstore.Authors": SELECT;
    catalog sql object "_SYS_"
    BIC:"{acct}.{package}.model::Bookstore.BookAuthors}":
    SELECT;
    catalog sql object "_SYS_"
    BIC:"{acct}.{package}.model::Bookstore.BookAuthorsView}":
    SELECT;
}
```

清单 5.7 为演示应用程序定义只读角色

目前，我们需要定义的就是这些。在下一节中，您将学习如何部署此角色并将其分配给最终用户。

## 5.7 部署与测试

现在，我们已创建构成示例应用程序的所有相关存储库工件，准备好部署应用程序并开始测试。在本节中，我们将了解如何使用 Eclipse IDE 和 SAP HCP 驾驶舱工具执行这些任务。

### 5.7.1 激活 SAP HANA XS 项目

如在第 5.3 节中所述，在 Eclipse IDE 开发过程中创建的所有源代码工件最初都保存到本地计算机的工作区文件夹中。因此，在测试 SAP HANA XS 应用程序之前，必须先将此工作区文件夹的内容与远程 SAP HANA 存储库同步。

如果您已按照第 5.3 节中概述的 SAP HANA XS 项目设置步骤操作，那么触发此同步过程所需的所有配置都应已就绪。在此，您可以使用在第 5.2.2 节中创建的存储库工作区来打开远程 SAP HANA 存储库连接并同步文件。在 Eclipse IDE 中，执行此任务的步骤如下：

- 1. 右键单击 SAP HANA XS 项目根文件夹，并选择 TEAM • ACTIVATE ALL... 菜单选项，如图 5.31 所示。
- 2. 这将打开图 5.32 所示的 ACTIVATE INACTIVE OBJECTS 对话框。在此，选择或取消选择要同步的工件，然后单击 OK 按钮以触发激活。此时，文件将被复制到远程 SAP HANA 存储库，并且如果没有语法错误，则会被激活。

![](img/cf7012644082c115a2181376d9b7486d_204_0.png)

图 5.31 在远程 SAP HANA 存储库中激活项目：第 1 部分

请注意，在对应用程序进行单元测试和应用缺陷修正时，将使用相同的过程来执行增量同步。或者，如果您愿意，可以通过右键单击特定存储库文件并直接激活它来执行一次性激活。

![](img/cf7012644082c115a2181376d9b7486d_205_0.png)

图 5.32 在远程 SAP HANA 存储库中激活项目：第 2 部分

### 5.7.2 将显示角色分配给用户帐户

一旦您的 SAP HANA XS 项目被激活，您应该会在 SAP HANA 存储库中看到几个新安装的对象：在第 5.4 节中定义的表和视图、SAP HANA XS 应用程序本身等等。存储库工件列表中包含在第 5.6.3 节中创建的安全角色。在测试 SAP HANA XS 应用程序之前，您需要将此角色分配给您想要用于测试应用程序的用户帐户。

要执行此角色分配，必须在目标 SAP HANA 实例中执行一个存储过程。使用 SAP HCP 试用帐户时，执行此过程所需的步骤如下：

- 1. 在 Eclipse IDE 中，打开 SAP HANA DEVELOPMENT 透视图，并切换到 Systems 选项卡。
- 2. 选择远程 SAP HANA 实例的连接节点，并单击顶级工具栏上的 SQL 按钮（参见图 5.33）。

![](img/cf7012644082c115a2181376d9b7486d_206_0.png)

图 5.33 将显示角色分配给测试用户

- 3. 这将打开图 5.33 右侧所示的 SQL CONSOLE 窗口。在此编辑器中，您需要使用清单 5.8 中包含的语法构建对 HCP_GRANT_ROLE_TO_USER 过程的调用。
- 4. 构建好 CALL 过程语句后，单击 Execute 按钮以执行分配。

```
CALL "HCP"."HCP_GRANT_ROLE_TO_USER"(
 'acct_name', {pk_gname} := '{role_name}',
 '{user_name}');
```

清单 5.8 将显示角色授予最终用户

如果您使用的是客户或合作伙伴帐户，角色分配过程与试用帐户类似，但需要使用一组不同的存储过程。有关应调用哪些过程以及具体调用语法的详细信息，请参阅 SAP HANA 安全指南，可在线查阅 http://help.sap.com/hana_platform。

### 5.7.3 导入测试数据

完成角色分配后，我们的书店应用程序即可正式投入运营。但是，由于我们创建的表是空的，该应用程序实际上并不能发挥多大作用。因此，为了让应用程序运行起来，我们需要将一些测试数据加载到数据模型中。

虽然在 SAP HANA 中完成数据加载有多种方法，但一个方便的选择是使用 Eclipse IDE 中安装的 SAP HANA Tools 插件包含的数据导入向导。在此，我们可以选择从 CSV 文件、Excel 文件等上传测试数据。

为演示目的，我们随书源代码包（可从 www.sap-press.com/3638 下载）中包含了一系列 CSV 文件，您可以使用这些文件用一些示例数据预填充书店数据模型。要将这些文件导入到自定义书店架构中，请执行以下步骤：

- 1. 在 Eclipse IDE 中，打开 SAP HANA DEVELOPMENT 透视图，并从顶级菜单栏中选择 File > IMPORT... 菜单选项。
- 2. 这将打开图 5.34 所示的 IMPORT 对话框。在此，展开 SAP HANA Content 文件夹并选择 DATA FROM LOCAL FILE 选项。单击 NEXT > 继续。

![](img/cf7012644082c115a2181376d9b7486d_207_0.png)

图 5.34 从 Eclipse 导入测试数据：第 1 部分

- 3. 在下一步中，系统将提示您选择要上传数据的目标 SAP HANA 系统（参见图 5.35）。选择目标系统，并单击 NEXT >。

![](img/cf7012644082c115a2181376d9b7486d_208_0.png)

图 5.35 从 Eclipse 导入测试数据：第 2 部分

- 4. 选择要上传的源 CSV 文件以及要加载数据的目标表。如图 5.36 所示，此步骤还允许您指定字段分隔符、要上传的文件中的记录范围等。为演示目的，我们将选择默认文件编码、默认记录分隔符（逗号）和 IMPORT ALL DATA 复选框，因为我们希望一次性导入源文件中包含的所有测试数据。单击 NEXT > 按钮继续。
- 5. 在管理表定义和数据映射步骤（图 5.37）中，将源 CSV 文件中的字段映射到目标表中的相应字段。由于测试文件已完全填充，您可以选择图 5.37 中突出显示的 One to One 菜单选项以自动映射字段。在定义映射的同时，您可以在 IMPORT 对话框的底部面板中预览导入（参见图 5.37）。所有映射就位后，单击 Finish 按钮以启动导入过程。

