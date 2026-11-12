Finally, you can store the data object directly in the device's file system and save the path in the database. You then manually load the data when necessary. This is recommended for the largest objects.

As a rule of thumb, if your object is measured in kilobytes, it's probably modest; if it's measured in megabytes, it's large. However, this is an area where you definitely want performance testing. Just remember, the end users often use applications in unexpected ways. Don't be surprised when they add 100,000 entities to the persistent store or try to load a 10 MB text file. Try to test these extremes, if possible.

Fortunately, iOS 5 simplifies all this. Binary data attributes now have an Allows External Storage checkbox. Simply select this when configuring the attribute. The system will heuristically decide whether to store your binary data directly in the database or to simply store a URL and load the file as needed. All of this is transparently handled behind the scenes. There is, however, one small restriction: Once external storage is enabled, we cannot use the binary data in our fetch request's predicate.

# TOOLS

Performance testing is covered in more detail in Bonus Chapter B, which can be found at the book's website: http://www.freelancemadscience.com/book. However, it's worth noting that Instruments has a number of tools to help troubleshoot Core Data performance issues. These include instruments to track Core Data fetches, saves, faults, and cache misses. You will want to use these in conjunction with the regular allocations, leaks, and time profile when testing your application.

As always, you should focus on getting the application working properly first and then try to optimize the code based on actual performance data. Premature optimization often wastes your time without producing any tangible results.