```
188     ); // end call to addWindowListener
189 } // end DisplayQueryResults constructor
190 
191     // execute application
192     public static void main( String args[] )
193     {
194         new DisplayQueryResults();
195     } // end main
196 } // end class DisplayQueryResults
```

a) Displaying all authors from the Authors table

![](bbox=[0.38, 0.265, 0.87, 0.445])

b) Displaying the the authors' first and last names joined with the titles and edition numbers of the books they've authored

![](bbox=[0.38, 0.46, 0.87, 0.64])

c) Filtering the results of the previous query to show only the books with Java in the title

![](bbox=[0.38, 0.655, 0.87, 0.835])

# Fig. 28.28 | Displays contents of the database books. (Part 5 of 5.)

Lines 27–29 and 32 declare the URL, username, password and default query that are passed to the ResultSetTableModel constructor to make the initial connection to the