# Listing 18-6 *(continued)*

```
```java
out.print("How many chips do you have?");
out.print(" (Type a number,");
out.print(" or type 'Not playing') " );
reply = keyboard.nextLine();

if (!reply.equals("Not playing")) {
    numberOfChips = Integer.parseInt(reply);
    numberOfChips += 10;

    out.print("You now have ");
    out.print(numberOfChips);
    out.println(" chips.");
}
keyboard.close();
}
}
```
```

Some runs of the code in Listing 18-6 are shown in Figure 18-8. You want to give each player ten chips. But some party poopers in the room aren’t playing. So two people, each with no chips, may not get the same treatment. An empty-handed player gets ten chips, but an empty-handed party pooper gets none.

![](bbox=[0.23, 0.536, 0.786, 0.629])

![](bbox=[0.23, 0.658, 0.804, 0.737])

![](bbox=[0.23, 0.767, 0.862, 0.847])

**Figure 18-8:** Running the code in Listing 18-6.