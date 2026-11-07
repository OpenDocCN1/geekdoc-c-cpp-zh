# Making abstract data types

An Abstract Data Type (ADT) represents a concept, rather than a tangible object, and is always the base to other classes. A base class can be made into an ADT by initializing one or more of its methods with zero. These are known as “pure virtual methods” and must always be overridden in derived classes.

![](bbox=[0.118, 0.211, 0.176, 0.258])

adt.cpp

+   1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use
+   
+   ```cpp
+   #include <iostream>
+   using namespace std ;
+   ```

+   2. Declare a base ADT class named “Shape”, containing three pure virtual methods
+   
+   ```cpp
+   class Shape
+   {
+       public:
+           virtual int getArea() = 0 ;
+           virtual int getEdge() = 0 ;
+           virtual void Draw() = 0 ;
+   };
+   ```

+   3. Declare a derived class named “Rect”, containing two private variables
+   
+   ```cpp
+   class Rect : public Shape
+   {
+       private:
+           int height, width ;
+   };
+   ```

+   4. In the derived class declaration, insert a public constructor and destructor
+   
+   ```cpp
+   public :
+       Rect( int initWidth, int initHeight )
+       {
+           height = initHeight ;
+           width = initWidth ;
+       }
+   
+   ~Rect() ;
+   ```

![](bbox=[0.118, 0.673, 0.205, 0.733])

It is illegal to create an instance object of an ADT – attempting to do so will simply create a compiler error.

+   5. In the derived “Rect” class declaration, declare three public methods to override the pure virtual methods declared in the “Shape” base class
+   
+   ```cpp
+   int getArea() { return height * width ; }
+   int getEdge() { return ( 2 * height ) + ( 2 * width ) ; }
+   
+   void Draw()
+   {
+       for ( int i = 0 ; i < height ; i++ ) {
+           for ( int j = 0 ; j < width ; j++ ) { cout << "x" ; }
+           cout << endl ;
+       }
+   }
+   ```