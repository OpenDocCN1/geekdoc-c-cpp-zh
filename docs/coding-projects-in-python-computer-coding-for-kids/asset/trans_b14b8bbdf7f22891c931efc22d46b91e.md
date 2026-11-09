

## 10  获取奇数位置的字母

接下来，你需要创建一个类似的函数，用于生成消息中所有奇数编号字母的列表。请把这个函数放在第9步代码的下面。

```python
def get_odd_letters(message):
    odd_letters = []
    for counter in range(0, len(message)):
        if not is_even(counter):
            odd_letters.append(message[counter])
    return odd_letters
```

![](img/6b18a113f7aa9338e32f3ac1fa217987_137_0.png)

### 记住：列表和长度

在列表和字符串中，Python 从 0 开始计数，并使用函数 len() 来获取字符串的长度。例如，如果你输入 len('secret')，Python 会告诉你字符串 'secret' 有 6 个字符长。但因为第一个字母在位置 0，所以最后一个字母在位置 5，而不是 6。

## 11  交换字母顺序

现在你已经把偶数位字母放在一个列表中，奇数位字母放在另一个列表中，可以用它们来加密消息了。下一个函数将交替从这两个列表中取出字母，并放入一个新列表。但它不会按原始顺序组装，而是以奇数位字母开头，而不是偶数位字母。请把这个函数放在第10步代码的下面。

```python
def swap_letters(message):
    letter_list = []
    if not is_even(len(message)):
        message = message + 'x'
    even_letters = get_even_letters(message)
    odd_letters = get_odd_letters(message)
    for counter in range(0, int(len(message)/2)):
        letter_list.append(odd_letters[counter])
        letter_list.append(even_letters[counter])
    new_message = ''.join(letter_list)
    return new_message
```

如果消息的字母数为奇数，就额外地添加一个 x。

循环遍历奇数位和偶数位字母列表。

将下一个奇数位字母添加到最终消息。

将下一个偶数位字母添加到最终消息。

join() 函数把字母列表转换成字符串。

### ▷ 工作原理

swap_letters() 函数把所有奇数位和偶数位字母交替放入一个新列表。它从单词的第一个字母开始构建列表，而 Python 将这个位置计为奇数号。

![](img/6b18a113f7aa9338e32f3ac1fa217987_137_1.png)

### 专家提示

**整数位置**

你在循环范围中使用了 len(message) / 2，因为偶数位和奇数位字母列表的长度都是原消息的一半。你通过让程序在必要时添加一个 x，确保消息的长度总是偶数，这样它就能被 2 整除。然而，结果将是浮点值（带小数点，如 3.0 或 4.0），而不是整数（整数，如 3 或 4）。如果你尝试用浮点数作为列表项的位置，Python 会报错，所以要用 int() 函数将它转换为整数。

```
>>> mystring = 'secret'
>>> mystring[3.0]
Traceback (most recent call last):
  File "<pyshell#1>", line 1, in <module>
    mystring[3.0]
TypeError: string indices must be integers
```

如果你使用了浮点数（如 3.0）而不是整数（如 3），Python 就会给出这样的错误消息。

## 12  更新循环

swap_letters() 函数有一个非常实用的特性：如果你对加密后的消息运行它，它就会将其解密。因此，你可以根据用户的需要，用这个函数来加密或解密消息。请对你第6步创建的 while 循环进行以下修改。

![](img/6b18a113f7aa9338e32f3ac1fa217987_138_0.png)

```python
while True:
    task = get_task()
    if task == 'encrypt':
        message = get_message()
        encrypted = swap_letters(message)
        messagebox.showinfo('Ciphertext of the secret message is:', encrypted)
    elif task == 'decrypt':
        message = get_message()
        decrypted = swap_letters(message)
        messagebox.showinfo('Plaintext of the secret message is:', decrypted)
    else:
        break
root.mainloop()
```

使用 swap_letters() 加密消息。

显示加密后的消息。

使用 swap_letters() 解密消息。

显示解密后的消息。

## 13  运行加密

测试你的程序。在任务窗口中选择“encrypt”。当消息窗口弹出时，输入间谍可能想保密的那种消息。试试输入：“中午在公园的秋千旁见我”。

## 14  运行解密

如果你选中加密后的文本并复制它，就可以在下一次循环时选择“decrypt”选项。在消息窗口中粘贴加密后的消息，并点击 OK。然后你就会再次看到原始消息。

![](img/6b18a113f7aa9338e32f3ac1fa217987_139_0.png)

## 15  解密这串文本！

你的加密程序现在应该可以正常工作了。为了确认，尝试解密下面显示的文本。现在，你可以把 Python 代码分享给朋友，并开始发送秘密消息了！

![](img/6b18a113f7aa9338e32f3ac1fa217987_139_1.png)

## 技巧与调整

下面是一些点子，可以让你的秘密消息即使被敌方特工——比如爱多管闲事的兄弟姐妹——截获，也更难被读懂！

- **去除空格**

  让加密更安全的一种方法是去掉空格和所有标点字符，比如句号和逗号。为此，在输入消息时不要包含空格和标点。只要确保与你交换消息的朋友知道这个约定就行。

![](img/6b18a113f7aa9338e32f3ac1fa217987_139_2.png)

### 交换后反转

为了让人更难破解你的加密，可以在用 `swap_letters()` 加密之后，再将消息反转。为此，你需要创建两个不同的函数——一个用于加密，一个用于解密。

1. **加密函数**

   `encrypt()` 函数先交换字母，然后反转字符串。这几行代码使用了 `swap_letters()` 函数。

   ```python
   def encrypt(message):
       swapped_message = swap_letters(message)
       encrypted_message = ''.join(reversed(swapped_message))
       return encrypted_message
   ```

   在字母被交换后，将消息反转。

2. **解密函数**

   `decrypt()` 函数位于 `encrypt()` 函数下方。它首先反转加密后的消息，然后使用 `swap_letters()` 将字母放回正确的顺序。

   ```python
   def decrypt(message):
       unreversed_message = ''.join(reversed(message))
       decrypted_message = swap_letters(unreversed_message)
       return decrypted_message
   ```

   通过再次反转消息，来撤销加密函数的反转操作。

   这一行将字母放回正确的顺序。

3. **使用新函数**

   现在，你需要更新程序中的无限循环部分，用这些函数来代替 `swap_letters()` 函数。

   ```python
   while True:
       task = get_task()
       if task == 'encrypt':
           message = get_message()
           encrypted = encrypt(message)
           messagebox.showinfo('Ciphertext of the secret message is:', encrypted)
       elif task == 'decrypt':
           message = get_message()
           decrypted = decrypt(message)
           messagebox.showinfo('Plaintext of the secret message is:', decrypted)
       else:
           break
   ```

   新的 `encrypt()` 函数取代了 `swap_letters()`。

   新的 `decrypt()` 函数取代了 `swap_letters()`。

   别忘了保存你的工作。

![](img/6b18a113f7aa9338e32f3ac1fa217987_140_0.png)

### 添加“假”字母

另一种加密消息的方法是在每两个字母之间插入随机字母。因此，单词“secret”可能会变成“stegcarielta”或“shcvcarieste”。和“交换后反转”的技巧一样，你需要两个不同的函数——一个用于加密，一个用于解密。

> shcvcarieste!

![](img/6b18a113f7aa9338e32f3ac1fa217987_141_0.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_141_1.png)

所有绿色的字母都是假字母。

1. **添加另一个模块**

   从 `random` 模块中导入 `choice()` 函数。这使你可以从字母列表中随机选取假字母。把这行代码输入到文件顶部附近，位于导入 Tkinter 函数的命令之下。

   ```python
   from tkinter import messagebox, simpledialog, Tk
   from random import choice
   ```

2. **加密**

   要加密消息，你需要准备一个假字母列表，用来插入到真实字母之间。下面的代码将循环遍历消息，每轮向 `encrypted_list` 中添加一个真实字母和一个假字母。

   > 这是一个假字母吗？

   ![](img/6b18a113f7aa9338e32f3ac1fa217987_141_2.png)

   ```python
   def encrypt(message):
       encrypted_list = []
       fake_letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'i', 'r', 's', 't', 'u', 'v']
       for counter in range(0, len(message)):
           encrypted_list.append(message[counter])
           encrypted_list.append(choice(fake_letters))
       new_message = ''.join(encrypted_list)
       return new_message
   ```

   在真实字母之间添加假字母。

   将消息中的一个字母添加到 `encrypted_list`。

   将一个假字母添加到 `encrypted_list`。

   将 `encrypted_list` 中的字母连接成一个字符串。

