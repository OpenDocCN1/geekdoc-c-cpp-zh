```
```csharp
10    // prompt for and input three floating-point values
11    Console.Write("Enter first floating-point value: ");
12    double number1 = double.Parse(Console.ReadLine());
13    Console.Write("Enter second floating-point value: ");
14    double number2 = double.Parse(Console.ReadLine());
15    Console.Write("Enter third floating-point value: ");
16    double number3 = double.Parse(Console.ReadLine());
17
18    // determine the maximum of three values
19    double result = Maximum(number1, number2, number3);
20
21    // display maximum value
22    Console.WriteLine("Maximum is: " + result);
23  }
24
25  // returns the maximum of its three double parameters
26  static double Maximum(double x, double y, double z)
27  {
28      double maximumValue = x; // assume x is the largest to start
29
30      // determine whether y is greater than maximumValue
31      if (y > maximumValue)
32      {
33          maximumValue = y;
34      }
35
36      // determine whether z is greater than maximumValue
37      if (z > maximumValue)
38      {
39          maximumValue = z;
40      }
41
42      return maximumValue;
43  }
44 }
```
```

Enter first floating-point values: 3.33
Enter second floating-point values: 1.11
Enter third floating-point values: 2.22
Maximum is: 3.33

Enter first floating-point values: 2.22
Enter second floating-point values: 3.33
Enter third floating-point values: 1.11
Maximum is: 3.33

Enter first floating-point values: 2.22
Enter second floating-point values: 1.11
Enter third floating-point values: 3.33
Maximum is: 3.33

Fig. 7.2 | Method Maximum with three parameters. (Part 2 of 2.)