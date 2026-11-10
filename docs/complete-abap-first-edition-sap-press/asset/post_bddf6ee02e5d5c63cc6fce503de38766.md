
- **Pooled tables and cluster tables:** Pooled tables and cluster tables are an SAP-specific category of database tables that has one-to-many relationships with underlying database tables. In other words, when you define a pooled table or a cluster table in ABAP Data Dictionary, it can create multiple database tables in the underlying database. These tables are usually used by SAP to store internal control information, documentation, and so on.

## Transparent, pool, and cluster tables

These tables shouldn't be used to store business data. SAP recommends transforming all existing pooled tables and cluster tables to transparent tables. Similar to transparent tables, you can use Open SQL statements to access pooled and cluster tables; however, you can't use Native SQL statements for pooled and cluster tables.

You can read more about these tables at http://help.sap.com/abapdocu_750/en/index.htm?file=abenddic_database_tables_poolclu.htm.

- **Global temporary tables (GTTs):** With the release of SAP NetWeaver 7.5, a new table category, *global temporary tables*, has become available. GTTs are special transparent tables used to store temporary data within a database logical unit of work (LUW). A database LUW exists between each dialog step. Each dialog step comprises programming logic between two successive screens. Individual dialog steps of a program can be executed by different work processes in the application server, and a program consists of multiple dialog steps. GTTs allow you to split complicated database processes into multiple steps, such as storing temporary subtotals.

  GTTs are designed specifically for storing temporary data within a database LUW and thus incur far lower administration costs than regular transparent tables. A GTT is always empty at the start of a database LUW, which implies that it should be cleared at the end of each database LUW. Database systems generally provide native support for GTTs by implicitly defining the data in a GTT database table as transaction-specific data. This ensures that the data in a GTT is implicitly deleted at the end of a database LUW (when a database commit or rollback is performed).

  If a GTT defined in ABAP Data Dictionary is filled explicitly using Open SQL statements, then it should be cleared explicitly at the end of a database LUW using the statement `DELETE FROM dbtab`. A GTT should also be explicitly cleared if ABAP statements such as `COMMIT WORK`, `COMMIT CONNECTION`, `ROLLBACK WORK`, `ROLLBACK CONNECTION`, or associated Native SQL statements are used. The `COMMIT WORK` and `ROLLBACK WORK` statements clear the GTTs of all currently open database connections, but you can delete the GTTs of the specified connection by using the `COMMIT CONNECTION` and `ROLLBACK CONNECTION` statements.

  If an ABAP Data Dictionary GTT isn't cleared explicitly via the `DELETE FROM dbtab` statement before an implicit database commit is performed, it will result in the runtime error `COMMIT_GTT_ERROR`. This runtime error is raised even if the table is empty if the statement `DELETE FROM dbtab` is supplied with a `WHERE` clause. The explicit clearing of ABAP Data Dictionary GTTs is forced by SAP to ensure that the code is transparent and easy to understand. For example, the developer may be surprised to find the table empty in between a programming module if the table was cleared implicitly by the database system due to a database LUW performed by an RFC. Explicitly clearing GTTs also helps to avoid platform dependencies, because not all database systems implicitly clear GTTs. GTTs can be accessed just like regular transparent tables via both Open SQL and Native SQL statements. However, SAP recommends using only Open SQL statements when working with GTTs.

- 3. The Dictionary: Change Table View consists of multiple tabs to maintain various properties of the database table. The Delivery and Maintenance tab is selected by default. Under this tab, you can maintain the settings for Delivery Class and Data Browser/Table View Maintenance:
  - Delivery CLASS: This field allows you to select the type of data the database table will contain. Use F4 help to select from one of the available options, as shown in Figure 10.4. The option selected for Delivery CLASS will control the transport of table data during installation, upgrades, and client copies. This setting also influences transport between customer systems. For this example, select A so that you can store application data in this table.
  - Data Browser/Table View Maintenance: This field allows you to restrict whether data can be entered by the user manually or the table can be updated only through programs (i.e., Transaction SE16). Select the relevant option from the dropdown list. Use F1 help on both fields to learn more about these settings.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_401_0.png)

**Figure 10.4** Delivery and Maintenance Tab

- 4. Once the settings are maintained in the Delivery and Maintenance tab, click the Fields tab. This tab allows you to maintain the fields for the database table (see Figure 10.5). The Fields tab presents a table control to maintain various attributes for the field.

Under the Fields tab is a table containing several columns:

  - FIELD: Provide a name for the field. The acceptable characters for field names are letters, numbers, and underscore. The field name must begin with a letter. A field name must not be longer than sixteen characters.
  - KEY: Select this checkbox if the field is part of the table key. All the key fields should be at the top of the table contiguously.
  - INITIAL VALUES: Select this checkbox to set a NOT NULL flag in the database. This setting is useful when adding new fields to the existing database table, because the system will automatically fill the field with type-compatible initial values for all the rows of the field. If this flag is not set for new fields in an existing table, the system will assign a NULL value for all the rows of the field. Because there's no counterpart for NULL in ABAP, this field can then be
  - **DATA TYPE/LENGTH/DECIMAL PLACES/SHORT DESCRIPTION:** These fields are disabled by default and filled automatically based on the data element provided in the previous field. If you wish to maintain the data type, length, decimal places, and short description manually, click the PREDEFINED TYPE button (see Figure 10.6) and enter the details manually. Note that only limited functionality is provided for fields without data elements. These fields can't have foreign keys or fixed values defined. There is no F1 help for these fields.
  - **GROUP:** When including a structure in the table, the structure can be assigned a group name. ABAP programs can access the fields of this include structure together or individually using the group name. Note that the components of the include structure are part of the table, so they can be accessed directly using the table name reference. Providing a group name is optional.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_403_0.png)

**Figure 10.6** Predefined Type

- 5. Once you've finished with the entries under the FIELDS tab, go to the ENTRY HELP/CHECK tab. The ENTRY HELP/CHECK tab shows information about the associated check table, input help, and search help for the fields (see Figure 10.7).

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_403_1.png)

**Figure 10.7** Entry Help/Check Tab

Click the INFORMATION icon (lowercase i) in the window to learn more about these options.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_405_0.png)

**Figure 10.9** Maintain Enhancement Category

- 8. Once the enhancement category for the table is maintained, you need to maintain the technical settings for the table before it can be activated.

Technical settings define how the table is created in the database. Save your table before calling the technical settings screen. To maintain technical settings for the table, click the TECHNICAL SETTINGS button (see Figure 10.10) in the application toolbar to call the Dictionary: Maintain Technical Settings screen (see Figure 10.11). This will open Transaction SE13.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_405_1.png)

**Figure 10.10** Calling Technical Settings Screen

- 9. You can maintain the following technical settings for the database table on this screen (see Figure 10.11):
  - **DATA CLASS:** This setting is significant only for Oracle and Informix database platforms. For all other database platforms, this setting should be ignored.
