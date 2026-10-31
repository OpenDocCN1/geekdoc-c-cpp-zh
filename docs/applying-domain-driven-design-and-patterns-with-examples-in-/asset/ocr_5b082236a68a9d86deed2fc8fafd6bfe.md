+   - **What backends are supported?**
+   
+   This is a typical example of something that could become a long and tedious feature enumeration, so I won't go into detail here. Let's just say that NHibernate supports several different databases (most of the major commercial and open source databases). Check the site [NHibernate] for current information. You can also write your own plugin if you miss the database you need to work with.

+   - **Not just an O/R Mapper**
+   
+   NHibernate is pretty focused on being an O/R Mapper and nothing else. The philosophy is to do one thing and do it well.

# Note

Of course, NHibernate does other things as well, but those other things are just not the focus. And they are not too many or too big either.

+   - **Advanced caching**
+   
+   Advanced caching is one area where NHibernate isn't really up to par when compared to Hibernate, but I think it's rapidly becoming better. On the other hand, to me that's not usually a big deal. There are many problems with second-level caching, so that option is often ruled out.

+   - **Advanced support for controlling transactions**
+   
+   Support for manual transaction control is pretty good in NHibernate. There are situations where you might be taken by surprise if you don't watch out (for instance, when you execute a query in the middle of a transaction, NHibernate will then `flush()` changes to the database before executing the query). That's a tradeoff between querying not going "through" the cache or ordinary transaction control. The good news is that it's controllable by your code.
+   
+   To bind this to Chapter 8, the typical way of dealing with transactions in NHibernate is "manual control."

# Note

On top of that, you can also build something that uses any of the more automatic approaches mentioned in Chapter 8.