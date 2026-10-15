```
oSheet.get_Range("A" + i.ToString(), "C" + i.ToString()).Value = values;
    i++;
}

oXL.Visible = true;
oXL.UserControl = true;
```

The problem with above code is too much Excel logic is mixed with the application logic. Now we can see the new code with proxy pattern implemented.

# New Code with Proxy Pattern

```
ExcelProxy proxy = new ExcelProxy();
proxy.Save(_list);
```

The code is only 2 lines and the Excel COM object creation, cell value assigning etc are taken care by the ExcelProxy class.

![](bbox=[0.19, 0.365, 0.365, 0.45])

# Application Execution

On executing the application we can see the results inside Microsoft Excel.