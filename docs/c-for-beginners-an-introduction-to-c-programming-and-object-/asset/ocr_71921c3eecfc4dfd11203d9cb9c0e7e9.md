# 9. Functions

```
```cpp
}

int main ()
{
    //Declare variables to store user inputs
    //And to store calculated areas
    int radius, base, length, width, area_rectangle;
    float height, area_circle, area_triangle;
    //Ask the user to enter the radius of a circle
    cout << endl << endl
         << "Enter the radius of a circle: ";
    //Wait for the user to enter
    cin >> radius;
    //Call area function to calculate area of a circle
    area_circle = area (radius);
    cout << endl
         << "Area of the Circle with Radius: " <<
            radius
         << " is: " << area_circle;

    //Ask the user to enter the base and height of a triangle
    cout << endl << endl
         << "Enter the base and height of a triangle:
         ";
    //Wait for the user to enter
    cin >> base >> height ;
    //Call area function to calculate area of a triangle
    area_triangle = area (base, height);
    cout << endl
         << "Area of the Triangle with base: " << base
         << " height: " << height
         << " is: " << area_triangle;

    //Ask the user to enter the length and width of a rectangle
    cout << endl << endl
         << "Enter the length and width of a rectangle
         ";
    //Wait for the user to enter
    cin >> length >> width ;
    //Call area function to calculate area of a rectangle
    area_rectangle = area (length, width);
    cout << endl;
```
```