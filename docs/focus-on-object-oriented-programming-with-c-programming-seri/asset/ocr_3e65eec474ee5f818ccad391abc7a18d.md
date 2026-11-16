The efficiency that we gained is obvious.

+   - Several of the Portal functions can be reused
+   - The declarations for Window and Door are terse and understandable in terms of the functionality of Portal
+   - Both Window and Door can be stereotyped as a Portal when convenient.

For example:

```
for (i = 0; i < max; ++i)
    portallist[i] -> open();
```

Clearly this method for opening all Windows and Doors is superior to handling each type separately. As the application matures, more types of Portals will probably be added. But since the code deals with all types of Portals, it will not have to change. Thus, the polymorphic behavior of the abstract class Portal provides a more maintainable and robust design!

Note that forcing Window and Door to inherit from Portal is not necessary to the proper functioning of the application. The application could be designed without the abstract class. However, creating the abstract Portal class results in a superior design that promotes polymorphism and code reuse.