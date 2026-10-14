If you’re using git, you’ll be happy to know that spago gives you a pre-populated .gitignore file.

We can build the project by running:

```
npx spago build
```

or we can build AND run the project by running:

```
npx spago run # should print out the <spaghetti-emoji>
```

# 4.1.4. A Second Project

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

# 4.2. Editor and Plugins

At the time of this writing, there are PureScript plug-ins for the following editors:

+   1. Atom
+   2. Emacs
+   3. Sublime
+   4. Vim
+   5. VSCode