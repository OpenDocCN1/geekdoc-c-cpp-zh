```
using System.Reflection;
using System.ComponentModel;
```

Change the ProcessCommand method to seek the appropriate command processor class, as shown here:

```
static void ProcessCommand(string command, string pars)
{
    foreach (var type in
        from type in Assembly.GetExecutingAssembly().GetTypes()
        where type.IsSubclassOf(typeof(CommandProcessor))
        select type)
{
    var attrs = type.GetCustomAttributes(typeof(DisplayNameAttribute), false);
    if (attrs.Length == 0) continue;
    var displayName = (attrs[0] as DisplayNameAttribute).DisplayName;
    if (String.Compare(displayName, command, true) == 0)
    {
        var processor = Activator.CreateInstance(type) as CommandProcessor;
        if (processor != null) processor.ProcessCommand(pars);
    }
}
```

At this point, your console application is refracted so that it supports command processor classes. When you start the application, you can check that it understands the "list" and "quit" commands but nothing else. Figure 4-11 shows the modified code.

![](bbox=[0.143, 0.558, 0.795, 0.693])

FIGURE 4-11: The refractored console knows the list command

Now, let's extract an item template from this project. Because the modification you will apply to CommandProcessorItem.cs will result in a syntactically invalid file, check the Build Action property of this file in the Properties window. Replace a few parts of the file with the $safetename$ template parameter, as shown here:

```
using System;
using System.ComponentModel;
```

```
namespace ConsoleBase
```