12. Given a wind chill, display its classification according to the following table:

| Wind Chill | Classification |
|---|---|
| 10°F or above | Not dangerous or unpleasant |
| −10°F or higher but less than 10°F | Unpleasant |
| −30°F or above but less than −10°F | Possible frostbite |
| −70°F or higher but below −30°F | Dangerous, frostbite likely |
| Less than −70°F | Flesh may freeze in half a minute |

# Section 5.5

For Exercises 1–6, describe the output produced.

```
1. for (int i = 0; i <= 3; i++)
       cout << i << " squared = " << i*i << endl;

2. for (int i = 5; i > 0; i--)
       cout << i << " squared = " << i*i << endl;

3. int k = 5;
   for (int i = k; i <= 5; i++)
   {
       cout << i + k << endl;
       k = 1;
   }

4. int s = 5;
   for (int i = s; i < 5; i++)
       cout << i + s << endl;
   cout << "***\n";

5. int s = 1;
   while (s <= 10)
   {
       cout << 2*s << endl;
       s *= 2;
   }

6. int s = 20;
   while (s/2 < 10)
   {
       cout << 2*s << endl;
       s /= 2;
   }
```

For Exercises 7–14, write C++ statements to do what is asked for.