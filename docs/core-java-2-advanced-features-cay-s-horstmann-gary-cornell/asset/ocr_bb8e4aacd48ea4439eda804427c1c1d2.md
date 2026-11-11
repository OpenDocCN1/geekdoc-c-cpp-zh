# Listing 5.4 (Continued)

```
```java
225   props = new Properties();
226   try (InputStream in = Files.newInputStream(Paths.get("database.properties")))
227   {
228      props.load(in);
229   }
230   String drivers = props.getProperty("jdbc.drivers");
231   if (drivers != null) System.setProperty("jdbc.drivers", drivers);
232   }
233
234   /**
235    * Gets a connection from the properties specified in the file database.properties.
236    * @return the database connection
237    */
238   private Connection getConnection() throws SQLException
239   {
240      String url = props.getProperty("jdbc.url");
241      String username = props.getProperty("jdbc.username");
242      String password = props.getProperty("jdbc.password");
243
244      return DriverManager.getConnection(url, username, password);
245   }
246
247   /**
248    * This panel displays the contents of a result set.
249    */
250
251   class DataPanel extends JPanel
252   {
253      private java.util.List<JTextField> fields;
254
255      /**
256       * Constructs the data panel.
257       * @param rs the result set whose contents this panel displays
258       */
259
260      public DataPanel(RowSet rs) throws SQLException
261      {
262         fields = new ArrayList<>();
263         setLayout(new GridBagLayout());
264         GridBagConstraints gbc = new GridBagConstraints();
265         gbc.gridwidth = 1;
266         gbc.gridheight = 1;
267
268         ResultSetMetaData rsmd = rs.getMetaData();
269         for (int i = 1; i <= rsmd.getColumnCount(); i++)
```
```