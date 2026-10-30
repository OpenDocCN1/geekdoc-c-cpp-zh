# Access File Formats

Since Access 2007, the default file format for Access database files has been ACCDB instead of MDB. It's worth a moment of your time to understand why this changed and how it affects how Access 2019 works with older Access database files.

Since its inception, Access has used a database engine named Jet (an acronym for Joint Engine Technology). With Access 2007, the Access development team wanted to add significant new features to Access, such as multivalue and attachment fields. Because the new features were so significant, they couldn't retrofit Jet with the code necessary to support the new features. As a result, Microsoft developed an entirely new database engine, the Access Connectivity Engine (ACE).

Access 2019 supports several file formats, including the following:

+   - Access 2007–2019 ACCDB
+   - Access 2002–2003 MDB
+   - Access 2000 MDB

If you are unfortunate enough to work in an environment where Access 2003 is still being used, you will need to stick with the Access 2002–2003 MDB format for compatibility purposes. In that same light, if you are using older databases that use database replication or user-level security, you will need to stick with the MDB formats. Access ACCDB files do not support replication or user-level security.

In Access 2019, you can open older Access 2002–2003 and Access 2000 MDB files and make any desired changes to them, but you'll only be able to use features specific to those versions. Some of the new Access features won't be available, particularly those features that rely on the ACE database engine.

You can convert a database saved in a previous format by opening the database in Access 2019, choosing File ▸ Save As, and then, in the Save As dialog box, choosing any one of the different Access formats.

# The Access 2019 Interface

After you create or open a new database, the Access screen will look similar to Figure 2.4. Across the top of the screen is the Access Ribbon. On the left, you see the Navigation pane. These two components make up the bulk of the Access interface. In addition, you have at your disposal the Quick Access toolbar, which you can customize with the commands you use most frequently.

# The Navigation pane

The Navigation pane, at the left of the screen, is your primary navigation aid when working with Access. The Navigation pane shows tables, queries, forms, reports, and other Access object types. It can also display a combination of different types of objects.