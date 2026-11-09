# Chapter 10

# Managing Server-Side Data

In the previous chapters, we examined the pieces of a basic GWT application in App Engine. We built a GUI, set up a simple RPC, and strung all of the plumbing together to get an application working. In this chapter, we’re going to implement our chat program using GWT. We won’t spend much time looking at how to build the GUI—there are entire books on building GUIs in GWT, and GWT’s own documentation of its UI classes is excellent. What we’ll spend most of our time on is *datastore*, the mechanism that lets us work with persistent data in App Engine. Just like in Python, we need to do some extra work to make classes persistent and queryable. Now we’ll look at how to do that using Java.

We’ll also touch on some other issues of the server-side plumbing in the Java side of App Engine. Specifically, App Engine puts some restrictions on what code can do and how it can run in the App Engine cloud environment, and we’ll examine what those restrictions are and what effect they have on how we write the server side of our App Engine applications.

# 10.1  Data Persistence in Java

If you look back at Chapter 4, *Managing Data in the Cloud*, on page 53, you’ll remember that we needed to do some extra work in our Python code to store data and to make things work correctly in the cloud. The same thing is true in Java. Unfortunately, this is one of the places where the static typing of Java makes things a bit more cumbersome. The basic back-end datastore used by App Engine is exactly the same as in Python, but making it work with Java takes a bit more thought.