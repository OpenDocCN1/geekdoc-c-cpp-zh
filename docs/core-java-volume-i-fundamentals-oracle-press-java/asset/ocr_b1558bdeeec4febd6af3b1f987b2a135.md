```
```java
91  * @param right the spacing to use to the right
92  * @return this object for further modification
93  */
94  public GBC setInsets(int top, int left, int bottom, int right)
95  {
96      this.insets = new Insets(top, left, bottom, right);
97      return this;
98  }
99
100 /**
101  * Sets the internal padding
102  * @param ipadx the internal padding in x-direction
103  * @param ipady the internal padding in y-direction
104  * @return this object for further modification
105  */
106 public GBC setIpad(int ipadx, int ipady)
107 {
108     this.ipadx = ipadx;
109     this.ipady = ipady;
110     return this;
111 }
112 }
```
```

# **java.awt.GridBagConstraints 1.0**

+   - `int gridx, gridy`  
+   specifies the starting column and row of the cell. The default is 0.
+   - `int gridwidth, gridheight`  
+   specifies the column and row extent of the cell. The default is 1.
+   - `double weightx, weighty`  
+   specifies the capacity of the cell to grow. The default is 0.
+   - `int anchor`