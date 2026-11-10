To create a title, proceed with the following steps:

+   1. Right-click the program name in Object Navigator and select Create • GUI Titles.
+   2. The Create Title window will open (see Figure 12.43). Maintain a title code and the Title text. Click Continue.

![](bbox=[0.148, 0.239, 0.633, 0.358])

Figure 12.43  Create Title

+   3. Once the title is created and activated, you can load the title as shown in Listing 12.5.

```
MODULE status_100 OUTPUT.
SET TITLEBAR 'TITLE'.
ENDMODULE.
```

**Listing 12.5**  Set Title

# 12.9.4  Modifying Screen Fields Dynamically

The attributes of screen fields are set statically at design time. However, it's possible to modify some of these attributes at runtime. The screen field attributes can be accessed using a predefined SCREEN structure. We can access each screen element by looping the screen structure as shown:

```
LOOP AT SCREEN.
MODIFY SCREEN.
ENDLOOP.
```

The screen structure (see Figure 12.44) has various attributes that can be modified at runtime in the ABAP program. The name component holds the names of the screen fields that can be checked to apply the changes to specific screen fields. If the screen fields are assigned to a group, the group name can be accessed by checking the group1, group2, group3, and group4 fields. By grouping the screen fields, we can apply the changes consistently to all fields of the group.