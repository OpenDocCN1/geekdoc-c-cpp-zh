# ## 11.3 Inline Formatting Using Escape Character Sequences

There are some types of formatting that is difficult or impossible to implement directly using ODS styles and options. However, through the use of an escape character it is possible to pass destination-specific commands directly to the destination that builds the output. The escape character alerts ODS that the associated formatting sequence of characters are not to be used directly by ODS, but rather are to be passed to the receiving destination.

The escape character should be one that you do not otherwise use in your SAS programs. Since I tend not to use the tilde as a negation mnemonic, it makes a good escape character. The escape character is designated using the ODS ESCAPECHAR option.

```
    ods escapechar='~';
```

The escape character is used to note an escape sequence that may contain one or more destination commands or functions. The syntax varies by the kind of command.

| Type | General Form | Used to | Section |
|---|---|---|---|
| Formatting Functions | `~{function text}` | Control pagination, superscripts, subscripts. | 11.3.1<br>11.3.2 |
| Style Modification | `~S={attribute characteristics}`<br>`~{style elements and attributes}` | Assign style attributes. | 11.3.3 |
| Sequence Codes | `~code` | Manipulate line breaks, wrapping, and indentations. | 11.3.4 |
| Raw Text Insertion | `~R/destination "rawtext"`<br>`~R "rawtext"` | Insert destination-specific codes. | 11.3.5 |

# ### SEE ALSO

Carpenter (2007a, Section 8.6) discusses inline formatting in the context of PROC REPORT steps.

Haworth, Zender, and Burlew (2009) discuss the use of the escape character and inline formatting sequences in a variety of usages.

Zender (2007) covers all the basics in this easy-to-read SAS Global Forum paper on inline formatting. If you want to know more, this should be the first paper that you read on this topic.