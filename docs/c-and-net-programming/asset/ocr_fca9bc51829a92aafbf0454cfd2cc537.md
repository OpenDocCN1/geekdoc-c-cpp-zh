# 3. Using WSDL generated proxy class

In this method a Proxy class for the web service is generated and this proxy class is used further. This method is more type safe and less error prone as once the proxy class generated, it handles all the SOAP messages, serialization and ensure that all the problems are dealt at the compile time instead of runtime. To use this service, there is a need to do "Add Web reference" and add the webservice reference. Alternatively WSDL.exe, a command line tool, can also be used to generate the proxy classes and use these classes. "Add web Reference" is also using the same WSDL.exe to generate the proxy classes.

# 2. Writing code to use the proxy class to perform the operations, the proxy class will then communicate to the web service using SOAP and get back the results to us.

```
protected void Button1_Click(object sender, EventArgs e)
{
    if (txtn1.Text != string.Empty
    && txtn2.Text != string.Empty)
    {
        try
        {
            int n1 = Convert.ToInt32(txtn1.Text);
            int n2 = Convert.ToInt32(txtn2.Text);

            ArithmeticService.Service service = new ArithmeticService.Service();

            Label1.Text = "Addition " + service.Add(n1, n2).ToString();
            Label2.Text = "Difference " + service.Subtract(n1, n2).ToString();
            Label3.Text = "Multiplication " + service.Multiply(n1, n2).ToString();
        }
        catch(Exception)
        {
            throw;
        }
    }
}
```

# 3. Running the website

# 23.4 Passing and Returning DataSets from Web Services

# 23.4.1 ADO .NET DataSets

AU : May-18, Dec.-18

+   - With .NET, one can easily couple Web Services with .NET's new data services to provide a powerful data delivery mechanism that works over the Web, making it