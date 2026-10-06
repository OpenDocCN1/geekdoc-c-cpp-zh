# Chapter 10: Documenting an Existing Database 253

![](bbox=[0.118, 0.126, 0.882, 0.298])

Figure 10-14. Engineer To Logical Model

and get the ALTER DDLs for adding columns to the database, and no logical
model is needed. If you are making larger changes or changes that will use
transformation scripts to add columns to new tables or other changes like that,
have a logical model is definitely worth it.

If you decide to create the logical model and start maintaining the database
objects with Data Modeler, the logical diagram might not look exactly the way you
want it to after the reverse engineering. If you want to change the layout,
it can move the elements in the diagram to the places you want or use the
functionalities Data Modeler offers for automatically making the layout better. Specifically, right-click the canvas and choose Layout. You might also want
to create subviews or layouts, as explained in Chapters 3 and 4.

The relationship names are after engineering the foreign key names in the database.
Depending on how the database was designed and created, those names might be
completely technical, making no sense to the human eye. In those cases, it might
be worth renaming the relationships to something more meaningful.

# # Importing Documentationnfrom a Third-Party Modeling Tool

You might have databases that already have documentation and you would like to
get that documentation into Data Modeler so you don't have to start from scratch.
You, of course, insert the design into Data Modeler manually, but there are
other possibilities too. You might have the documentation in a VAR file that has been
created from Sterling COOL (DBA v2.1 or Sterling Bsnteam v7.2), Cayenne Bsnteam Bsnteam
v7.2, Rational Rose, Together, JDeveloper, MEGA, or PowerDesigner v12. Or you
might have it in ERWin 4.1 or 7.3 or in Oracle Designer. Or you might have your
data warehouse documentation in Cube Views metadata or Microsoft XMLA. There
isupport for many other modeling tools in Data Modeler. The tools include Oracle

*1*