functionality. In this section, we look at building a script to derive from BaseWeaponController and look for presses on the number keys 1 to 9 to choose the currently selected weapon. You can see this script in action in the Blaster game example from Chapter 15.

```
using UnityEngine;
namespace GPC
{
    [AddComponentMenu("CSsharpBookCode/Common/Weapons/Standard Slot Controller")]
    public class StandardSlotWeaponController : BaseWeaponController
    {
        public bool allowWeaponSwitchKeys = true;
```

Above, our new script derives from BaseWeaponController. We include a Boolean variable, allowWeaponSwitchKeys, for toggling weapon switching on or off.

```
public void Update()
{
    if (!allowWeaponSwitchKeys)
        return;

    // do weapon selection / switching slots
    // ----------------------------------------
    if (Input.GetKey(KeyCode.Less))
        PrevWeaponSlot(true);
    else if (Input.GetKey(KeyCode.Greater))
        NextWeaponSlot(true);
}
```

Update() starts with a quick to check to see if weapon switching is allowed, dropping out if it is not. Next, when the greater than or less than keys are pressed, we call either PrevWeaponSlot() or NextWeaponSlot() to switch weapons.

```
// keys 1-9
string theKey = Input.inputString;
if (theKey == "")
    return;
```

Input.inputString provides us with a string containing the most recent key pressed on the keyboard. Above, we store the value of Input.inputString in theKey and then check it to see whether it is empty. If the string is empty, no key has been pressed so we drop out.

```
var val = (Char.ConvertToUtf32(theKey, 0)-49);
if(val>-1 && val < weapons.Length)
    SetWeaponSlot(val);
    }
}
```

Rather than checking input for every key from 1 to 9, we take the string theKey and convert it into a number. Char.ConvertToUtf32 will convert a string into a Unicode code. The numbers 1-9 are represented by the numbers 49 to 58. If we take the code from Char.ConvertToUtf32 and subtract 49 from it, we get a number between 0 and 9 – perfect numbers to pass into the SetWeaponSlot() function for choosing which weapon slot to use. Char.ConvertToUtf32 takes two