![](bbox=[0.161, 0.056530000000000004, 0.49285, 0.20353])

**FIGURE 7-25** Formlet used for the name and country input

![](bbox=[0.161, 0.30685, 0.49285, 0.41233])

**FIGURE 7-26** Formlet used for the phone number and ID

# # Creating an HTML5 Page

As previously mentioned, WebSharper supports HTML5 pages. Listing 7-64 shows how to draw two rectangles on an HTML5 *Canvas* element, as shown in Figure 7-27.

+   **LISTING 7-64** Drawing rectangles on an HTML5 *Canvas* element

```
namespace Website

open IntelliFactory.WebSharper
open IntelliFactory.WebSharper.Html
open IntelliFactory.WebSharper.Html5

module ScriptModule = {
[JavaScript>
let example1 (ctx: CanvasRenderingContext2D) = =
ctx.fillStyle = "rgb(100, 0, 0)"
ctx.fillRect(10., 10., 50., 50.);
ctx.fillStyle = "rgba(0, 0, 100, 0.5)"
ctx.fillRect(30., 30., 50., 50.);

[JavaScript>
let Main() {
let element = HTML5.Tags.Canvas []
}
```