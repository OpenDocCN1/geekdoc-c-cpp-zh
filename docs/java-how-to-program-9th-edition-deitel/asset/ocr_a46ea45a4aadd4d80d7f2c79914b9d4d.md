```
47
48 // required setter
49 public void setLeftOperand( int value )
50 {
51     leftOperand = value;
52 } // end method setLeftOperand
53
54 // gets the rightOperand
55 public int getRightOperand()
56 {
57     return rightOperand;
58 } // end method getRightOperand
59
60 // required setter
61 public void setRightOperand( int value )
62 {
63     rightOperand = value;
64 } // end method setRightOperand
65
66 // gets the resultValue
67 public int getResult()
68 {
69     return result;
70 } // end method getResult
71
72 // required setter
73 public void setResult( int value )
74 {
75     result = value;
76 } // end method setResult
77
78 // gets the operationType
79 public String getOperationType()
80 {
81     return operationType;
82 } // end method getOperationType
83
84 // required setter
85 public void setOperationType( String value )
86 {
87     operationType = value;
88 } // end method setOperationType
89
90 // returns the left hand side of the equation as a String
91 public String getLeftHandSide()
92 {
93     return leftOperand + " " + operationType + " " + rightOperand;
94 } // end method getLeftHandSide
95
96 // returns the right hand side of the equation as a String
97 public String getRightHandSide()
98 {
```