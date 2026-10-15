token stored in the browser. The print view page looks very similar to other pages, but there is one difference. It is implemented in pure JavaScript without React. The code in print.js file is very simple. It reads data about the bug from the query string. Then, the title, severity, and description fields are used to dynamically construct a simple HTML representation of the bug.

```
const container = document.getElementById("root");
const qs = new URLSearchParams(window.location.search);
const bug = {
  title: decodeURIComponent(qs.get("t")),
  severity: decodeURIComponent(qs.get("s")),
  description: decodeURIComponent(qs.get("d"))
}

container.innerHTML = "<h1>" + bug.title + "</h1>" +
  "<h3>" + bug.severity + "</h3>" +
  "<p>" + bug.description + "</p>";
```

This HTML markup is rendered by directly assigning it to the innerHTML property of the root container of the page. The query string is a DOM XSS source, and it can easily be manipulated by the attacker. The parameters are passed directly to innerHTML, a DOM XSS sink, without any data validation or sanitization.

![](bbox=[0.12, 0.62, 0.91, 0.84])