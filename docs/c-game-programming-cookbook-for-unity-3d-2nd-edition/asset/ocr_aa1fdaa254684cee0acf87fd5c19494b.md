parameters; a String to convert followed by the index number of the character you want to convert.

With a converted value in the local variable val, we check that it is greater than -1 and less than _weapons.Length to be sure that the number coming in is valid for weapon selection. If it is, we pass the value in to SetWeaponSlot() to choose the weapon.

NOTE: This is not actually a great way of doing this. Unfortunately, although it minimizes the amount of code it has the trade-off of inefficiency. Checking strings is expensive, in terms of processing, so although it works in simple situations it would not be optimized for more complex games. The best way to do this would be the simplest – to either just stick to using next/prev weapon buttons or to check each number on the keyboard with a set of if statements such as:

```
if (Input.GetKey("1"))
{
    SetWeaponSlot(0);
}
if (Input.GetKey("2"))
{
    SetWeaponSlot(1);
}
```