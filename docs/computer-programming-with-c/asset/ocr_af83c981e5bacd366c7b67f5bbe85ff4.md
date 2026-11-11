![](bbox=[0.204, 0.111, 0.767, 0.469])

We will be able to access the members `id`, `title`, `author`, and `price` for each of the Book objects by using a membership operator “.”. For example, the following statement will accept the members (`id`, `title`, `author`, and `price`) of object `b[0]` as input from the user:

```
```cpp
scanf("%d%s%s%f",&b[0].id,b[0].title,b[0].author,&b[0].price);
```
```

Since we have only taken the members of `b[0]` as input, the state of array `b` assuming input data as `{id=1, title="C++", author="Kunal", price=900}` is shown in the Figure 9.13.

Similarly, we can accept members of objects `b[1]` and `b[2]` as input from the user. Following `for` loop will accept the details for each of the Book objects `b[0]`, `b[1]`, and `b[2]` as input from the user because we have specified the range of loop variable `i` from 0 to 2.

![](bbox=[0.204, 0.714, 0.768, 0.917])