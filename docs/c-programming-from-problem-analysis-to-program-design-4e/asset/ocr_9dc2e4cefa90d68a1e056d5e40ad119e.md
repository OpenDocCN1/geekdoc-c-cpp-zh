A second class will be created to test the ManateeSighting class. To do this, additional data is needed by the class using the ManateeSighting class. As noted in the problem specification, the application class allows the user to enter values so that the ManateeSighting class can be instantiated. Local variables for location and arrays for date and count are declared in the application class. The two arrays will be dimensioned to a maximum number of 20 entries. The number of actual records will be used to construct the ManateeSighting object. For testing purposes, a single location is entered and sighting data recorded for that location. The user is able to enter additional location data. The application could be modified to create arrays of data about multiple locations.

DESIGN A SOLUTION

The desired output is to display the location, number of sightings during the most active month, and date (including the month name) in which the most manatees were sighted. Figure 7-12 shows a prototype of what the final output might look like.

![](bbox=[0.27, 0.44, 0.68, 0.63])

FIGURE 7-12 Prototype for Manatee Application

Class diagrams are used to help design and document both data and behavior characteristics. Figure 7-13 shows the class diagrams for the manatee application example.