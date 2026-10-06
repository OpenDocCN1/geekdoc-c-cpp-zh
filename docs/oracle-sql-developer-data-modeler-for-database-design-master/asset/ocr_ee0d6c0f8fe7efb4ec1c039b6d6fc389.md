# Chapter 8: Designing a Data Warehouse Database 189

![](bbox=[0.125, 0.135, 0.871, 0.555])

**Figure 8-4.** A logical model for Data Vault

right-click the logical model again and choose Change Object Names Prefix. In the Change Object Names Prefix dialog, select Add Classification Prefix. If you want to have the prefixes also in the constraint names, then run Change Object Names Prefix and Apply Naming Standards for Keys And Constraints only after that.

In a Data Vault, each table must have some predefined columns. You can, of course, define them on the entity and engineer to the table if you want, but you can also use a transformation script to add the columns to the engineered tables or apply a template during forward engineering. A hub should have the business keys needed (a business key is a key for which the business has some kind of meaning), a surrogate key (SQN or hash key), last seen date (LSDT), load date (LDTS), and record source (RSRC). A link should have a surrogate key (SQN or hash key), last seen date (LSDT), load date (LDTS), record source (RSRC), and the hub keys. A satellite should have a surrogate key (SQN or hash key) inherited from the