```
$k = 0; //This is the index of array $a.
for ($j = 0; $j <= COLUMNS - 1; $j++) { //Iterate through columns
for ($i = 0; $i <= ROWS - 1; $i++) {
$b[$i][$j] = $a[$k];
$k++;
}
}
for ($i = 0; $i <= ROWS - 1; $i++) { //Iterate through rows
for ($j = 0; $j <= COLUMNS - 1; $j++) {
echo $b[$i][$j], "\t";
}
echo "\n";
}
?>
```

# ## 35.7 Review Questions: True/False

Choose **true** or **false** for each of the following statements.

+   1. Processing each row individually means that every row is processed separately, and the result of each row can then be used individually for further processing.

+   2. The following code fragment displays the word “Okay” when the sum of the elements of each column is less than 100.
+   ```
+   for ($i = 0; $i <= ROWS - 1; $i++) {
+       $sum = 0;
+       for ($j = 0; $j <= COLUMNS - 1; $j++) {
+           $sum += $a[$i][$j];
+       }
+   }
+   if ($sum < 100) echo "Okay";
+   ```

+   3. Processing each column individually means that every column is processed separately and the result of each column can be then used individually for further processing.

+   4. The following code fragment displays the sum of the elements of each column.
+   ```
+   $sum = 0;
+   for ($j = 0; $j <= COLUMNS - 1; $j++) {
+       for ($i = 0; $i <= ROWS - 1; $i++) {
+           $sum += $a[$i][$j];
+       }
+   }
+   ```