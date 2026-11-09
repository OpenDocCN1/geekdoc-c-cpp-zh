![](bbox=[0.036, 0.051, 0.229, 0.354])

# # Adjusting main.py

Now we must adjust `main.py`. This is where we store the rules and run the objects such as the ball. Again there is a starter file from last time with some spaces for you to add the new code. The final file should look like that in Code Box 4.5.

```
**Code Box 4.5** `main.py`

````python
from tkinter import *
import table, ball

# initialise global variables
x_velocity = 10
y_velocity = 10

# order a window from the tkinter window factory
window = Tk()
window.title("MyPong")
````
```

Do not forget to  
import ball

*(continues on the next page)*