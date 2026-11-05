```
return volumeToCut % factor;
}
```

*Code Listing 61: Create IntelliTest for method*

As before, the preceding code listing tells the calling method that the method under contract will result in the cut volume always equaling the bin volume. This means that all the steel has been cut perfectly and no off-cuts resulted by using the specific factor.

To generate a new IntelliTest for the ProductionVolumePerBin() method, right-click on the method and select Create IntelliTest from the context menu.

![](bbox=[0.2, 0.35, 0.85, 0.7])

*Figure 45: Create IntelliTest*

Visual Studio will now display the Create IntelliTest window where you can configure additional settings for your generated IntelliTest.