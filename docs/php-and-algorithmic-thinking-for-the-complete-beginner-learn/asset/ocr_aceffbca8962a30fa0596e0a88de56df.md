| Procedure | Value of Variable min in Your Mind! |
|---|---|
| The first person comes by. He weighs 165 pounds. Keep his weight in your mind (imagine a variable in your mind named `min`.) | `min = 165` |
| The second person comes by. He weighs 170 pounds. He does not weigh less than the weight you are keeping in variable `min`, so you must ignore his weight. Variable `min` in your mind still contains the value 165. | `min = 165` |
| The third person comes by. He weighs 160 pounds, which is less than the weight you are keeping in variable `min`, so you must forget the previous value and keep the value 160 in variable `min`. | `min = 160` |
| The fourth person comes by. He weighs 180 pounds. He does not weigh less than the weight you are keeping in variable `min`, so you must ignore his weight. Variable `min` still contains the value 160. | `min = 160` |

When the procedure finishes, the variable `min` in your mind contains the weight of the lightest man!

Following are the flowchart and the corresponding PHP script that prompts the user to enter the weight of four people and then finds and displays the lightest weight.