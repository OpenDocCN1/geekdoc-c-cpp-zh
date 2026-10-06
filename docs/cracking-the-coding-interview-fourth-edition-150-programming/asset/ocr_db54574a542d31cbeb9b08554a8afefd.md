# Solutions to Chapter 19 | Moderate

19.6 Given an integer between 0 and 999,999, print an English phrase that describes the integer (eg, "One Thousand, Two Hundred and Thirty Four")

pg 89

# SOLUTION

This is not an especially challenging problem, but it is a long and tedious one. Your viewer is unlikely to ask to see every detail, but he / she will be interested in how you approach the problem.

```
public static String numstring(int num) {
    StringBuilder sb = new StringBuilder();

    // Count number of digits in num.
    int len = 1;
    while (Math.pow((double)10, (double)len) < num) {
        len++;
    }

    String[] wordarr1 = {"", "One", "Two", "Three", "Four \ "
                        "Five", "Six", "Seven", "Eight", "Nine"};
    String[] wordarr11 = {"", "Eleven", "Twelve", "Thirteen", 
                          "Fourteen", "Fifteen", "Sixteen", 
                          "Seventeen", "Eighteen", "Nineteen"};
    String[] wordarr10 = {"", "Twenty", "Thirty", "Forty ", 
                         "Fifty", "Sixty", "Seventy", "Eighty ", 
                         "Ninety "};

    String[] wordarr100 = {"", "Hundred", "Thousand"};
    int tmp;
    if (num == 0) {
        sb.append("Zero");
    } else {
        if (len > 3 && len % 2 == 0) {
            len++;
        }
        do {
            // greater than 999
            tmp = (num / (int)Math.pow((double)10, (double)len-2));
            // If tmp is 2 digit number and not a multiple of 10
            if (tmp / 10 == 1 && tmp%10 != 0) {
                sb.append(wordarr11[tmp % 10]);
            } else {
                sb.append(wordarr10[tmp / 10]);
            }
            sb.append(wordarr1[tmp % 10]);
        } while (len > 3);
        // ... logic continues in image
```