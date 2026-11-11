# Listing 4.8 (Continued)

```
```java
106    String urlString = "" + props.remove("url");
107    String contentType = "" + props.remove("Content-Type");
108    if (contentType.equals("multipart/form-data")) {
109    {
110        var generator = new Random();
111        String boundary = new BigInteger(256, generator).toString();
112        contentType += ";boundary=" + boundary;
113        props.replaceAll((k, v) ->
114            v.toString().startsWith("file:")
115                ? propsPath.getParent().resolve(Paths.get(v.toString().substring(7)))
116                : v);
117    }
118    String result = doPost(urlString, contentType, props);
119    System.out.println(result);
120    }
121
122    public static String doPost(String url, String contentType, Map<Object, Object> data)
123        throws IOException, URISyntaxException, InterruptedException
124    {
125        HttpClient client = HttpClient.newBuilder()
126            .followRedirects(HttpClient.Redirect.ALWAYS).build();
127
128        BodyPublisher publisher = null;
129        if (contentType.startsWith("multipart/form-data")) {
130        {
131            String boundary = contentType.substring(contentType.lastIndexOf('=') + 1);
132            publisher = MoreBodyPublishers.ofMimeMultipartData(data, boundary);
133        }
134        else if (contentType.equals("application/x-www-form-urlencoded")) {
135            publisher = MoreBodyPublishers.ofFormData(data);
136        else
137        {
138            contentType = "application/json";
139            publisher = MoreBodyPublishers.ofSimpleJSON(data);
140        }
141
142        HttpRequest request = HttpRequest.newBuilder()
143            .uri(new URI(url))
144            .header("Content-Type", contentType)
145            .POST(publisher)
146            .build();
147        HttpResponse<String> response
148            = client.send(request, HttpResponse.BodyHandlers.ofString());
149        return response.body();
150    }
151 }
```
```