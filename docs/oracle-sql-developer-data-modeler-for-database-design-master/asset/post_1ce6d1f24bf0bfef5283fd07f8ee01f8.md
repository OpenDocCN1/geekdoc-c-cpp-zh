
## Chapter 8: Designing a Data Warehouse Database 185

the logical model and select Set Classification Types. In the dialog that opens you can specify which entities are, for instance, of type Fact. You can define additional classification types for an entity by selecting Additional Classification Types in the Browser pane. On the diagram a capital D in the top-left corner of the entity shows that this is an entity of dimension, and a capital F shows it is a fact table. If you want to see the classification type name or have defined several classification types for an entity, right-click the diagram and choose View Details | Classification Types. Figure 8-1 shows a design for a star schema (left) and snowflake (right) in ER notation using Modeler with the classification types displayed.

When you are ready with the ER model, you can move to the relational model as described in Chapter 5 by running the Engine To Relational command. This transformation is done automatically based on the logical model, preferences, and properties. If you want surrogate keys generated automatically (IDs) for your tables, as usually recommended for DW databases, refer to the define Create Surrogate Key property for your entities (usually dimensions). And if you want the fact table to have a primary key constructed only on foreign keys from parent tables, first define the relationships as identifying (see Chapter 4 for more information on the identifying relationship) for all the relationships you want for the primary key. Then go to the properties of the Fact entity and define a unique identifier for it on the Unique key. Then go to the properties of this unique key (double-click the Properties icon) and set the unique identifier to Primary Key.

![](img/431f8ac8f273fa89a28377c500ed60d7_211_0.png)

FIGURE 8-1. logical dimensional model for star schema and snowflake

Oracle SQL Data Modeler for Database Design Mastery 186

Then select the Attributes And Relations tab and select all the relationships for the primary key, as shown in Figure 8-2. Now the fact table will have a primary key. If you are using the automatically generated IDs and want to use this dimensional model as a base for a multidimensional model, select Relational Model as the Bound Model setting when creating the multidimensional model (more about this later in chapter). If you select Logical Model, you will not see the IDs (because they are created for the relational model) to be able to link the dimensional model entities and multidimensional model objects. If you want to base the multidimensional model on the logical model, define the logical model manually. Any other IDs except the primary surrogate key you must add manually (such as possible IDs for the entity you might want to use when mapping to the multidimensional model). And remember that in the Design Properties dialog on the Setting | Naming Standards | Templates you can define the name for the automatically generated surrogate key

![](img/431f8ac8f273fa89a28377c500ed60d7_212_0.png)

**Figure 8-2.** Defining a primary key for a fact entity

Chapter 8: Designing a Data Warehouse Database 187

(Surrogate Key) and its column (Surrogate Key Column). After engineering, there are two things to do: you must set the constraint names correctly if they are not automatically set and associate the prefixes to the tables according to their classification type. If you do not want to have prefixes on the constraint names, go your relational model in the Browser pane, right-click, and choose Apply Naming Standards For Keys And Constraints; right-click the relational model again and Change Object Names Prefix. In the Change Object Names Prefix dialog, select Add Prefix. Figure 8-3 shows the snowflake example on the right; you can see that the classification prefixes are not in key and constraint names. If you want the prefixes in constraint names, then Run Object Names Prefixes and only after that Run Applying Naming Standards For Keys And Constraints. Figure 8-3 shows the star schema on the left so you can see that classification prefixes are also in key and constraint names.

Because the dimensional model is a standard framework, it includes templates or patterns for modeling situations for business needs, such as slowly changing dimensions (SCDs), fact table, heterogeneous products, pay-in-advance databases, event-handling databases (factless tables), snapshot fact tables, dimension table structure, periodic snapshot surrogate keys, degenerate dimensions, denormalized flattened dimensions, multiple hierarchies in dimensions, flags and indicators as textual dimension attributes, calendar date dimensions, role-playing dimensions, junk dimensions,

![](img/431f8ac8f273fa89a28377c500ed60d7_213_0.png)

FIGURE 8-3. A relational dimensional model for star schema and snowflake

Oracle SQL Developer Data Modeler for Database Design Mastery 188

dimensions, outrigger dimensions, and many more. In this book I do not go through these, but I encourage you to find more information about them and use the ones you find useful.

You can find a lot of literature about these solutions and best practices for designing data warehouses. Instance, www.kimballgroup.com is a good place to start.

## Data Vault

Data Vault is an emerging method for modeling a data warehouse. It was created by Dan Lindstedt. Data Vault is a hybrid of third normal form and star schema. There are excellent books on Data Vault by Dan Lindstedt and Kent Graziano available. You can find more about Data Vault from LearnDataVault.com or http://danlindstedt.com/about/data-vault-basics/

When starting to model your data warehouse as Data Vault, you must first define the classification types for hubs, links, and satellites. As mentioned earlier, you can do this in the Design Properties. You can also define the prefixes for them, such as HUB_ for Hubs and SAT_ for Satellites. To define a Data Vault model, you must first define the hubs and associated satellites. Then create the many-to-many relationships between the hubs. If you want the resulting link table to be named for example LNK_Sales.

> TIP
> In Preferences (on the Data Modeler | Relational tab), you can define the length of the surrogate key or select an MD5 hash.

When the local model is completed, select Engineer To Relational. Figure 8-4 shows an example of a logical Data Vault. After running the Engineering To Relational command, you should define the classification type to the tables created. In the Browser pane, select your relational model, right-click, and choose Set Classification Types. From the Classification Types list, select Link and in Find LNK. Select the tables and click the arrow pointing to the right. Click Apply or OK. It's time to be the same you saw earlier for start and snowflake; in other words, the constraint names correct and associate the prefixes to the tables according to their classification type. If you do not want to have table prefixes on the constraint names, go your relational model in the Browser pane, right-click, and choose Apply Naming Standards For Keys And Constraints; then

![](img/431f8ac8f273fa89a28377c500ed60d7_214_0.png)

Chapter 8: Designing a Data Warehouse Database 189

![](img/431f8ac8f273fa89a28377c500ed60d7_215_0.png)

**Figure 8-4.** A logical model for Data Vault

right-click the logical model again and Change Object Names Prefix. If you want to have the prefixes also in the constraint names, then run Change Object Names Prefix and Apply Naming Standards For Keys And Constraints only after that.

In a Data Vault, each table must have some predefined columns. You can, of course, define them on the entity and engineer to the table if you want, but you can also use a transformation script to add the columns to the engineered tables or apply a template during forward engineering. A hub should have the business keys needed (a business key is a key for which the business has some kind of meaning), a surrogate key (SQN or hash key), last seen date (LSDT), load date (LDTS), and record source (RSRC). A link should have a surrogate key (SQN or hash key), last seen date (LSDT), load date (LDTS), record source (RSRC), and the hub keys. A satellite should have a surrogate key (SQN or hash key) inherited from the
