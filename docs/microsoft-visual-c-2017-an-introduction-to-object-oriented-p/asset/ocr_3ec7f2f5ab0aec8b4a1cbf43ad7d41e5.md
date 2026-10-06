# You Do It

# Using AND and OR Logic

In the next steps, you create an interactive program that allows you to test AND or OR logic for yourself. The program decides whether a delivery charge applies to a shipment. If the customer lives in Zone 1 or Zone 2, shipping is free, as long as the order contains fewer than 10 boxes. If the customer lives in another zone or if the order is too large, then delivery charge applies.

+   1. Open a new file named DemoORAND, and then enter the first few lines of the program. Define constants for ZONE1, ZONE2, and the LOW_QUANTITY limit as well as variables to hold the customer's input strings, which will be converted to the zone and number of boxes in the shipment.

```csharp
using System;
using System.Console;
class DemoORAND
{
    static void Main()
    {
        const int ZONE1 = 1, ZONE2 = 2;
        const int LOW_QUANTITY = 10;
        string inputString;
        int quantity;
        int deliveryZone;
    }
```

+   2. Enter statements that describe the delivery charge criteria to the user and accept keyboard values for the customer's delivery zone and shipment zone.

```csharp
WriteLine("Delivery is free for zone {0} or {1}",
ZONE1, ZONE2);
WriteLine("when the number of boxes is less than {0}",
LOW_QUANTITY);
WriteLine("Enter delivery zone ");
inputString = ReadLine();
deliveryZone = Convert.ToInt32(inputString);
WriteLine("Enter the number of boxes in the shipment");
inputString = ReadLine();
quantity = Convert.ToInt32(inputString);
```

(continues)