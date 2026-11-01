# Default Naming Context

If a distinguished name is not specified in the path, the binding process will be made to the default naming context. You can read the default naming context with the help of rootDSE. LDAP 3.0 defines rootDSE as the root of a directory tree on a directory server. For example:

```
LDAP://rootDSE
```

or

```
LDAP://servername/rootDSE
```

By enumerating all properties of the rootDSE, you can get the information about the defaultNamingContext that will be used when no name is specified. schemaNamingContext and configurationNamingContext specify the required names to be used to access the schema and the configuration in the Active Directory store.

The following code is used to get all properties of rootDSE:

```
try
{
    using (var de = new DirectoryEntry())
    {
        de.Path = "LDAP://magellan/rootDSE";
        de.Username = @"cn\innovation\christian";
        de.Password = "Pa$$word";

        PropertyCollection props = de.Properties;
        foreach (string prop in props.PropertyNames)
        {
            PropertyValueCollection values = props[prop];
            foreach (string val in values)
            {
                Console.Write('('0: ', prop);
                Console.WriteLine(val);
            }
        }
    }
    catch (COMException ex)
    {
        Console.WriteLine(ex.Message);
    }
}
```

code snippet DirectoryServicesSamples/Program.cs

> > To have this code running on your machine, you must change the path to the object to access, including the server name.

This program shows the default naming context (defaultNamingContext DC=cninnovation, DC=local), the context that can be used to access the schema (CN=Schema, CN=Configuration, DC=cninnovation, DC=local), and the naming context of the configuration (CN=Configuration, DC=cninnovation, DC=local), as you can see here:

```
currentTime: 20090925131508.0Z
subschemaSubentry: CN=Aggregate,CN=Schema,CN=Configuration,DC=cninnovation,DC=local
DC=local
dsServiceName: CN=NTDS Settings,CN=NAGELLAN,CN=Servers,
CN=Default-First-Site-Name,CN=Sites,CN=Configuration,DC=cninnovation,DC=local
namingContexts: DC=cninnovation,DC=local
```