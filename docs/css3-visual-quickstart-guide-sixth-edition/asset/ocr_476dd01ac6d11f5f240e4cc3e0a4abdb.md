# # Specifying the Quote Style

Although most writers will use the keyboard to add quotation marks to text, HTML includes the quotation tag: <q>...</q>. This tag places browser-default quotation marks around the indicated text. With CSS, you can define the exact characters to be used as quotation marks using the quotes property (Table 9.6). Although English uses single (...) or double (...) quotation marks, this is by no means the norm for all languages.

# ## To define the bullet style:

+   1. Add the quotes property to your declaration block. Type quotes, followed by a colon (:). quotes:

You can add this to any specific element, or you can key it off of a specific language as explained in “Styling for a particular language” (Chapter 4).

| Value |
|---|
| "<string>" |
| none |
| inherit |

Code 9.5. Added to ui-generatedcontent-properties.css—in this example 4, the quotation marks are set to use « », which is standard for many European languages, including French.

```
/* ui-generatedcontent-properties.css */
* { quotes: '«' '»' '‹' '›'; }
```

![](bbox=[0.54, 0.38, 0.94, 0.59])

Code 9.5 applied to Code 9.1: The quotes are now set using angle quotation marks, which is standard for many European languages. I’ve magnified the image so that you can get a better look.