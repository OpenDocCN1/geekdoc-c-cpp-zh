
5. Create an append query that appends all records from the LeadList table to the LeadList_NoDups table. When you run the append query, you'll get a message similar to the one shown in Figure 11.11.

## FIGURE 11.11

Now you can append all records excluding the duplicates.

![](img/1e45673ab6eca9d20e67635ff5b9b318_405_0.png)

Not familiar with append queries? Turn back to Chapter 10 to get an in-depth explanation.

Because the CustomerNumber field in the LeadList_NoDups table is set as the primary key, Access won't allow duplicate customer numbers to be appended. In just a few clicks, you've effectively created a table free from duplicates. You can now use this duplicate-free table as the source for any subsequent analysis!

CAUTION
Be aware that Access makes no fuzzy logical determination to see if records may duplicate. It processes your request literally. For instance, a simple mistyping of an address or phone number would mean that rows that actually are duplicates would be allowed. You'll want to keep this in mind, especially when working with textual fields where data entry is manual.

## Removing Duplicates with One Make-Table Query

Here's a trick that will allow you to remove duplicates by running a make-table query:

- 1. Select the Create tab and choose Query Design.
- 2. In the Show Table dialog box, select your table that contains duplicates.
- 3. Add all fields from your table to the query design grid.
- 4. On the Query Tools Design tab, select the Property Sheet command. The Property Sheet shown in the following figure appears.

All you have to do here is change the Unique Values property to Yes. Close the Property Sheet and change the query type to a Make Table Query.

![](img/1e45673ab6eca9d20e67635ff5b9b318_406_0.png)

## Common Transformation Tasks

Besides duplicate records, you’ll find that many of the unpolished data sets that come to you will require other types of transformation actions. This section covers some of the more common transformation tasks you’ll have to perform.

## Filling in blank fields

Often, you’ll have fields that contain empty values. These values are considered null—a value of nothing. Nulls are not necessarily a bad thing. In fact, if used properly, they can be an important part of a well-designed relational database. That said, you may find that you need to fill in blank fields with some logical code that indicates a missing value.

Filling in the null values in your data set is as simple as running an update query. In the example shown in Figure 11.12, you’re updating the null values in the DollarPotential field to zero.

It’s important to note that there are actually two kinds of blank values: null and empty string (""). When filling in the blank values of a text field, include the empty string as a criterion in your update query to ensure that you don’t miss any fields. In the example shown in Figure 11.13, you’re updating the blank values in the Segment field to “Other.”

## FIGURE 11.12

This query will update the null values in the DollarPotential field to a value of 0.

![](img/1e45673ab6eca9d20e67635ff5b9b318_407_0.png)

## FIGURE 11.13

This query will update blank values in the Segment field to a value of "Other."

![](img/1e45673ab6eca9d20e67635ff5b9b318_407_1.png)

## Concatenating

It's always amazing to see anyone export data out of Access and into Excel, only to concatenate (join two or more character strings end to end) and then re-import the data back into Access. You can easily concatenate any number of ways in Access with a simple update query.

## Concatenating fields

Look at the update query shown in Figure 11.14. In this query, you're updating the MyTest field with the concatenated row values of the Type field and the Code field.

## FIGURE 11.14

This query concatenates the row values of the Type field and the Code field.

![](img/1e45673ab6eca9d20e67635ff5b9b318_408_0.png)

TIP
It’s a good idea to create a test field in order to test the effects of your data transformation actions before applying changes to the real data.

Take a moment to analyze the following query breakdown:

- - **[Type]:** This tells Access to use the row values of the Type field.
- - **&:** The ampersand is a character operator that joins strings together.
- - **[Code]:** This tells Access to use the row values of the Code field.

## FIGURE 11.15

The MyTest field now contains the concatenated values of the Type field and the Code field.

| Type | Code | MyTest |
|------|------|--------|
| DB   | 100199 | DB100199 |
| DB   | 200   | DB200   |
| DB   | 100199 | DB100199 |
| DB   | 100199 | DB100199 |
| DB   | 100199 | DB100199 |
| DB   | 100199 | DB100199 |
| DB   | 100199 | DB100199 |
| DB   | 100199 | DB100199 |
| DB   | 100199 | DB100199 |
| DB   | 100199 | DB100199 |
| DB   | 200   | DB200   |
| DB   | 100199 | DB100199 |

## Augmenting field values with your own text

You can augment the values in your fields by adding your own text. For example, you may want to concatenate the row values of the Type field and the Code field but separate them with a colon. The query in Figure 11.16 does just that.

### FIGURE 11.16

This query concatenates the row values of the Type field and the Code field and separates them with a colon.

![](img/1e45673ab6eca9d20e67635ff5b9b318_409_0.png)

Take a moment to analyze the following query breakdown:

- - **[Type]:** This tells Access to use the row values of the Type field.
- - **&:** The ampersand is a character operator that joins strings together.
- - **":":** This text will add a colon to the concatenated string.
- - **&:** The ampersand is a character operator that joins strings together.
- - **[Code]:** This tells Access to use the row values of the Code field.

Figure 11.17 shows the results of this query.

> **NOTE**
> 
> When specifying your own text in a query, you must enclose the text in quotes. You can concatenate numeric data without the quotes.

## FIGURE 11.17

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

## Changing case

Making sure the text in your database has the correct capitalization may sound trivial, but it's important. Imagine you receive a customer table that has an address field where all the addresses are lowercase. How is that going to look on labels, form letters, or invoices? Fortunately, for those who are working with tables containing thousands of records, Access has a few built-in functions that make changing the case of your text a snap.

The LeadList table shown in Figure 11.18 contains an Address field that is in all lowercase letters.

## FIGURE 11.18

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
