user_ans5). The answers are stored in variables as (ans1, ans2, ans3, ans4, ans5). These answers are compared to the real answers using if conditional. A counter score is incremented by 1 each time the user gets a correct answer and finally the counter is printed to see how many correct answers the user gets.

```
```python
# Game 2 - Math Quiz Game

print("This is a game where you find basic mathematical operations for 2 integer numbers n1 and n2 \n")
n1 = 8
n2 = 2

ans1 = n1 + n2
ans2 = n1 - n2
ans3 = n1 * n2
ans4 = n1 % n2

user_ans1 = int(input(f"{n1} + {n2} = "))
user_ans2 = int(input(f"{n1} - {n2} = "))
user_ans3 = int(input(f"{n1} * {n2} = "))
user_ans4 = int(input(f"{n1} % {n2} = "))
print()

score = 0

if ans1 == user_ans1:
    score += 1
if ans2 == user_ans2:
    score += 1
if ans3 == user_ans3:
    score += 1
if ans4 == user_ans4:
    score += 1

print(f"You have got {score} answers correct")
```
```