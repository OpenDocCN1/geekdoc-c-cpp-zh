
第一行创建一个 `System.Random` 对象，`Get-EndPassword` 函数接受单个输入参数，并作为下一行的上限。`ForEach` 为范围内的每个数字选择一个 33 到 127 之间的随机字符代码，并将字符添加到变量 `$NewPassword` 中。当 `ForEach` 执行完毕后，生成的 `$NewPassword` 从函数返回。最后一行调用 `Export-ModuleMember` 函数，这使其在包管理器控制台中可用。

![](img/67a6707ff505c052edb96c0128fb3096_1378_0.png)

# 向 NuGet 包添加文件

使用你创建的两个文件，你将使用 NuGet Package Explorer 创建一个 NuGet 包。打开 NuGet Package Explorer。在 Common tasks（常用任务）对话框中选择 Create a new package（创建新包）。图 G-27 显示了选择 Create a new package 后的 NuGet Package Explorer 界面。

![](img/67a6707ff505c052edb96c0128fb3096_1379_0.png)

图 G-27

将 `.ps1` 和 `GenRandomPassword.ps1` 文件都拖到 NuGet Package Explorer 中标题为 Package contents（包内容）的窗格中。对于这两个文件，NuGet Package Explorer 都会识别它们为 PowerShell 脚本，并询问你是否希望将文件置于 tools 文件夹中。对这两个文件都回答 Yes（是），以便 Package Explorer 创建 tools 文件夹并将两个文件都放入其中。现在，你需要编辑包的元数据。

# 编辑 NuGet 包元数据

你需要编辑包的元数据，以针对你的特定包进行定制。从菜单中选择 Edit Metadata（编辑元数据）。主要字段是 Id 字段。Id 字段应设置为你的 NuGet 包名称。在本示例中，将 Id 字段更改为 GenRandomPassword。图 G-28 显示了编辑元数据后的 NuGet Package Explorer 界面。

![](img/67a6707ff505c052edb96c0128fb3096_1379_1.png)

图 G-28

完成元数据编辑后，点击 Package metadata 窗格左上角如图 G-28 所示的勾号。

# 部署 NuGet 包

现在你可以发布 NuGet 包了。为了将包发布到托管的 NuGet 库，你可以使用 File Publish（文件发布）项。但测试包的最好方法之一将其保存到本地或文件共享 NuGet 库。从 NuGet Package Explorer 菜单中选择 File > Save（文件 > 保存），并将 `.nupkg` 文件保存到你在上方 File Share Hosting（文件共享托管）部分使用的本地文件夹或文件共享中。

打开 Package Manager Console（包管理器控制台），并将 NuGet 源设置为你的本地库。输入以下命令安装 GenRandomPassword NuGet 包：

```
Install-Package GenRandomPassword
```

安装包后，测试你在 NuGet 包中向控制台添加的命令。以下命令将生成一个 12 个字符的随机字符串。

```
Get-RndPassword 12
```
