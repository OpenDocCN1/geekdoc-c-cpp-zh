The world is made up of a multitude of cultures, each of which has a language and a set of defined ways in which it views and consumes numbers, uses currencies, sorts alphabetically, and so on. The .NET Framework defines languages and regions using the Request for Comments 1766 standard definition (tags for identification of languages — www.ietf.org/rfc/rfc1766.txt), which specifies a language and region using two-letter codes separated by a dash. The following table provides examples of some culture definitions:

| CULTURE CODE | DESCRIPTION |
|---|---|
| en-US | English language; United States |
| en-GB | English language; United Kingdom (Great Britain) |
| en-AU | English language; Australia |
| en-CA | English language; Canada |
| fr-CA | French language; Canada |

The examples in this table define five distinct cultures. These five cultures have some similarities and some differences. Four of the cultures speak the same language (English), so the language code of “en” is used in these culture settings. Following the language setting is the region setting. Even though most of these cultures speak the same language, it is important to distinguish them further by setting their region (such as US for the United States, GB for the United Kingdom, AU for Australia, and CA for Canada). These settings reflect the fact that the English used in the United States is slightly different from the English used in the United Kingdom, and so forth. Beyond language, differences exist in how dates and numerical values are represented. This is why a culture’s language and region are presented together.

![](bbox=[0.55, 0.32, 0.9, 0.85])

The differences between the cultures in the table do not break down by region only. Many countries contain more than a single language, and each may have its own preference for notation of dates and other items. For example, en-CA specifies English speakers in Canada. Because Canada is not only an English-speaking country, it also includes the culture setting of fr-CA for French-speaking Canadians.

# Understanding Culture Types

The culture definition just given is called a specific culture definition. This definition is as detailed as you can possibly get, defining both the language and the region. The other type of culture definition is a neutral culture definition. Each specific culture has a specified neutral culture with which it is associated. For instance, the English language cultures shown in the previous table are separate, but they also belong to one neutral culture: EN (English). The diagram presented in Figure 27-1 illustrates how these culture types relate to one another.

FIGURE 27-1

From this diagram, you can see that many specific cultures belong to a neutral culture. Higher in the hierarchy than the neutral culture is an invariant culture, which is an agnostic culture setting that should be utilized when passing items (such as dates and numbers) around a network. When performing these kinds of operations, you should make your back-end data flows devoid of user-specific culture settings. Instead, apply these settings in the business and presentation layers of your applications.