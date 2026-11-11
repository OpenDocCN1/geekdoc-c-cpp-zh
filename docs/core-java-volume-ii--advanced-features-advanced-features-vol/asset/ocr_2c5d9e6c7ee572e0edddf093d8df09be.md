# Listing 5.4  *(Continued)*

```
```java
if (!rsmd.getColumnClassName(i).equals("java.lang.String"))
    tb.setEditable(false);

fields.add(tb);

gbc.gridx = 1;
gbc.anchor = GridBagConstraints.WEST;
add(tb, gbc);
}
}

/**
 * Shows a database row by populating all text fields with the column values.
 */
public void showRow(ResultSet rs)
{
    try
    {
        if (rs == null) return;
        for (int i = 1; i <= fields.size(); i++)
        {
            String field = rs == null ? "" : rs.getString(i);
            JTextField tb = fields.get(i - 1);
            tb.setText(field);
        }
    }
    catch (SQLException ex)
    {
        for (Throwable t : ex)
            t.printStackTrace();
    }
}

/**
 * Updates changed data into the current row of the row set.
 */
public void setRow(RowSet rs) throws SQLException
{
    for (int i = 1; i <= fields.size(); i++)
    {
        String field = rs.getString(i);
        JTextField tb = fields.get(i - 1);
        if (!field.equals(tb.getText()))
            rs.updateString(i, tb.getText());
    }
    rs.updateRow();
}
```
```