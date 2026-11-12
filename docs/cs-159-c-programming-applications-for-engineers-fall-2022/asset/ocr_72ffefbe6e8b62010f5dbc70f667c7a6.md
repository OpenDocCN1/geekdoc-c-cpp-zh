| Misapplication of switch: | Improvement by reducing number of cases: |
| :--- | :--- |
| switch(score) {
    case 100:
    case 99:
    case 98:
    case 97:
    case 96:
    case 95:
    case 94:
    case 93:
    case 92:
    case 91:
    case 90: grade = 'A';
        break;
    case 89:
    case 88: | switch(score / 10) {
    case 10: score = 'A';
        break;
    case 9: score = 'B';
        break;
    case 8: score = 'C';
        break;
    case 7: score = 'D';
        break;
    case 6: score = 'F';
        break;
    default: score = 'F';
} |

# Reminder:

+   * There is a natural temptation to only and always make use of the if/else with for all selection needs.
+   * Consider whether the use of a switch or a conditional expression might be a better choice in some situations. The result may be shorter and more readable logic.