
currently logged-in user. regedit shows which key is being examined by displaying it with an open folder icon in the tree view.

![](img/d7d2ffa0a76feaab821930e95daace93_869_0.png)

FIGURE 29-17

The HKCU\Control Panel\Appearance key has three named values set, although the default value does not contain any data. The column in the screenshot marked Type details the data type of each value. Registry entries can be formatted as one of three data types:

- REG_SZ (which roughly corresponds to a .NET string instance; the matching is not exact because the registry data types are not .NET data types)
- REG_DWORD (corresponds roughly to uint)
- REG_BINARY (array of bytes)

An application that stores data in the registry will do so by creating a number of registry keys, usually under the key HKLM\Software\<CompanyName>. Note that it is not necessary for these keys to contain any data. Sometimes the very fact that a key exists provides the data that an application needs.

## The .NET Registry Classes

Access to the registry is available through two classes in the Microsoft.Win32 namespace: Registry and RegistryKey. A RegistryKey instance represents a registry key. This class implements methods to browse child keys, to create new keys, or to read or modify the values in the key — in other words, to do everything you would normally want to do with a registry key, including setting the security levels for the key. RegistryKey will be the class you use for much of your work with the registry. Registry, by contrast, is a class that allows for singular access to registry keys for simple operations. Another role of the Registry class is simply to provide you with RegistryKey instances that represent the top-level keys, the different hives, to enable you to navigate the registry. Registry provides these instances through static properties, and there are seven of them called, respectively, ClassesRoot, CurrentConfig, CurrentUser, DynData, LocalMachine, PerformanceData, and Users. It should be obvious which property corresponds to which hive.

So, for example, to obtain a RegistryKey instance that represents the HKLM key, you would write:

```
RegistryKey hklm = Registry.LocalMachine;
```

The most obvious difference is in how you open a registry key at a given location in the registry. The Registry class does not have any public constructor that you can use, nor does it have any methods that let you go directly to a key, given its name. Instead, you are expected to browse down to that key from the top of the relevant hive. If you want to instantiate a RegistryKey object, the only way is to start off with the appropriate static property of Registry, and work down from there. So, for example, if you want to read some data in the HKLM\Software\Microsoft key, you would get a reference to it like this:

```
RegistryKey hklm = Registry.LocalMachine;
RegistryKey hkSoftware = hklm.OpenSubKey("Software");
RegistryKey hkMicrosoft = hkSoftware.OpenSubKey("Microsoft");
```

A registry key accessed in this way will give you read-only access. If you want to write to the key (that includes writing to its values or creating or deleting direct children of it), you need to use another override to OpenSubKey, which takes a second parameter, of type bool, that indicates whether you want read-write access to the key. For example, if you want to be able to modify the Microsoft key (and assuming that you are a system administrator with permission to do this), you would write this:

```
RegistryKey hklm = Registry.LocalMachine;
RegistryKey hkSoftware = hklm.OpenSubKey("Software");
RegistryKey hkMicrosoft = hkSoftware.OpenSubKey("Microsoft", true);
```

Incidentally, because this key contains information used by Microsoft's applications, in most cases you probably shouldn't be modifying this particular key.

The OpenSubKey() method is the one you call if you are expecting the key to be present. If the key isn't there, it returns a null reference. If you want to create a key, you should use the CreateSubKey() method (which automatically gives you read-write access to the key through the reference returned):

```
RegistryKey hklm = Registry.LocalMachine;
RegistryKey hkSoftware = hklm.OpenSubKey("Software");
RegistryKey hkOwn = hkSoftware.CreateSubKey("MyOwnSoftware");
```

The way that CreateSubKey() works is quite interesting. It creates the key if it does not already exist, but if it does exist, it quietly returns a RegistryKey instance that represents the existing key. The reason for the method behaving in this manner has to do with how you normally use the registry. The registry, overall, contains long-term data such as configuration information for Windows and for various applications. It is not very common, therefore, that you find yourself in a situation where you need to explicitly create a key.

What is much more common is that your application needs to make sure that some data is present in the registry — in other words, create the relevant keys if they do not already exist, but do nothing if they do. CreateSubKey() fills that need perfectly. Unlike the situation with FileInfo.Open(), for example, there is no chance with CreateSubKey() of accidentally removing any data. If deleting registry keys is your intention, you will need to call the RegistryKey.DeleteSubKey() method. This makes sense given the importance of the registry to Windows. The last thing you want is to completely break Windows accidentally by deleting a couple of important keys while you are debugging your C# registry calls!

## 4.6 Data Analysis and Visualization

Data analysis and visualization are essential steps in the data science workflow. They allow us to extract meaningful insights from raw data and communicate those insights effectively through visual representations.

In this section, we will cover the following topics:

- Exploratory Data Analysis (EDA)
- Statistical summaries and distributions
- Data cleaning and preprocessing
- Visualization libraries and tools
- Creating effective charts and plots

The pandas library in Python provides powerful data structures and functions for data manipulation. Combined with visualization libraries such as Matplotlib and Seaborn, it becomes straightforward to perform comprehensive analyses.

| Metric | Description | Python Function |
|--------|-------------|-----------------|
| Mean | Average value | `df.mean()` |
| Median | Middle value | `df.median()` |
| Std Dev | Spread indicator | `df.std()` |
| Correlation | Relationship strength | `df.corr()` |

A well-designed visualization can reveal patterns, trends, and outliers that might otherwise remain hidden in the raw data.

> "A picture is worth a thousand words" — this is especially true in the context of data analysis, where visual insights often lead to better decision-making.

This means that you can have multiple instances of the same application all working from the same store.

The second type of access for isolated storage is user, assembly, and domain. In this case, each application instance works off its own isolation store. This is detailed in Figure 29-19.

![](img/d7d2ffa0a76feaab821930e95daace93_872_0.png)

FIGURE 29-18

FIGURE 29-19

In this case, each application instance works off its own store, and the settings that each application instance records are related only to itself. This is a more fine-grained approach to isolated storage.

For an example of using isolated storage from a Windows Forms application (although you can use this from an ASP.NET application just as well), you can use the ReadSettings() and SaveSettings() methods shown next to read and write values to isolated storage as opposed to maybe doing the same directly in the registry.

> It is important to note that the only code shown here is for the ReadSettings() and SaveSettings() methods. There is more code to the application, and you can see the rest in the download code file in the sample titled SelfPlacingWindow.

To start, you need to rework the SaveSettings() method. For this next bit of code to work, you need to add the following using directives:

```
using System.IO;
using System.IO.IsolatedStorage;
using System.Text;
```

The SaveSettings() method is detailed in the following code example:

```
void SaveSettings()
{
    IsolatedStorageFile storFile = IsolatedStorageFile.GetUserStoreForDomain();
    IsolatedStorageFileStream storStream = new
    IsolatedStorageFileStream("SelfPlacingWindow.xml",
    FileMode.Create, FileAccess.Write);

    System.Xml.XmlTextWriter writer = new
    System.Xml.XmlTextWriter(storStream, Encoding.UTF8);
    writer.Formatting = System.Xml.Formatting.Indented;

    writer.WriteStartDocument();
    writer.WriteStartElement("Settings");
    writer.WriteStartElement("BackColor");
    writer.WriteValue(BackColor.ToKnownColor().ToString());
    writer.WriteEndElement();
