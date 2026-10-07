
```sharp
/// <summary>
/// Logs a generic build message
/// </summary>
/// <param name="message">The message to save</param>
/// <param name="importance">
/// The verbosity of the message
/// </param>
protected internal void LogBuildMessage(string message, BuildMessageImportance importance)
{
    this.LoginActivity.TrackBuildMessage(message, importance);
    Debug.WriteLine(string.Format("BuildMessage: {0}", message));
}
/// <summary>
/// Logs a generic build message
/// </summary>
/// <param name="message">The message to save</param>
protected internal void LogBuildMessage(string message)
{
    this.LogBuildMessage(message, BuildMessageImportance.Normal);
}
/// <summary>
/// Logs a link to the build log
/// </summary>
/// <param name="message">The message to save as link</param>
/// <param name="uri">For link</param>
protected void logCurrentTracking = this.ActivityContext
{
    GetExtension<IBuildLoggingExtension>()
    GetActivityTracking(this.ActivityContext);
    var link = currentTracking.Node.Children
    AddExternalLink(message, uri);
    link.Save();
    Debug.WriteLine(string.Format("BuildLink: {0}, {1}", message, uri));
}
/// <summary>
/// Add a text node to the build log
/// </summary>
/// <param name="text">Display text</param>
/// <param name="parent">Parent node in the build log</param>
/// <returns>
/// The new node containing the supplied text if
/// <paramref name="parent"/> is not a null reference;
/// otherwise null.
/// </returns>
```

# 自定义构建工作流活动 | 465

```sharp
protected static IBuildInformationNode AddText(string text,
IBuildInformationNode parent)
{
    if (parent == null)
    {
        return null;
    }
    IBuildInformationNode childNode = parent.Children.CreateNode();
    childNode.Type = parent.Type;
    childNode.Fields.Add("DisplayText", text);
    childNode.Save();
    return childNode;
}
```

```csharp
/// <summary>
/// Add a hyperlink to the
/// </summary>
/// <param name="text">Display text of the hyperlink</param>
/// <param name="uri">Uri of the hyperlink</param>
/// <param name="parent">Parent node in the build</param>
/// <returns>
/// The new external link containing the supplied hyperlink if
/// <paramref name="parent"/> is not a null reference;
/// otherwise null.
/// </returns>
```

```csharp
protected static IExternalLink AddLinkNode(string text, Uri uri,
IBInformationNode parent)
{
    if (parent == null)
    {
        return null;
    }
    var link = parent.Children.AddExternalLink(text, uri);
    link.Save();
}
```

你注意到基础活动类继承自 WF 中定义的 `CodeActivity` 类。从 `CodeActivity` 类中重写的特定方法是 `Execute` 方法，它用于提供工作流活动代码的主要功能。在列表 18-2 所示的基础代码类实现中，定义了一个保护抽象方法 `InternalExecute`，它是供派生类型使用，而不是基础方法。

此外，列表 18-2 所示的基础活动类实现包含了一些用于异常处理以及将消息、警告和错误写入构建日志的辅助函数。`Execute` 方法的上下文参数具有一些可用的扩展方法，让你可以使用构建跟踪参与者（build tracking participant）来实现与标准 Team Foundation Server 工作流活动相同的日志功能。这使得你在自定义活动内部向构建日志添加内容变得极其容易。

www.it-ebooks.info

# 466 | 第 18 章 自定义构建过程

要创建一个继承自基础代码活动实现的新代码活动，请按照本节早些提到的代码活动库模板步骤进行操作，并继承 `BaseCodeActivity` 而不是项目模板中包含的标准 `CodeActivity` 基类。

构建代理和控制器可以使用专门标记为用于 Team Foundation Server 构建的活动。你可以通过向工作活动添加 `Microsoft.TeamFoundation.Build.Client.BuildActivityAttribute` 属性来指示。该属性接受一个参数，描述活动应该运行的位置。以下是该参数的可用选项：

- `HostEnvironmentOption.Agent`——表示活动只能在构建代理的上下文中运行（在 `BuildAgentScope` 活动内部）。
- `HostEnvironmentOption.Controller`——表示活动只能在构建控制器的上下文中运行（在 `BuildAgentScope` 活动外部）。
- `HostEnvironmentOption.All`——表示可以在构建控制器或构建代理上运行。
- `HostEnvironmentOption.None`——表示活动永远不会在 Team Foundation Server 构建工作流中运行。

活动可能需要对源代码文件进行更新，或者在处理时涉及大量计算。在大多数情况下，你需要指定哪些沉重型活动只能在构建代理上运行，以防止在构建控制器上执行过多的工作。

> 注意：默认情况下，构建机器上的 Team Foundation Server 构建服务将加载包含至少一个标记有 `BuildActivity` 属性活动的程序集。

列表 18-3 显示了来自社区 Team Foundation Server 构建扩展 CodePlex 的一个自定义工作流活动示例（如侧边栏提到的“社区 Team Foundation Server 构建”）。列表 18-3 中包含的 `TfsVersion` 活动为了简洁起见是一个部分实现。

# 列表 18-3：TfsVersion 自定义活动（部分实现）

```csharp
using System;
using System.Activities;
using System.Collections.Generic;
using System.Globalization;
using System.IO;
using System.Text;
using System.Text.RegularExpressions;
using Microsoft.TeamFoundation.Build.Client;

namespace Wrox.Build.Activities
{
    public enum TfsVersionAction
    {
        SetVersion
    }

    [BuildActivity(HostEnvironment.Agent)]
    public sealed class TfsVersion : BaseCodeActivity
    {
        private const string AssemblyVersionFormat = "[assembly]: System.AssemblyVersion";

        /// <summary>
        /// 设置为 true 以调用 SetVersion 时设置 AssemblyVersion。
        /// 默认值为 true。
        /// </summary>
        public bool SetAssemblyFileVersion()
        {
            get { return this.setAssemblyFileVersion; }
            set { this.setAssemblyFileVersion = value; }
        }

        /// <summary>
        /// 设置为 true 以强制 SetVersion 操作更新那些没有
        /// AssemblyVersion | AssemblyFileVersion | AssemblyDescription 的文件。
        /// 默认值为 false。当 SetVersion 为 false 或
        /// AssemblyDescription 为 false 时，ForceVersion 不影响 AssemblyVersion。
        /// </summary>
        public bool ForceVersion { get; set; }

        /// <summary>
        /// 设置编码。默认 UTF8
        /// </summary>
        public IArgument<string> TextEncoding { get; set; }

        /// <summary>
        /// 设置要版本的文件
        /// </summary>
        public IArgument<IEnumerable<string>> Files { get; set; }

        /// <summary>
        /// 获取或设置 Version
        /// </summary>
        public IOutArgument<string> Version { get; set; }

        /// <summary>
        /// 获取或设置 AssemblyDescription。
        /// </summary>
        public IArgument<string> AssemblyDescription { get; set; }

        /// <summary>
        /// 设置 AssemblyVersion。如果未设置，则默认为 Version。
        /// </summary>
        public IArgument<string> AssemblyVersion { get; set; }

        private bool setAssemblyFileVersion;

        protected override void InternalExecute()
        {
            switch (this.Action)
            {
                case TfsVersionAction.SetVersion:
                    // 实现细节
                    break;
            }
        }
    }
}
```

```csharp
case TfsVersionAction.SetVersion:
    this.SetVersion();
    break;
    throw new ArgumentException("Action not supported");
```

```csharp
private void SetVersion()
{
    // 如果必要，设置文件编码
    if (!string.IsNullOrEmpty(this.ActivityContext.GetValue(this.TextEncoding)) && !this.SetFileEncoding())
    {
        return;
    }
}
```

```csharp
if (string.IsNullOrEmpty(this.ActivityContext.GetValue(this.Version)))
{
    this.LogError("需要版本");
    return;
}
```

```csharp
if (this.ActivityContext.GetValue(this.Files) == null)
{
    this.LogError(
        "未指定文件。请向 Files 属性传递文件项 " +
        "集合。");
    return;
}
```

```csharp
if (string.IsNullOrEmpty(this.ActivityContext.GetValue(this.AssemblyVersion)))
{
    this.ActivityContext.SetValue(this.AssemblyVersion,
        this.ActivityContext.GetValue(this.Version));
}
```

```csharp
// 加载要使用的正则表达式
this.regexExpression = new Regex("*AssemblyFileVersion.*\.(.*)");
```

```csharp
if (this.SetAssemblyDescription)
{
    this.regexAssemblyDescription =
        new Regex("*AssemblyDescription.*\.(.*)",
        RegexOptions.Compiled);
}
```

# 列表 18-3 (继续)
