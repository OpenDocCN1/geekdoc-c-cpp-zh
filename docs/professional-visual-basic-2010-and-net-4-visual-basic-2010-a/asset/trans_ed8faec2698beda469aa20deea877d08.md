
```
FileIOPermissionAccess.AllAccess,
"C:\Test"
oFp.PermitOnly()
'Try
Dim strmWrite As New IO.StreamWriter(
    File.Open("C:\Test\Permission.txt",
    IO.FileMode.Open))
strmWrite.WriteLine("Hi there!")
strmWrite.Flush()
strmWrite.Close()
Dim objWriter As New IO.StreamWriter(
    File.Open("C:\Test\NoPermission.txt",
    IO.FileMode.Open))
objWriter.WriteLine("Hi there!")
objWriter.Flush()
objWriter.Close()

'Uncomment the lines below (comment those above) to reverse the test.

'Dim oFp = New FileIOPermission(FileIOPermissionAccess.Read, "C:\")
'oFp.PermitOnly()
'Dim temp = oFp.AllFiles.ToString()
'Dim strmWrite = New IO.StreamWriter(
'    File.Open("C:\Test\Permission.txt",
'    IO.FileMode.Open))
'strmWrite.WriteLine("Hi there!")
'strmWrite.Flush()
'strmWrite.Close()
'Dim objWriter = New IO.StreamWriter(
'    File.Open("C:\Test\NoPermission.txt",
'    IO.FileMode.Open))
'objWriter.WriteLine("Hi there!")
'objWriter.Flush()
'objWriter.Close()
'Catch objA As System.Exception
'MessageBox.Show(objA.Message)
'End Try
End Sub
```

来自 Form1.vb 的代码片段

第一个示例尝试访问文件系统中的文件。这演示了 FileIOPermission 类的用法。在 C:\ 驱动器上创建一个名为 Test 的新文件夹。在此文件夹中创建两个新文件，第一个文件 C:\Test\Permission.txt 将使用创建账户时分配的默认权限。第二个文件 C:\Test\NoPermission.txt（这些文件不包含在下载中）的权限已被修改。

为此，请右键单击文件并选择“属性”来访问文件的属性。在“属性”对话框中选择“安全”选项卡，然后使用“高级”按钮。在“高级安全设置”对话框中，使用“更改权限”按钮打开“高级安全设置”对话框。接下来，转到此对话框的底部，取消选中“包括可从该对象的父项继承的权限”复选框。您需要确认要将此文件的安全设置添加到文件本身。在通过单击“确定”按钮返回原始的“属性”对话框后，您需要删除“授权用户”的设置。为此，您需要使用“编辑”按钮访问“权限”对话框，在其中可以使用“删除”按钮。完成此操作后，您将删除经过身份验证的用户对此文件的默认修改权限。结果应如图 32-3 所示的权限级别。请注意，只有三个组或用户名被分配了权限。

![](img/d99870e80390742f93963da7be0b2e61_1030_0.png)

# 图 32-3

查看前面的代码片段，注意 Sub TestFileIOPermission 首先向当前用户授予 FileIO 写权限，并尝试访问这两个文件。对于 NoPermissions.txt 文件，这将失败，因为代码访问安全性无法在运行时向用户授予额外的访问权限。您可以在图 32-4 所示的错误中看到此结果。

![](img/d99870e80390742f93963da7be0b2e61_1030_1.png)

# 图 32-4

现在测试相反的情况，将上述方法的前半部分注释掉，并取消注释后半部分。现在该方法使用 PermitOnly 分配将用户限制为 FileIO 权限集的只读权限。在这种情况下，代码在尝试写入 Permission.txt 文件时会失败，因为此设置的限制比操作系统允许的更严格。您可以在图 32-5 所示的错误中看到此结果。

![](img/d99870e80390742f93963da7be0b2e61_1031_0.png)

图 32-5

# 用户访问控制

随着 Windows Vista 的推出并延续到 Windows 7，开发人员开始意识到一种新的安全模型：用户访问控制（UAC）。UAC 的核心前提是，即使具有管理员权限的用户也应通常在降级权限的用户账户上下文中运行。这个概念很简单，是一种最佳实践。不幸的是，与任何权限被削减的情况一样，应用程序开发人员和用户在提升权限下运行了太长时间，以至于每当系统打断他们想要做的事情时，他们都会感到不满。但要让安全机制发挥作用，有时最好保持访问受限，并迫使您认识到何时授予访问权限。这正是 UAC 系统所做的：它锁定访问；您仍然有能力授予该访问权限，但系统会让您暂停并评估是否应授予该访问权限。如果您在意外情况下收到 UAC 提示，或者意识到您不完全信任的软件正在尝试获得您可能未预料到或不希望它拥有的特权访问，那么这比系统不提示您授予该访问权限要好得多。所有这些只需点击一下鼠标即可。

UAC 的名声不太好，部分原因是它在定制应用程序开发人员甚至 Microsoft 开发人员能够走在所需代码更改之前，就作为 Vista 的一部分被介绍给最终用户。因此，用户们会问：“为什么我会收到这个提示？”开发人员当时没有真正好的答案，只能回答：“因为 Vista 改变了一些东西。”不幸的结果是，许多人和组织关闭了 UAC。然而，作为开发人员，您现在应该在自己的桌面上重新启用它，并开始理解如何在默认约束之内和之外工作。

# 定义应用程序 UAC 设置

默认情况下，在 Visual Studio 2010 中，您的应用程序设置包含与 UAC 相关的信息。您可以创建应用程序，使其附带某些权限。在应用程序清单中，您将找到 requestedPrivileges 部分。此部分定义了应用程序请求的 UAC 执行级别。

要访问应用程序清单，请在解决方案资源管理器中右键单击项目，然后选择“属性”。在“属性”窗格中，选择“应用程序”选项卡，您会找到一个标记为“查看 Windows 设置”的按钮。选择此按钮将在编辑器窗口中打开您的应用程序清单（app.manifest）XML 文件。在 XML 中，您将找到 requestedPrivileges 节点，以下代码块中显示了该节点的副本：

```
<requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">
    <!-- UAC Manifest Options
        If you want to change the Windows User Account Control level replace the
        requestedExecutionLevel node with one of the following.

        <requestedExecutionLevel level="asInvoker" uiAccess="false" />
        <requestedExecutionLevel level="requireAdministrator" uiAccess="false" />
        <requestedExecutionLevel level="highestAvailable" uiAccess="false" />

        Specifying requestedExecutionLevel node will disable file and registry
        virtualization. If you want to utilize File and Registry Virtualization
        for backward compatibility then delete the requestedExecutionLevel node.-->
    <requestedExecutionLevel level="asInvoker" uiAccess="false" />
</requestedPrivileges>
```

来自 app.manifest 的代码片段

这段 XML 的美妙之处在于，Microsoft 花时间加入了关于 requestedExecutionLevel 设置的有意义的 XML 注释。默认情况下，如前面的代码片段所示，您的应用程序请求以 asInvoker 运行。因此，正如前面在查看您以哪个组身份运行时讨论的那样，这意味着您以用户身份运行，而不是管理员身份。

正如注释所表明的，可以将其更改为 requireAdministrator，因此请进行此更改。接下来，确保在 ProVB_Security 项目的 ButtonTest 单击事件处理程序中，Sub DisplayPrincipalIdentity() 和 Sub TestFileIOPermission() 都未被注释。最后，在 Sub TestFileIOPermission() 中，确保已恢复哪个块被注释；代码应类似于之前的清单，其中方法的后半部分被注释，前半部分未被注释。现在您已表明此应用程序需要管理员权限，您可以重复第一个测试，即用户账户没有写入 NoPermission.txt 的权限，但代码尝试授予权限。请注意，此测试取决于管理员是否有权限访问文件 C:\Test\NoPermission.txt。保存对 app.manifest 的更改并尝试运行应用程序。如果您在 Windows 7 上运行，并且没有使用“以管理员身份运行”启动 Visual Studio 2010，您应该会看到图 32-6 中所示的错误。

![](img/d99870e80390742f93963da7be0b2e61_1032_0.png)

图 32-6
