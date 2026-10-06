# Solutions to Chapter 19 | Moderate

```
37  if (tmp > 0) {
38      sb.append(wordarr100[len / 2]);
39  }
40      num = num % (int)(Math.pow((double)10, (double)len-2));
41      len = len-2;
42  } else { // Number is less than 1000
43      tmp = num % 100;
44      if (tmp != 0) {
45          sb.append(wordarr1[tmp]);
46          sb.append(wordarr100[len / 2]);
47      }
48      tmp = num % 10;
49      if(tmp / 10 == 1 && tmp % 10 != 0) {
50          sb.append(wordarr11[tmp % 10]);
51      } else {
52          sb.append(wordarr10[tmp / 10]);
53          sb.append(wordarr1[tmp % 10]);
54      }
55      len = 0;
56  }
57  } while(len > 0);
58  
59  return sb.toString();
60 }
```