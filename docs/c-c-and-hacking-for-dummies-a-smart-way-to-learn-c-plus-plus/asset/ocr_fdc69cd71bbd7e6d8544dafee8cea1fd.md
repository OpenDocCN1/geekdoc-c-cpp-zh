# # Chapter 2 – Examples of Relational Models

Since I have been using thepeople’s database in the previous chapter, I will now give to you a contacts database as a perfect example of a relational model.

A simple database for contacts typically looks like this:

| First Name | Last Name | Email Address |
|---|---|---|
| John | Doe | johndoe@email.com |
| Mae | Lee | maelee@email.com |

In this table, we have three columns that are looking for specific data. The first column requests for the first name. The second for the last name and the third for the email address of the person.

Our rows, excluding the first row, refers to a single entity. The row for our first entity refers to the person with the name John Doe and his email is johndoe@email.com. The row for our second entity refers to Mae Lee with an email address of maelee@email.com.

This is an example of a database with two entities divided by three columns.

Let us say that John Doe has two email addresses while Mae Lee has three. Some people will end up adding columns to add the additional data. Hence, the table will end up like this.

| First Name | Last Name | Email 1 | Email 2 | Email 3 |
|---|---|---|---|---|
| John | Doe | johndoe@… | johndoe2@… | NULL |
| Mae | Lee | maelee@… | maelee2@… | maelee3@… |

There is a problem here if we use this kind of database design. First, what if the problem we have at hand is to find how many email address each person has? It is quite difficult