For example, searching in our description property of the `Recipe` entity can potentially be very expensive if the user has verbose descriptions and/or uses Unicode characters in the description.

To improve performance of searches in this field, we could create a second property on the `Recipe` entity that strips the Unicode characters from the description and also removes common words such as *a*, *the*, and *etc*. If we then perform the search on this derived property, we can drastically improve search performance.

The downside to using search-only properties is that we need to maintain them. Every time the description field is edited, we need to update the derived property as well.

# ### Expensive Calculations

In a normalized database, calculated values are not stored. It is considered cheaper to recalculate the value as needed than to store it in the database. However, from a user experience point of view, the opposite can frequently be true. In cases where the calculation takes a human-noticeable amount of time, it may very well be better for the user to store that calculation in the entity and recalculate it only when one of its dependent values has changed. For example, if we store the first and last names of a user in our Core Data repository, then it might make sense to store the full name as well.

# ### Intelligent Relationships

Relationships in a Core Data Model are like salt in a cooking recipe. Too much and you ruin the recipe; too little and something is missing. Fortunately, there are some simple rules we can follow when it comes to relationships in a Core Data repository.

# ### Follow the Object Model

Core Data is first and foremost an object model. The entities in our model should represent the data as accurately as possible. Just because a value might be duplicated across several objects (or rows from the database point of view) does not mean it should be extruded into its own table. Many times it is more efficient for us to store that string several times over in the entity itself than to traverse a relationship to get it.