The unit of measure can be presented in different but equivalent ways. F# can convert these different representations to a consistent format. From the execution result in Listing 6-17, you can see that the variables kgm21 to kgm24 show the same result kg/m².

# **LISTING 6-17** Different definition formats convert to consistent format

```
Define unit of measure
<Measure> type kg
<Measure> type m

<Measure> type kgm21 = kg/m ^ -2
<Measure> type kgm22 = kg/m
<Measure> type kgm23 = kg/(m * m)
<Measure> type kgm24 = kg/(m ^ 2)

Execution result
<Measure>
type kg
<Measure>
type m
<Measure>
type kgm21 = kg m ^ 2
<Measure>
type kgm22 = kg/m ^ 2
<Measure>
type kgm23 = kg/m ^ 2
<Measure>
type kgm24 = kg/m ^ 2
```

Units of measure can be converted as well. Listing 6-18 shows a function that converts *gram* to *kilogram*.

# **LISTING 6-18** Converting units from *gram* to *kilogram*

```
// define gram
<Measure> type g

// define kilogram
<Measure> type kg

// define a conversion function that converts gram to kilogram
let convertGramToKilogram (x : float<g>) = x / 1000.0/g/kg
```

> **Note** The unit of measure exists only at F#'s compile time, C# code is not able to access the unit of measure. The *float<measureUnit>* can be viewed only as a double in C# code.