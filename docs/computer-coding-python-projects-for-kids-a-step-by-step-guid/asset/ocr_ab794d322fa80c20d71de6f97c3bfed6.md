# Making the GUI

You’re going to write your code in two sections. First you’ll set up some functions to get input from the user, then you’ll write the code that does the encryption and decryption. Now let’s get started – you never know when you might need to send a secret message to someone!

![](bbox=[0.686, 0.076, 0.963, 0.203])

# 1. Create a new file

Open IDLE and create a new file. Save it as “secret_messages.py”.

![](bbox=[0.025, 0.324, 0.299, 0.427])

# 2. Add the modules

You need to import some widgets from Python’s Tkinter module. This will let you use some of its GUI features, such as messagebox to display information to the user, and simpledialog to ask them questions. Type this line at the top of your file.

```
```python
from tkinter import messagebox, simpledialog, Tk
```
```

# 3. Encrypt or decrypt?

Now create a function, `get_task()`, to open a dialogue box that asks the user whether they want to encrypt or decrypt a message. Add the function under the code you added in Step 2.

```
```python
def get_task():
    task = simpledialog.askstring('Task', 'Do you want to encrypt or decrypt?')
    return task
```
```

This line asks the user to type in “encrypt” or “decrypt”, then saves their response in the variable task.

Pass the value in task back to the code that used this function.

This word will appear as a title in the dialogue box.

# 4. Get the message

Create a new function, `get_message()`, to open a dialogue box asking the user to type in the message they want to encrypt or decrypt. Add this function under the code you added in Step 3.

```
```python
def get_message():
    message = simpledialog.askstring('Message', 'Enter the secret message: ')
    return message
```
```

This line asks the user to type the message, then saves it in the variable message.

Pass the value in message back to the code that used this function.