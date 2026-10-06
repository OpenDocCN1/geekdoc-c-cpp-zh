# # Thank You

RECEIPT

| Data | Microsoft Translator |
| --- | --- |
| Published by | Microsoft Translator |
| Type | Limited Subscription |
| | https://datamarket.azure.com/

You can cancel your service plan by visiting: https://datamarket.azure.com/

![](bbox=[0.166, 0.267, 0.203, 0.285])

**EXPLORE THIS DATASET**
Launch the Dataset explorer which allows you to browse the dataset interactively.

**MICROSOFT POWERPOINT FOR EXCEL 2010**
Learn how to use Microsoft PowerPoint for Excel 2010 to create self-service BI (business) solutions, facilitating sharing and collaboration on user-generated BI solutions in Microsoft SharePoint Server 2010 environment, and extended to corporate enterprise operational efficiencies through Microsoft SQL Server 2008 R2

**TABLEAU SOFTWARE**
Learn how to visualize this dataset in Tableau. Tableau provides drag-and-drop data-visualization based on proven practices and patented technology from Stanford University. Tableau allows you to publish dashboards to the web with one click. Rapid-fire intelligence that anyone can use.

# ### FIGURE 4-14 Proxy class file for fixed-query dataset

# ### LISTING 4-51 Invoking the C# proxy class from F#

open System.Linq

```
// define a translate function by taking an English sentence and translating to
Chinese let translateTxt = =
let serviceRootUri = new System.Uri("https://api.datamarket.azure.com/Bing/MicrosoftTranslator/\");"
```

```
// the account key is the same as in the previous section
let accountKey = <id>
```

```
// create a translator container that is defined in the proxy class
let tc = Microsoft.TranslatorContainer(serviceRootUri)
tcc.Credentials <- new System.Net.NetworkCredential(accountKey, accountKey)
```

```
// translate from English(en) to Chinese (zh-CH)
let translationQuery = tc.Translate(txt, "zh-CH", "en")
let translationResult = translationQuery.Execute().ToList().FirstOrDefault()
```

```
// if there is no translation result, something went wrong so return empty string
if (translationResult = null) then
    System.String.Empty
else translationResult.Text
```

CHAPTER 4 Type Providers 207