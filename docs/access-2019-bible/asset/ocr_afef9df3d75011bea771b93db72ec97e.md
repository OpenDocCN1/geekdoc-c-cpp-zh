# CHAPTER 26

# Understanding the Access Event Model

# ## IN THIS CHAPTER

+   - Mastering Access event programming
+   - Reviewing common events
+   - Understanding event sequences

When working with a database system, you may perform the same tasks repeatedly. Instead of doing the same steps each time, you can automate the process with VBA macros. Database management systems continually grow as you add records to a form, build new queries, and create new reports. As the system grows, many of the database objects are saved for later use—for a weekly report or monthly update query, for example. You tend to create and perform many tasks repetitively. Every time you add contact records, you open the same form. Likewise, you print the same form letter for contacts that have purchased a vehicle in the past month.

You can add VBA code throughout your application to automate these tasks. The VBA language offers a full array of powerful commands for manipulating records in a table, controls on a form, or just about anything else. This chapter continues the previous chapters’ discussions of working with procedures in forms, reports, and standard modules.

> ### ON THE WEB
> 
> In this chapter, you'll use the database file `Chapter26.accdb`. Download this database file from the book's website if you want to follow along with the examples in this chapter.

This chapter focuses on the Access event model, a vitally important aspect of Access development. As you’ll see in this chapter, Access provides a wide variety of events to trigger your code in response to user actions.