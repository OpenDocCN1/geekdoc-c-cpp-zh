access to it. Utilize the module this way:

```
const { formatDate} = require("./format-date");
console.log(formatDate(new Date(2017, 9, 13),
"dddd the Do"));
// → Friday the 13th
```

We can define require, in its most minimal form, like this:

```
require.cache = Object.create(null);
function require(name) {
  if (! (name in require.cache)) {
    let code = readFile(name);
    let module = {exports: {}};
    require.cache[name] = module;
    let wrapper = Function("require, exports, module", code);
    wrapper(require, module.exports, module);
  }
  return require.cache[name].exports;
}
```

In this code, readFile is a powered function that reads a file and sends back its contents as a string. Standard JavaScript does not offer such functionality, but several other JavaScript environments such as Node.js and the browser offers their unique ways of accessing files. The above example bluffs that readFile exists. To keep away from loading the same module several times, you need a store (cache) of already loaded modules. If called, it examines if the demanded module loads and, if not, it loads it. It requires reading the module’s code, enclosing it within a function and calling it. The layout of the ordinal package from earlier is a function and not an object. The CommonJS modules create an empty layout object using the module system for you to export, restore that with values by overwriting module.exports. Modules do this to export a single value instead of a layout object. By describing exports, require and module as parameters for the created enclosing function (and setting the right values while calling it), the loader ensures that these bindings are accessible within the module’s scope. Strings set to require is interpreted to a filename or web address vary in separate systems. When it starts with “./” or “../,” it is usually translated as relative to the existing module’s filename. So “./format-date” will be the file called format-date.js in the same directory.

If the name is not relative, Node.js will search for a package that is installed by that name.

Now, instead of writing your own INI file parser, you can utilize one from NPM.