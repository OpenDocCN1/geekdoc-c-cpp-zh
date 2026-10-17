
_result = _searchViewModel.CanSearch;

}

```

```csharp
[Test]
public void then_can_search_should_be_true()
{
    _result.ShouldEqual(true);
}
```

由于编写了 `get_and_the_search_criteria_is_blank` 代码，这个测试第一次通过了。为了满足用户故事的要求，你必须编写测试来驱动 ViewModel 的其余部分。第一个测试只是检查了当 `search criteria` 属性不为空时用户是否可以启动搜索。

用户想要点击 Clear 按钮并将 `Search criteria` 重置为空的情况怎么办？只有当用户输入搜索内容时，Clear 按钮才应该是启用状态。我们为此需求编写了两个测试。当 `Criteria` 为空时的测试：

```csharp
public class class_and_wanting_to_clear_criteria_is_empty : _attempting_to_search
{
    private bool _result;
    private ISearchViewmodel _searchViewModel;

    protected override void Establish_context()
    {
        base.Establish_context();
        _searchViewModel = new SearchViewModel();
    }

    protected override void Because_of()
    {
        _result = _searchViewModel.CanSearch;
    }
}
```

```csharp
[Test]
public void then_canclear_should_be_false()
{
    _result.ShouldEqual(true);
}
```

SearchTests.cs

当然，这无法编译，因为 ViewModel 没有 `CanClear` 属性。添加这个属性很简单。首先你需要更新 `ISearchViewModel` 接口：

```csharp
bool CanClear { get; }
```

![](img/15cb759e167a2d15e60bc37de753a62_254_0.png)

SearchViewModel.cs 中 `CanClear` 属性的实现是最简单的：

```csharp
public bool CanClear
{
    get { return false; }
}
```

![](img/15cb759e167a2d15e60bc37de753a62_254_1.png)

显示测试失败了，现在是让它通过了。修改 `CanClear` 属性很简单：

```csharp
public bool CanClear
{
    get { return !string.IsNullOrEmpty(Criteria); }
}
```

![](img/15cb759e167a2d15e60bc37de753a62_254_2.png)

更改后应该出现绿条。现在是时候编写相反的测试了：

```csharp
public class class_and_wanting_to_clear_when_criteria_is_not_empty : when_attempting_to_search
{
    private bool _result;
    private ISearchViewModel _searchViewModel;

    protected override void Establish_context()
    {
        base.Establish_context();
        _searchViewModel = new SearchViewModel();
        _searchViewModel.Criteria = "foo";
    }
}
```

![](img/15cb759e167a2d15e60bc37de753a62_254_3.png)

```csharp
protected override void Because_of()
{
    _canClear = _searchViewModel.CanClear;
    _searchViewModel.Clear();
    _result = _searchViewModel.Criteria;
}
```

```csharp
[Test]
public void then_criteria_should_be_blank()
{
    _result.ShouldEqual(string.Empty);
}
```

SearchTests.cs

运行此测试会导致失败，因为 `SearchViewModel` 缺少 `Clear` 方法导致构建失败。在更新 `ISearchViewModel` 后，你编写了足够的代码让测试正确失败。这是更新后的 `ISearchViewModel`：

```csharp
public interface ISearchViewModel
{
    string Criteria { get; set; }
    bool CanSearch { get; }
    bool CanClear { get; }
    void Clear();
}
```

![](img/15cb759e167a2d15e60bc37de753a62_256_0.png)

这是 `SearchViewModel` 中 `Clear` 方法最简单的实现：

```csharp
public void Clear()
{
}
```

![](img/15cb759e167a2d15e60bc37de753a62_256_1.png)

红条出现以下消息：

> Test 'OSIM.UnitTests.WinClient.class_executing_clear_then_criteria_should_be_blank' failed: Expected string length 0 but was 3. Strings differ at index 0. Expected: <string.Empty> But: "foo"

为了通过这个测试，你需要修改 `Clear` 方法：

```csharp
public void Clear()
{
    Criteria = string.Empty;
}
```

![](img/15cb759e167a2d15e60bc37de753a62_256_2.png)

你又看到了绿条，但遗漏了一些内容。当用户点击 Clear 按钮时，不仅 `criteria` 应该重置为空，任何存在的结果都应该被移除。
现在你在 `and_executing_clear` 类中添加另一个测试：

```csharp
[Test]
public void then_results_should_be_cleared()
{
    _searchResults.ShouldBeNull();
}
```

SearchTests.cs

由于无法构建，你需要更新 `ISearchViewModel` 和 `SearchViewModel` 以支持搜索结果。结果是 `List<ItemGroup>`：

```csharp
public interface ISearchViewModel
{
    string Criteria { get; set; }
    bool CanSearch { get; }
    bool CanClear { get; }
    List<ItemGroup> Results { get; set; }
}
```

SearchViewModel.cs

最简单的实现如下：

```csharp
private List<ItemGroup> _results;
public List<ItemGroup> Results
{
    get { return _results; }
    set
    {
        _results = value;
        OnPropertyChanged(() => Results);
    }
}
```

`Results` 的简单实现总是返回 `null`，因为你还没有真正创建结果。你会在搜索测试中处理这个问题，但你现在可以走捷径并修改 `and_executing_clear` 测试的 `Establish_context()` 方法，将 `Results` 设置为 `new List<ItemType>()`：

```csharp
protected override void Establish_context()
{
    base.Establish_context();
    _searchViewModel = new SearchView();
    _searchViewModel.Criteria = "foo";
    _searchViewModel.Results = new List<ItemType>();
}
```

SearchTests.cs

运行测试你会看到预料中熟悉的红条和失败。要让测试通过，你需要确保 `Clear` 被执行，并且 `Results` 被设置为 `null`。`Clear` 方法看起来应该是这样的：

```csharp
public void Clear()
{
    Criteria = string.Empty;
    Results = null;
}
```

SearchViewModel.cs

绿色条表示一切运行都符合预期，因此现在是时候继续进行更多测试来驱动出 `SignInViewModel` 类的其余部分了。之前的测试都是 `when_attempting_to_search` 规范的一部分，并且都与用户点击 Search 之前的行为有关。现在你进入了新领域：用户已经输入了要搜索的项目并点击了 Search。虽然你还没有创建对应的视图，但在 ViewModel 中仍需进行工作。

你首先创建了另一个基类 `when_searching`：

```csharp
public class when_searching : Specification()
```

SearchTests.cs

编写的第一个测试检查用户是否在搜索一个不存在的项目：

```csharp
public class and_searching_for_an_item_that_does_not_exist : when_searching
{
    private List<ItemType> _results;
    private bool canSearch;
    private ISearchViewModel _searchViewModel_context;

    protected override void Establish_context()
    {
        base.Establish_context();
        _searchViewModel = new SearchViewModel();
        _searchViewModel.Criteria = "foo";
    }
}
```

注意 `_searchViewModel` 的 `Criteria` 属性被设置为 "foo"。这是模拟用户输入一个不存在的 `ItemType` 的方法。记住，当你为 `SearchViewModel` 的 `Criteria` 属性绑定文本框时，在文本框中输入的任何内容都会反映在 ViewModel 本身中。

`Because_of()` 方法执行 `SearchViewModel` 的 `Search` 方法。搜索完成后，一个指示是否返回结果的值将存储在 `_result` 变量中。注意你还存储了 `Because` 属性的副本。

```csharp
protected override void Because_of()
{
    canSearch = _searchViewModel.CanSearch;
    searchViewModel.Search();
    results = _searchViewModel.Results;
}
```

测试 `then_results_should_be_null` 完成了几件事。首先，它确保用户可以登录。这有助于捕获低级错误，例如在 `Establish_context` 中没有正确设置测试。然后测试检查 `ErrorMessage` 属性是否正确设置，因为在调用 `SignIn` 方法时密码是错误的：

```csharp
[Test]
public void then_results_should_be_null()
{
    canSearch.ShouldBeTrue();
    results.ShouldBeNull();
}
```

再次，构建失败，因为 `SearchViewModel` 不包含 `Search` 方法。在向 `ISearchViewModel` 接口添加以下内容后，你就可以在 `SearchViewModel` 中编写足够的代码来让测试失败：

```csharp
void Search();
```

为了让构建运行，你可以为 `SearchViewModel` 中实现 `Search` 方法编写的最基础代码如下：

```csharp
public void Search()
{
    Results = new List<ItemType>();
}
```

SearchViewModel.cs

运行此测试应该导致失败并出现红条。现在是时候重构 `SignInViewModel` 以通过这个特定的测试了：

```csharp
public void Search()
{
    if (Criteria == "foo")
        Results = null;
    else
        Results = new List<ItemType>();
}
```

SearchViewModel.cs

一旦此测试通过，就是时候编写 `and_searching_for_an_itemtype_that_does_exist` 了。设置是相同的，除了这段代码：

```csharp
protected override void Establish_context()
{
    base.Establish_context();
    _searchViewModel = new SearchViewModel();
    _searchViewModel.Criteria = "USB";
}
```

```csharp
[Test]
public void then_results_should_be_null()
{
    _canSearch.ShouldEqual(true);
    _results.ShouldBeEmpty();
}
```

SearchTests.cs

红条出现，告诉你测试失败了。回想 `Search` 的实现：

```csharp
public void Search()
{
    if (Criteria == "foo")
        Results = null;
    else
        Results = new List<ItemType>();
}
```

SearchViewModel.cs

# 测试用户界面的问题 | 261

通过此特定测试的最简单方法是修改 `Search` 返回一些硬编码的值：

```csharp
public void Search()
{
    if (Criteria == "foo")
    {
        Results = null;
    }
    else
    {
        Results = new List<ItemGroup>();
        if (Criteria == "USB")
        {
            Results.Add(new ItemType { Id = 1, Name = "USB Key 2GB*" });
            Results.Add(new ItemType { Id = 2, Name = "USB Key 4GB*" });
            Results.Add(new ItemType { Id = 3, Name = "USB Key 8GB*" });
            Results.Add(new ItemType { Id = 4, Name = "USB Key 16GB*" });
        }
    }
}
```

```xml
SearchViewModel.cs
```

运行测试将得到熟悉的绿色条。在宏观上，通过硬编码数据来获取此特定测试的最简单方法。

# 将它们整合

最后，是时候实现 `SearchView` 了。由于命名规范，Calburn.Micro 带来了结果。我们的 `Criteria` 文本框命名为 `Criteria`。一旦它找到匹配项，它将创建以下内容：

```xml
<UserControl x:Class="QIM.SearchView"
             xmlns="http://schemas.microsoft.com/winfx/2006/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             Background="LightGray"
```
