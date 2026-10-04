Again, the output shows that the print_info function that called is for the car class, not the for the SC300 class. But it looked like you declared this as a virtual.

On the other hand, when you pass by value, you still have an SC300 defined in the main program that you call print_car, but now it is a parameter that is passed by value.

In the preceding case, you create an SC300 object in your main code and pass this to the print_car function using a pass by reference. When this function is called, the memory for the parameter has a reference stored. This is basically a pointer, and it has a reference to the object that was passed. No data is copied. Because the SC300 class is derived from the car class, it is OK to pass in the SC300 as a reference.

When the function is called, in this case, there is space aside in memory for a car object. Then, the values from the argument are copied into the car object that has been allocated. In this case, the base_price and model_name, which were defined in the car class, but not the various Booleans which packages were selected.

So, when you call print_info within the print_car function, you go to that reference and call print_info on. Because the thing it is referring to the SC300 object that was created before, it will try to call the print_info command for the SC300 class. Because print_info was declared to be virtual, it will look for the most specific version of that function, which is defined in the SC300 class.

Thus, the thing that's sitting in memory is a car-not an SC300; It has no memory of originally coming from SC300; all it knows is it's a car. As a result, when you call print_info on that object, it's going to use the print_info command defined for the car class, not the one defined for SC300 class.

![](bbox=[0.038, 0.57, 0.962, 0.868])