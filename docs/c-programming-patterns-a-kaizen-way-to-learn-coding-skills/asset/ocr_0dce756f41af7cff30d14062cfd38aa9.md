<table>
<thead>
<tr><th colspan=7>Column level Repetitive Action</th></tr>
<tr><th rowspan=3>row</th><th colspan=6>lower_limit &lt;= col &lt;= upper_limit</th></tr>
<tr><th colspan=3>lower_limit</th><th colspan=3>upper_limit</th></tr>
<tr><th></th><th>1</th><th>2</th><th></th><th>1</th><th>2</th></tr>
</thead>
<tbody>
<tr><td>1</td><td>5</td><td>totalRows</td><td>totalRows +1 - 1</td><td>5</td><td>totalRows</td><td>totalRows +1 - 1</td></tr>
<tr><td>2</td><td>4</td><td>totalRows -1</td><td>totalRows +1 - 2</td><td>6</td><td>totalRows + 1</td><td>totalRows + 2 - 1</td></tr>
<tr><td>3</td><td>3</td><td>totalRows -2</td><td>totalRows +1 - 3</td><td>7</td><td>totalRows + 2</td><td>totalRows + 3 - 1</td></tr>
<tr><td>4</td><td>2</td><td>totalRows -3</td><td>totalRows +1 - 4</td><td>8</td><td>totalRows + 3</td><td>totalRows + 4 - 1</td></tr>
<tr><td>5</td><td>1</td><td>totalRows -4</td><td>totalRows +1 - 5</td><td>9</td><td>totalRows + 4</td><td>totalRows + 5 - 1</td></tr>
</tbody>
</table>

<table>
<thead>
<tr><th colspan=5>Column level Repetitive Action</th></tr>
<tr><th rowspan=3>row</th><th colspan=4>if-condition( lower_limit &lt;= col &lt;= upper_limit)</th></tr>
<tr><th colspan=2>lower_limit</th><th colspan=2>upper_limit</th></tr>
<tr><th>default</th><th>3</th><th>default</th><th>3</th></tr>
</thead>
<tbody>
<tr><td>1</td><td>5</td><td>totalRows +1 - row</td><td>5</td><td>totalRows + row - 1</td></tr>
<tr><td>2</td><td>4</td><td>totalRows +1 - row</td><td>6</td><td>totalRows + row - 1</td></tr>
<tr><td>3</td><td>3</td><td>totalRows +1 - row</td><td>7</td><td>totalRows + row - 1</td></tr>
<tr><td>4</td><td>2</td><td>totalRows +1 - row</td><td>8</td><td>totalRows + row - 1</td></tr>
<tr><td>5</td><td>1</td><td>totalRows +1 - row</td><td>9</td><td>totalRows + row - 1</td></tr>
</tbody>
</table>

The lower_limit & upper_limit are consistent for all the rows. It’s now generalised for any number of rows to print numeric value. So our if-condition becomes

<table>
<tbody>
<tr><th>if-condition</th><td>lower_limit &lt;=col&lt;= upper_limit</td></tr>
<tr><th>Mathematical expression</th><td>(totalRows +1 - row) &lt;= col &lt;= (totalRows + row - 1)</td></tr>
<tr><th>Syntax</th><td>if( col &gt;= ( ( totalRows - row ) + 1 ) &amp;&amp;<br>col &lt;= ( ( totalRows + row ) - 1 ) )</td></tr>
</tbody>
</table>

When the if-condition satisfied, it will print the row value at that position at a particular row or else will print space character. Since we know that the total maximum of 9 columns are needed to print the bottom of pattern. The for-loop condition is given as;

<table>
<tbody>
<tr><th>loop-condition</th><td>lower_limit &lt;=col&lt;= upper_limit</td></tr>
<tr><th>Mathematical expression</th><td>1&lt;= col &lt;= 9</td></tr>
<tr><th>Syntax</th><td>for( col = 1 ; col &lt;= 9 ; col++ )</td></tr>
</tbody>
</table>

The *upper_limit* of col variable of inner for-loop which is a **value 9** is required to be generalised.

The hard-coded values in logical condition makes program to be fail for different input values. Somehow, it has to be generalised using variables considered for program.