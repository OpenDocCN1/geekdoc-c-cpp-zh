```
```python
37     elif choice == 2: #d10 roll
38         die = random.randint(1, 10)
39     elif choice == 3: #d100 roll
40         die = random.randint(1, 100)
41     elif choice == 4: #d4 roll
42         die = random.randint(1, 4)
43     elif choice == 5: #d8 roll
44         die = random.randint(1, 8)
45     elif choice == 6: #d12 roll
46         die = random.randint(1, 12)
47     elif choice == 7: #d20 roll
48         die = random.randint(1, 20)
49     else: #simple error message
50         print "Shouldn't be here. Invalid choice"
51     return die
52
53 def multiDie(dice_number, die_type):
54     """Add die rolls together, e.g. 2d6, 4d10, etc
55          ."""
56 #---- Initialize variables
57     final_roll = 0
58     val = 0
59
60     while val < dice_number:
61         final_roll += randomNumGen(die_type)
62         val += 1
63     return final_roll
64
65 def test():
66     """Test criteria to show script works."""
67
68     _1d6 = multiDie(1,1)    #1d6
69     print "1d6 = ", _1d6,
70     _2d6 = multiDie(2,1)    #2d6
71     print "\n2d6 = ", _2d6,
72     _3d6 = multiDie(3,1)    #3d6
73     print "\n3d6 = ", _3d6,
```
```