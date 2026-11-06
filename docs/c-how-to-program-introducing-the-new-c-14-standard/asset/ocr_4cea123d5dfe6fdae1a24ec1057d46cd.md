a call to the `invalid_argument` constructor that allows us to specify a custom error-message string. After the exception object is created, the `throw` statement immediately terminates function `setTime` and the exception is returned to the code that attempted to set the time.

Invalid values cannot be stored in the data members of a `Time` object, because

+   - when a `Time` object is created, its default constructor is called and each data member is initialized to 0, as specified in lines 17–19 of **Fig. 9.1**—setting `hour`, `minute` and `second` to 0 is the universal-time equivalent of 12 AM (midnight)—and
+   - all subsequent attempts by a client to modify the data members are scrutinized by function `setTime`.