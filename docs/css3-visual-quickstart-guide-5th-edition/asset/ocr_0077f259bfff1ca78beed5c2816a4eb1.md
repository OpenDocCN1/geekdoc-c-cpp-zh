Sometimes the exact syntax of the official CSS specification will be slightly different from the "sand-box" version created for a specific browser.

To avoid confusion and ensure forward compatibility of CSS code, each rendering engine has adopted its own prefix to use CSS properties that are unique to that browser. The prefixes for each browser are shown in Table 1.2.

These CSS extensions sometimes overlap and conflict when different browsers promote their own solutions. The good news is that due to the nature of CSS, you can include versions of each of the properties for individual browsers, so that the browser will use whichever version it suits

Throughout the book, I include browser extensions, when appropriate, that you can ensure the widest interoperability of your styles.

```
selector {-moz-property: value;
-webkit-property: value;
o-property: value;
ms-property: value;
property: value; }
```

+   Browser CSS extensions can all be included as available to ensure that the style is applied if available to a particular browser.

> Although you don't have to include a semicolon with last definition in a list, experience shows that adding this semicolon can prevent future headaches. For example, if you later decide to add a new definition to the rule and forget to put in the required semicolon before the addition, you may cause the rule to fail completely. What's worse, not only will that one definition will fail, but all the definitions in the rule won't be used.

> Most browser manufacturers drop an extension of a style within two releases after they adopt the official version. This practice allows designers to catch up before their style sheets stop working.

> Don't confuse the selector of an HTML tag with its attributes. In the following tag, for example, img is the selector, and src is an attribute:

```
<img src="picture.gif">
```

| Extension | Rendering Engine | Browser(s) | Example |
|---|---|---||
| -moz- | Mozilla | Firefox, Camino | -moz-border-radius |
| -ms- | Trident | Internet Explorer | -ms-layout-grid |
| -o- | Presto | Opera | -o-border-radius |
| -webkit- | Webkit | Chrome, Safari | -webkit-border-radius |