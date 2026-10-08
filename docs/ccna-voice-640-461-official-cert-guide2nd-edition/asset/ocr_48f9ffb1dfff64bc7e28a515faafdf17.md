Figure 13-16 shows the LDAP Directory Configuration page.

![](bbox=[0.118, 0.103, 0.801, 0.532])

Figure 13-16 LDAP Directory Configuration Page

# Bulk Administration Import of CUC Users

Import users using the Bulk Administration Tool is a fast and easy way to create multiple-accounts if the required user information can be formatted as a CSV file. To import users, follow these steps:

+   1. Navigate to Tools > Bulk Administration Tool.
2. Under Select Operation, select Create. (Note that you can also Update, Delete, or Export.).
3. Under Select Object Type, choose Users With Mailbox.
4. Under Override CSV Fields When Creating User Accounts, select User Template Yes and select the desired Template.
5. Under Select File, browse to the .csv file that contains the user import information.
6. Specify a Failed Filename.
7. Click Submit.

**Note:** The formatting of the .csv is critical to the success of the import. The easiest way to get a correctly formatted file is to perform a BAT Export of a single user. The .csv file then has all the necessary information you need to create the import file correctly. This is