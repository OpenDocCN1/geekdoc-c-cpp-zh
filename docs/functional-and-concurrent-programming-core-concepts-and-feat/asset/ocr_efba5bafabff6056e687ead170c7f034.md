Let’s unpack this. Function readFile returns a Try that contains either a list of lines or an I/O exception. Function parse return an Either value. It produces a pair when a line can be parsed (right) or leaves the line unchanged (left). Each pair contains the name of a city and a temperature, but the temperature is wrapped in an option to handle strings that cannot be converted to integer values. Finally, function stateOf maps cities to states but uses options to deal with cities that are not in the database.

The very first thing convert does is apply map to the Try value returned by readFile. If it is an exception, map leaves it unchanged, and convert returns a Failure value with the I/O exception. Otherwise, we have a list of lines to work with: Make it lazy with view, and apply parse to each line using map. Function filter is then applied to what is now a list of Either values. Each value is either a line that could not be parsed or a pair with a city name and an optional temperature. These values are tested using forall, which is true on any Left value but applies a test on Right values.⁴ Thus, unparsed lines are left as they are, but pairs are potentially eliminated. The test that is used to eliminate them invokes stateOf on the city name and checks that the option being returned contains the string "TX". This test is false on None (unknown cities) and on options with a string other than "TX" (cities outside of Texas).

The next stage of the pipeline uses map to transform each remaining Either value (variable badLineOrPair in the code). The first transformation converts Fahrenheit temperatures to Celsius. Unparsed lines are again left unchanged because map only transforms Right values. The conversion itself is achieved by using map on an option that contains the temperature. The second and final transformation creates a string from each Either value by adding square brackets to an unparsed line or by formatting a city name with a temperature. The temperature, now in Celsius, is extracted from its option, with getOrElse being used to replace missing temperatures with the string "unknown".

This variant of convert produces the same output as before on the sample file. On a file with defects such as:

```
Austin: hot
Chicago: 88
Big
Spring: 92
```

it produces the list ["Austin: unknown", "[Big]"]. Chicago is eliminated for being out of Texas, and Spring for not being in the database.

Note that, in this programming style, errors tend to propagate down the pipeline in the form of an empty Option, a failed Try, or a left Either value. By contrast, a thrown exception would go up to the top of the pipeline, unhandled by the higher-order functions above it and ignoring all the stages below it.

Compared to its previous version, the updated code for function convert may look complicated, especially if you are new to functional programming, but error handling is rarely easy. Alternative approaches, without Option, Try, Either, and their higher-order methods, are unlikely to be simpler.

⁴This line is tricky: filter is applied to a sequence, forall to a value of type Either, and contains to an option.