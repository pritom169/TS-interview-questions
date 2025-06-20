## What is the difference between JS and TS?

JS is natively executed inside the browser. That means any other language can not be executed.
The TS code needs to be transpiled into JS code, and only then it cane be executed inside the brower.

TS is not a seperate language. It has been built on top of Javascript. All the features of JS like
variables, arrays, classes, functions, all this stuff exists in TS.

When developing an application it, we have to run the application and if there are any errors, we would
have got it in runtime. Because TS provides type safety, we can catch the error much faster and we can
get the error in compiling time.

## Does TS improve our code out of the box?

Not exactly. We need to enable strict compiler options (strict: true).
