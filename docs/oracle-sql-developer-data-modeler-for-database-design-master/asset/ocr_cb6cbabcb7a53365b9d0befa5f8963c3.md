# Chapter 5: Introducing Logical Database Design (Relational Model) 131

can be done to table and column abbreviations. The comparison is case sensitive, and only whole words or words with the underscore _ are replaced. For example, these rows in the CSV file would have a different result:

CUSTOMER, CUST
CUSTOMER, CUST

The first one would replace, for instance, Customer_ID with CUST_ID, but the latter one would not find the word Customer at all because of the case sensitivity. Neither of them would replace CUSTOMID with CUSTID because CUSTOM in that word is not a single word or part of a word separated with an underscore. CUSTOM_ID would be replaced by CUST_ID by the latter row in the CSV file.

You start a name abbreviation by selecting the CSV file; click the Browse button in the Name Abbreviations dialog and find the correct file. For the separator, you can define a comma or any other separator. If you select a separator that does not exist in the file, you will get an error message. After you select the file, you select the scope and direction for the transformation. If you want to keep the original letter case when changing part of the name, select Keep Case. If you want to use the letter case defined in the CSV file, disable this property. For instance, if you have a column containing: customer_name, and you disable the Keep Case property, the column name will be changed to CUST_name. When the property is selected, the column name will be changed to CUST_NAME. When you have selected the right setting, click OK. If you have several designs open, select the design you want to perform the models. The changes are made, and the log will show all the changes, as shown in Figure 5-29. You can save the log if you want.

> NOTE
If you perform name abbreviations in both directions with the same file and settings, names and abbreviations should be the same as they were when you started. In this case, the name/abbreviations combinations must be unique.

In datamodel/datamodel/templates, you can find two example files for name abbreviations: ABREVS_SAMPLE.csv and plurals.csv. The plurals.csv file is an example of a use case of this utility. If you decide in the middle of the project that the table names should actually be plurals/singulars instead of singular/plurals, you can use this utility to change the naming quite easily.

![](bbox=[0.176, 0.666, 0.173, 0.703])