# The ProductDB class

```
using System;
using System.ComponentModel;
using System.Data;
using System.Data.SqlClient;

namespace HalloweenServiceLibrary
{
    [DataObject]
    class ProductDB
    {
        [DataObjectMethod(DataObjectMethodType.Select)]
        public static Product GetProduct(string productID)
        {
            SqlConnection con = new SqlConnection(GetConnectionString());
            string sel = "SELECT * " +
                "FROM Products WHERE ProductID = '" + productID + "'";
            SqlCommand cmd = new SqlCommand(sel, con);
            con.Open();
            SqlDataReader rdr =
                cmd.ExecuteReader(CommandBehavior.CloseConnection);
            Product p = new Product();
            if (rdr.Read())
            {
                p.CategoryID = rdr["CategoryID"].ToString();
                p.Name = rdr["Name"].ToString();
                p.UnitPrice = Convert.ToDecimal(rdr["UnitPrice"]);
            }
            rdr.Close();
            return p;
        }

        private static string GetConnectionString()
        {
            return "Data Source=localhost\\sqlexpress;" +
                "Initial Catalog=Halloween;Integrated Security=True";
        }
    }
}
```