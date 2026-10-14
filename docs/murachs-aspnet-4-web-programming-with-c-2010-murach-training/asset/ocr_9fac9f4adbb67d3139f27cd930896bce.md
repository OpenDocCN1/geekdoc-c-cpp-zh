# The CategoryDB.cs file

```
[DataObjectMethod(DataObjectMethodType.Delete)]
public static int DeleteCategory(Category category)
{
    SqlConnection con = new SqlConnection(GetConnectionString());
    string del = "DELETE FROM Categories "
        + "WHERE CategoryID = @CategoryID "
        + "AND ShortName = @ShortName "
        + "AND LongName = @LongName";
    SqlCommand cmd = new SqlCommand(del, con);
    cmd.Parameters.AddWithValue("CategoryID", category.CategoryID);
    cmd.Parameters.AddWithValue("ShortName", category.ShortName);
    cmd.Parameters.AddWithValue("LongName", category.LongName);
    con.Open();
    int i = cmd.ExecuteNonQuery();
    con.Close();
    return i;
}
```

```
[DataObjectMethod(DataObjectMethodType.Update)]
public static int UpdateCategory(Category original_Category, Category category)
{
    SqlConnection con = new SqlConnection(GetConnectionString());
    string up = "UPDATE Categories "
        + "SET ShortName = @ShortName, "
        + "LongName = @LongName "
        + "WHERE CategoryID = @original_CategoryID "
        + "AND ShortName = @original_ShortName "
        + "AND LongName = @original_LongName";
    SqlCommand cmd = new SqlCommand(up, con);
    cmd.Parameters.AddWithValue("ShortName", category.ShortName);
    cmd.Parameters.AddWithValue("LongName", category.LongName);
    cmd.Parameters.AddWithValue("original_CategoryID", original_Category.CategoryID);
    cmd.Parameters.AddWithValue("original_ShortName", original_Category.ShortName);
    cmd.Parameters.AddWithValue("original_LongName", original_Category.LongName);
    con.Open();
    int updateCount = cmd.ExecuteNonQuery();
    con.Close();
    return updateCount;
}
```