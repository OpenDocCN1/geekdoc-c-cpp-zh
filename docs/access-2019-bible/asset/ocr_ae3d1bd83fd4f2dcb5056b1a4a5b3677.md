# TABLE 3.3 Numeric Field Settings

| Field Size Setting | Range | Decimal Places | Storage Size |
|---|---|---|---|
| Byte | 0 to 255 | None | 1 byte |
| Integer | -32,768 to 32,767 | None | 2 bytes |
| Long Integer | -2,147,483,648 to 2,147,483,647 | None | 4 bytes |
| Single | -3.4 × 10^38 to 3.4 × 10^38 | 7 | 4 bytes |
| Double | -1.797 × 10^308 to 1.797 × 10^308 | 15 | 8 bytes |
| Replication ID | N/A | N/A | 16 bytes |
| Decimal | -9.999 × 10^27 to 9.999 × 10^27 | 15 | 12 bytes |

# CAUTION

Many errors are caused by choosing the wrong numeric type for number fields. For example, notice that the maximum value for the Integer data type is 32,767. We once saw a database that ran perfectly for several years and then started crashing with overflow errors. It turned out that the overflow was caused by a particular field being set to the Integer data type, and when the company occasionally processed very large orders, the 32,767 maximum was exceeded.

Be aware that overflow may occur simply by adding two numbers together or by performing any mathematical operation that results in a value too large to be stored in a field. Some of the most difficult bugs occur only when circumstances (such as adding or multiplying two numbers) cause an overflow condition at run time.

Design your tables very conservatively and allow for larger values than you ever expect to see in your database. This is not to say that using the Double data type for all numeric fields is a good idea. The Double data type is very large (8 bytes) and might be somewhat slow when used in calculations or other numeric operations. Instead, the Single data type is probably best for most floating-point calculations, and Long Integer is a good choice where decimal points are irrelevant.

# Large Number

The Large Number data type holds values from -2^63 to 2^63-1. Those are bigger numbers than most people need. It was added to Access mainly for compatibility with other databases that have this data type, specifically SQL Server.

If you use Large Number, be aware that not all versions of Access prior to 2019 support this data type. If you're linking to or importing from a database that uses this data type, check the Support Large Number (BigInt) Data Type for Linked/Imported Tables check box in the Current Database tab of Access Options.

# Date/Time

The Date/Time data type is a specialized number field for holding dates or times (or dates and times). When dates are stored in a Date/Time field, it's easy to calculate days between