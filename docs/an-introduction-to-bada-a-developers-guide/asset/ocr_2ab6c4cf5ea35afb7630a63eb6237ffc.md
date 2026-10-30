```
// Create left softkey (SOFTKEY_0)
// Create a Bitmap and decode image
Bitmap* pBitmap = null;
Image* pImage = new Image();
pImage->Construct();
pBitmap = pImage->DecodeN(L"/Res/bada.png", BITMAP_PIXEL_FORMAT_ARGB8888);

SetSoftkeyIcon(SOFTKEY_0, *pBitmap, pBitmap);

delete pImage;
delete pBitmap;

// Create right softkey (SOFTKEY_1)
SetSoftkeyText(SOFTKEY_1, "Right");

// Assign action IDs for both the softkeys
SetSoftkeyActionId(SOFTKEY_0, ID_SOFTKEY_LEFT);
SetSoftkeyActionId(SOFTKEY_1, ID_SOFTKEY_RIGHT);

// Register event listener
AddSoftkeyActionListener(SOFTKEY_0, *this);
AddSoftkeyActionListener(SOFTKEY_1, *this);
```

# Hints, Pitfalls, and Related Topics

If both an icon and text are set for the same soft key at the same time, the text takes precedence over the icon. A soft key can be enabled or disabled using the SetSoftkeyEnabled() method, with the enable parameter set to either true or false.

# Related Recipes

+   - Add a Form to a Frame-based App
+   - Add a Simple Button Control to a Form

# Recipe 2.3: Add an Options Menu to a Form and Get User Selections

# Problem Description

You want to add an options menu to a Form and get the user’s selections.

# The Recipe

The following configuration is required for this recipe: