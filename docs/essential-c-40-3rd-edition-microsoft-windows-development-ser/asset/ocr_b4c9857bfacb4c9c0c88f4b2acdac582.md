```
foreach (CommandLineSwitchAliasAttribute attribute in
property.GetCustomAttributes(
typeof(CommandLineSwitchAliasAttribute), false))
{
options.Add(attribute.Alias.ToLower(), property);
}
}
return options;
}
}
```

# LISTING 17.16: Updating CommandLineHandler.TryParse() to Handle Aliases

```
using System;
using System.Reflection;
using System.Collections.Generic;
public class CommandLineHandler
{
// ...
public static bool TryParse(
string[] args, object commandLine,
out string errorMessage)
{
bool success = false;
errorMessage = null;
Dictionary<string, PropertyInfo> options =
CommandLineSwitchAliasAttribute.GetSwitches(
commandLine);
foreach (string arg in args)
{
PropertyInfo property;
string option;
if (arg[0] == '/' || arg[0] == '-')
{
string[] optionParts = arg.Split(
new char[] { ':', ' ' }, 2);
option = optionParts[0].Remove(0, 1).ToLower();
if (options.TryGetValue(option, out property))
{
success = SetOption(
commandLine, property,
optionParts, ref errorMessage);
}
else
{

```