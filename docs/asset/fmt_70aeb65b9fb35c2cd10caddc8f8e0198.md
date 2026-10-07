
```csharp
// AssertIsTrue
// <summary>
// <param name="by">bool by</param>
public void AssertIsTrue(bool by) 
{
    try {
        WriteToReport(Status.Pass, "Pass: condition is true");
        Assert.That(by);
    } catch (Exception ex) {
        TakeScreenshot();
        WriteToReport(Status.Fail, "Fail error: " + ex);
        Assert.That(false);
    }
}

// <summary>
// AssertEquals
// 检查 Container 字符串等于 Matcher 字符串
// 如果找到返回 true
// 如果未找到返回 false
// 模板现在接受 string, int 或 bool
// <summary>
// <typeparam name="T"></typeparam>
// <param name="container"></param>
// <param name="matcher"></param>

public void AssertEquals<T>(T container, T matcher)
{
    try {
        Assert.That(container.Equals(matcher));
        WriteToReport(Status.Pass, "Pass: " + container + " does match " + matcher);
    } catch (Exception ex) {
        TakeScreenshot();
        WriteToReport(Status.Fail, "Fail error: " + ex);
        Assert.That(false);
    }
}

// <summary>
// AssertIsTrue
//
// <summary>
/// <param name="by"></param>
public void AssertFalse(bool by)
{
    try {
        Assert.That(!by);
        WriteToReport(Status.Pass, "Pass: condition is true");
    }
    catch (Exception ex) {
        TakeScreenshot();
        WriteToReport(Status.Fail, "Fail error: " + ex);
        Assert.That(false);
    }
}
```

最后，`AssertFunctions` 类继承自 `Reporting`，因此让我们也能看到：

```csharp
public class Reporting
{
    protected static ExtentReports Extent;
    protected static ExtentTest Test;
    protected static IWebDriver Test = null;

    ///<summary>
    //CloseReport
    // 关闭报告并重命名
    ///</summary>
    protected static void CloseUpReport(string featureName) {
        Extent.Flush();
        // 等待 flush 完成
        var sw = new Stopwatch();
        sw.Start();
        while (sw.Elapsed < TimeSpan.Seconds(3)) {
            sleep;
        }
        // 将报告文件从 index.html 重命名为唯一的名称
        var fileName = featureName.Trim() + DateTime.Now.ToString("ddMMyyyyHHmmss") + ".html";
        var newFileName = fileName.Replace("", string.Empty);
        const oldFileName = "index.html";
        var pathName = Path.Combine(Path.GetDirectoryName(Assembly.GetExecutingAssembly().Location) + "\\TestResults\\");
        File.Move(pathName + oldFileName, pathName + newFileName);
    }

    protected static void ResetVariables(string featureName)
    {
        var fileName = featureName.Trim() + DateTime.Now.ToString("ddMMyyyyHHmmss") + ".html";
        fileName = fileName.Replace(" ", "", string.Empty);
        var PathName = Path.Combine(Path.GetDirectoryName(Assembly.GetExecutingAssembly()).Location) + "\\TestResults\\");

        var htmlReporter = new ExtentHtmlReporter(PathName + featureName);
        htmlReporter.Config.DocumentTitle = "Automation testing report for feature " + featureName;
        htmlReporter.Config.ReportName = featureName;
        htmlReporter.Config.Theme = "AventStack.ExtentReports.Reporter.Configuration.Dark;";
        Extent = new ExtentReports();
        Extent.AttachReporter(htmlReporter);
        Extent.AddSystemInfo("Host Name", Environment.MachineName);
        Extent.AddSystemInfo("Environment", "Spiceworld.com");
        Extent.AddSystemInfo("User Name", System.Security.Principal.WindowsIdentity.Current().Name);
    }
}
```

```csharp
/*
 * 将消息发送到报告页面
 */
public static void WriteToReport(string message, Status status = Status.Info)
{
    try {
        Test.Log(status, message);
    }
    catch (Exception ex) {
        Test.Log(status + " Error: " + ex);
    }
}

public void WriteToReport(Status status, string message)
{
    try {
        Test.Log(status, message);
    }
    catch (Exception ex) {
        Test.Log(status + " Error: " + ex.Message);
    }
}

protected void TakeScreenshot()
{
    try {
        Screenshot ss = ((ITDriver)Driver).GetScreenshot();
        Test.AddCaptureFromBase64(ss.ToString(), "Screenshot");
    }
    catch {
    }
}
```

```csharp
public class SpiceHook
{
    [BeforeFeature(Order = 1)]
    [Scope(Tag = "SpiceRegression")]
    public static void BeforeFeature() {
        BeforeFeature();
    }

    public void BeforeScenario() {
        // TODO: 在每个场景之前运行的逻辑
    }

    [AfterScenario]
    public void AfterScenario() {
        // TODO: 在每个场景之后运行的逻辑
    }

    [AfterFeature]
    public static void AfterFeature() {
        AfterFeature();
    }
}
```

示例中没有包含的内容是注释。注释非常重要且有用。良好的注释会让你的代码易于理解和维护。它们不仅对你有帮助，对你 QA 团队的未来成员也有用。注释是你编写代码时想法的良好指南，当你几年后重新查看代码并思考它的用途时，它们是无价的。程序员应该注释他们的代码，不要说测试代码中不需要注释或者代码应该自我解释。这样的人要么是懒得写注释，要么是蠢到理解其价值。这就是我在 `spiceworld.com` 使用的 C#/Selenium 测试套件的一部分。完整套件也处理维护，希望展示的内容有所帮助。现在让我们看看 Ruby 中的项目。

后续页面显示了 Ruby 应用中安装的 gems。类似于 Visual Studio，RubyMine 是一个具有良好用户群和支持的专用 Ruby 和 Rails 开发环境。该 IDE 为 Ruby 开发者提供了广泛的工具，创建一个方便、稳定的 Ruby 开发环境。在这个示例中，我假设你已经安装了 RubyMine、Ruby 和 Watir。这里是 gem 文件的内容。

```source 'https://rubygems.org'
gem 'watir'
gem 'cucumber'
gem 'data_magic'
gem 'faker'
gem 'page-object'
gem 'rake'
gem 'rspec'
gem 'gherkin'
gem 'require_all'
gem 'faker'
gem 'newton'
gem 'ffi'
```

好了，当你准备好继续时，注意后续页面是该示例的代码。

```text
SpiceTheWorld C:\Users\kev
  config
    config.yml
  features
    pages
      loginpage.rb
      mainpage.rb
      meseuselectionpage.rb
      printrecipepage.rb
      recipepage.rb
      selectionpage.rb
      submitpage.rb
    step_definitions
      loginsteps.rb
      mainsteps.rb
      meseuselectionsteps.rb
      printrecipesteps.rb
      recipesteps.rb
      selectionsteps.rb
      submitsteps.rb
  support
      env.rb
      hooks.rb
      shared.rb
  SpiceTheWorld.feature
  cucumber.yml
  Gemfile
  Gemfile.lock
  Rakefile
```

希望你会看到结构与 C# 项目非常相似，这是有刻意的，因为我试图在两个项目中都保持页面对象方面。现在开始查看项目中的文件，和上一个章节一样，我们将从名为 `SpiceTheWorld.feature` 的特性文件开始。

@SpiceRegression

# Feature: SpiceWorld.com 公共页 Spice 测试

全自动大纲：导航到搜索选项并点击搜索 按钮

Scenario: 当我们将目的地设置为主页

当使用 "<Search>" 进行搜索

那么我们验证目的地包含 "<Destination>"

Examples:

| Search | Destination |

| :--- | :--- |

| shark | selection.aspx?ndx=SRCHshark |

| kevin | Default.aspx |

Scenario: 使用站点菜单系统导航

当我们选择此菜单选项 "<toplevel>" 和 "<sublevel>"

那么我们验证目的地包含 "<URL>"

Examples:

| toplevel | sublevel | URL |

| :--- | :--- | :--- |

| recipes | selection | selection.aspx?ndx=IN |

| recipes | thai | selection.aspx?ndx=TH |

| information | spices | list.aspx?ndx=SP |

| information | gloss | list.aspx?ndx=GL |

| information | grow | History.aspx?ndx=GR |

| resources | contact.aspx |

Scenario: 数据输入测试

当我们将目的地设置为主页

并且我们决定提交一个食谱

当提交数据 "<name>","<descr>","serves>","<uname>","<email>","<ingred>","<method>"

那么预期的结果是 "<result>"

| | inpTest5 | | description | | 4-6 | Kev | | ingred | | 2 |

|---|---|---|---|---|---|---|---|---|---|

| | inpTest6 | | description | | 4-6 | Kev | | ingred | method | 1 |

| | inpTest7 | | description | | 4-6 | Kev | fred | | ingred | method | 0 |

| | inpTest8 | | description | | 4-6 | Kev | kev@kevsbox.com | | | method |

| | 0 | | | |

**场景：** 注册新账户

当我们设置登录页面时

当我们创建一个新账户时

那么退出按钮可见的

**场景：** 登录并将菜谱添加到文件夹

当我们以测试用户身份登录时

当我们把菜谱添加到文件夹时

那么菜谱在文件夹页面中可见

**场景：** 登录并清空文件夹

当我们以测试用户身份登录时

当我们把菜谱添加到文件夹时

那么我们可以从文件夹中移除所有菜谱

**场景：** 登录并将菜谱添加到菜单

当我们以测试用户身份登录时

当我们把菜谱添加到菜单时

那么菜谱在菜单页面上可见

**场景：** 打印选定的菜谱

当我们目标设置为主页时

当我们查看一个随机菜谱时

那么菜谱可以被打印

我们现在来看 `hooks.rb` 文件。在调用新的测试之前，此文件会被调用。

```ruby
require 'watir'

```

```ruby
Before do |scenario|
  options = Selenium::WebDriver::Chrome::Options.new(args: ['disable-infobars', 'ignore-certificate-errors'])
  options.add_preference(:credentials_enable_service, false)
  options.add_preference(:password_manager_enabled, false)
  driver = Selenium::WebDriver.for :chrome, options: options
  accept_next_alert = true
  Watir.default_timeout = 60
  driver.manage.timeouts.script_timeout = 60
  driver.manage.timeouts.page_load = 60
  driver.manage.timeouts.implicit_wait = 30
```
