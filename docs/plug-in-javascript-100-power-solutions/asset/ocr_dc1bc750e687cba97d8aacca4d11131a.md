# Chapter 9: Text Effects 275

Next, a pair of flags are checked to see whether a fade is already in process on id. If the argument what the used is 'text', then the CF_Flagtext property of id is tested or set. Otherwise, if it is 'back', its CF_Flagback property is tested or set, like this:

```
if (O(id) ['CF_Flag' + what]) {
    if (O(id) ['CF_Int' + what]) return
    else clearInterval(O(id) ['CF_ID' + what])
} else O(id) ['CF_Flag' + what] = true
```

If a fade is running and the plugin-in is not interruptible, the plugin-in returns; any current repeating interrupts are halted, ready for new ones to be set up. If the flag is not set, the assigned value true indicates that a fade is in progress.
After this, if the colors was passed without passing the required # character, it is added:

```
if (color1[0] == '#') color1 = color1.substr(1)
if (color2[0] == '#') color2 = color2.substr(1)
```

Next, local variables are assigned values that will be used later:

```
var step = Math.round(msecs / INTERVAL)
var index = 0
var count = 0
var direc = 1
var cols = []
var steps = []
```

The last five are simple initializations, while the first one gives step a value that will calculate the difference between transition frames so the whole effect will take milliseconds.
After this, the cols[] array is populated with the triplet color values, and the steps[] array with the step values for each triplet between frame, like this:

```
for (var j = 0; j < 3; ++j) {
    var tmp = HexDec(color2.substr(j * 2, 2))
    cols[j] = HexDec(color1.substr(j * 2, 2))
    steps[j] = (tmp - cols[j]) / step
}
```

The local prop is then assigned a property name, either color or backgroundColor, depending on the value in the argument:

```
if (what == 'text') var prop = 'color'
else var prop = 'backgroundColor'
```

This is what makes the plugin-in dual functional: either the foreground or background color will be changed.