
> CAUTION
> After your table is saved, if you change a field name that is also used in queries, forms, or reports, you have to change it in those objects as well. One of the leading causes of errors in Access applications stems from changing the names of fundamental database objects, such as tables and fields, but neglecting to make all the changes required throughout the database. Overlooking a field name reference in the control source of a control on the form or report, or deeply embedded in VBA code somewhere in the application, is far too easy.

## Specifying a data type

When you enter a field, you must also decide what type of data each of your fields will hold. In Access, you can choose any of several data types. The available data types are shown in Table 3.2.

### TABLE 3.2 Data Types Available in Microsoft Access

| Data Type | Type of Data Stored | Storage Size |
|---|---|---|
| Short Text | Alphanumeric characters | 255 characters or fewer |
| Long Text | Alphanumeric characters | 1GB of characters or less |
| Number | Numeric values | 1, 2, 4, or 8 bytes; 16 bytes for Replication ID (GUID) |
| Large Number | Numeric values | 8 bytes |
| Date/Time | Date and time data | 8 bytes |
| Currency | Monetary data | 8 bytes |
| AutoNumber | Automatic number increments | 4 bytes; 16 bytes for Replication ID (GUID) |
| Yes/No | Logical values: Yes/No, True/False | 1 bit (0 or -1) |
| OLE Object | Pictures, graphs, sound, video | Up to 1GB (disk space limitation) |
| Hyperlink | Link to an Internet resource | 1GB of characters or less |
| Attachment | A special field that enables you to attach external files to an Access database | Varies by attachment |
| Calculated | A field that stores a calculation based on other fields in the table | Determined by setting the Result Type property |
| Lookup Wizard | Displays data from another table | Generally 4 bytes |

Figure 3.7 shows the Data Type drop-down list used to select the data type for the field you just created.

### FIGURE 3.7

The Data Type drop-down list.

![](img/1e45673ab6eca9d20e67635ff5b9b318_86_0.png)

One of these data types must be assigned to each of your fields. Some of the data types have additional options, such as Field Size for Short Text fields and Number fields.

Here are the basic questions to consider when choosing the data type for new fields in your tables:

- **What is the data type?** The data type should reflect the data stored in the field. For example, you should select one of the numeric data types to store numbers like quantities and prices. Don't store data like phone numbers or Social Security numbers in numeric fields, however; your application won't be performing numeric operations like addition or multiplication on phone numbers. Instead, use text fields for common data, such as Social Security numbers and phone numbers.

> NOTE
> Numeric fields never store leading zeros. Putting a zip code such as 02173 into a numeric field means only the last four digits (2173) are actually stored.

- **What are the storage requirements of the data type you've selected?** Although you can use the Numeric data type with a field size of Long Integer in place of Integer or Byte, the storage requirements of a Long Integer (4 bytes) are twice that of Integer. This means that twice as much memory is required to use and manipulate the number and twice as much disk space is required to store its value. Use the smallest data type/field size you can that will still hold the largest value you will ever have in that field.

## Part II: Understanding Access Tables

- Will you want to sort or index the field? Because of their binary nature, Long Text and OLE Object fields can't be sorted or indexed. Use Long Text fields sparingly. The overhead required to store and work with Long Text fields is considerable.

- What is the impact of the data type on sorting requirements? Numeric data sorts differently from text data. Using the numeric data type, a sequence of numbers will sort as expected: 1, 2, 3, 4, 5, 10, 100. The same sequence stored as text data will sort like this: 1, 10, 100, 2, 3, 4, 5. If it's important to sort text data in a numeric sequence, you'll have to first apply a conversion function to the data before sorting.

Tip
If it's important to have text data representing numbers to sort in the proper order, you might want to prefix the numerals with zeros (001, 002, and so on). Then the text values will sort in the expected order: 001, 002, 003, 004, 005, 010, 100.

- Is the data text or date data? When working with dates, you're almost always better off storing the data in a Date/Time field than as a Short Text field. Text values sort differently from dates (dates are stored internally as numeric values), which can upset reports and other output that rely on chronological order.

New Feature
The Large Number data type was added to Access 2019. Its main purpose is to support compatibility with other databases that use this data type, such as SQL Server. If you use Large Number, your database will not be compatible with older versions of Access. Only use Large Number if you have a specific reason to do so.

Don't be tempted to store dates in one Date/Time field and time in another Date/Time field. The Date/Time field is specifically designed to handle both dates and times, and, as you'll see throughout this book, it's quite easy to display only the date or time portion of a Date/Time value.

A Date/Time field is also meant to store a discrete date and time, and not a time interval. If keeping track of durations is important, you could use two Date/Time fields—one to record the start and the other at the end of a duration—or one Long Integer field to store the number of elapsed seconds, minutes, hours, and so forth.

- What reports will be needed? You won't be able to sort or group Long Text or OLE data on a report. If it's important to prepare a report based on Long Text or OLE data, add a Tag field like a date or sequence number, which can be used to provide a sorting key, to the table.

### TABLE 3.3 Numeric Field Settings

| Field Size Setting | Range | Decimal Places | Storage Size |
|---|---|---|---|
| Byte | 0 to 255 | None | 1 byte |
| Integer | -32,768 to 32,767 | None | 2 bytes |
| Long Integer | -2,147,483,648 to 2,147,483,647 | None | 4 bytes |
| Single | -3.4 × 10^38 to 3.4 × 10^38 | 7 | 4 bytes |
| Double | -1.797 × 10^308 to 1.797 × 10^308 | 15 | 8 bytes |
| Replication ID | N/A | N/A | 16 bytes |
| Decimal | -9.999 × 10^27 to 9.999 × 10^27 | 15 | 12 bytes |

> CAUTION
> Many errors are caused by choosing the wrong numeric type for number fields. For example, notice that the maximum value for the Integer data type is 32,767. We once saw a database that ran perfectly for several years and then started crashing with overflow errors. It turned out that the overflow was caused by a particular field being set to the Integer data type, and when the company occasionally processed very large orders, the 32,767 maximum was exceeded.
> 
> Be aware that overflow may occur simply by adding two numbers together or by performing any mathematical operation that results in a value too large to be stored in a field. Some of the most difficult bugs occur only when circumstances (such as adding or multiplying two numbers) cause an overflow condition at run time.
> 
> Design your tables very conservatively and allow for larger values than you ever expect to see in your database. This is not to say that using the Double data type for all numeric fields is a good idea. The Double data type is very large (8 bytes) and might be somewhat slow when used in calculations or other numeric operations. Instead, the Single data type is probably best for most floating-point calculations, and Long Integer is a good choice where decimal points are irrelevant.

## Large Number

The Large Number data type holds values from -2^63 to 2^63-1. Those are bigger numbers than most people need. It was added to Access mainly for compatibility with other databases that have this data type, specifically SQL Server.

If you use Large Number, be aware that not all versions of Access prior to 2019 support this data type. If you're linking to or importing from a database that uses this data type, check the Support Large Number (BigInt) Data Type for Linked/Imported Tables check box in the Current Database tab of Access Options.

## Date/Time

The Date/Time data type is a specialized number field for holding dates or times (or dates and times). When dates are stored in a Date/Time field, it's easy to calculate days between
