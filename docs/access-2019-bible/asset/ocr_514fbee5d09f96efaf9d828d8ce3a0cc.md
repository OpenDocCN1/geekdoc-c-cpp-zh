# FIGURE 11.17

The MyTest field now contains the concatenated values of the Type field and the Code field, separated by a colon.

| Type | Code | MyTest |
|---|---|---|
| DB | 100199 | DB:100199 |
| DB | 200 | DB:200 |
| DB | 100199 | DB:100199 |
| DB | 100199 | DB:100199 |
| DB | 100199 | DB:100199 |
| DB | 100199 | DB:100199 |
| DB | 100199 | DB:100199 |
| DB | 100199 | DB:100199 |
| DB | 100199 | DB:100199 |
| DB | 100199 | DB:100199 |
| DB | 200 | DB:200 |

# Changing case

Making sure the text in your database has the correct capitalization may sound trivial, but it's important. Imagine you receive a customer table that has an address field where all the addresses are lowercase. How is that going to look on labels, form letters, or invoices? Fortunately, for those who are working with tables containing thousands of records, Access has a few built-in functions that make changing the case of your text a snap.

The LeadList table shown in Figure 11.18 contains an Address field that is in all lowercase letters.

# FIGURE 11.18

The Address field is in all lowercase letters.

| Address | City | State | PostalCode |
|---|---|---|---|
| 46 gin craighton w ebrems dr | agawam | ma | 01001 |
| 426 bewlis rd | agawam | ma | 01001 |
| 651 shemelkin ln | agawam | ma | 01001 |
| 44 almgirn dr | agawam | ma | 01001 |
| 35 mallin | brimfield | ma | 01010 |
| 460 fill rd | chicopee | ma | 01020 |
| 320 minerald st ste 4 | chicopee | ma | 01020 |
| 4010 shiradan st | chicopee | ma | 01022 |
| 5046 wisterivir rd | chicopee | ma | 01022 |
| 40 meple st | east longmeadow | ma | 01028 |
| 242 bish st | holyoke | ma | 01040 |
| 42 whatang ferms rd | holyoke | ma | 01040 |

To fix the values in the Address field, you can use the StrConv function, which is a function that converts a string to a specified case. To use the StrConv function, you must provide two required arguments: the string to be converted and the conversion type.

```
StrConv(string to be converted, conversion type,)
```