A parameter (@affiliate is included in the query which allows to pass in a specific affiliate id for the affiliate to search on. Also as per need the wizard can be used to create the stored procedure for.

5. Next, select the SQL Data Adapter again, and this time, select the "Generate Dataset..." link under the Properties window. From here one can create a Data Set called dsAffiliatePurchase and add an instance of it to the Web service Designer Surface.

6. Now, access the code behind for the Web service and create a Web Method that looks like this,

```
<WebMethod()> _
Public Function GetAffiliateDetail(ByVal AffiliateID As Integer) _
As dsAffiliatePurchase

SqlDataAdapter1.SelectCommand.Parameters.Item("@affiliate").Value = AffiliateID
SqlDataAdapter1.Fill(DsAffiliatePurchase1, "purchase")
GetAffiliateDetail = DsAffiliatePurchase1

End Function
```

# The working explanation

+   - Notice that the GetAffiliateDetail Web Method returns an instance of dsAffiliatePurchase. ADO.NET takes care of the details of serializing the Dataset into XML. The first line of code sets the @affiliate parameter to the value passed into the Web service by the consumer. The second line of code "fills" the instance of the dataset that was added to Designer Surface into the "purchase" table (which is just a name... in this case it does not have the actual structure of the "purchase" table that was named when it was dragged-and-dropped originally from the Server Explorer in step 4 above). The third line of code then sets the results in the dataset to the return value for the Web Method.
+   - When compiled and tested using Web service Help Page to enter the AffiliateID, one can see the values of the dataset passed back as serialized into XML.

# 23.4.3 Returning Dataset from Web Services

Below is the process description of how to create a webservice which returns a DataSet and a Client Which displays the DataSet in a Grid.

# Step 1 : Writing a Web service

Open a New WebService project say WebService1. Create a Stock Table on SQL Desktop Edition with the Following Fields Stock Code, Description, Price (any fields as per need), and Add some dummy data.