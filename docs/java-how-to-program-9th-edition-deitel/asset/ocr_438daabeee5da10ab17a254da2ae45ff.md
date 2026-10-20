```
123     rowSet.populate( getAddresses.executeQuery() );
124     return rowSet;
125 } // end try
126 finally
127 {
128     connection.close(); // return this connection to pool
129 } // end finally
130 } // end method getAddresses
131 
132 // save a new address book entry
133 public String save() throws SQLException
134 {
135     // check whether dataSource was injected by the server
136     if ( dataSource == null )
137         throw new SQLException( "Unable to obtain DataSource" );
138 
139     // obtain a connection from the connection pool
140     Connection connection = dataSource.getConnection();
141 
142     // check whether connection was successful
143     if ( connection == null )
144         throw new SQLException( "Unable to connect to DataSource" );
145 
146     try
147     {
148         // create a PreparedStatement to insert a new address book entry
149         PreparedStatement addEntry =
150             connection.prepareStatement( "INSERT INTO ADDRESSES " +
151                 "(FIRSTNAME,LASTNAME,STREET,CITY,STATE,ZIP)" +
152                 "VALUES ( ?, ?, ?, ?, ?, ? )" );
153 
154         // specify the PreparedStatement's arguments
155         addEntry.setString( 1, getFirstName() );
156         addEntry.setString( 2, getLastName() );
157         addEntry.setString( 3, getStreet() );
158         addEntry.setString( 4, getCity() );
159         addEntry.setString( 5, getState() );
160         addEntry.setString( 6, getZipcode() );
161 
162         addEntry.executeUpdate(); // insert the entry
163         return "index"; // go back to index.xhtml page
164     } // end try
165     finally
166     {
167         connection.close(); // return this connection to pool
168     } // end finally
169 } // end method save
170 } // end class AddressBean
```

Fig. 30.6 | AddressBean interacts with a database to store and retrieve addresses. (Part 4 of 4.)

# Injecting the DataSource into Class AddressBean

A DataSource (package javax.sql) enables a web application to obtain a Connection to a database. Lines 26–27 use annotation @Resource to inject a DataSource object into the