Not to put too fine a point on it, but you shouldn't have to go through that process at all. Visual Studio does a lot of the data management for you if you let it, and I recommend that you do.

# Using the System.Data Namespace

The System.Data namespace is another namespace that gets mixed up between the code world and the visual tools world. Though it is more of a relationship between the form controls and the Data namespace, it often seems like the data lives right inside the controls, especially when you're dealing with Windows Forms.

In the following sections, you deal primarily with the visual tools, which are as much a part of the C# experience as the code. First, I go over connecting to data sources, and then I show you how to write a quick application using one of those connections. Finally, I go over a little of the code side.

To make all this work, you need to have some kind of schema set up in your database. It can be a local project of your own creation or a sample schema. The next section tells you how.

# Setting up a sample database schema

To get started, direct your browser to http://msftdbprodsamples.codeplex.com/releases/view/55330. If this URL doesn't work, search the web for SQL Server 2012 samples and find the nearest CodePlex link. It should get you there.

This page offers a whole bunch of sample listings — sample applications and sample schemas, as well as reporting databases and OLTP bits and a bunch of other stuff. The sample applications are full-blown applications that show complete end-to-end implementation of data-driven software built using .NET. Some are in C#, some are in Visual Basic. The sample schemas are databases only and are designed for database administrators to practice getting experience in handling the system.

Any of the sample schemas will work. If you want exactly the same one as I use in the examples here, choose the AdventureWorks2012 Data File. Other options may be a better fit for the work you're doing.

To install, download the MDF file and put it somewhere that makes sense to you. You'll eventually reference it in your project, so a local location like C:\Databases might be good.