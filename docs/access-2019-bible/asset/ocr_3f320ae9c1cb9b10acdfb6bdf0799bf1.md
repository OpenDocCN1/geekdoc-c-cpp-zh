# When to index

Generally speaking, you should index fields that are frequently searched or sorted. Remember that indexes slow down certain operations, such as inserting records and some action queries.

Long Text and OLE Object fields can't be indexed. It would be impossible for Access to maintain an index on these complex data types.

An index should not be used if a field contains very few unique values. For example, you won't see a significant benefit from indexing a field containing a person's gender or a Yes/No field. Because there is a limited range of values in such fields, Access easily sorts the data in these fields.

Use a multiple-field index in situations where sorts are often simultaneously performed on multiple fields (for example, first and last names). Access will have a much easier time sorting such a table.

# Understanding tblCustomers Field Properties

After you enter the field names, data types, and field descriptions, you may want to go back and further refine each field. Every field has properties, and these are different for each data type. In tblCustomers, you must enter properties for several data types. Figure 3.11 shows the property area for the field named CreditLimit. Notice that there are two tabs on the property box: General and Lookup.

# FIGURE 3.11

The property area for the Currency field named CreditLimit.

![](bbox=[0.15, 0.86, 0.75, 0.92])

# Tip

Figure 3.11 shows ten properties available for the CreditLimit Currency field. Other types, such as Number, Date/Time, Short Text, or Yes/No, show more or fewer options.