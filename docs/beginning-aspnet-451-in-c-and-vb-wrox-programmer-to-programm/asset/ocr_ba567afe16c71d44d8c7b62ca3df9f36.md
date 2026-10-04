# Creating Your Tables | 431

| COLUMN NAME | DATA TYPE | ALLOW NULLS | DESCRIPTION |
| --- | --- | --- | --- |
| Id | int | No | The primary key and identity of the table. |
| Title | varchar(200) | No | Contains the title of the review. |
| Summary | varchar(max) | No | Contains a short summary or teaser text for the review. |
| Body | varchar(max) | Yes | Contains the full body text of the review. |
| GenreId | int | No | Contains the ID of a genre that the review belongs to. |
| Authorized | bit | No | Determines whether the review is authorized for publication by an administrator. Unauthorized reviews will not be visible on the website. |
| CreateDateTime | datetime | No | The date and the review is created. |
| UpdateDateTime | datetime | No | The date and the review is updated. |

+   8. Make the Id column the primary key, and set it (Identity property) to Yes as you do in steps 4 and 5.

+   9. Click the CreateDateTime column and then on the Column Properties grid, type getdate() in the field for the Default Value or Binding property, as shown in Figure 12-2. This inserts the current date and new rows if you do not supply an value.

+   10. Repeat the preceding step for the UpdateDateTime column.

+   11. When you're done, press Ctrl+S to save the table and call it Review. Close the table designer by pressing Ctrl+F.

# How it Works

The Table Designer in SSMS is perfectly straightforward. You type new column name and define data type for the column, and you're pretty much done.  For those columns, you set it (Identity property) to Yes. This means that SQL Server automatically assigns a new sequential number to each new row that you insert. By the first row in the table gets an ID of 1, and the ID of subsequent rows is increased by one. You can change the default behavior by setting the Identity Increment and Identity Specification element for the column.

![](bbox=[0.568, 0.506, 0.931, 0.783])

FIGURE 12-2

*