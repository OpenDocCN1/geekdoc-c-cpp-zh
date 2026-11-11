```
~~~java
41 /**
42  * This table model computes the cell entries each time they are requested. The table contents
43  * shows the growth of an investment for a number of years under different interest rates.
44  */
45 class InvestmentTableModel extends AbstractTableModel
46 {
47    private static double INITIAL_BALANCE = 100000.0;
48
49    private int years;
50    private int minRate;
51    private int maxRate;
52
53    /**
54     * Constructs an investment table model.
55     * @param y the number of years
56     * @param r1 the lowest interest rate to tabulate
57     * @param r2 the highest interest rate to tabulate
58     */
59    public InvestmentTableModel(int y, int r1, int r2)
60    {
61       years = y;
62       minRate = r1;
63       maxRate = r2;
64    }
65
66    public int getRowCount()
67    {
68       return years;
69    }
70
71    public int getColumnCount()
72    {
73       return maxRate - minRate + 1;
74    }
75
76    public Object getValueAt(int r, int c)
77    {
78       double rate = (c + minRate) / 100.0;
79       int nperiods = r;
80       double futureBalance = INITIAL_BALANCE * Math.pow(1 + rate, nperiods);
81       return String.format("%.2f", futureBalance);
82    }
83
84    public String getColumnName(int c)
85    {
86       return (c + minRate) + "%";
87    }
88 }
~~~
```