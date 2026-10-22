![](bbox=[0.17, 0.06, 0.85, 0.41])

# Figure 5.2: Flow of seller pages

The shipping option is very simplistic. It displays each order that has not yet been shipped, one order per page. The seller may choose to skip to the next, or may ship the order, using the information from the page as appropriate.

The shipping function is clearly not going to survive long in the real world, but shipping is also one of those areas where reality is often stranger than you might think. Overspecify it up front, and we’re likely to get it wrong. For now let’s leave it as it is, confident that we can change it as the user gains experience using our application.

# Data

Finally, we need to think about the data we’re going to be working with.

Notice that we’re not using words such as schema or classes here. We’re also not talking about databases, tables, keys, and the like. We’re simply talking about data. At this stage in the development, we don’t know whether we’ll even be using a database—sometimes a flat file beats a database table hands down.

Based on the use cases and the flows, it seems likely that we’ll be working with the data shown in Figure 5.3, on the next page. Again, using pencil and paper seems a whole lot easier than some fancy tool, but use whatever works for you.