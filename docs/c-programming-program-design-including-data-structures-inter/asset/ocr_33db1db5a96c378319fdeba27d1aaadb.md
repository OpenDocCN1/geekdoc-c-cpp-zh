```
```cpp
using namespace std;                                                       //Line 5

int main()
{                                                                          //Line 7
    rectangleType yard;                                                    //Line 8
    double fenceCostPerFoot;                                               //Line 9
    double fertilizerCostPerSquareFoot;                                    //Line 10
    double length, width;                                                  //Line 11
    double billingAmount;                                                  //Line 12

    cout << fixed << showpoint << setprecision(2);                         //Line 13

    cout << "Line 14: Enter the length and width of the "                  //Line 14
         << "yard (in feet): ";                                            //Line 15
    cin >> length >> width;                                                //Line 16
    cout << endl;

    yard.setDimension(length, width);                                      //Line 17

    cout << "Line 18: Enter the cost of fence "                            //Line 18
         << "(per foot): $";                                               //Line 19
    cin >> fenceCostPerFoot;                                               //Line 20
    cout << endl;

    cout << "Line 21: Enter the cost of fertilizer "                       //Line 21
         << "(per square foot): $";                                        //Line 22
    cin >> fertilizerCostPerSquareFoot;                                    //Line 23
    cout << endl;

    billingAmount = yard.perimeter() * fenceCostPerFoot                    //Line 24
                  + yard.area() * fertilizerCostPerSquareFoot;

    cout << "Line 25: Amount due: $" << billingAmount                      //Line 25
         << endl;

    boxType package;                                                       //Line 26
    double height;                                                         //Line 27
    double wrappingCostPerSquareFeet;                                      //Line 28

    cout << "Line 29: Enter the length, width, and height "                //Line 29
         << "of the package (in feet): ";                                  //Line 30
    cin >> length >> width >> height;                                      //Line 31
    cout << endl;

    package.setDimension(length, width, height);                           //Line 32

    cout << "Line 33: Enter the cost (25 to 50 cents) of "                 //Line 33
         << "wrapping per square foot: ";                                  //Line 34
    cin >> wrappingCostPerSquareFeet;                                      //Line 35
    cout << endl;

    billingAmount = wrappingCostPerSquareFeet                              //Line 36
                  * package.area() / 100;

    if (billingAmount < 1.00)                                              //Line 37
        billingAmount = 1.00;                                              //Line 38
```
```