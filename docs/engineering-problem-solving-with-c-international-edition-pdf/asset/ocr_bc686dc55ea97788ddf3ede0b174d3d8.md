```
/*--------------------------------------------------------------*/
/* Class declaration for Rectangle.                             */
/*                                                              */
/* filename: rectangle.h                                        */
/*--------------------------------------------------------------*/
/*--------------------------------------------------------------*/
#include "Point.h"   //Required for Point
class Rectangle
{
   private:
   // Declaration of data members;
   double width, height;
   Point origin;

   public:
   // Public interface
   // Default constructor
   Rectangle();
   // Parameterized constructor
   Rectangle(double w, double p, double x, double y);
   // Accessor methods.
   double getWidth() const;
   double getHeight() const;
   Point getOrigin() const;

   //Mutator methods.
   void setWidth(double w);
   void setHeight(double h);
   void setOrigin(Point p);

   //Additional operations
   void move(double dx, double dy);
   double area() const;
   void print(ostream&) const;
};
/*--------------------------------------------------------------*/
```

```
/*--------------------------------------------------------------*/
/* Class Implementation for Rectangle.                          */
/*                                                              */
/* filename: Rectangle.cpp                                      */
/*--------------------------------------------------------------*/
/*--------------------------------------------------------------*/
#include "Rectangle.h"   //Required for Rectangle
Rectangle::Rectangle():origin(0,0)
{
   cout << "Constructing Rectangle() ..." << this << endl;
   width=height=1;
}
Rectangle::Rectangle(double w, double h,
                     double x, double y):origin(x,y)
{
   cout << "Constructing Rectangle(parameter list)..."
        << this << endl;
```