
These 3 products are very great and adapted to specific requirements but in this part, we will detail the use of Serilog for simplicity purpose but feel free to explore Log4NET and Nlog solutions if you have a special interest for your application to use it.

### 5.2.1 Microsoft .NET Core logging system

Microsoft provides now packages for logging, tracing and debugging features of your application. This wrapper offers you basic functionality for the logging and trace needs of your application.

![](img/3d310cc066dda6e2dfa67a650614076f_65_0.png)

Here is simple program for logging the activities of your application using these Microsoft packages.

### SampleMsLog.cs

```
public static void Main(string[] args = null)
{
    ILoggerFactory LoggerFactory = new
    LoggerFactory().AddConsole[...];
    ILogger logger =
    LoggerFactory.CreateLogger<Program>();
    logger.LogInformation("This is a test of logging information system.");
}
```

First of all you have to begin by creating a log factory instance, next you have to specify the provider you want to use for effectively doing your logging (in the sample: “AddConsole”).

This is simple solution for creating a basic logging system but if your development has special requirements for logging, trace and debug you should go further and explore the possibility to use a more advanced system for doing so: Serilog.

### 5.2.2 Advanced structured logging system: Serilog

Serilog is a structured logging system, currently implemented with .NET standard 2.0 so you can use it within a .NET Core 3 project. Serilog is a Library providing diagnostic logging to files. It is easy to setup, and unlike other logging libraries, it is built with powerful structured event data in mind so is very well adapted to desktop application development.

With this logging system you can implement a console debugging window for following each event of your application you have decided to follow and having a real time view of the internals of your application in real time.

#### 5.2.2.1 Install Serilog

You have to add the NuGet package “Serilog” with the package manager GUI in Visual Studio or with the package manager command line. After that you will have to install the package(s) specific to the type of output you want to use (it is called “Sinks”).

A “Sink” describes the type of logging you want to implement for you project.

There are many other types of Sinks already available beside file and console you can write the loggings of your application in database, in the cloud or in the Microsoft Teams system ...

#### 5.2.2.2 Configuration

The configuration of Serilog is straightforward and in most case does not require a specific configuration file. Nevertheless, you have the possibility to use one config file for responding to specific requirements of your logging system (check the reference website for more information)

If you have special needs in that matter you can also refer back to the GitHub (Serilog is open source) repository.

#### 5.2.2.3 Create a Logger and use Sinks

First of all, you have to create a logger object:

```
Log.Logger = new LoggerConfiguration().CreateLogger();
```

Once the Logger object is created it has to be linked to a specified external representation (for example a file or a console window)

For a console logging system.

```
Log.Logger.WriteTo.Console();
```

Or for using a text file for output:

```
Log.Logger.WriteTo.File("log.txt",
outputTemplate: "{Timestamp:yyyyMMdd
HH:mm:ss } {Message:lj}");
```

You can find more information about the formatting of the logging at the provided reference websites (links provided below).

#### 5.2.2.4 Logging Levels

Once the logger is fully configured you can start to log to the level Information:

```
Log.Information("Here is the logging!");
```

There are several levels to use to do your logging:

- Verbose
- Debug
- Information
- Warning
- Error
- Fatal

You can configure your logger to output only at a defined level.

Here is a simple sample program for illustrating the basic use of Serilog.

### ProgramSampleSerilog.cs

```
static void Main(string[] args)
{
    Console.WriteLine("Hello Serilog!");
    var loggerConfiguration = new
        LoggerConfiguration()
        .WriteTo.ColoredConsole()
        .Enrich.WithMachineName()
        .MinimumLevel.Debug();
    var logger =
        loggerConfiguration.CreateLogger();
    Log.Logger = logger;
    Log.Information("Starting up.");
    var sleepPeriodInSeconds = 60;
    if (args.Length > 0 &&
        int.TryParse(args[0], out sleepPeriodInSeconds))
    {
        Log.Information("Sleep interval provided {SleepPeriodInSeconds}", sleepPeriodInSeconds);
    }
    var sleepPeriod =
        TimeSpan.FromSeconds(sleepPeriodInSeconds);
    while (true)
    {
        var coinToss = Random.Next(0, 2);
        Log.Information("Coin Toss... {CoinToss}", coinToss);
        var instance = coinToss == 0 ? new WithPropertyInit() : null;
        Log.Information("Doing Work... {NameOfProp}", instance?.NameOfProp());
        Log.Information("{Instance}", instance);
        Thread.Sleep(sleepPeriod);
    }
}
```

As we can see Serilog can be very easy to use, and offer a large amount of customization capabilities. This is a particularly relevant choice in many application development scenarios. This is an open source project with vibrant community working on it and the documentation is abundant.

You can look deeper into the use of Serilog:

- http://www.serilog.net
- https://www.github.com/serilog

## 5.3 DATA ACCESS: ENTITY FRAMEWORK CORE

With .NET Core 3, the developer can still use classical ways (as done with .NET Framework) to access the database (Command, Request Reader...) but for modern advanced software solution the data access have to be layered in a standardized way (with ORM).

The data access in .NET Core should be done (that's not mandatory, but it's highly recommended) by using the Entity Framework Core component (a NuGet package). This is the ORM (Object Relational Mapper) developed by Microsoft inherited from the dotnet framework (Entity Framework).

The Entity Framework Core has followed the trend set, as .NET Framework, to a lighter multiplatform environment.

EF Core includes a set of APIs allowing you to use a structured (with a good readability of the code and good maintainability) way to access your data. It allows you to work with data with .NET object instances (with LINQ request support).

EF Core simplifies your work for making the Data Access Layer of your application. Actually, EF Core can generate that layer for you.

### 5.3.1 Database Provider

As its predecessor, Entity Framework 6, EF Core already integrates many database providers as:

- SQL server
- MySQL
- SQLite
- Oracle
- PostgreSQL
- CosmosDB (NoSQL database from Microsoft)
- ... and many more providers continue to be added as the EF Core community is a most vibrant one.

More providers can be found here:

![](img/3d310cc066dda6e2dfa67a650614076f_71_0.png)

### 5.3.2 Architecture of the EF Core

The EF Core provides to the developer an integrated layered solution that provides the possibility to abstract the database operations of the application, to use .NET objects.

This layering provides a better flexibility regarding the database hosting system (for example if you have to change the type of database you use).

It provides also the ability for the developer to use advanced .NET features for manipulating data objects like: the use of Lambda function, the use of LINQ request.

The following schema illustrate the general architecture of EF Core:

![](img/3d310cc066dda6e2dfa67a650614076f_72_0.png)

### 5.3.3 EF Core Installation

For getting EF Core available in your project you have to include a specific package regarding the type of database you want to use and the EF tools allowing to use the advanced features in your code.

Here are the packages to include if you use SQL server:
