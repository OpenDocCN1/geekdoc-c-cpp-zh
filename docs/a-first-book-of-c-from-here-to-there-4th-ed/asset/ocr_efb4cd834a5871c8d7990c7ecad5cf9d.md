method where in memory the object it’s to operate on is located. In this way, it enables the method to access the object and its data members directly. For example, the statement `oldDate.showDate()` passes the oldDate object’s address to the showDate() member method.

Two questions at this point are as follows:

+   - How is this address passed to `showDate()`?
+   - Where is this address stored?

The answer to the first question is that the address is passed to the called function as a hidden argument. Therefore, the call `oldDate.showDate()` passes `oldDate` to `showDate()`. Recall from Section 8.1 that placing the address operator, &, in front of an identifier means “the address of,” so the expression `&oldDate` should be read as “the address of oldDate.” In effect, then, the call `oldDate.showDate()` corresponds to `showDate(&oldDate)`. Although this call is invalid because it violates the syntax rules for calling a member method, it clearly illustrates that an address is passed. The question then is how is the passed address saved and accessed by `showDate()`?

It’s saved in the same manner as any passed address must be saved—by using a pointer. This special pointer is created automatically as a hidden argument for each nonstatic class method, when the method is defined. The name of this special pointer is this, described next.

# The this Pointer

The this pointer is added automatically to each nonstatic class method as a hidden argument. When a method is called, the calling object’s address is passed to it and stored in the method’s this pointer. Therefore, each member method actually receives an extra argument that’s the address of an object.

Although it’s not usually necessary to do so, the address in the this pointer can be used explicitly in the called method. For example, when `showDate()` is called by the expression `oldDate.showDate()`, the this pointer in `showDate()` can be used to access any data member in the oldDate object by using the following syntax:

```
(*this).month accesses oldDate’s month member.
(*this).day accesses oldDate’s day member.
(*this).year accesses oldDate’s year member.
```

These relationships are shown in Figure 11.4. As shown, the starting address of the oldDate object is also the address of the object’s first data member. Except for the dot notation to locate the correct member item, it’s the same technique for passing addresses that you saw in Section 8.4.