```
```java
154        removedColumns.clear();
155        });
156    tableMenu.add(showColumnsItem);
157
158    JMenuItem hideRowsItem = new JMenuItem("Hide Rows");
159    hideRowsItem.addActionListener(event ->
160    {
161        int[] selected = table.getSelectedRows();
162        for (int i : selected)
163            removedRowIndices.add(table.convertRowIndexToModel(i));
164        sorter.setRowFilter(filter);
165    });
166    tableMenu.add(hideRowsItem);
167
168    JMenuItem showRowsItem = new JMenuItem("Show Rows");
169    showRowsItem.addActionListener(event ->
170    {
171        removedRowIndices.clear();
172        sorter.setRowFilter(filter);
173    });
174    tableMenu.add(showRowsItem);
175
176    JMenuItem printSelectionItem = new JMenuItem("Print Selection");
177    printSelectionItem.addActionListener(event ->
178    {
179        int[] selected = table.getSelectedRows();
180        System.out.println("Selected rows: " + Arrays.toString(selected));
181        selected = table.getSelectedColumns();
182        System.out.println("Selected columns: " + Arrays.toString(selected));
183    });
184    tableMenu.add(printSelectionItem);
185    }
186
187    private void updateCheckboxMenuItems()
188    {
189        rowsItem.setSelected(table.getRowSelectionAllowed());
190        columnsItem.setSelected(table.getColumnSelectionAllowed());
191        cellsItem.setSelected(table.getCellSelectionEnabled());
192    }
193 }
```
```

+   - **javax.swing.table.TableModel 1.2**
+     - Class `getColumnClass(int columnIndex)`
+       gets the class for the values in this column. This information is used for sorting and rendering.