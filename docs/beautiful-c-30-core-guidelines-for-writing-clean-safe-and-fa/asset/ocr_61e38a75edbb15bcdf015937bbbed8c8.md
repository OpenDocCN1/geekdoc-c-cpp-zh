# Passing and returning by non-const reference

At the start of this chapter, we talked about input parameters and output parameters. There is a third type of parameter called an in-out parameter. Like an out parameter, this is also a reference or pointer to a non-const object. Typically, in-out parameters sit between in and out parameters in a function declaration, so we can expand the prototypical function described at the start thus:

Click here to view code image

```
Return-value, identifier(input-parameters, input-output parameters,

                                output-parameters);
```

The thrust of this guideline is to separate inputs from outputs so that inputs lie between the parentheses of a function declaration, while outputs are limited to the return type. Can we apply that wisdom to this style of parameter?

Consider a reporting object collecting data from a variety of sources. Each source exposes a function that takes a reporting object and some additional parameters and returns the number of items added to the object. For example:

Click here to view code image

```
class Report { ... };

int report_rendering(int, int, Report&); // input parameters...
int report_fileIO(int, int, int, Report&); // then in-out parameter

std::pair<Report, int> collect_report(const char*
```