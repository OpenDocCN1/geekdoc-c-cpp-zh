```
```text
06/28/2022  03:43 PM    <DIR>          .
06/28/2022  03:43 PM    <DIR>          ..
06/28/2022  03:43 PM               600 .browserslistrc
06/28/2022  03:43 PM               274 .editorconfig
06/28/2022  03:43 PM               548 .gitignore
06/28/2022  03:43 PM    <DIR>          .vscode
06/28/2022  03:43 PM             2,926 angular.json
06/28/2022  03:43 PM             1,424 karma.conf.js
06/28/2022  03:43 PM    <DIR>          node_modules
06/28/2022  03:43 PM           810,217 package-lock.json
06/28/2022  03:43 PM             1,038 package.json
06/28/2022  03:43 PM             1,060 README.md
06/28/2022  03:43 PM    <DIR>          src
06/28/2022  03:43 PM               287 tsconfig.app.json
06/28/2022  03:43 PM               863 tsconfig.json
06/28/2022  03:43 PM               333 tsconfig.spec.json
                  11 File(s)        819,570 bytes
                   5 Dir(s)  1,235,352,477,696 bytes free
```
```

Type `code .` to open the project in VS Code. Once in VS Code, open the terminal and type `npm start` to start the application. Since this is the first time we are using the CLI for this project, it again asks if we want to share our usage data. I'll say yes. It then compiles the application and generates the application bundles.

```
```text
Local setting: enabled
Effective status: enabled
✔ Browser application bundle generation complete.

Initial Chunk Files | Names     | Raw Size
vendor.js           | vendor    | 1.73 MB
polyfills.js        | polyfills | 315.31 kB
styles.css, styles.js | styles   | 207.35 kB
main.js             | main      | 48.30 kB
runtime.js          | runtime   | 6.51 kB

                    | Initial Total | 2.29 MB

Build at: 2022-06-28T22:45:15.289Z - Hash: 32eb575df8bded9d - Time: 10304ms

** Angular Live Development Server is listening on localhost:4200, open your browser on http://localhost:4200/ **

✔ Compiled successfully.
```
```

Ctrl+click this link to open the application in the browser. And here it is, our new Angular application.