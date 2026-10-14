
```
mkdir /dev/purescript
```

Next, create the project directory:

```
cd /dev/purescript
mkdir fp-book # or some other name you like better
cd fp-book
```

Before we go further *make sure that you're in your project directory.*

Next, we are going to do the following to fully create our PureScript project:

+   1. Initialize the project for working with `npm` and `npx`.
+   2. Install `purescript` and `spago` (Locally).
+   3. Initialize the project for working with `git` (Optional). This is useful if you use VSCode.

## Initialize Project for `npm` and `npx`

To initialize your project so that we can install `npm` packages and use `npx` to run the compiler and build tool from inside your project, run:

```
npm init -y
```

This will create a file call `package.json`. This will keep track of any packages we install for both production and development. For example, we may install `uuid` and `uuid-validate` which are node `npm` packages that are required by the PureScript package `purescript-uuid`.

## Future-proofing

Since technology changes so quickly, new versions of libraries, compilers and tools can break code in this book. To guarantee that you're using the exact same version I used when I wrote this book, I will ask you to install `spago` and `purescript` using their explicit versions. You can choose to not do this, but then you'll be on your own regarding breaking changes in the compiler.

Don't worry that you're missing out on something just because you're using an older version of the compiler (circa 2020). The concepts that you'll learn here are universal and will be valuable for decades to come.

## Install `purescript` and `spago` into your Project

To locally install the PureScript compiler, `purescript` and the build tool, `spago`, run:

```
```bash
npm install --save-dev spago@0.20.0 purescript@0.14.1
```
```

or to live dangerously and install the latest versions run (remember, you’re on your own if you choose this):

```
```bash
npm install --save-dev spago purescript
```
```

Notice the `--save-dev` option. This will tell `npm` that these packages are only for development.

To verify that we have installed the compiler locally, we’ll use `npx` (NOTICE the `x`):

```
```bash
npx purs --version # should print out 0.14.1
```
```

`npx` looks in our local `node_modules` directory for `purs`, the name of the PureScript compiler, and then runs it passing all other command line Parameters to it. The parameter `--version` tells `purs` to print out it’s version.

To verify that we have installed the build tool locally, run:

```
```bash
npx spago version # should print out 0.20.0
```
```

## Initialize Project for `git` (Optional)

To prepare our project for version control using `git`, run:

```
```bash
git init # should print `Initialized empty Git repository in <dir>`
```
```

Although this is optional, I’d still recommend doing this.

## 4.1.3. Initialize PureScript Project

The final step is to initialize this project for building a PureScript program using `spago`:

```
```bash
npx spago init
```
```

If you’re curious to see everything that `spago` creates, you should take a look at the contents of your project directory:

```
```bash
ls -l
```
```

If you’re using git, you’ll be happy to know that spago gives you a pre-populated .gitignore file.

We can build the project by running:

```
npx spago build
```

or we can build AND run the project by running:

```
npx spago run # should print out the <spaghetti-emoji>
```

## 4.1.4. A Second Project

While this seems like a lot to do to get up and running, most of it was first-time configuration.

To start a second project involves:

```
# make project directory
mkdir /dev/purescript/second-project
# enter project
cd /dev/purescript/second-project
# initialize for using `npm` and `npx`
npm init -y
# add compiler and build tools to the project
npm install --save-dev spago@0.20.0 purescript@0.14.1
# initialize our `git` repo (Optional)
git init
# create a skeleton PureScript project
npx spago init
# build and run the skeleton project
npx spago run
```

## 4.2. Editor and Plugins

At the time of this writing, there are PureScript plug-ins for the following editors:

+   1. Atom
+   2. Emacs
+   3. Sublime
+   4. Vim
+   5. VSCode

![](img/8c0e9b687c62642e828ccb5481e11313_139_0.png)

If, in the future, this location changes due to some change in npm, you'll have to locate the PureScript compiler in node_modules and configure with the appropriate path.

Once properly configured, the editor will be able to compile when we save our code and give us error messages in a pop-up window when we hover our mouse over it:

![](img/8c0e9b687c62642e828ccb5481e11313_139_1.png)

## 4.2.3. Configure Editor

Use Ctrl-Shift-P on Windows/Linux or Cmd-Shift-P on the Mac to open the Command Pallete. Then type open settings:

![](img/8c0e9b687c62642e828ccb5481e11313_140_0.png)

Select `Preferences: Open Settings (JSON)` and you will now be editing your `settings.json`.

Place the following code in the JSON object:

```
```json
"[purescript]": {
    "editor.tabSize": 2
}
```
```

It doesn’t matter if you place it first, middle or last:

![](img/8c0e9b687c62642e828ccb5481e11313_140_1.png)

Make sure you save and close the file.

Next let’s add a Snippet for the Mathematical Symbol for the `forall` keyword.

Open up the `Command Palette` again and type `snippet`:

![](img/8c0e9b687c62642e828ccb5481e11313_140_2.png)

Select `Preferences: Configure User Snippets` and you get another menu:

![](img/8c0e9b687c62642e828ccb5481e11313_141_0.png)

If you already have Snippets file then choose it. Mine here is called javascript.json.code-snippets.

If this is your first time creating Snippets then choose New Global Snippets file... and name it something you'll remember:

![](img/8c0e9b687c62642e828ccb5481e11313_141_1.png)

You'll then be presented with your snippets JSON file:

```
{
  // Place your global snippets here. Each snippet is defined under a snippet name and has a scope, prefix, body and
  // description. Add comma separated ids of the languages where the snippet is applicable in the scope field. If scope
  // is left empty or omitted, the snippet gets applied to all languages. The prefix is what is
  // used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
  // $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders.
  // Placeholders with the same ids are connected.
  // Example:
  // "Print to console": {
  //   "scope": "javascript,typescript",
  //   "prefix": "log",
  //   "body": [
  //     "console.log('$1');",
  //     "$2"
  //   ],
  //   "description": "Log output to console"
  // }
}
```

Next add the following text to the end of the JSON object:

```
"Forall": {
  "scope": "purescript",
  "prefix": "fa",
  "body": "∀"
}
```

![](img/8c0e9b687c62642e828ccb5481e11313_142_0.png)

If you’re reading this as a PDF, then you can copy/paste from this book. If you’re reading this on paper, then you’ll need to type this code.

The easiest way to type `∀`, is to copy and paste it from the internet. Either Google for `unicode forall` or get the ForAll here.

![](img/8c0e9b687c62642e828ccb5481e11313_142_1.png)

Then select the `∀` and copy and paste it into the JSON file.

Make sure you save and close the file.

Once this is configured (you may have to restart VSCode), you can type `fa` followed by `Tab` and the `fa` will be replaced by `∀`. This is configured to only work when you’re editing `purescript` files.

And finally, I’d suggest installing the `One Dark Pro` extension. It’s the one I’ll use in the screenshots and it’s color scheme works well with PureScript and Haskell.

If you’d like to do this, then simply install the extension and then click on the `Set Color Theme` button:

![](img/8c0e9b687c62642e828ccb5481e11313_142_2.png)

You are now ready to start programming in PureScript.
