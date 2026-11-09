```
```python
# replace all instances negative words with stars matching the length of these words

negative_words = "bad kill haters"

def block(text):
    # split words into list of words
    for negative in negative_words.split():
        if negative in text:
            text = text.replace(negative, len(negative)*'*')
    return text

text = "haters kill love"
blocked_text = block(text)

print(f"Original text : {text}")
print(f"Blocked text : {blocked_text}")
```
```

Original text : haters kill love
Blocked text : ****** **** love

# Practice Problems

+   1. Palindrome is a word which reads the same forward as backward, such as Civic, Level, Mom, Noon and radar. Write a program that return true if the phrase is a palindrome.
+   2. Write a program that prints how many one-character repeats are there in a given text.
+   3. Write a program that generate random n length alphanumeric password.
+   4. Write a program to replace comma with dots in given string, such as “32,323,23” to “32.323.23”