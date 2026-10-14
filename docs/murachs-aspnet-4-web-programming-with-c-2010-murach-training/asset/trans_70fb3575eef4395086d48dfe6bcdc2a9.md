

## 万圣节商店应用购物车页面中的后退按钮问题示例

1. 用户将两件商品添加到购物车。购物车数据存储在会话状态中，当前包含两件商品：一件疯猫（Deranged Cat）售价 19.99 美元，一件飞蝙蝠（Flying Bats）售价 69.99 美元。浏览器窗口中显示的购物车如下图所示：

![](img/c024ccf88e28c30c07dd410d4342288f_708_0.png)

2. 用户选择疯猫商品，并点击“删除项目”按钮将其删除。该商品从会话状态的购物车中删除，更新后的页面被发送到浏览器：

![](img/c024ccf88e28c30c07dd410d4342288f_708_1.png)

3. 用户最终还是决定要购买疯猫，于是点击浏览器的“后退”按钮对象。指定“Pragma”为键、“no-cache”为值可禁用缓存。

## 用于禁用页面缓存的代码

```
Response.Cache.SetCacheability(HttpCacheability.NoCache);
Response.Cache.SetExpires(Now.AddSeconds(-1));
Response.Cache.SetNoStore();
Response.AppendHeader("Pragma", "no-cache");
```

## 说明

- 你可以通过让浏览器不缓存包含状态敏感数据的页面来限制“后退”按钮的影响。然后，当用户试图使用“后退”按钮返回某个页面时，该页面可能会被重新加载，或者可能会显示一条警告消息，说明该页面已过期。如果显示了警告消息，用户可以点击“刷新”按钮重新加载页面。
- 你可以将禁用浏览器页面缓存的代码放在处理页面 Load 事件的方法中。每次加载页面时都应执行此代码。
- 遗憾的是，此图所述技术并非适用于所有浏览器。因此，你可能需要使用下一张图中的技术来防止“后退”按钮问题。

## 如何使用时间戳避免“后退”按钮问题

图20-14展示了避免“后退”按钮问题最可靠的方法。在这里，你会看到一个网页的代码，该网页使用时间戳来确定提交的页面是否是最新的。基本技术是在页面提交时将时间戳记录在两个地方：视图状态和会话状态。然后，视图状态的时间戳被发送回浏览器，并与页面上的其余信息一起缓存，而会话状态的时间戳则保存在服务器上。

稍后，当用户第二次提交页面时，Page_Load 方法会调用一个名为 IsExpired 的私有方法。该方法从视图状态和会话状态中检索时间戳并加以比较。如果它们相同，则页面是最新的，IsExpired 返回 False。但如果它们不同，则表明用户提交的页面是通过“后退”按钮从浏览器缓存中取回的。在这种情况下，IsExpired 方法返回 True。然后，Page_Load 方法重定向到名为 Expired.aspx 的页面，该页面随即显示一条消息，说明页面已过期，无法提交。

请注意，在比较会话状态和视图状态中的时间戳项之前，IsExpired 方法会检查这两个项是否存在。如果不存在，该方法返回 False，这样当前时间戳就可以同时保存在会话状态和视图状态中。

当然，要让这种方法起作用，页面必须回发到服务器。这意味着，如果你首先想检查当前页面是否尚未过期，就不能使用按钮的 PostBackUrl 属性来显示另一个页面。例如，假设用户从购物车中删除一个商品，然后使用“后退”按钮将其重新加回，如图20-12所示。然后，如果用户点击“结账”按钮或“继续购物”按钮，你希望显示 Expired 页面，这样用户就会知道购物车是不准确的。要做到这一点，“结账”和“继续购物”按钮必须将购物车页面回发到服务器，而使用 PostBackUrl 属性则不会发生这种情况。

顺便提一下，这种技术也可以用来处理用户点击“刷新”按钮时出现的问题。这会将页面提交到服务器并获得新的响应，从而刷新页面，因此与浏览器缓存无关。然而，这可能会导致一些问题，比如用户在不知情的情况下两次订购同一商品。不过，由于大多数用户点击“后退”按钮的次数远远多于“刷新”按钮，“刷新”按钮导致的错误要少得多。这就是大多数 Web 开发人员忽略此问题的原因。

## 一个通过检查时间戳来避免“后退”按钮问题的页面

```
public partial class Cart : System.Web.UI.Page
{
    private CartItemList cart;

    protected void Page_Load(object sender, EventArgs e)
    {
        if (IsExpired())
            Response.Redirect("Expired.aspx");
        else
            this.SaveTimeStamps();
            cart = CartItemList.GetCart();
            if (!IsPostBack)
                this.DisplayCart();
    }

    private bool IsExpired()
    {
        if (Session["Cart_TimeStamp"] == null)
            return false;
        else if (ViewState["TimeStamp"] == null)
            return false;
        else if (ViewState["TimeStamp"].ToString() ==
                 Session["Cart_TimeStamp"].ToString())
            return false;
        else
            return true;
    }

    private void SaveTimeStamps()
    {
        DateTime dtm = DateTime.Now;
        ViewState.Add("TimeStamp", dtm);
        Session.Add("Cart_TimeStamp", dtm);
    }
    .
    .
}
```

## 说明

- 避免“后退”按钮问题的一种方法是使用时间戳。页面保存通过 Now 属性获得的时间戳的两个副本：一个在视图状态中，另一个在会话状态中。
- IsExpired 方法测试视图状态和会话状态中的时间戳，以确保它们相同。如果它们不相同，则说明用户提交的页面是从浏览器缓存中获取的。

## 注意

- 一些开发者更倾向于使用随机数而不是时间戳。这两种技术都可以。

