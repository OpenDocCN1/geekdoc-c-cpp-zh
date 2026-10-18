```
cout << "m = " << m << "\n" << "n = " << n << "\n";
}
int main()
{
gamma g(5, 10.75, 20, 30);
cout << "\n";
g.show_x();
g.show_y();
g.show_mn();
return 0;
}
```

The output of Program 8.7 would be:

+   beta initialized
+   alpha initialized
+   gamma initialized
+   x = 5
+   y = 10.75
+   m = 20
+   n = 30

> NOTE: beta is initialized first, although it appears second in the derived constructor. This is because it has been declared first in the derived class header line. Also, note that alpha(a) and beta(b) are function calls. Therefore, the parameters should not include types.

C++ supports another method of initializing the class objects. This method uses what is known as initialization list in the constructor function. This takes the following form: