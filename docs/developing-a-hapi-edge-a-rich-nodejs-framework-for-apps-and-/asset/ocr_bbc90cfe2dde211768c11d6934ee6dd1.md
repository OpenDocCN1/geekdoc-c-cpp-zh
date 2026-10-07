# Reporters

Using coverage is a must when it comes to developing modules in the hapi ecosystem. All of the modules published under the hapijs organization demand 100% code coverage. Therefore, if you plan to contribute any changes or enhancements to these modules you must add tests for the changed code. There may be naysayers when come to code coverage, but it's the mechanism that has been chosen to help gauge code works. In addition to adding tests that cover every line and code path in a module, hapijs maintainers also review the tests and code to help ensure its accuracy. A person can cover a line with a test that checks a wrong assumption, engineers are ultimately responsible for checking the code and the tests.

# Reporters

Lab comes packed with numerous reporters as well as support for any custom reporters. The reporters have evolved over the years from feedback from the community. Currently, lab supports the following reporters.

+   - console - CLI output
- html - report to an html stream, pipe to a file
- json - JSON formatted report
- junit - JUnit XML format
- tap - TAP format
- lcov - lcov format
- clover - clover XML format
- custom

Previously, in the code coverage section, the 'console' and 'html' reporters were demonstrated as it relates to reporting coverage. However, the 'html' reporter does more, it also reports on the tests run and how long each took. An example of the 'html' reporter as it relates to individual tests is shown here: