Now, because you told your new file that you wanted a new class made, you should see some default code in your Player.cs file – it will look like this:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace CreatingClasses // Your namespace will probably be something different.
{
    class Player // If you named your class/file with a different name, that’s what will be here instead of Player
    {
    }
}
```

That's put us where we want to be, with a brand new class.

# Adding Instance Variables

Right now, there is little in this class so the first thing we do is add a few variables. Remember, one of the main points of an object is that they track and monitor their own data. These are stored as variables for the object. Because each class object or instance has its own data, we call the variables by the name of instance variables. Let’s say that your game has two players; each can track their own scores by themselves inside those instance variables.

For our simple class, we want to track three things – the name of the player, the number of lives they have left, and their score. We want to create one instance variable for each of these so, inside the curly braces of our class, we add the following code: