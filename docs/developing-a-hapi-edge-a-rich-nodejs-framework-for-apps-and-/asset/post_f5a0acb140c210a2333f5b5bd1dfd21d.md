
Next you can see our code example for doing the same thing. Notice that true and exist are functions in code.

```
expect(foo).to.exist();
expect(bar).to.be.true();
```

In addition to the inconsistencies described earlier, we wanted an assertion library that was small, simple, and intuitive. lab was stripped out that was dealing with plugins, extensions, and the overhead of supporting testing the browser. This resulted in much of the functionality we needed, but it resulted in about 300 lines that is trivial to read and understand.

Finally, code allowed deeper integration between the test runner and the assertion library. This allowed us to get total assertion counts to measure the tests' comprehensive and to verify that every assertion created is indeed executed.

Lab has over other ways as well. For example, transpiler support has been added to support CoffeeScript or JSX code. Additionally, lab now has support baked in, so that requests to hapi follow the same coding style. This has been useful for developers to know ahead of time if they are violating any style rules ahead of asking for a commit to be merged. One of the drawbacks of lab, however, is that it's designed and runs only on the server at this point. However, this will likely change as its popularity grows and more developers desire to use it for client-side testing.

## Installing lab

Lab may be useful to install globally in your environment. Similarly to other node.js modules, the installation of lab can be accomplished using npm. This is shown below.

```
$ npm install -g lab
```

While you can install lab globally, you don't need to. Instead, all of the hapi core modules include lab in the devDependencies section of the package.json. Any recent version of lab is fine to install globally and locally, as the two won't conflict when running tests. The next example shows how to install lab only locally and save it to the devDependencies section of the package.json.

```
$ npm install lab --save-dev
```

After you have installed lab you should verify that it's working correctly. If installed globally, lab will be available in the PATH environment variable. Otherwise, you will need to run the lab binary from the node_modules/.bin folder. To verify a global lab install, simply run lab -h. If you want to verify a local install, then you need to run node ./node_modules/.bin/lab -h. You should get the help page for lab.

As an aside, it may be helpful to auto-update the PATH when navigating into a folder with children node_modules/.bin folders. This will make local binaries runnable the same way as global binaries.

## Installing code

Similar to how lab was installed, you should also install code. Remember, lab doesn't have a built-in assert library that is included out-of-the-box. Therefore, you should use code, chai, or any of the other modules that you prefer. You can again, run npm install code --save-dev to save this in your package.json file or add it in manually.

## Writing a sample test

All tests should be located in a test folder within the root of your project. This is a pattern that is nearly ubiquitous in the Node.js community. How you choose to name your test files is up to you, there isn't an established naming convention across the board. However, a pattern that is used throughout the modules in the hapi organization is to name each test file the same as the corresponding module that it's responsible for testing. For the purposes of this exercise, create a file in test named index.js. Populate index.js with the code below.

```
var Code = require('code');
var Lab = require('lab');

var lab = exports.lab = Lab.script();

lab.test('lab exists', function (done) {
  Code.expect(lab).to.exist();
  done();
});
```

Simply type the command lab in the root of the project to run the test above. The output will look like following:

$ lab

1 tests complete
Test duration: 5 ms
No global variable leaks detected

Hopefully that wasn't difficult or shocking. As you can see from the output, the time it takes to run the test is reported along with a default reporter for dot notations.

## Principles of lab

Let's take a look at the core lab principles to keep in mind.

### Always asynchronous

In the previous section, you saw what a simple lab test looks like. One of the defining characteristics of lab is that tests are always assumed to be asynchronous. Instead of inspecting the length of the arguments object and running tests differently that have an argument for done, all lab tests must receive a callback argument and execute it when the test is complete. If an argument wasn't expected by the test, then the test immediately fails with an explanation. For example, the test below:

```
// Load modules

var Code = require('code');
var Lab = require('lab');

var lab = exports.lab = Lab.script();

lab.test('lab exists', function () {
  Code.expect(lab).to.exist();
});
```

When we run lab we get the following output:

```
$ lab
```

Error: Function for test "lab exists" should take exactly one argument

Similarly, if an argument is accepted in the test function but isn't executed, an error will occur. However, this error will be a timeout for the test itself. We can have time-out by removing done() . This can be done by writing the following test.

```
var Code = require('code');
var Lab = require('lab');
```

The resulting output for this test will look as follows:

$ lab

Failed tests:
+ 1) lab exists
   Timed out (2000ms)

### Test scripts

Another assumption of lab is that the global object shouldn't be polluted with variables. Whereas other frameworks will attach describe to the global object, lab tries a different approach of isolating each test. Each of the test functions is only available on lab object that's returned by script().

### Safe globals

Lab takes a step further and checks the global object for new properties after running tests. This is usually a sign of a missing when declaring a variable. However, this feature can be disabled by passing -l or --leaks to the binary. Similarly, if there is a known global that should exist you can pass it as an argument to -I or --ignore. For example, if you want to ignore a property named foo, set on the global object, you would execute lab as:

```
$ lab --ignore foo
```

### Experiments

While lab tests can be made to look like mocha and jasmine behavior-BDD style tests, they can also be named entirely. Whereas BDD styles use describe and it, lab also offers the options to experiment and test instead. The functions describe and experiment are interchangeable, just as it and test are. The style you choose is entirely to you, and there isn't a wrong answer. One of the things is nice about using the experiments style, however, it does reinforce the notion that an engineer is creating the tests and there is some attempt to be scientific about them.

An experiment is useful for wrapping a group of similar tests. For example, if you are testing lab itself, you may write experiment tests that are wrapped in an experiment demonstrated below.

```
// Load modules
var Code = require('code');
var Lab = require('lab');

var lab = exports.lab = Lab.script();
lab.experiment('lab', function () {
  lab.test('exists', function (done) {
    Code.expect(lab).to.exist();
    done();
  });
lab.test('has properties', function (done) {
    Code.expect(Object.keys(lab)).to.not.have.length(0);
    done();
  });
});
```

Then if you run these tests in verbose mode, you will get the following:

```
$ lab -v
lab
1) exists (3 ms)
2) has properties (1 ms)
```
