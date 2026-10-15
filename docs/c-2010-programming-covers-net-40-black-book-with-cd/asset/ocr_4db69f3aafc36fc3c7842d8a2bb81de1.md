```
var Number1 = document.getElementById("Number1").value;
var Number2 = document.getElementById("Number2").value;
var service = new tempuri.org.OperationService();
service.Subtract(parseFloat(Number1), parseFloat(Number2), onSuccess, null, null);
}
function callMul() {
var Number1 = document.getElementById("Number1").value;
var Number2 = document.getElementById("Number2").value;
var service = new tempuri.org.OperationService();
service.Multiply(parseFloat(Number1), parseFloat(Number2), onSuccess, null, null);
}
function callDiv() {
var Number1 = document.getElementById("Number1").value;
var Number2 = document.getElementById("Number2").value;
var service = new tempuri.org.OperationService();
service.Divide(parseFloat(Number1), parseFloat(Number2), onSuccess, null, null);
}
function onSuccess(result) {
document.getElementById("result").value = result;
}
</script>
</asp:Content>
```

The design view of the Default.aspx page appears, as shown in Figure 19.45:

![](bbox=[0.18, 0.46, 0.81, 0.79])

Figure 19.45: Showing the Design View of the Default.aspx File

+   2. Set the Default.aspx file of the MyAjaxEnableWCFService website as your home page.

+   3. Press the F5 key or select the Debug→Start Debugging option from the menu bar to run the application. The output of the MyAjaxEnableWCFService website appears, as shown in Figure 19.46: