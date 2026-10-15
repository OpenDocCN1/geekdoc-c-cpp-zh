or action may interpret URLs as data or even executable code. URLs that use data or JavaScript sudo protocols behave in this way, and they're often used by attackers. Preventing this requires parsing URLs and only allowing safe protocols such as HTTP or HTTPS. Let's take a look at the short code snippet that uses React to create an HTML paragraph. This snippet will allow us to see how React automatically applies HTML escaping when rendering content.

```
React.createElement("p", {}, "Just text");
```

We use the React.createElement method. We pass "p" as the type of the element we are creating, empty JavaScript object as props, and the "Just text" as the content of the paragraph element.

```
<p>Just text</p>
```

The resulting element is rendered as a simple paragraph HTML tag with text content. Now, we use the same React.createElement method, but we pass a scripting payload as content.

```
React.createElement("p", {},
"<script>alert(document.domain)</script>");
```

The payload contains a malicious script tag with a call to the alert function. This time, the rendered HTML code looks different. The paragraph tag looks exactly the same as in the previous example, but the context has been processed by React.

```
<p>&lt;script&gt;alert(document.domain)&lt;/script&gt;</p>
```