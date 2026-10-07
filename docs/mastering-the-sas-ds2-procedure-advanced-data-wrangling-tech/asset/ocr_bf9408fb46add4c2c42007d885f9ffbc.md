# # Chapter 2: Introduction to the DS2 Language

+   2.1 Introduction ................................................................................................................ 7

+   2.2 DS2 Programming Basics ................................................................................................ 7
2.2.1 General Considerations ................................................................................................. 7
2.2.2 Program Structure ................................................................................................. 9
2.2.3 Program Blocks ............................................................................................................ 11
2.2.4 Methods ............................................................................................................................ 12
2.2.5 System Methods ............................................................................................................ 12
2.2.6 User-Defined Identifiers and Scope ....................................................................... 16
2.2.8 Data Program Execution............................................................................................... 21

+   2.3 Converting a SAS DATA Step to a DS2 Data Program ................................................ 21
2.3.1 A Traditional SAS DATA Step ................................................................................ 21
2.3.2 Considerations ....................................................................................................... 22
2.3.3 The Equivalent DS2 Data Program............................................................................... 22

+   2.4 Review of Key Concepts ................................................................................................ 23

# ## 2.1 Introduction

In this chapter, we will describe the basic components and construction of DS2 programs. Along the way, we'll note similarities and differences between DS2 data programs and traditional Base SAS DATA steps. We'll also convert an existing DATA step to a DS2 data program and execute our first DS2 program using PROC DS2.

# ## 2.2 DS2 Programming Basics

# ### 2.2.1 General Considerations

I like to describe DS2 as a next-generation language that combines the flexibility, control, and power of DATA step programming, the rich ANSI SQL data palette, and the benefits of object-based code modularity. At first glance, the DS2 language is comfortably similar to the DATA