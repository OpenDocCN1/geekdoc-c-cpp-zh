# UNDERSTANDING
PRODUCTIVITY APPS

The original iPhone Human Interface Guidelines (HIG) organized applications into three general categories: utility, productivity, and immersive applications. Utility applications provide a single view of the data with little or no interaction. Productivity applications manage and organize complex data. Immersive applications use custom views and controls, taking over the entire screen to provide a rich, interactive user experience.

Apple has since dropped these categories from the iOS HIG, and that makes a certain amount of sense. As the platform continues to mature, developers naturally push against these boundaries. Few modern applications fit cleanly into one of these categories. Even back when the iPhone first came out, many applications used a hybrid approach. Look at the iPod app. Its Cover Flow interface injects an immersive element into an otherwise straightforward productivity app.

However, there seems to be some benefit to at least thinking about these categories, especially when you are designing a new application. They can help you identify your application's core features and then focus your design to maximize those features.

We looked at a simple utility application in Chapter 1. Honestly, there's not a lot to say about them. Utility apps provide a quick way to access relatively simple information. One screen, a few settings—if you're thinking of anything more complicated than that, you should probably consider a different approach.

Over the next few chapters, we will look at productivity applications. These apps manage and organize complex data. While you may provide some custom user interfaces, you should focus heavily on usability. Work to create a clean, streamlined solution that helps the user to move through the data in an unobtrusive and intuitive manner.

Productivity applications typically use three tools to organize and interact with your data: UITabBarController, UINavigationController, and UITableView. You may not need all three, but these are the primary built-in tools for sifting through data.

The UITabBarController lets the user easily switch between different tasks or different groups of data. For example, the Clock application lets the user choose between the different time-related tasks: World Clock, Alarm, Stopwatch, and Timer. The iPod app, on the other hand, allows the user to select different views of their data: Albums, Artists, Genres, Songs, Playlists, Videos, and so on. The App Store mixes both approaches, displaying three data groups (Features, Categories, and Top 25) and two tasks (Search and Updates).