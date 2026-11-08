+   7.
+   
+   **a.**
+   ```cpp
+   void bagType::set(string s, double a, double b, double c, double d)
+   {
+       style = s;
+       l = a;
+       w = b;
+       h = c;
+       price = d;
+   }
+   ```
+   
+   **b.**
+   ```cpp
+   void bagType::print() const
+   {
+       cout << "Bag Type: " << style << ", length = " << l
+            << ", width = " << w << ", height = " << h
+            << ", price = $" << price << endl;
+   }
+   ```
+   
+   **c.**
+   ```cpp
+   bagType::bagType()
+   {
+       style = "";
+       l = 0.0;
+       w = 0.0;
+       h = 0.0;
+       price = 0.0;
+   }
+   ```
+   
+   **d.** `newBag.print();`
+   
+   **e.** `bagType tempBag("backPack", 15, 8, 20, 49.99);`

9. The functions print, updatePay, and getNumOfServiceYears are accessors; functions setData and updatePay are mutators.

+   11.
+   
+   **a.** 14
+   
+   **b.** 3
+   
+   **c.** The class temporary has only one constructor. Because this is a constructor with default parameters, it can be used to initialize an object without specifying any parameters. For example, the following statement creates the object newObject and its instance variables are initialized to `""`, 0, and 0, respectively.
+   
+   ```cpp
+   temporary newObject;
+   ```

13. The statement in Line 1 creates object1 and initializes the instance variables of this object to `""`, 0, 0, that is, object1.description = `""`; object1.first = 0.0; and object1.second = 0.0;. The statement in Line 2 creates object2 and initializes the instance variables of this object as follows: object2.description = `"rectangle"`; object2.first = 3.0; and object2.second = 5.0;. The statement in Line 3 creates object3 and initializes the instance variables of this object as follows: object3.description = `"circle"`; object3.first = 6.5; and object3.second = 0.0;. The statement in Line 4 creates object4 and