The flow function simply returns the current flow as determined by the position member variable, as shown here:

```
double throttle::flow( ) const
// Precondition: shut_off has been called at least once to initialize the throttle.
// Postcondition: The value returned is the current flow as a proportion of
// the maximum flow.
{
    return position / 6.0;   // Divide by 6.0, since the throttle has six positions.
}
```

Since flow is a constant member function, we must include the keyword const at the end of the function's head.

The final throttle function is called is_on. The function returns a boolean true-or-false value, indicating whether the fuel flow is on. Here is one way to implement is_on so that it returns the correct boolean value:

```
bool throttle::is_on( ) const
// Precondition: shut_off has been called at least once to initialize the throttle.
// Postcondition: If the throttle's flow is above 0, then the function
// returns true; otherwise, it returns false.
{
    return (flow( ) > 0);
}
```

# Member Functions May Activate Other Members

The implementation of is_on illustrates a final important feature of member functions: The implementation of a member function may activate other member functions. For example, our implementation of is_on activates the flow member function. When flow is used within the body of is_on, it is used without an object name such as my_throttle or control. No object name is needed in front of it—we just write flow( ); the actual instance of flow that will be used is determined by the activation of is_on. So when my_throttle.is_on is activated, it uses my_throttle.flow. On the other hand, when control.is_on is activated, it uses control.flow.

# PROGRAMMING TIP
STYLE FOR BOOLEAN VARIABLES

In the return statement of is_on, we wrote: return (flow( ) > 0);. The test in the parentheses is evaluated, and the true-or-false value of this test is returned by