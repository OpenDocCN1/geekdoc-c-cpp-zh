# Display 4.5 Buying Pizza (part 2 of 3)

```
12 int main()
13 {
14     int diameterSmall, diameterLarge;
15     double priceSmall, priceLarge;
16
17     getData(diameterSmall, priceSmall, diameterLarge, priceLarge);
18     giveResults(diameterSmall, priceSmall, diameterLarge, priceLarge);
19
20     return 0;
21 }

22 void getData(int& smallDiameter, double& priceSmall,
23               int& largeDiameter, double& priceLarge)
24 {
25     cout << "Welcome to the Pizza Consumers Union.\n";
26     cout << "Enter diameter of a small pizza (in inches): ";
27     cin >> smallDiameter;
28     cout << "Enter the price of a small pizza: $";
29     cin >> priceSmall;
30     cout << "Enter diameter of a large pizza (in inches): ";
31     cin >> largeDiameter;
32     cout << "Enter the price of a large pizza: $";
33     cin >> priceLarge;
34 }

35 void giveResults(int smallDiameter, double priceSmall,
36                  int largeDiameter, double priceLarge)
37 {
38     double unitPriceSmall, unitPriceLarge;
39
40     unitPriceSmall = unitPrice(smallDiameter, priceSmall);
41     unitPriceLarge = unitPrice(largeDiameter, priceLarge);
42     cout.setf(ios::fixed);
43     cout.setf(ios::showpoint);
44     cout.precision(2);
45     cout << "Small pizza:\n"
46          << "Diameter = " << smallDiameter << " inches\n"
47          << "Price = $" << priceSmall
48          << " Per square inch = $" << unitPriceSmall << endl
49     cout << "Large pizza:\n"
50          << "Diameter = " << largeDiameter << " inches\n"
51          << "Price = $" << priceLarge
52          << " Per square inch = $" << unitPriceLarge << endl;
53     if (unitPriceLarge < unitPriceSmall)
54         cout << "The large one is the better buy.\n";
```

The variables diameterSmall, diameterLarge, priceSmall, and priceLarge are used to carry data from the function getData to the function giveResults.

One function called within another function