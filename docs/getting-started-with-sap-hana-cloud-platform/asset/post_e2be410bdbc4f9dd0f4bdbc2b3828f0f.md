

![](img/cf7012644082c115a2181376d9b7486d_202_0.png)

Figure 5.30 Defining a Security Role: Part 2

Once the wizard completes, we'll end up with an empty file called (role_name).hdbrole. Listing 5.7 demonstrates the syntax needed to fill in the role details. Here, the role is defined via the initial role clause. The {acct} token refers to the target SAP HCP account, and the package is the fully qualified package used to define the role (e.g., hcpbook.bookstore.storefront). Within the role definition itself, we assign the application privilege we created in this section to the role, as well as some object privileges that will allow users to query entries from our bookstore data model. The latter is needed to process the OData requests from the SAPUI5 client application.

```
role ({acct} :package):display_access {
    application privilege: {acct}.{package}::Basic;
    catalog sql object "_SYS_"
    BIC:"{acct}.{package}.model::Bookstore.Books": SELECT;
    catalog sql object "_SYS_"
    BIC:"{acct}.{package}.model::Bookstore.Authors": SELECT;
    catalog sql object "_SYS_"
    BIC:"{acct}.{package}.model::Bookstore.BookAuthors":
    SELECT;
    catalog sql object "_SYS_"
    BIC:"{acct}.{package}.model::Bookstore.BookAuthorsView":
    SELECT;
}
```

Listing 5.7 Defining a Display-Only Role for the Demo Application

For now, that's all we have to define. In the next section, you'll learn how to deploy this role and assign it to end users.

## 5.7 Deployment and Testing

Now that we've created all of the relevant repository artifacts that make up our sample application, we're ready to deploy our application and start testing it. In this section, we'll see how these tasks are performed using the Eclipse IDE and SAP HCP Cockpit tools.

### 5.7.1 Activating the SAP HANA XS Project

As we noted in Section 5.3, all of the source code artifacts created during the development process in the Eclipse IDE are initially saved to a workspace folder on your local machine. Therefore, before you can test your SAP HANA XS application, you must first synchronize the contents of this workspace folder with the remote SAP HANA Repository.

If you followed along with the SAP HANA XS project setup steps outlined in Section 5.3, then all of the necessary plumbing should be in place to trigger this synchronization process. Here, you can utilize the repository workspace created in Section 5.2.2 to open the remote SAP HANA Repository connection and sync the files. Within the Eclipse IDE, this task is carried out as follows:

- 1. Right-click on the SAP HANA XS project root folder and select the TEAM • ACTIVATE ALL... menu option, as shown in Figure 5.31.
- 2. This will open the ACTIVATE INACTIVE OBJECTS dialog box shown in Figure 5.32. From here, select or deselect the artifacts you wish to sync, and then click on the OK button to trigger the activation. At this point, the files will be copied to the remote SAP HANA Repository and, if there are no syntax errors, activated.

![](img/cf7012644082c115a2181376d9b7486d_204_0.png)

Figure 5.31 Activating the Project In the Remote SAP HANA Repository: Part 1

Note that this same process would be used to perform incremental sync-ups whenever you're unit testing the application and applying defect corrections. Or, if you prefer, you can perform one-off activations by right-clicking on a particular repository file and activating it directly.

![](img/cf7012644082c115a2181376d9b7486d_205_0.png)

Figure 5.32 Activating the Project in the Remote SAP HANA Repository: Part 2

### 5.7.2 Assigning the Display Role to a User Account

Once your SAP HANA XS project is activated, you should see several new objects installed in the SAP HANA Repository: the tables and views we defined in Section 5.4, the SAP HANA XS application itself, and so forth. Included in this list of repository artifacts is the security role we created in Section 5.6.3. Before you can test your SAP HANA XS application, you need to assign this role to the user account(s) you want to use to test the application.

To perform this role assignment, you must execute a stored procedure within the target SAP HANA instance. When working with an SAP HCP trial account, the steps required to execute this procedure are as follows:

- 1. Within the Eclipse IDE, open the SAP HANA DEVELOPMENT perspective, and switch over to the Systems tab.
- 2. Select the connection node for your remote SAP HANA instance, and click on the SQL button in the top-level toolbar (see Figure 5.33).

![](img/cf7012644082c115a2181376d9b7486d_206_0.png)

Figure 5.33 Assigning the Display Role to a Test User

- 3. This will open the SQL CONSOLE window shown on the right-hand side of Figure 5.33. Within this editor, you'll want to build the call to the HCP_GRANT_ROLE_TO_USER procedure, using the syntax contained in Listing 5.8.
- 4. Once you've crafted your CALL procedure statement, click on the Execute button to perform the assignment.

```
CALL "HCP"."HCP_GRANT_ROLE_TO_USER"(
 'acct_name', {pk_gname} := '{role_name}',
 '{user_name}');
```

Listing 5.8 Granting the Display Role to an End User

If you're working with a customer or partner account, the role assignment process is similar to that of the trial account but calls for the use of a different set of stored procedures. You can find details regarding which procedures to call and the specific call syntax in the SAP HANA Security Guide, available online at http://help.sap.com/hana_platform.

### 5.7.3 Importing Test Data

After the role assignments are complete, our bookstore application is officially open for business. However, because the tables we created are empty, the application doesn't really do all that much. Therefore, to get things up and running, we need to load our data model with some test data.

Although there are many ways of accomplishing data loads in SAP HANA, one convenient option is to use the data import wizard included with the SAP HANA Tools plug-ins installed in the Eclipse IDE. Here, we have the option of uploading test data from CSV files, Excel files, and so forth.

For the purposes of our demonstration, we've included a series of CSV files with the book's source code bundle (downloadable from www.sap-press.com/3638) that you can use to prepopulate the bookstore data model with some sample data. To import these files into your custom bookstore schema, perform the following steps:

- 1. Within the Eclipse IDE, open the SAP HANA DEVELOPMENT perspective, and select the File > IMPORT... menu option from the top-level menu bar.
- 2. This will open the IMPORT dialog box shown in Figure 5.34. From here, expand the SAP HANA Content folder and select the DATA FROM LOCAL FILE option. Click on NEXT > to continue.

![](img/cf7012644082c115a2181376d9b7486d_207_0.png)

Figure 5.34 Importing Test Data from Eclipse: Part 1

- 3. In the next step, you'll be prompted to select the target SAP HANA system you want to upload the data to (see Figure 5.35). Select the target system, and click on NEXT >.

![](img/cf7012644082c115a2181376d9b7486d_208_0.png)

Figure 5.35 Importing Test Data from Eclipse: Part 2

- 4. Select the source CSV file that you want to upload and the target table where you want to land the data. As you can see in Figure 5.36, this step also allows you to specify the field delimiter, ranges of records within the file to upload, and so forth. For our purposes, we'll choose the default file encoding, the default record delimiter (comma), and the IMPORT ALL DATA checkbox, because we want to pull in all the test data contained in the source file in one go. Click on the NEXT > button to continue.
- 5. In the MANAGE TABLE DEFINITION and DATA MAPPINGS step (Figure 5.37), map the fields from the source CSV file to the corresponding fields in the target table. Because the test files are fully populated, you can select the One to One menu option highlighted in Figure 5.37 to automatically map the fields. As the mapping(s) are being defined, you can preview the import in the bottom panel of the IMPORT dialog box (see Figure 5.37). Once all the mappings are in place, click on the Finish button to kick off the import process.

