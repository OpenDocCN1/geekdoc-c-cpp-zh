bug is to properly sanitize the rendered JSON objects. Our goal here is to prevent string content of the object from being interpreted as HTML markup. We have already seen that this may be used to trick the browser into executing code provided by the attacker. The simplest solution is to replace special characters, like angle brackets, that delimit HTML tags with their unicode encodings in JavaScript. This will preserve their meaning in JavaScript, but will keep it from breaking HTML parsing. Similar to DOMPurify, you may want to use a robust, specialized library instead of rolling out your own solution.

is an example of a library in this space. The Company backtracker uses rendering, and it renders a JSON object. In this case, it also leads to a code injection vulnerability. We will fix the vulnerability by sanitizing the rendered JSON object. In this case, we will use the simple replacement technique. Let's take one more look at how we render the configuration.

```
```javascript
import express from 'express';
import { loadConfiguration, startServer } from 'snowpack';
import React from 'react';
import ReactDOMServer from 'react-dom/server.js';

const app = express();
app.set('view engine', 'ejs');

async function main() {
  const config = await loadConfiguration({}, 'snowpack.config.mjs');
  const devServer = await startServer({ config: config });
  const runtime = devServer.getServerRuntime();

  app.get('/new.html', async (req, res) => {
    const importedComponent = await runtime.importModule('/dist/NewBug.js');
    const reactComponent = importedComponent.exports.NewBug;

    const element = React.createElement(reactComponent, null);
    const markup = ReactDOMServer.renderToString(element);

    const config = {
      navigateToBug: req.query.mtb || true
    };

    res.render('new', { req, markup, config });
  });

  app.listen(8081);
}
```
```