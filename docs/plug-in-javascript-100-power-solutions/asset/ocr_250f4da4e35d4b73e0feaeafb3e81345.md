```
if (j < cclen)
{
    d = number[j] * 2
    chksum += d < 10 ? d : d - 9
}

if (chksum % 10 != 0) return false

var date = new Date()
date.setTime(date.getTime())

if (year.length == 4) year = year.substr(2, 2)

if (year > 50) return false
else if (year < (date.getFullYear() - 2000)) return false
else if ((date.getMonth() + 1) > month) return false
else return true
```