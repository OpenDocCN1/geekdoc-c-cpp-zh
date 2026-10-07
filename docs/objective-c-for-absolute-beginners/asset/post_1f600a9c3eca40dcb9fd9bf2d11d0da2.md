
To seed the random function, tap Seed Random Number Generator. To generate the random number, tap Generate Random Number Generator.

# Summary

Great job! Interface Builder saves you lot of time when creating User Interfaces. You have a powerful set of objects to use in your application and are responsible for a minimal amount of coding. Interface Builder handles many of the details you would normally have to deal with.

You should be familiar with the following terms:

- XIB files
- Model-View-Controller (MVC)
- Architectural pattern
- Human interface guidelines (HIGs)
- Outlets
- Actions

# Exercises

- Extend the random number generator app to show a date and time in a Label when the app starts.
- Adjust the Date and Time message for “Generator Seeded” to fit nicely in the label.
- After showing a date and time label, add a button to update the data and time label with the new time.

# Chapter 11

# Storing Information

As a developer, there will be many different situations in which you will need to store data. Users will expect your application (app) to remember preferences and other information each time they launch it. In previous chapters, we discussed the Book Store app. With this app, users expect your application to remember all of the books in the bookstore and have it default to a database location. Your application will need a way to store this information, retrieve it, and possibly sort this data. Working with data can sometimes be difficult. Fortunately, Apple has provided methods and frameworks to make this process easy.

In this chapter, we discuss two different formats in which data will need to be stored. We will start by discussing saving preferences for the Mac and the iPhone, and then move on using a SQLite database in our application that stores and retrieves data.

# Storage Considerations

There are some major storage differences between the Mac and the iPhone, and these differences will affect how you work with data. Let's start by first discussing the Mac and how you will need to develop for it.

On the Mac, by default, applications are stored in the Applications folder. Each user has their own folder where preferences and information related to that user are stored. Not all of the users will have access to write to the Applications folder or to the application bundle itself.

On iPhone and iPad, developers do not need to deal with different users. Every person who uses the iPhone has the same permissions and the same folders. There are some other factors to consider with the iPhone, though. Every application on the iPhone is in its own "sand box." This means that files written by an application can only be seen and used by that individual application. This makes for a more secure environment for the iPhone, but it also presents changes in the way we work with data storage.

# Preferences

There are things to consider when deciding where to store certain kinds of information. The easiest way to store information is within the preferences file, but this method has some downsides.

- All of the data is both read and written at the same time. If you are going to be writing or writing large amounts of data, this could take time and slow down your application. As a general rule, your preference file should never be larger than 100K. If your preference file starts to become larger than 100k, consider using Core Data as a way to store your information.
- The preference file does not provide many options when it comes to searching and ordering information.

The preference file is really nothing more than a standardized file with accompanying classes and methods to store application information. A preference would be, for example, the sorting column and direction (ascending/descending) of a list. Anything that is generally customizable with any app should be in a preference file.

# Writing Preferences

Apple has provided developers with the NSDefaults class; this class makes it very easy to read and write preferences for the iPhone and Mac OS X. The great thing is, in this case, you can use the same code for the iPhone and Mac OS X. The only difference between the two implementations is the location of the preference file.

> NOTE: For Mac OS X, the preference file is named com.yourcompany.applicationname.plist and is located in the /Users/username/Library/Preferences folder. On the iPhone, the preference file is located in application bundle in the Library/Preferences folder.

All you need to do write preferences is to create an NSDefaults object. This is done with the following line:
`UserDefaults *prefs = [NSUserDefaults standardUserDefaults];`
This instantiates the object's prefs and you now use it to set preference values. Next, you need to set the preference keys for the values that you would like to save. The previous Book Store app example will be used to demonstrate specific instructions throughout the rest of this chapter. As a bookstore, might want to save a username or password in the preferences. You also might want to save things as a default book category or recent searches. The preference file is a great place to store this type of information because this is the kind of information that only needs to be read when the application is launched.

Also, on the iPhone, it is often necessary to save your current state. If a person is using your application and then gets a phone call, you want to be able to bring them back to the exact place they were when they are done phone call. This is less necessary now with IOS 4 and 5 and the implementation of multitasking, but your users will still appreciate it if your application remembers what they were doing the next time it is launched

Once you have instantiated the object, you can just call setObjectForKey an object. If we wanted to save the username of sherlock.holmes, we would just call the following line of code:

```
[prefs setObject:@"sherlock.holmes forKey:@"username"]
```

You can use setInteger, setDouble, setBool, setFloat, and setObject, depending on the type of information you are storing in the preference file. Let's say you the number of books a user wants to see in the list. Here is an example of using setInteger to store your preference:

```
[prefs setInteger:10 forKey:@"booksInList"]
```

After a certain period of time your app will automatically write the preference file. You can force your app to save the preferences by calling the synchronize function but this is not necessary in most cases. To call the synchronize function you would write the following line:

```
[synchronize]
```

With just three lines of code, we are able to create a preference object, set two preference values, and write the preference file. It is a very easy and clean process. Here is all of the code:

```
NSDefaults *prefs = [NSUserDefaults standardUserDefaults];
[prefs setObject:@"sherlock.holmes forKey:@"username"];
[prefs setInteger:10 forKey:@"booksInList"]
```

# Reading Preferences

Reading preferences is similar to writing preferences, and is just as easy. Just like writing, the first step is to obtain the NSUserDefaults object. This is done exactly the same way as it was done in the writing process:

`NSDefaults *prefs = [NSUserDefaults standardUserDefaults];`

Now that we have the object, we are able to access the preference values that are set. For writing, we use the setObject syntax; for reading, we use the stringForKey function. In the writing example, we set preferences for the username and for the number of books in the list to display. We can read these out using the following simple lines of code:

```
NSString *username = [prefs stringForKey:@"username"];
NSInteger booksInList = [prefs integerForKey:@"booksInList"]
```

Pay close attention to what is done in each of these lines. We start out by declaring the variable username, which is an NSString. This variable will be used to store the preference value of the username stored in the preferences. Then, we assign it to the value of the preference username. You will notice in the read example we do not use the synchronize function. This is because we have not changed the values of the preferences; therefore, we do not need to make sure it is written to a disk.

# Databases

We have discussed how to store some pieces of information and retrieve them at a later point. If you have more information that needs to be stored? What if you need to conduct a search within this information or put it in some sort of order? These kinds of situations call for a database.

Let's start by discussing what a database is. A database is a tool for storing a significant amount of information in a way that it can be searched or retrieved. When using a database, usually small chunks of the data are retrieved at a time rather than the entire file. Many applications use in your daily life are based on databases of some sort. Your supermarket uses a database to retrieve prices for different items. A simple example of a database is a spreadsheet. You may have many columns and many rows in your spreadsheet. To store in a database, these are considered attributes. The rows in your spreadsheet would be considered different records.

# Storing Information in a Database

Databases are usually an intimidating subset for a developer: most developers associate databases with enterprise database servers such as Microsoft SQL Server or Oracle. These applications take time to set up and require constant management. For most developers, a database system like Oracle would be too much to handle.

Luckily, Apple has included a small compact database engine SQLite in the Mac, iPhone, and iPad. This allows you to gain many of the features of the complex databases without the overhead.

SQLite will provide you with a lot of flexibility in storing information for your application. It stores the entire database in a single file. It is fast, reliable, and easy to implement in your application. The best thing about the SQLite database is that there is no need to perform any installation of software; Apple has taken care of that for you.

However, SQLite does some limitations that, as a developer, you should be aware of:

- SQLite was designed to be used as a single user database. You will not want to use SQLite in an environment where more than one person will be accessing the same database. This could lead to data loss or corruption.
