Table 3.2 Syntax for defining and initializing variables and constants (objects) in C++.

Operation | Syntax | Examples
| --- | --- | ---
Definition of a variable or constant (object) named by identifier and with features set by type. The initial value is set with the initializer list {}. If const is added, then the object cannot be changed (no new values are allowed). This is the preferable way to initialize objects in C++. {} is called zero-initialization since an object is guaranteed to have its default constructor called, which for built-in types sets its value to 0. | const type identifier { value }; | // Vara and const initialized with {} int x {}; // Create x and set to 0 x += 1; // Can increase by 1
// Create const y and set to 100 - cannot change const int y {} 100; //y += 1; // Error, cannot change constant
// Create c and set to ASCII code of 'A' char c { 'A' }; // Can display on the screen
std::cout << "c = " << c << std::endl;
// A variable of floating arithmetic double radius { 2.54 };
// Create const kPI of floating type const double kPI { 3.141592653589 }; // Compute and display area
std::cout << "Area = " << kPI * radius * radius;
hbool flag { true }; // A logical var init to true