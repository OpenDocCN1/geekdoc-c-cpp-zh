```
Console.WriteLine("j = {0}", j);        //
Invoke the delegate.
    bool boolResult = del();
Console.WriteLine("j = {0}. b = {1}", j,
boolResult);
}
    static void Main() {
        Test test = new Test();

test.TestMethod(5);
        // Prove that del2 still has a
copy of
        // local variable j from
TestMethod.
        bool result = test.del2(10);

Console.WriteLine(result);
Console.ReadKey();
    }
}
}
```

Once the above code is compiled, it shows the following result –

+   - j = 0
+   - j = 10. b = True
+   - True

# Statement Lambda

There is also statement lambdas that hold two or three statements but are not included in the construction of