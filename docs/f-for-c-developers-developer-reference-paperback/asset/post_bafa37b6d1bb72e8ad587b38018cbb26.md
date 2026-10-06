
```fsharp
type MyControl() =
  inherit Web.Control;

  [JavaScript> this.Body = ScriptModule.Main() => _
  override
```

**Note** The segment output -> _ is used to convert the output to a Formlet type. The segment -> _ tells the F# type inference system to figure out the output.
Because sprint is not supported in WebSharper, the execution results are you need to use code such as the following to convert a data to a string:
`string data.Name + ":" + string data.Country`

![](img/63aaf94e22830ab98ce16c5946be8ef6_479_0.png)

**Figure 7-24** Execution result from the formlet sample in Listing 7-62

## Using a Formlet Type as a Wizard

In this section, you will expand the previous sample to get more personal information, such as phone number and ID number. The ID number of a person from the USA is the Social Security Number (SSN), while Canada and UK use the Social Insurance Number (SIN) and National Insurance number (NI). Depending on the input here, the UI changes appropriately. The execution results are shown in Figure 7-25 and Figure 7-26. If the user selects Canada, the next page will show SIN as the ID type. The `MorePersonalInfo` formlet takes an ID name and uses it to display the appropriate label on the UI. The Rpc in the code provides a seamless way to interact with the server. (See Listing 7-63.)

**Listing 7-63** Using a formlet as a wizard and to create seamless interactions with the server

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
    Enhance.FormContainerConfiguration.Default with
    Header = "Sample" | Enhance.FormPart.Text | > Some
  }
  let personF =
    PersonForm()
    |> Enhance.SubmitAndResetButtons
    |> Enhance.WithCustomFormContainer {
        fc with {
            Description = "Step1"
            |> Enhance.FormPart.Text
            |> Some
        }
    }
  let idF nationality =
    MorePersonalInfo nationality
    |> Enhance.SubmitAndResetButtons
    |> Enhance.CustomFormContainer {
        fc with {
            Description = "Step2"
            |> Enhance.FormPart.Text
            |> Some
        }
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
  _
```

![](img/63aaf94e22830ab98ce16c5946be8ef6_482_0.png)
**Figure 7-25** Formlet used for the name and country

![](img/63aaf94e22830ab98ce16c5946be8ef6_482_1.png)
**Figure 7-26** Formlet used for the phone number and ID

## Creating an HTML5 Page

As previously mentioned, WebSharper supports HTML5 pages. Listing 7-64 shows how to draw rectangles on a *Canvas* element, as shown in Figure 7-27.

**LISTING 7-64** Drawing rectangles on a *Canvas* element

```fsharp
namespace Website

open IntelliFactory.WebSharper
open IntelliFactory.WebSharper.Html
open IntelliFactory.WebSharper.Html5

module ScriptModule = {
  [JavaScript>
  let example1 (ctx: CanvasContext2D) =
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

![](img/63aaf94e22830ab98ce16c5946be8ef6_483_0.png)
**FIGURE 7-27** Rectangles on an HTML5 canvas

The combination of WebSharper and F# can provide nice animations. In Listing 7-65, a rectangle is drawn and moved progressively from the left to the right.

**LISTING 7-65** HTML animation

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

> Note The .aspx page needs to be updated to reflect the MyCanvasAnimationViewer type name.

WebSharper provides a nice way to use F# to build solutions. However, WebSharper enables complex algorithms designed in F# and renders the result with HTML5. Here are the benefits of using WebSharper:

- It's a single language used for the full web stack. Imagine you have some existing .NET or F# algorithm implementation. WebSharper can make the development much easier.
- The inconsistency between browsers is taken care of by the framework.
- It automatically takes advantage of emerging technologies such as HTML5.
