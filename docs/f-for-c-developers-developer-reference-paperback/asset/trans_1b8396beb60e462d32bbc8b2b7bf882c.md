

```fsharp
type MyControl() =
  inherit Web.Control;

  [JavaScript> this.Body = ScriptModule.Main() => _
  override
```

**注意** 分段输出 `-> _` 用于将输出转换为 Formlet 类型。分段 `-> _` 告诉 F# 类型推断系统去确定输出。
由于 WebSharper 不支持 sprint，在执行结果中，你需要使用如下所示的代码将数据转换为字符串：
`string data.Name + ":" + string data.Country`

![](img/63aaf94e22830ab98ce16c5946be8ef6_479_0.png)

**图 7-24** 列表 7-62 中 formlet 示例的执行结果

## 将 Formlet 类型用作向导（Wizard）

在本节中，你将扩展之前的示例以获取更多个人信息，例如电话号码和身份证号码。美国人的身份证号码是社会安全号码（SSN），而加拿大和英国使用社会保险号码（SIN）和国民保险号（NI）。根据此处的输入，UI 将发生相应的变化。执行结果如图 7-25 和图 7-26 所示。如果用户选择加拿大，下一页将显示 SIN 作为 ID 类型。`MorePersonalInfo` formlet 接收一个 ID 名称并使用它在 UI 上显示相应的标签。代码中的 Rpc 提供了一种与服务器交互的无缝方式。（参见列表 7-63。）

**列表 7-63** 使用 formlet 作为向导并与服务器创建无缝交互

```fsharp
namespace Website

open IntelliFactory.WebSharper
open IntelliFactory.WebSharper.Html
open IntelliFactory.WebSharper.Formlet
open IntelliFactory.WebSharper.Formlet.Controls
```

```fsharp
module ScriptModule = 

type Person = {
  Name: string
  Country: string
  Phone: string
  IDNumber: string
}
with
  member this.Output() =
  let output = "(\n" + string this.Name + ";"
    + string this.Country + ";"
    + string this.Phone + ";"
    + string this.IDNumber + ";",
  ")
```

```fsharp
[Rpc]
let countries() = ["USA", "SSN", "Canada", "SIN", "UK", "NI"]
```

```javascript
[JavaScript]
let PersonForm () = Formlet<Person>
let name = ""
| Controls.IsNotEmpty("Empty name not allowed")
| Enhance.WithValidationIcon
| Enhance.WithTextLabel("Name")
```

```fsharp
let countryF = 
  Select(0)
  | Enhance.WithTextLabel("Country")
  Formlet.Yield(fun data => {Name = name; Country = data; Phone=""; IDNumber=""})
```

```fsharp
<> nameF
<> countryF
| Enhance.WithLegend("Add a new Person")
| Enhance.WithFormContainer
```

```javascript
[JavaScript]
let MorePersonInfo idName = Formlet<Person>
let phoneF = ""
Controls.Input ""
| Validator.IsNotEmpty("Please input phone number")
| Enhance.WithValidationIcon
| Enhance.WithTextLabel("Phone")
```

```fsharp
let idF = ""
Controls.Input ""
| Validator.IsNotEmpty("Please give your id number")
| Enhance.WithValidationIcon
| Enhance.WithTextLabel(idName)
```

```fsharp
Formlet.Yield (fun phone id -> {Name = ""; Country = ""; Phone=phone; IDNumber = id})

<> phoneF
<> idF
|> Enhance.WithLegend "Add a New Person"
|> Enhance.WithFormContainer
```

```javascript
[JavaScript>
let Main () = {
  let output = Label []
  let fc = {
    Enhance.FormConfiguration.Default with
    Header = "Sample" | Enhance.FormPart.Text | Some
  }
  let personF =
    PersonForm()
    |> Enhance.SubmitAndButtons
    |> Enhance.CustomFormContainer {
            Description = "Step1"
            |> Enhance.FormPart.Text
            |> Some
        }
  let idF =
    MorePersonalInfo nationality
    |> Enhance.SubmitAndButtons
    |> Enhance.CustomFormContainer {
            Description = "Step2"
            |> Enhance.FormPart.Text
            |> Some
        }
  Formlet.Do {
    let! p = personF
    let! i = idF (p.Country)
    Formlet.OneFrame (fun () -> Div [Text "Thank you!"])
    |> Formlet.Map (fun -> {
        Name = p.Name;
        Country = p.Country;
        Phone = i.Phone;
        IDNumber = i.IDNumber
    })
  }
  |> Formlet.Flow
  |> Formlet.Map ignore
}

type MyControl() =
  inherit Web.Control()

  [JavaScript>
  override this.Body = ScriptModule.Main() => _
```

![](img/63994e22830ab98ce16c5946beef6_482_0
**图 7-25** 用于姓名和国家的 formlet

![](img/63aaf94e22830ab98ce16c5946be8ef6_482_png
**图 7-26** 用于电话号码和身份证号的 formlet

## 创建 HTML5 页面

如前所述，WebSharper 支持 HTML5 页面。列表 64 显示了如何在 *Canvas* 元素上绘制矩形，如图 7-27 所示。

**列表 7-64** 在 *Canvas* 元素上绘制矩形

```fsharp
namespace Website

open IntelliFactory.WebSharper
open IntelliFactory.WebSharper.Html
open IntelliFactory.WebSharper.Html5

module ScriptModule = {
  [JavaScript>
  let example1 (ctx: Context2D) =
    ctx.fillStyle = "rgb(100, 0, 0)"
    ctx.fillRect(10., 10., 50., 50.);
    ctx.fillStyle = "rgba(0, 0, 100, 0.5)"
    ctx.fillRect(30., 30., 50., 50.);

  [JavaScript>
  let Main() {
    let element = HTML5.Tags.Canvas []
    let canvas = As-<CanvasElement> element.Dom
    canvas.Height <- 100
    canvas.Width <- 100
    example1(canvas.getContext "2d")
    Div [Attr.Style "Float: center"] <- [element]
  }

type MyControl() =
  inherit Web.Control()

  [JavaScript>
  override this.Body = ScriptModule.Main() => _
```

![](img/63aaf94e22830ab98ce16c5946beef6_483_0
**图 7-27** HTML5 canvas 上的矩形

WebSharper 和 F# 的结合可以提供良好的动画。在列表 65 中，一个矩形被绘制并从左向右移动。

**列表 7-65** HTML 动画

```fsharp
open System
open IntelliFactory.WebSharper
open IntelliFactory.WebSharper.Html
open IntelliFactory.WebSharper.Html5

module CanvasAnimation =
  [JavaScript>
  let AnimatedCanvas width height caption =
    let element = Tags.New "Canvas" []
    let canvas = As-<CanvasElement> element.Dom
    canvas.Width <- width
    canvas.Height <- height
    let ctx = canvas.getContext "2d"
    let getTime = ref 0
    let rec loop =
      async {
        do! Async.Sleep 50
        do draw(ctx, getTime)
        do getTime := !getTime + 1
        do loop
      }
    draw(ctx, !getTime);
    Async.Start loop
    Div [ Width [string width] ] Attr.Style "float:left" ] << [
      Div [ Attr.Style "float:center" ] << [
        element
        P [ Align "center"] << [
          I [Text <| "Example " + caption]
        ]
      ]
    ]
```

```javascript
[JavaScript]
let Main () =
  let example14 (ctx: CanvasContext2D, time:int) =
    ctx.Save()
    let previous = time - 1
    ctx.ClearRect(float previous, 20., 20., 20.)
    ctx.Rect(float time, 20., 20., 20.)
    ctx.FillRect(time, 20., 20., 20.)

ctx.Restore()
```

```fsharp
Div [
  AnimatedCanvas 150 150 "1"
  Div [ Attr.Style "clear:both"] ]
]

type MyCanvasAnimationViewer() =
  inherit Web.Control()
  [JavaScript]
  override this.Body = CanvasAnimation.Main () => _
```

> 注意 .aspx 页面需要更新以反映 MyCanvasAnimationViewer 类型名。

WebSharper 提供了一次使用 F# 构建解决方案的良好方法。然而，WebSharper 能够启用 F# 设计的复杂算法并使用 HTML5 渲染结果。以下是使用 WebSharper 的优势：

- 使用单一语言用于整个 Web 栈。假设你有现有的 .NET 或 F# 算法实现。WebSharper 可以让开发变得简单得多。
- 浏览器之间的不一致性由框架处理。
- 它会自动利用如 HTML5 等新兴技术。

