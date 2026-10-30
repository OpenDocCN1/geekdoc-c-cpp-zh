# ## Enable Design Changes for Tables in Datasheet View

The Enable Design Changes for Tables in Datasheet View check box allows you to make structural changes to your tables in Datasheet view, as opposed to having to be in Design view. In most well-designed Access applications, the users never see the tables in either Design view or Datasheet view, instead interacting with data via forms. If your application allows viewing tables in Datasheet view, you should uncheck this option to prevent unwanted changes to your tables’ designs.

# ## Check for Truncated Number Fields

Checking this option makes numbers appear as ##### when the column is too narrow to display the entire value. (This behavior has been in Excel for a long time.) Unchecking this box truncates values that are too wide to be displayed in the datasheet, which means that users see only a part of the column’s value when the column is too narrow and might misinterpret the column’s contents.

# ## Picture Property Storage Format

Under Picture Property Storage Format, you can choose how graphic files are stored in the database. Your options are:

+   - **Preserve Source Image Format (Smaller File Size):** Choose this option if you want to store the image in the original format, which also reduces the database size.
+   - **Convert All Picture Data to Bitmaps (Compatible with Access 2003 and Earlier):** Choose this option if you want to store all images as bitmaps, which increases the database size but keeps it compatible with previous versions of Access (Access 2003 and earlier).

You have the option to Preserve Source Image Format to conserve disk space by reducing the database file’s size. (This option is only available in the ACCDB file format.) When using this option, Access only stores one copy of an image (in its original format) and dynamically generates a bitmap when the image is displayed on a form or report.

# ## Navigation options

The settings in the Navigation section let you define parameters that affect how users navigate your database as an application.