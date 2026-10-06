text() private function returns the text for a given cell. If cell() returns a null pointer, the cell is empty, so we return an empty string.

```
QString Spreadsheet::formula(int row, int column) const {
  Cell *c = cell(row, column);
  if (c) {
    return c->formula();
  } else {
    return "";
  }
}
```

The formula() function returns the cell's formula. In many cases, the formula and the text are the same; for example, the formula "Hello" evaluates to the string "Hello", so if the user types "Hello" into a cell and presses Enter, that cell will show the text "Hello". But there are a few exceptions:

+   - If the formula is a number, it is interpreted as such. For example, the formula "1.50" evaluates to double value 1.5, which is rendered as a right-aligned "1.5" in the spreadsheet.

+   - If the formula starts with a single quote, the rest of the formula is interpreted as text. For example, the formula "12345" evaluates to the string "12345".

![](bbox=[0.058, 0.655, 0.895, 0.998])