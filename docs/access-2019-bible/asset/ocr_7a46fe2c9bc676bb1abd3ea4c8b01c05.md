The data linked to Access applications comes in a variety of formats. There is no practical way to document every possible type of linking operation in a single chapter. So, this chapter discusses the essential steps required to link to external data and gives a few examples demonstrating how these processes are performed in Access, instead of filling page after page with examples that may or may not be relevant to your work.

As you'll soon see, knowledge of the external data format is critical to a successful linking operation. You must have some notion of the external data format before you can successfully import data into your Access application or incorporate the data into an Access database through linking. This chapter points out many of the issues involved if you choose to link to external data; it's intended to serve as a guide as you perform these operations in your Access applications.

# Fixing Links

We'll discuss the Linked Table Manager later in this chapter in detail. For now, follow these steps to fix the linked tables in Chapter07.accdb:

+   1. Copy the Chapter 07 folder to your computer and make a note of the location.
+   2. Open Chapter07.accdb.
+   3. Click Linked Table Manager in the Import & Link group on the External Data tab of the Ribbon. The Linked Table Manager appears.
+   4. Click the Select All button, make sure Always Prompt For New Location is checked, and then click OK. You'll be prompted for the new location for each of the linked tables.
+   5. Using the table of filenames provided earlier in this chapter, browse to each file. The Linked Table Manager displays a message that all selected linked tables were successfully refreshed. The name of the table it's currently trying to refresh is in the title bar of the file dialog box.
+   6. Click Close to close the Linked Table Manager.

Now you can follow along with the examples in this chapter.

# Linking External Data

As the database market continues to grow, the need to work with information from many different sources will escalate. If you have information captured in a SQL Server database or an old Excel spreadsheet, you don't want to reenter the information from these sources into Access. Also, the processes or policies at your company may require that the data live in these external files, and you don't want to risk having duplicate data that gets out of sync. Ideally, you want to open an Access table containing the data and use the information in its native format, without having to copy it or write a translation program to access it. In many cases, the capability of accessing information from one database format while working in another is often an essential starting point for many business projects.