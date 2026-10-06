# 188 Oracle SQL Developer Data Modeler for Database Design Mastery

dimensions, outrigger dimensions, and many more. In this book I do not go through these, but I encourage you to find more information about them and use the ones you find useful.

You can find a lot of literature about these solutions and best practices for designing data warehouses. Instance, www.kimballgroup.com is a good place to start.

# Data Vault

Data Vault is an emerging method for modeling a data warehouse. It was created by Dan Lindstedt. Data Vault is a hybrid of third normal form and star schema. There are excellent books on Data Vault by Dan Lindstedt and Kent Graziano available. You can find more about Data Vault from LearnDataVault.com or http://danlindstedt.com/about/data-vault-basics/

When starting to model your data warehouse as a Data Vault model, you must first define the classification types for hubs, links, and satellites. As mentioned earlier, you can do this in the Design Properties dialog. You can also define the prefixes for them, such as HUB_ for Hubs and SAT_ for Satellites. To define a Data Vault model, you must first define the hubs and associated satellites and define the classification types for them. Then create the many-to-many relationships between the hubs. The relationship as you would like the resulting link table to be named. If you want to use prefixes for Link tables note the relationships with the prefix, for example LNK_SalesProduct. Also remember on the hubs to select Create Surrogate Key in the Entity Properties dialog on the General tab because all tables in Data Vault should have a key as a surrogate key, for example an MD5 hash.

> TIP
In Preferences (on the Data Modeler | Relational tab), you can define the length of the surrogate key or select a domain for.

When the local model is completed, select Engineer To Relational Model. Figure 8-4 shows an example of a logical Data Vault model.

After running the Engineering To Relational Model command, you should define the classification type to the link tables created. In the Browser pane, select your relational model, right-click, and choose Set Classification Types. From the Classification Types list, select Link and in Find type LNK. Select the tables and click the arrow pointing to the right. Click Apply or OK. It's time to be the same two you saw earlier for start and snowflake; in other words, the constraint names correct if they are not automatically and associate the prefixes to the tables according to their classification type. If you do not want to have table prefixes on the constraint names, go to your relational model in the Browser pane, right-click, and choose Apply Naming Standards for Keys And Constraints; then

![](bbox=[0.166, 0.582, 0.166, 0.622])