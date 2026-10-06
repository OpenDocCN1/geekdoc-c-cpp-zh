logic, Validation icon, and a TextLabel. The data received by nameF and countryF are passed into the callback function defined in Formlet.Yield (fun name data -> (Name = name; Country data =)). The callback function takes two parameters, return from nameF and countryF and form a Person record defined at the beginning of the source code.

# LISTING 72 Using a formlet with WebSharper

```
namespace Website

open IntelliFactory.WebSharper
open IntelliFactory.WebSharper.Html
open IntelliFactory.WebSharper.Formlet
open IntelliFactory.WebSharper.Formlet.Controls

module ScriptModule =
  type Person = {
    Name: string
    Country: string
  }

  [Rpc]
let countries() =
    [ "USA", "From USA"; "Canada", "From Canada"; "UK", "From United Kingdom" ]

  [JavaScript]
let PersonFormlet () : Formlet<Person> =
  let nameF =
    Controls.Input"
    | Validator.IsEmpty "Empty name not allowed"
    | Enhance.WithValidationIcon
    | Enhance.WithTextLabel "Name"
let countryF =
    Select(countries())
    | Enhance.WithTextLabel "Country"
  Formlet.Yield (fun name data -> (Name = name; Country = data))
  <*>\let countryF
    | Enhance.SubmitAndResetButtons
    | Enhance.WithLegend "Add a New Person"
    | Enhance.WithFormContainer

  [JavaScript]
let Main () =
  let p = PersonFormlet()
  let output = Label []
  let formlet = Formlet.Run (fun data -> output.Text <- string data.Name + ":" + data.Country) p
  Div [
    formlet
    output :>
```