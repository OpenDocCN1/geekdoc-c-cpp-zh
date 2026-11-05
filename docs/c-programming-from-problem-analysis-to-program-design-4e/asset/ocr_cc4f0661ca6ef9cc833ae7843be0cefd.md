```
```csharp
namespace DBExample
{
    public partial class DbGUI :Form
    {
        private OleDbConnection dbConn;    // Connection object
        private OleDbCommand dbCmd;        // Command object
        private OleDbDataReader dbReader;  // Data Reader object
        private Member aMember;
        private string sConnection;
        private string sql;

        public DbGUI()
        {
            InitializeComponent();
        }

        private void btnLoad_Click(object sender, EventArgs e)
        {
            try
            {
                // Construct an object of the OleDbConnection
                // class to store the connection string
                // representing the type of data provider
                // (database) and the source (actual db).
                sConnection =
                    "Provider=Microsoft.ACE.OLEDB.12.0;" +
                    "Data Source=member.accdb";
                dbConn = new OleDbConnection(sConnection);
                dbConn.Open();

                // Construct an object of the OleDbCommand
                // class to hold the SQL query. Tie the
                // OleDbCommand object to the OleDbConnection
                // object.
                sql = "SELECT * FROM memberTable ORDER " +
                    "BY LastName ASC, FirstName ASC;";
                dbCmd = new OleDbCommand();
                dbCmd.CommandText = sql;
                dbCmd.Connection = dbConn;

                // Create a dbReader object.
                dbReader = dbCmd.ExecuteReader();

                while (dbReader.Read())
                {
                    aMember = new Member
                        (dbReader["FirstName"].ToString(),
                        dbReader["LastName"].ToString());
                    this.lstBxMembers.Items.Add(aMember);
                }
                dbReader.Close();
                dbConn.Close();
            }
        }
    }
}
```
```