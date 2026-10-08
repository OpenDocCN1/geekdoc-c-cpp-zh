```
char ch3 = 0;
Distribution dd;

if (is >> ch1 >> dd.year
    >> ch2 >> dd.young >> dd.middle >> dd.old
    >> ch3) {
    if (ch1!='(' || ch2!=':' || ch3!=')') {
        is.clear(ios_base::failbit);
        return is;
    }
} 
else
    return is;
d = dd;
return is;
}
```

This is a straightforward application of the ideas from Chapter 10. If this code isn’t clear to you, please review that chapter. We didn’t need to define a Distribution type and a >> operator. However, it simplifies the code compared to a brute-force approach of “just read the numbers and graph them.” Our use of Distribution splits the code up into logical parts to help comprehension and debugging. Don’t be shy about introducing types “just to make the code clearer.” We define classes to make the code correspond more directly to the way we think about the concepts in our code. Doing so even for “small” concepts that are used only very locally in our code, such as a line of data representing the age distribution for a year, can be most helpful.

Given Distribution, the read loop becomes

```
string file_name = "japanese-age-data.txt";
ifstream ifs (file_name);
if (!ifs) error("can't open ",file_name);

// ...

for (Distribution d; ifs>>d;) {
    if (d.year<base_year|| end_year<d.year)
        error("year out of range");
    if (d.young+d.middle+d.old != 100)
        error("percentages don't add up");
    // ...
}
```