# Listing 5.3 (Continued)

```
```java
93    PreparedStatement stat;
94    if (!author.equals("Any") && !publisher.equals("Any"))
95    {
96        stat = conn.prepareStatement(authorPublisherQuery);
97        stat.setString(1, author);
98        stat.setString(2, publisher);
99    }
100    else if (!author.equals("Any") && publisher.equals("Any"))
101    {
102        stat = conn.prepareStatement(authorQuery);
103        stat.setString(1, author);
104    }
105    else if (author.equals("Any") && !publisher.equals("Any"))
106    {
107        stat = conn.prepareStatement(publisherQuery);
108        stat.setString(1, publisher);
109    }
110    else
111        stat = conn.prepareStatement(allQuery);
112
113    try (ResultSet rs = stat.executeQuery())
114    {
115        while (rs.next())
116            System.out.println(rs.getString(1) + ", " + rs.getString(2));
117
118    }
119
120    /**
121     * Executes an update statement to change prices.
122     * @param conn the database connection
123     */
124    public static void changePrices(Connection conn) throws SQLException
125    {
126        String publisher = select("Publishers", publishers.subList(1, publishers.size()));
127        System.out.print("Change prices by: ");
128        double priceChange = in.nextDouble();
129        PreparedStatement stat = conn.prepareStatement(priceUpdate);
130        stat.setDouble(1, priceChange);
131        stat.setString(2, publisher);
132        int r = stat.executeUpdate();
133        System.out.println(r + " records updated.");
134    }
135
136    /**
137     * Asks the user to select a string.
```
```