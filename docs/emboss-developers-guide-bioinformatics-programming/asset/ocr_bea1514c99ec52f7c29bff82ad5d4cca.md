```
maximum: "1"
header: "Translation frames"
values: "1:1, 2:2, 3:3, F:Forward three frames, -1:-1, -2:-2, -3:-3, R: Reverse three frames, 6:All six frames"
delimiter: ","
codedelimiter: ":"
information: "Frame(s) to translate"
]
```

would present to the user something like:

```
Translation frames
1 1
2 2
3 3
F Forward three frames
-1 -1
-2 -2
-3 -3
R Reverse three frames
6 All three frames
Frame(s) to translate[1]:
```

To select from the list, the user specifies one (or sometimes more) labels, or partial text descriptions. The program is given a list of text labels as input. In this example, the minimum and maximum number of selections are set to one in the ACD definition, therefore only one selection value is allowed. For example, these are all valid selections:

```
"1"
"F"
"Forward"
"For"
"R"
"Reverse"
"Rev"
```

If the maximum count had been set to 3, say, then the following would be valid:

```
"-1,F,6"
```

Default value A default value is set using the default : global attribute.

Key attributes None.

# A.2.4.2 selection

A list of options (text descriptions) with automatically generated numerical labels.

The user is presented with a limited list of options they can choose from. The choices are numbered automatically from 1 up. The option descriptions are typically more verbose than for list definitions.