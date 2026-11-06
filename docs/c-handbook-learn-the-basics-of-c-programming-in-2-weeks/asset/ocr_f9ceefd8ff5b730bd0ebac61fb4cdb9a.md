# 1. Unicode Strings

| DATA TYPE | Description |
|---|---|
| Nchar | Maximum length of 4,000 characters. ( Fixed length Unicode) |
| Nvarchar | Maximum length of 4,000 characters. (Variable length Unicode) |
| nvarchar(max) | Maximum length of 231characters (SQL Server 2005 only). ( Variable length Unicode) |
| Ntext | Maximum length of 1,073,741,823 characters. ( Variable length Unicode ) |

# 2. Non-Unicode Strings

| DATA TYPE | FROM | TO |
|---|---|---|
| Char | Char | Maximum length of 8,000 characters. ( Fixed length non-Unicode characters) |
| Varchar | Varchar | Maximum of 8,000 characters. (Variable-length non-Unicode data). |
| varchar(max) | varchar(max) | Maximum length of 231characters, Variable-length non-Unicode data (SQL Server 2005 only). |
| Text | text | Variable-length non-Unicode data with a maximum length of 2,147,483,647 characters. |

# 5. Binary

| DATA TYPE | Description |
|---|---|
| Binary | Maximum length of 8,000 bytes.(Fixed-length binary data ) |
| Varbinary | Maximum length of 8,000 bytes. (Variable length binary data) |
| varbinary(max) | Maximum length of 231 bytes (SQL Server 2005 only). ( Variable length Binary data) |
| Image | Maximum length of 2,147,483,647 bytes. ( Variable length Binary Data) |

# 6. Miscellaneous

This category involves the following data types:

+   - timestamp – This data type stores a unique number that becomes updated whenever a row becomes updated. You may access this unique number in any part of your database.
+   - xml – This data type stores XML (i.e. Extensible Markup Language) information. You may save XML data in columns or variables.
+   - table – This type saves the results of your database queries so that you can use