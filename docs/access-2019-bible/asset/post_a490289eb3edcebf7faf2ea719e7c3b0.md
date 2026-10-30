
+   - Text File
+   - XML File
+   - PDF or XPS
+   - Email
+   - Access
+   - Word Merge
+   - More: Click this button to open the More drop-down list, which has the following options:
+     - Word
+     - SharePoint List
+     - ODBC Database
+     - HTML Document
+     - dBASE File

Obviously, Microsoft has prepared Access well for its role as a "landing pad" for data.

## Importing External Data

An import copies external data into an Access database. The external data remains in its original state, but, after the import, a copy exists within Access. When you import a file (unlike when you link tables), Access converts a copy of the data from an external source into records in an Access table. The external data source is not changed during the import. No connection to the external data source is maintained once the import process is complete.

You can import information to new or existing tables. Every type of data can be imported to a new table. However, some types of imports—such as spreadsheets and text files—don’t necessarily have a table structure compatible with Access. In those cases, Access will create a table structure for you. If you want to control the structure of the table, you should create the table before importing.

## Importing from another Access database

You can import items from a source database into the current database. The objects you import can be tables, queries, forms, reports, macros, or modules. Import an item into the current Access database by following these steps:

+   1. Open the destination database you want to import into. In this case, open the Chapter06_1.accdb database.
+   2. Select the External Data tab.
+   3. Click Import & Link > New Data Source > From Database > Access, and then click the Browse button to select the filename of the source database (Chapter06_2.accdb).

## **1. 引言**

随着人工智能技术的飞速发展，大语言模型（Large Language Model, LLM）已成为自然语言处理领域的核心技术。它们通过在海量文本数据上进行预训练，学习到了丰富的语言知识和世界知识，能够胜任文本生成、问答、摘要、翻译等多种任务。然而，大语言模型在带来巨大机遇的同时，也伴随着一系列严峻的安全挑战。

这些安全挑战不仅涉及模型本身可能被恶意利用（如生成虚假信息、恶意代码），还涉及模型在训练和部署过程中可能引入的偏见、隐私泄露等问题。因此，系统性地研究大语言模型的安全问题，并提出有效的防护策略，对于推动人工智能技术的健康、可持续发展具有至关重要的意义。

## **2. 大语言模型面临的主要安全威胁**

大语言模型的安全威胁可以从多个维度进行分类。从攻击者的视角来看，主要可以分为以下三类：

+   - **提示注入攻击**：攻击者通过精心设计的输入提示，诱导模型执行非预期的操作，例如忽略系统指令、泄露敏感信息或生成有害内容。
+   - **数据投毒攻击**：攻击者在模型的训练数据中植入恶意样本，导致模型在特定触发词下产生错误或有害的输出。
+   - **模型窃取与逆向攻击**：攻击者通过大量查询接口，尝试逆向推导模型的参数或训练数据，从而窃取模型的核心知识产权或隐私信息。

## FIGURE 6.3

The Save Import Steps feature lets you save frequently executed import processes for future use.

![](img/1e45673ab6eca9d20e67635ff5b9b318_220_0.png)

+   6. **Check the Save import steps check box.** Access will display the Save as and Description fields.

+   7. **Provide a name for the import process to make it easy to recall the saved import’s purpose and then click Save Import.** You can execute the saved import again at a later date by clicking the Saved Imports button in the Import & Link group of the External Data tab of the Ribbon. From the Manage Data Tasks dialog box (see Figure 6.4), you can change the name of the saved import, the location of the source file, and the description of the saved import. All other information about the saved import (such as the destination table name) can’t be changed. If you need to change other information, create a new saved import with the proper parameters.

## Part II: Understanding Access Tables

![](img/1e45673ab6eca9d20e67635ff5b9b318_221_0.png)

![](img/1e45673ab6eca9d20e67635ff5b9b318_221_1.png)

## FIGURE 6.4

The Saved Imports feature lets you rerun previous saved import processes.

![](img/1e45673ab6eca9d20e67635ff5b9b318_221_2.png)

## Importing from an Excel spreadsheet

You can import data from Excel spreadsheets to a new or existing table. The primary rule when importing Excel data is that each cell in a column must contain the same type of

data. When you're importing Excel data into a new table, Access guesses at the data type to assign to each field in the new table based on the first few rows of Excel data (other than column headings). An import error may occur if any Excel row past the first few rows contains incompatible data. In Figure 6.5, the Age column should contain all numeric data, but it contains an age written out as words. This is likely to cause an error during the import process. The data in Row 5 should be changed so that the entire column contains numeric data (as shown in Figure 6.6).

You can import all the data from an Excel spreadsheet, or just the data from a named range of cells. Naming a range of cells in your spreadsheet can make importing into Access easier. Often a spreadsheet is formatted into groups of cells (or ranges). One range may contain a listing of sales by customer, for example, while another may include total sales for all customers, totals by product type, or totals by month purchased. By providing a range name for each group of cells, you can limit the import to just one section of the spreadsheet data.

## FIGURE 6.5

Access can import data from an Excel spreadsheet, but there are some restrictions.

![](img/1e45673ab6eca9d20e67635ff5b9b318_222_0.png)

This data will cause import problems.

4. Select Import the Source Data into a New Table in the Current Database and click OK. The first Import Spreadsheet Wizard screen (see Figure 6.7) shows lists of worksheets or named ranges, and a preview of the data, in the Excel spreadsheet.

## FIGURE 6.7

The Import Spreadsheet Wizard.

![](img/1e45673ab6eca9d20e67635ff5b9b318_224_0.png)

5. Select a worksheet or named range and click Next.

6. On the next screen (shown in Figure 6.8), select the First Row Contains Column Headings check box and click Next. Normally you don't want the Excel column headings stored as field data. Access uses the column headings as the field names in the new table.

## FIGURE 6.8

Does the first row contain column headings?

![](img/1e45673ab6eca9d20e67635ff5b9b318_225_0.png)

7. On the next screen (shown in Figure 6.9), you can override the default field name and data type, remove fields from the import, and create an index on a field. When you're done, click Next.

## FIGURE 6.9

You can override any of the default settings Access has chosen.

![](img/1e45673ab6eca9d20e67635ff5b9b318_226_0.png)

8. On the next screen, set a primary key for the new table (see Figure 6.10) and click Next. A primary key uniquely identifies each row in a table.

## FIGURE 6.10

Specify a primary key for the new table.

![](img/1e45673ab6eca9d20e67635ff5b9b318_227_0.png)

## CAUTION

Be somewhat wary when choosing a primary key for the imported file. The field you choose must conform to the rules of primary keys: no value can be null, and no duplicates are allowed. The purpose of a table's primary key is to uniquely identify the rows in the table, so if no column in the Excel spreadsheet is appropriate for this purpose, it's probably best to let Access add a default primary key field. The primary key added by Access is always an AutoNumber and always conforms to data normalization rules.
Primary keys are discussed in Chapters 3 and 4.

+   9. Specify the new table's name and click Finish.

## CAUTION

If you import an Excel file with the same name as an Excel file you've already linked, Access will ask if you want to overwrite the existing file. Unless you actually intend to replace the linked table, you must give the newly imported table a new name.

+   10. If you want to, save the import process for later execution. The new table now appears in the Navigation pane.

## Importing a SharePoint list

SharePoint lists are candidate data sources for Access databases. Because SharePoint lists reside on web servers, SharePoint data is accessible across a network to qualified users. This gives Access the ability to share data virtually anywhere in the world.

Part VIII is dedicated to understanding and working with SharePoint Services.

Because SharePoint is deployed on a large number of corporate intranets, Access is likely to continue as a component in enterprise environments.

## Importing data from text files

There are many reasons for text file output, such as business-to-business (B2B) data transfers. Also, mainframe data is often output as text files to be consumed in desktop applications. Access can import from two different types of text files: delimited and fixed width. The Access Import Text Wizard assists you in importing or exporting both delimited and fixed-width text files.

## Delimited text files

In delimited text files (sometimes known as comma-delimited text files, comma-separated-values text files, or tab-delimited text files), each record is on a separate line in the text file. The fields on the line contain no trailing spaces, normally use commas or tab characters as field separators, and might have certain fields that are enclosed in qualifying characters (such as single or double quotation marks). Here’s an example of a comma-delimited text file:

```
1,Davolio,Nancy,5/1/14 0:00:00,4000
2,Fuller,Andrew,8/14/14 0:00:00,6520
3,Leverling,Janet,4/1/14 0:00:00,1056
4,Peacock,Margaret,5/3/15 0:00:00,4000
5,Buchanan,Steven,10/17/15 0:00:00,5000
6,Suyama,Michael,10/17/15 0:00:00,1000
7,King,Robert,1/2/14 0:00:00,1056
8,Callahan,Laura,3/5/14 0:00:00,1056
9,Dodsworth,Joseph,11/15/14 0:00:00,1056
```

Notice that the file has nine records (rows of text) and five fields. A comma separates each field. In this example, text fields are not qualified with double quotation marks. Notice also that the rows are different lengths because of the variable data within each row.
