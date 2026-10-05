```
const string ServerUrl = 
  "https://yourwebservice.azurewebsites.net/";
HttpClient client = null;
client = new HttpClient();
client.BaseAddress = new Uri(ServerUrl);
```