In this chapter data set size is often used as a decision point for determining which of these techniques to use. But what exactly is a large data set? This answer too will be situational. It will depend a lot on your OS and your hardware (including available memory and processing capabilities). You will know a data set is large when you have to be careful with the techniques used to process it. For table lookups this chapter will give you alternatives. Each is a compromise between processing efficiency and coding complexity. Each section should give you sufficient information to help you make an informed decision. In all cases you will probably want to test your candidate techniques using your data and your hardware.

# 6.1 and 6.2 IF – THEN/ELSE

This is the slowest and least sophisticated of the techniques discussed in this chapter; however, these techniques may be adequate for small data sets and simple lookups.

# 6.3 Merges and Joins

These techniques tend to be slower than the use of formats (6.5); however, they do allow the retrieval of multiple items.

# 6.4 Double SET Statement DATA Steps

Replacing the MERGE statement with a double SET statement generally provides a performance boost, but the technique is more programming intensive.

# 6.5 Format-Driven Lookup

These techniques tend to be substantially faster than the use of merges and joins. These techniques are probably the best first choice for most situations with small to somewhat large data sets.

# 6.6 Using Indexes

Indexes can improve the performance of merge and join techniques, especially when the indexes have already been created. Depending on the situation these techniques might outperform the use of formats.

# 6.7 Key Indexing (Array Processing)

The use of DATA step arrays and memory eliminates the need for sorting. Although there are potential memory constraints, key indexing typically out performs merges and joins, and for larger data sets out performs the use of formats. When it is possible to use them, array (direct addressing) techniques, such as these, will also generally outperform hash table techniques.

# 6.8 Hash Tables

Hash tables (hashing) is more flexible than array processing techniques, and except for array processing techniques, these techniques are typically the fastest of the lookup techniques. Coding requires an understanding of the DATA step component hash objects and methods. For very large data sets, the use of hash tables may be the only viable choice.

In each of the examples in this chapter we will be using lookup techniques to determine the clinic name based on the clinic number.

# SEE ALSO

An overview of lookup techniques, which includes several nice examples with explanations, can be found in Liu (2008). Aker (2002) and Carpenter (2001b) each discuss differences and programming techniques for lookups including those for match merging, format lookups, and the use of arrays. An overview of lookup techniques with emphasis on hash tables and hash objects can be found in Dorfman and Vyverman (2004b). Comparison papers on the efficiency of table lookup techniques include Stroupe and Jolley (2008) as well as Jolley and Stroupe (2007).