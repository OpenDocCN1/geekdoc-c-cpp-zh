

Library:

```
FWeb
```

Privileges Required:

Some of the functions of this namespace require privileges, as explained in the table below:

| Privilege group | Privilege level | Description |
|---|---|---|
| WEB_PRIVACY | NORMAL | Accessing the web history |

Summary

Selected important classes:

+   - HistoryItem
+   - WebHistory

This namespace contains classes and methods to interact with the browser engine. It contains classes that track browsing history. The functionality for displaying a web browser inside a window is handled by the Controls sub-namespace.

```
Osp::Web::Controls
```

Declared In:

```
FWebControls.h
```

Privileges Required:

To use the features of this namespace, you must have the following privilege group:

| Privilege group | Privilege level | Description |
|---|---|---|
| WEB_SERVICE | NORMAL | Constructing a web control |

Summary

Selected important classes:

+   - Web

This sub-namespace provides web browsing functionality to an application. A full web browser can be embedded in an application window just like any other control. This control can be used to download web content to the device and run Javascript (using the EvaluateJavaScriptN method of Web). The web control is based on the WebKit standard.

```
Osp::Xml
```

## Declared In:

```
FXml.h
```

## Library:

```
FXml
```

## Privileges Required:

None.

## Summary

Contains methods to manipulate XML documents using the standard libXml2 library for parsing document content.

# PART

# II

# Recipes

# Fundamentals

## Recipe 1.1: Save to and Restore from the Registry

### Problem Description

You want to write some application settings to the registry and restore them when your application launches again.

### The Recipe

The following configuration is required for this recipe:

**Namespaces used:**
`Osp::App, Osp::Base`

**Header files to #include:**
`FBase.h, FApp.h`

**Required libraries:**
`FBase, FApp`

**Required privilege level:**
`Normal`

**Required privilege groups:**
`None`

The application registry is where you store the application state. This may include application settings such as user preference information, the current player status in a game, or configuration information that you don’t want the user to have to re-enter each time the application is run. So, for example, if the user is several levels into a complicated game, they don’t want to start all over again if they quit the application and open it again later. By storing the game state in the registry, an application developer can let them resume their game playing at the point they chose to stop.

In this recipe we’ll demonstrate how to write values to and read them from the registry. Our example is a very simple currency application that provides up-to-date currency exchange rates for the UK pound against the US dollar and euro. We use the application registry to store the last known euro and dollar exchange values and the time that these values were last updated.

The recipe consists of the following steps:

+   1. Set up the initial values for our registry entries.
+   2. Read each entry from the registry. If the entry does not exist, create it.
+   3. Restore our application state from the registry entries.
+   4. Write the updated entry back to the registry when the application is about to terminate.

The App::AppRegistry class contains the methods to read from and write to the registry. In our class AppRegistrySample we read from the registry in the application’s OnAppInitializing method, which is sent a reference to the application’s registry:

```
bool
AppRegistrySample::OnAppInitializing(AppRegistry& appRegistry)
{
    // The keys for each registry entry
    String DollarKey ("LastDollarValue");
    String EuroKey ("LastEuroValue");
    String DateKey ("DateUpdated");

    // Set up initial values for our registry entries
    double DollarValue (1.53);
    double EuroValue(1.17);

    // Set the default date value to be the current time
    DateTime dateUpdated;
    SystemTime::GetCurrentTime(dateUpdated);
    String currentDateString = dateUpdated.ToString();

    result r;

    // Read the last known value of each setting from the registry
    // If the registry entry does not exist, create it
    r = appRegistry.Get(DollarKey, DollarValue);
    if (r == E_KEY_NOT_FOUND)
    {
```

```
appRegistry.Add(DollarKey, DollarValue);

r = appRegistry.Get(EuroKey, EuroValue);
if (r == E_KEY_NOT_FOUND)
{
    appRegistry.Add(EuroKey, EuroValue);
}

r = appRegistry.Get(DateKey, currentDateString);
if (r == E_KEY_NOT_FOUND)
{
    appRegistry.Add(DateKey, currentDateString);
}

// Save any updated data to the registry
r = appRegistry.Save();
//...
```

The first time the application is run the AppRegistry will already exist but will be empty. It's your responsibility to add registry entries. Each registry entry has a key – a String that identifies it – and a value – which can be either of type String, int or double. In our example we store the last known dollar and euro exchange rate as a double and the time that these values were last updated as a String converted from a DateTime value.

To read from the registry we use the AppRegistry::Get() method. If this returns a E_KEY_NOT_FOUND error, we create the registry entry with AppRegistry::Add(), setting it to our default value. Then we store these values in our internal data structure and use this to restore our application state. In our case we display a form with the values read from the registry, as shown in Figure R1.1.

![](img/a257d5fd53a79a244a20e587cd2f08f6_238_0.png)

Figure R1.1 We store the last known exchange rates and the time they were last updated in the application registry.

When the application is about to terminate, your application's OnAppTerminating() method will be called with a reference to your AppRegistry passed as a parameter. In this method you should update your registry entry

with the current values. In our example, we’ll update the registry entries for the current exchange rate and the time this information was last updated:

```
bool
AppRegistrySample::OnAppTerminating(AppRegistry& appRegistry,
    bool forcedTermination)
{
    String DollarKey ("LastDollarValue");
    String EuroKey ("LastEuroValue");
    String DateKey ("DateUpdated");

    result r;

    // Write the current settings out to the registry
    r = appRegistry.Set(DollarKey, mDollarRate);
    if (IsFailed(r))
    {
        // Handle error condition
    }
    r = appRegistry.Set(EuroKey, mEuroRate);
    if (IsFailed(r))
    {
        // Handle error condition
    }

    r = appRegistry.Set(DateKey, mDateUpdated);
    if (IsFailed(r))
    {
        // Handle error condition
    }

    // Make sure the changes are written out to persistent storage
    appRegistry.Save();

    return true;
}
```

We update our registry entries with the AppRegistry::Set() method. Notice that at the end of the method we call AppRegistry::Save(). This ensures that our updated registry entries are written to persistent storage. Our registry entries are now up to date, ready to restore our application the next time it is launched.

## Hints, Pitfalls, and Related Topics

The application registry should be used for storing application settings and similar state information, not for larger amounts of data that should either be stored in a File or Database object, as provided by the Io namespace. File is useful for storing large blocks of information that will generally be written out and read back into memory in one block. A Database object is a SQLite database that is useful for storing information that you want to search through and update easily.

## Recipe 1.2: Use Error Handling in bada

### Problem Description

bada does not support the standard C++ exception handling mechanism. However, you need to catch and handle exceptions, which you can do by exploiting the mechanisms built into bada.

### The Recipe

The following configuration is required for this recipe:

| Configuration | Value |
|---|---|
| **Namespaces used:** | N/A |
| **Header files to #include:** | N/A |
| **Required libraries:** | N/A |
| **Required privilege level:** | Normal |
| **Required privilege groups:** | None |

The content of this recipe is not related to any specific namespace. What we describe here is rather a generally valid concept and describes the way in which bada handles exceptions. The reason for this speciality lies in the fact that the bada SDK was designed with optimised runtime efficiency in mind. Most of the standard C++ was applied. However, the bada SDK does not comply with standard C++ exception handling. Although this is a very convenient and well-proven technique, it is also very heavyweight and resource intensive. The bottom line is: bada is for mobile devices, which are embedded devices that are resource restricted compared to desktop computers. Hence, programming for these devices should also be treated differently. That is why in bada there is no standard C++ exception handling.

The exception handling in bada was designed to be extremely lightweight and simple. To realise this, a specific type was defined that is called result. This result type holds information about exceptions that have occurred and can be queried accordingly. Many different values are defined for describing the potentially occurring exceptions. Later in this recipe we give a list of these values.

The most common way to make use of the result type in bada is to use it as a return value for relevant methods. The bada API that opens up the SDK

