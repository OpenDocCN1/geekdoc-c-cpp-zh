Without the pound signs, Access evaluates the date values as numeric expressions (10 divided by 1 divided by 2012, for example).

# Using the Between...And operator

You can request a range of records using another method—the Between...And operator. With Between...And, you can find records that meet a range of values—for example, all sales where the list price of the product was between $50 and $100. Using the previous example with dates, create the query shown in Figure 9.14.

# FIGURE 9.14

Using the Between...And operator. The results are the same as the query in Figure 9.13.

![](bbox=[0.15, 0.48, 0.65, 0.7])

The operands for the Between...And operator are inclusive. This means that sales on 10/1/2012 and 3/31/2013 are included in the query results.

# Searching for null data

A field might have no contents for several reasons. For example, perhaps the value wasn’t known at the time of data entry, or the person who did the data entry simply forgot to enter the information, or the field’s information was removed. Access does nothing with this field. Unless a default value is specified in the table design, the field simply remains empty. (A field is said to be null when it’s truly empty.)

Logically, null is neither true nor false. A null field is not equivalent to all spaces or to zero. A null field simply has no value.