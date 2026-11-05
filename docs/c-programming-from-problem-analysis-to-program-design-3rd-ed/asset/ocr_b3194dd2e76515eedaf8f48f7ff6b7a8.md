![](bbox=[0.176, 0.095, 0.859, 0.419])

Figure 7-10　PlayerApp memory representation

As you review the figure, note the difference between value types such as avg and gameCnt. Array objects and string types contain a reference to the location of the stored values. Many advanced concepts relating to arrays were illustrated in the PlayerApp application. Array were defined as private data members and local variables. You saw how you could instantiate arrays of user-defined class array objects. Arrays were returned from methods and sent in as arguments to methods. Many of these same features will be revisited with the Programming Example that follows.

# Programming Example: Manatee Application

This example demonstrates the use of collections in the analysis, design, and implementation of a program. Array and string objects are included. An application is created to monitor manatees, which are still in danger of extinction and are being monitored on a daily basis in some areas. To design this application, a number of string methods are used. Parallel arrays are created to store the location, date, and number present at each sighting. The application is designed using two classes, and the problem specification is shown in Figure 7-11.