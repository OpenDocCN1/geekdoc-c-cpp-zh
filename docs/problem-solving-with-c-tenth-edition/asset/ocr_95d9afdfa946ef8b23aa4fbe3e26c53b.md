because they are both at the same level of nesting. Later in this chapter, you will see some specific cases where it makes sense to use other indenting patterns, but unless there is some rule to the contrary, you should indent each level of nesting as illustrated in Display 3.3.

# PROGRAMMING TIP Use Braces in Nested Statements

Suppose we want to write an if-else statement to use in an onboard computer monitoring system for a racing car. This part of the program warns the driver when fuel is low but tells the driver to bypass pit stops if the fuel tank is close to full. In all other situations the program gives no output so as not to distract the driver. We design the following pseudocode:

If the fuel gauge is below 3/4 full, then:
    Check whether the fuel gauge is below 1/4 full and issue a low fuel warning if it is.
Otherwise (that is, if fuel gauge is over 3/4 full):
    Output a statement telling the driver not to stop.

If we are not being too careful, we might implement the pseudocode as follows:

```
if (fuelGaugeReading < 0.75)
    if (fuelGaugeReading < 0.25)
        cout << "Fuel very low. Caution!\n";
else
    cout << "Fuel over 3/4. Don't stop now!\n";
```

![](bbox=[0.6, 0.525, 0.785, 0.595])

This implementation looks fine, and it is indeed a correctly formed C++ statement that the compiler will accept and that will run with no error messages. However, it does not implement the pseudocode. Notice that this statement has two occurrences of if and only one else. The compiler must decide which if gets paired with the one else. We have nicely indented this nested statement to show that the else should be paired with the first if, but the compiler does not care about indenting. To the compiler, the preceding nested statement is the same as the following version, which differs only in how it is indented:

```
if (fuelGaugeReading < 0.75)
    if (fuelGaugeReading < 0.25)
        cout << "Fuel very low. Caution!\n";
else
    cout << "Fuel over 3/4. Don't stop now!\n";
```

Unfortunately for us, the compiler will use the second interpretation and will pair the one else with the second if rather than the first if. This is sometimes called the dangling else problem; it is illustrated by the program in Display 3.4.

The compiler always pairs an else with the nearest previous if that is not already paired with some else. But, do not try to work within this rule. Ignore