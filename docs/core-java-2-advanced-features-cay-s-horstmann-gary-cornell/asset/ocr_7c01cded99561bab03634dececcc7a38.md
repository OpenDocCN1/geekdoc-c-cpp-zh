# # CHAPTER 6

# # The Date and Time API

# ### In this chapter

+   - 6.1 The Time Line, page 352
+   - 6.2 Local Dates, page 355
+   - 6.3 Date Adjusters, page 358
+   - 6.4 Local Time, page 360
+   - 6.5 Zoned Time, page 361
+   - 6.6 Formatting and Parsing, page 365
+   - 6.7 Interoperating with Legacy Code, page 369

Time flies like an arrow, and we can easily set a starting point and count forward and backward in seconds. So why is it so hard to deal with time? The problem is humans. All would be easy if we could just tell each other: “Meet me at 1523793600, and don’t be late!” But we want time to relate to daylight and the seasons. That’s where things get complicated. Java 1.0 had a Date class that, in hindsight, naïve, and had most of its methods deprecated in Java 1.1 when a Calendar class was introduced. Its API wasn’t stellar, its instances were mutable, and it didn’t deal with issues such as leap seconds. The third time is a charm, and the java.time API introduced in Java SE 8 has remedied the flaws of the past and should serve us for quite some time. In this chapter, you will learn what makes time computations so vexing, and how the Date and Time API solves these issues.