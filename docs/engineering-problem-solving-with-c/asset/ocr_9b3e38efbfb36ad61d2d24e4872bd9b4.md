```
/*-------------------------------------------------*/
/* Program chapter7_12                             */
/* This program inputs a collection of points and  */
/* finds the Point that is closest to the origin   */
/*                                                 */
/* #include<iostream> //Required for cin, cout, cerr. */
/* #include<fstream> //Required for ifstream.       */
/* #include<string>   //Required for string.        */
/* #include<vector>   //Required for vector.        */
/* #include "Point.h" //Required for Point.         */
/* using namespace std;                            */
/*                                                 */
/* // Function prototypes.                         */
/* void readPointFile(istream& in,                  */
/*                    vector<Point>& v); //Pass by reference */
/* Point closeToOrigin(vector<Point> v); //Pass by value.   */
/*                                                 */
/* int main()                                      */
/* {                                               */
/*    //Declare objects.                           */
/*    Point p;                                     */
/*    string filename;                             */
/*    ifstream file1;                              */
/*                                                 */
/*    //Prompt user for file name and              */
/*    //open file.                                 */
/*    cout << "Enter filename ";                   */
/*    cin >> filename;                             */
/*    file1.open(filename);                        */
/*    if ( file1.fail() )                          */
/*    {                                            */
/*       cerr << "Error opening file " << filename << endl; */
/*       exit(1);                                  */
/*    }                                            */
/*                                                 */
/*    //Build Point vector                         */
/*    vector<Point> v;                             */
/*    readPointFile(file1, v);                     */
/*                                                 */
/*    //Find point closest to origin               */
/*    p = closeToOrigin(v);                        */
/*                                                 */
/*    cout << "(" << p.getX() << "," << p.getY() << ")"  */
/*         << " is closest to the origin." << endl; */
/*    return 0;                                    */
/*                                                 */
/*-------------------------------------------------*/
```