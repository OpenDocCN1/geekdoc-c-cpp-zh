# CHAPTER 10 Introduction to Inheritance

special handling, which is $10 for orders for $40 and $8 for higher-priced orders.
Create an application named CookieDemo2 that demonstrates several SpecialCookieOrder objects.

+   5. a. Create an application named AutomobileDemo that prompts a user for data for eight Automobile objects. The Automobile class includes auto-implemented properties for ID number, make, year, and price. Override the ToString() method to return all the details for an Automobile. During data entry, reprom the user if any ID number is a duplicate. Sort the objects in ID number order, and display all their data as a total of all their prices.
b. Using the Automobile class as a base, derive a FinancedAutomobile class that contains all the data of an Automobile, plus fields to hold the amount financed and interest rate. Override the parent class ToString() method to include the child's additional data. Create a program named AutomobileDemo2 that contains an array of four Automobile objects. Prompt the user for all the necessary data, and do not duplicate ID numbers and do not allow the financed to be greater than the price of the automobile. Sort all the records in ID number order and display them with a total price for all Automobiles a total financed.
c. Write an application named AutomobileDemo3 that uses an extension method for the FinancedAutomobile class. The method computes and returns the FinancedAutomobile's monthly payment (1/24 of the amount financed). The application should allow the user to enter data for four objects and then display all the data for each.

+   6. Create an application named ShapesDemo that creates several objects that descend from an abstract class GeometricFigure. Each GeometricFigure includes a height, width, and an area. Provide get and set accessors for each field except; the area is computed and read-only. Include an abstract method called ComputeArea() that computes the area of the GeometricFigure. Create three classes:
 A Rectangle is a GeometricFigure whose area is determined by multiplying width by height.
 A Square is a Rectangle in which the width and height are the same. Provide a constructor that accepts both height and width, forcing them to be equal if they are not. Provide a second constructor that accepts just one dimension and uses it for both height and width. The Square class uses the Rectangle's ComputeArea() method.
 A Triangle is a GeometricFigure whose area is determined by multiplying the width by height.

In the ShapesDemo class, after each object is created, pass it to a method that accepts a GeometricFigure argument in which the data is displayed. Change some dimensions of some of the figures, and pass each to the display method again.