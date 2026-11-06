# **17.10** *(File Matching Enhancement)*

It's common to have several transaction records with the same record key, because a particular customer might make several purchases and cash payments during a business period. Rewrite your accounts receivable file-matching program of Exercise 17.7 to provide for the possibility of handling several transaction records with the same record key. Modify the test data of Exercise 17.8 to include the following additional transaction records:

| Account number | Dollar amount |
|---|---:|
| 300 | 83.89 |
| 700 | 80.78 |
| 700 | 1.53 |

# **17.11**

Write a series of statements that accomplish each of the following. Assume that we've defined class `Person` that contains the private data members

```
string lastName;
string firstName;
string age;
int id;

and public member functions

// accessor functions for id
void setId( int );
int getId() const;

// accessor functions for lastName
void setLastName( string );
string getLastName() const;

// accessor functions for firstName
void setFirstName( string );
string getFirstName() const;

// accessor functions for age
void setAge( string );
string getAge() const;
```

Also assume that any random-access files have been opened properly.

+   a) Initialize the file named `data` with 100 records that store values `lastName = "unsigned", firstName = "" and age = "0"`.
+   
+   b) Input 10 last names, first names and ages, and write them to the file.
+   
+   c) Update a record that already contains information. If the record does not contain information, inform the user "No info".
+   
+   d) Delete a record that contains information by reinitializing that particular record.

# **17.12** *(Hardware Inventory)*

You are the owner of a hardware store and need to keep an inventory that can tell you what different tools you have, how many of each you have on hand and the cost of each one. Write a program that initializes the random-access file hardware.dat to 100 empty records, lets you input the data concerning each tool, enables you to list all your tools, lets you delete a record for a tool that you no longer have and lets you update any information in the file. The tool identification number should be the record number. Use the following information to start your file:

| Record # | Tool name | Quantity | Cost |
|---:|---|---:|---:|
| 3 | Electric sander | 7 | 57.98 |
| 17 | Hammer | 76 | 11.99 |