# 6 Loops 125

```
if(adults <= tkts)
    break;
else
    cout << "Error: Wrong number of
person\n";
}
    cost = adults*15 + (tkts-adults)*10;
    if(tkts > 3)
        cost *= 0.9;
    tot_cost += cost;
    rsvd_seats += tkts;
    if(rsvd_seats == SEATS)
        cout << "\nNot available seats. Income: "
 << tot_cost << "\n";
        return 0;
    break;
    case 2:
        cout << "\nFree seats: " << SEATS-rsvd_seats <<
 " Income: " << tot_cost << "\n" << "\n";n        break;
    case 3:
        return 0;
    default:
        cout << "\nWrong choice\n"
        break;
}
    return 0;
```

# THE do-while statement

Unlike the for and while statements where the expression is tested *before* the execution of the loop body, the do-while statement tests the controlling expression *after* each execution of the body. Therefore, a do-while loop is executed at least once. It has the form:

```
do
{
    /* block of statements (loop body) that is executed at least once and
then repeatedly executed as long as the value of exp is true. */
} while (exp);
```

The loop body is executed first, exp is evaluated. If it is false, the loop terminates. Otherwise, the loop body is executed again and exp is tested once. If it is false, the loop terminates. If not, the loop body is executed again. This process is repeated until exp becomes false.

+   * do-while statement must end with a ;