5. Tables of databases have two basic properties: field names and data types:

![](bbox=[0.15, 0.2, 0.9, 0.6])

Figure 15.6. Table properties

For example, if we are creating a database that will hold data regarding the staff in a company, the database table will have fields like the id (identification number), name, surname and age of the personnel. The id will be the unique key of each person which typically has an integer value. Name and surname will obviously be character strings and the age will also be an integer value. Note that name, surname or age can be the same for two persons while the id will be different for each one.

Let’s create this table in our database. The field names will be the id_field, name_field, surname_field and age_field. Data types will be AutoNumber, Text, Text and Number, respectively. After defining these fields and types, our database structure will be as in Figure 15.7.

We did set the type of the id_field as AutoNumber meaning that it will increment automatically when new data is inserted into the table. Therefore it is better to set this field as the key to access the data on the table. For this, select the id_field cell and click the Primary Key button as shown in Figure 15.8. A small key image will then appear at the left of the field as indicated in Figure 15.9.