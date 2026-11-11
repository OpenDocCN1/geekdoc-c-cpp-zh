```
```java
24     }
25   }
26
27   /**
28    * This frame contains the investment table.
29    */
30   class InvestmentTableFrame extends JFrame
31   {
32      public InvestmentTableFrame()
33      {
34         TableModel model = new InvestmentTableModel(30, 5, 10);
35         JTable table = new JTable(model);
36         add(new JScrollPane(table));
37         pack();
38      }
39   }
40
41   /**
42    * This table model computes the cell entries each time they are requested. The table contents
43    * shows the growth of an investment for a number of years under different interest rates.
44    */
45   class InvestmentTableModel extends AbstractTableModel
46   {
47      private static double INITIAL_BALANCE = 100000.0;
48
49      private int years;
50      private int minRate;
51      private int maxRate;
52
53      /**
54       * Constructs an investment table model.
55       * @param y the number of years
56       * @param r1 the lowest interest rate to tabulate
57       * @param r2 the highest interest rate to tabulate
58       */
59      public InvestmentTableModel(int y, int r1, int r2)
60      {
61         years = y;
62         minRate = r1;
63         maxRate = r2;
64      }
65
66      public int getRowCount()
67      {
68         return years;
69      }
70   }
71
```
```