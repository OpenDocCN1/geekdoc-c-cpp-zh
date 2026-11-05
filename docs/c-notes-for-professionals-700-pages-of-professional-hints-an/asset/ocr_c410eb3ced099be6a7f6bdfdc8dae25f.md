# Chapter 129: Using SQLite in C#

# Section 129.1: Creating simple CRUD using SQLite in C#

First of all we need to add SQLite support to our application. There are two ways of doing that

+   - Download DLL suiting your system from SQLite download page and then add to the project manually
+   - Add SQLite dependency via NuGet

We'll do it the second way

First open the NuGet menu

![](bbox=[0.04, 0.26, 0.58, 0.57])

and search for System.Data.SQLite, select it and hit Install

![](bbox=[0.04, 0.62, 0.97, 0.8])

Installation can also be done from Package Manager Console with

```
```
PM> Install-Package System.Data.SQLite
```
```

Or for only core features

```
```
PM> Install-Package System.Data.SQLite.Core
```
```