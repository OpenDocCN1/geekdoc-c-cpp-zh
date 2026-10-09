**TABLE 3.1: Sample Code for Tuple Declaration and Assignment (continued)**

| Example | Description | Example Code |
|---|---|---|
| 6. | Assign a named item tuple to a single implicitly typed variable that is implicitly typed, and then access the tuple items by name. | ```csharp<br>var countryInfo =<br>    (Name: "Malawi", Capital: "Lilongwe", GdpPerCapita: 226.50);<br>System.Console.WriteLine(<br>    $@"The poorest country in the world in 2017 was {<br>        countryInfo.Name}, {countryInfo.Capital}: {<br>        countryInfo.GdpPerCapita}");<br>``` |