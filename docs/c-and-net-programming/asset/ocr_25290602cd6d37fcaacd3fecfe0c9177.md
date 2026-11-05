# Retrieving data from the Registry

To retrieve any data from the Registry, the static OpenSubKey method of the Registry class is used that returns a RegistryKey instance of the given subkey. If the object is not null (in case the given subkey doesn't exist), the GetValue method can be used to retrieve the values. This method takes just one argument, the key name.

```
//opening the subkey
RegistryKey key = Registry.CurrentUser.OpenSubKey(@"SOFTWARE\TechSettings");
//if it does exist, retrieve the stored values
if (key != null)
{
    Console.WriteLine(key.GetValue("Setting1"));
    Console.WriteLine(key.GetValue("Setting2"));
    key.Close();
}
```

# Two Marks Questions with Answers

# Q.1 What is meant by Globalization and Localization ?

Ans. : Internationalization is the process of designing applications that support multiple languages. This is divided into Localization and Globalization.

Globalization is nothing but developing applications to support different languages. Existing applications can also be converted to support multiple cultures.

Whereas Localization means changing the already globalized app to cater to a specific culture or language Microsoft.Extensions.Localization is used for localizing the app content. Some of the other keywords that are used for Localization are IHtmlLocalizer, IStringLocalizer, IViewLocalizer and so on

# Q.2 Explain the Code Access Security (CAS) in .NET framework.

Ans. : .NET security model is used to prevent unauthorized access of resources and operations and also restrict the codes to perform particular tasks. Code Access Security is a part of that .NET security.

# Q.3 How would you ensure that all relevant registry entries were removed in the event that installation of your application failed ?

Ans. : You can ensure that registry entries are removed, as well as perform any other "clean-up" tasks, by creating an Installer class and writing the appropriate code in the Rollback event handler. Then create a new Custom Action and set the InstallerClass, and EntryPoint properties to appropriate values.