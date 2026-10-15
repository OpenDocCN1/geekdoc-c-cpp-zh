Visual Studio 2010 provides an editor for working with resource files. You have already seen some of the views available from the Resource Editor. Resources are categorized visually according to the data type of the resource. This chapter has covered only the handling of strings, but other categories exist (such as images, icons, audio files, miscellaneous files, and other items). These options are shown in Figure 27-24.

![](bbox=[0.14, 0.17, 0.8, 0.57])

FIGURE 27-24

# SUMMARY

This chapter has looked at some of the localization tools available to you. It started with a review of the Culture types and how to determine the preferred culture for either a thread or Web request. It looked at understanding how different cultures may treat the same date or number differently for display or just as importantly how .NET can automate this handling for you. It also examined differences with currency with a warning about the need to convert a value and not just swap the display formatting when dealing with currency. The chapter then looked at how .NET supports both Windows Forms and ASP.NET use of multiple resource files to provide support for different languages and cultures.

While .NET has provided many tools to help you with this process, you should keep in mind that these tools only make the process easier when looking; when you want to localize an application, you need to plan to work with someone familiar with the language, and ideally the culture, you will target.

In addition to making many of the changes described in this chapter, localization is a process that requires consideration of multiple different time zones, consideration for information that reads Left to Right vs cultures which expect information to flow Right to Left, and other issues that are outside the scope of the tools you use. While that seems like a lot, you'll note that the same concepts for using resource files exist between Windows Forms and ASP.NET.