

## UpdatePanel 控件的两个属性

| 属性 | 描述 |
|---|---|
| ChildrenAsTriggers | 确定面板中的控件是否被视为触发器，当控件导致回发时，面板的内容会被更新。默认值为 True。 |
| UpdateMode | 确定面板内容何时被更新。如果设置为 Always，则面板在每次回发时都会被更新。如果设置为 Conditional，则面板仅在其自身的触发器导致回发时才会被更新。嵌套的 UpdatePanel 控件在其父 UpdatePanel 控件被更新时始终会被更新。默认值为 Always。 |

## UpdatePanel 控件的起始 aspx 代码

```
<asp:UpdatePanel ID="UpdatePanel1" runat="server">
    <ContentTemplate>
    </ContentTemplate>
</asp:UpdatePanel>
```

## 指定触发器的 UpdatePanel 控件的 aspx 代码

```
<asp:UpdatePanel ID="UpdatePanel1" runat="server">
    <ContentTemplate>
        <asp:Button ID="Button2" runat="server" Text="Add" />
    </ContentTemplate>
    <Triggers>
        <asp:AsyncPostBackTrigger ControlID="Button1" EventName="Click" />
        <asp:PostBackTrigger ControlID="Button2" />
    </Triggers>
</asp:UpdatePanel>
```

## 描述

- UpdatePanel 控件的 ContentTemplate 元素包含在异步回发期间被更新的控件。UpdatePanel 控件可以嵌套。
- 你可以使用 Triggers 元素来指定导致面板被更新的控件。asp:AsyncPostBackTrigger 元素标识 UpdatePanel 控件内部或外部的控件，该控件触发异步回发。asp:PostBackTrigger 元素标识 UpdatePanel 控件内部的控件，该控件触发完整回发。

## 与其他控件的兼容性问题

- 如果将 GridView 和 DetailsView 控件的 EnableSortingAndPagingCallbacks 属性设置为 True，则它们不能在 update panel 中使用。
- 如果启用了非异步回发一部分的回调、将样式直接作为控件属性设置，或将 EnableClientScript 属性设置为 False，则 TreeView 控件不能在 update panel 中使用。
- 如果将样式直接作为控件属性设置，则 Menu 控件不能使用。
- FileUpload 控件只能用作 update panel 的回发触发器。
- Login、PasswordRecovery、ChangePassword 和 CreateUserWizard 控件只能在将其内容转换为可编辑模板时使用。

## 如何使用 Timer 控件

Timer 控件触发周期性异步回发。此控件通常放置在回发发生时被更新的 UpdatePanel 控件的 ContentTemplate 元素内部。如果它未放置在 UpdatePanel 控件内部，则会触发整个页面的完整回发。

图 21-9 说明了 Timer 控件的工作原理。首先，你可以通过设置控件的 Interval 属性来确定异步回发发生的频率。该属性以毫秒为单位进行测量（1/1000 秒）。在本图的示例中，Interval 属性设置为 10,000，即 10 秒。

当你设置 Interval 属性时，应注意不要指定过小的值。如果这样做，可能会对服务器造成严重负载，尤其是在许多人显示该页面时。在大多数情况下，5,000 到 10,000 毫秒可能是你想要使用的最小值。

此外，你不应该期望计时器非常准确。这是因为它受限于网页浏览器中 JavaScript 可用的计时机制，而这些机制可能偏差数百毫秒。

如果需要，你可以在同一页面上放置两个或多个 Timer 控件。在大多数情况下，你会将这些控件放置在不同的更新面板中。然后，你通常会将 UpdatePanel 控件的 UpdateMode 属性设置为 Conditional，以便一个面板中的 Timer 不会触发另一个面板的更新。

尽管你可以在同一个 update panel 中使用两个或多个 Timer 控件，但通常没有必要这样做。相反，如果你需要 update panel 根据网页中发生的情况以不同的速率刷新，你可以使用单个 Timer 控件并更改其 Interval 属性。如果你想使用具有预设间隔的两个或多个 Timer 控件，则可以使用控件的 Enabled 属性来确定在任何给定时间使用哪个控件。

## 设计视图中的 Timer 控件

![](img/c024ccf88e28c30c07dd410d4342288f_732_0.png)

## Timer 控件的两个属性

| 属性 | 描述 |
|---|---|
| Interval | 确定控件以毫秒为单位多久触发一次异步回发。默认值是 60,000 毫秒（60 秒）。 |
| Enabled | 确定当 Interval 属性指定的时间过去时是否发生回发。默认值为 True。你可能会将此属性设置为 False，如果你在同一面板中包含多个 Timer 控件，但希望在任何给定时间只有一个发起回发。 |

## 带有 Timer 控件的 UpdatePanel 控件的 aspx 代码

```
<asp:UpdatePanel ID="UpdatePanel1" runat="server">
    <ContentTemplate>
        <asp:Timer ID="Timer1" runat="server" Interval="10000">
        </asp:Timer>
    </ContentTemplate>
</asp:UpdatePanel>
```

## 描述

- Timer 控件应放置在计时器触发异步回发时被更新的 UpdatePanel 控件的 ContentTemplate 元素内部。
- 将 Interval 属性的值设置得过小可能会导致对 Web 服务器的负载增加以及对 Web 服务器的流量增加。
- Timer 控件的准确性取决于用户网页浏览器中 JavaScript 实现的准确性。

图 21-9    如何使用 Timer 控件

## 如何使用 UpdateProgress 控件

UpdateProgress 控件在异步回发进行时向用户显示信息。你在控件的 ProgressTemplate 元素中对该信息进行编码，如图 21-10 所示。这里，信息由简单文本组成，但你也可以包含控件。请注意，此文本仅在异步回发进行时显示。否则，它是隐藏的。

UpdateProgress 控件的 DynamicLayout 属性决定为控件的内容分配多少空间。默认情况下，仅在显示内容时分配空间。这意味着页面上出现在 UpdateProgress 控件之后的元素在显示内容时会向下移动，并在内容再次隐藏时移回。如果这不是你想要的，你可以通过将 DynamicLayout 属性设置为 False 来在内容未显示时也为其分配空间。开发人员需要确定哪种布局最适合页面。

在某些情况下，异步回发发生得如此之快，以至于 UpdateProgress 控件的内容在屏幕上闪烁。为了防止这种情况发生，你可以设置 DisplayAfter 属性来确定控件在异步回发开始后等待多长时间再显示其内容。默认情况下，此属性设置为 0.5 秒。然后，如果回发完成时间超过该时间，UpdateProgress 控件的内容就会显示在页面上。

在大多数情况下，你会将 UpdateProgress 控件编码在 UpdatePanel 控件内，如本图所示。然后，其内容仅在该面板发生异步回发时显示。但是，你也可以将 UpdateProgress 控件编码在 UpdatePanel 控件之外。然后，你可以将它的 AssociatedUpdatePanelID 属性设置为你想要使用它的面板的 ID。或者，你可以省略此属性，在这种情况下，其内容在任何异步回发发生时都会显示。

