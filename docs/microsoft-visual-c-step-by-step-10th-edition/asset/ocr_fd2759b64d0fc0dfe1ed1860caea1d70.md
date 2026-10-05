create firewalls that span a range of IP addresses if you need to open access to a set of computers.

The sample AdventureWorks database contains a table named Customer in the SalesLT schema. This table includes the columns containing the data presented by the Customers UWP app and several others. Using the Entity Framework, you can choose to ignore columns that are not relevant, but you won't be able to create new customers if any of the columns you do not allow nulls and do not have default values. In the Customer table, this restriction applies to the NameStyle, PasswordHash, rowguid and PasswordSalt columns (used to encrypt user passwords) as well as the rowguid and ModifiedDate columns (used by other sample apps from Microsoft reference this table). To avoid complications and to enable you to focus on the functionality of the app itself, in the next exercise, you'll remove these columns from the Customer table.

# To remove unneeded columns from the AdventureWorks database

+   1. In the Azure portal, select the navigation menu in the top-left corner, select All resources, and then select the AdventureWorks database.