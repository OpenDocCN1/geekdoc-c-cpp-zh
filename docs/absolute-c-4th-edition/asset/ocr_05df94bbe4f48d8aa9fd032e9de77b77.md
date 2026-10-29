the size of the discount. Your program will need to compute daily gross sales, which intuitively should just be the sum of all the individual sales bills. You may also want to calculate the largest and smallest sales of the day or the average sale for the day. All these can be calculated from the individual bills, but many of the functions for computing the bills will not be added until later, when you decide what types of sales you will be dealing with. To accommodate this, we make the function for computing the bill a virtual function. (For simplicity in this first example, we assume that each sale is for just one item, although with derived classes and virtual functions we could, but will not here, account for sales of multiple items.)

Displays 15.1 and 15.2 contain the interface and implementation for the class Sale. All types of sales will be derived classes of the class Sale. The class Sale corresponds to

# Display 15.1 Interface for the Base Class Sale

```
1
2 //This is the header file sale.h.
3 //This is the interface for the class Sale.
4 //Sale is a class for simple sales.
5
6 #ifndef SALE_H
7 #define SALE_H
8
9 namespace SavitchSale
10 {
11     class Sale
12     {
13     public:
14         Sale();
15         Sale(double thePrice);
16         double getPrice() const;
17         void setPrice(double newPrice);
18         virtual double bill() const;
19         double savings(const Sale& other) const;
20         //Returns the savings if you buy other instead of the calling object.
21     private:
22         double price;
23     };
24
25     bool operator < (const Sale& first, const Sale& second);
26     //Compares two sales to see which is larger.
27
28 } //SavitchSale
29
30 #endif // SALE_H
```