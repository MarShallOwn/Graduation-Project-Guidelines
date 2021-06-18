# Graduation Project Guidelines

Writing readable code is an art and following style guides is one way of ensuring our code is always clean, readable and consistent. Language specific style guides exist but general coding standards apply to all programming languages. These are not to be blindly followed; This Guideline will be updated frequently so keep an eye on it and strive to understand these and ask when in doubt.

**General**

our code should contain
- Flexibility
- Scalability
- Usability
- should be Loosely Coupled

**Naming**
- Use `PascalCase` for classes, `lowerCamelCase` for variables and functions, `SCREAMING_SNAKE_CASE` for constants, `_singleLeadingUnderscore` for private variables and functions.
```
// Example using Javascript

// lowerCamelCase for variables
let studentGrade = 100;
let getStudentGrade = () => {
    return 50;
}

// PascalCase for classes
class Student {
    constructor() {...}
}

const SECRET_KEY = 'saldkjasldkjasldkajsdoiamdadjasojdaodmasdjasod'
```
- Make use of meaningful variable names. Avoid abbreviations.
- Avoid object types in names (`user_array`, `email_method`, `CalculatorClass`, `ReportModule`).
- Name the enumeration parameter the singular of the collection. e.g when looping over a collection of books, say 'for book in books' **and not** 'for b in books'. It’s clearer this way.
```
// Example using Javascript

// Array of names
const names = ['Marwan', 'Moustafa', 'Mark', 'Abdo'];

// do a for each loop on the array
// that gets each element in the array and prints it
for(const name of names){
    console.log(name);
}
```
- Name variables, methods, and classes to reveal intent. Intent describes the function of the class, method or variable. A typical example is if we were describing a class method to sort a collection by a certain parameter. It’s preferred to define this as `obj.sort_by(param)`. It makes code more readable and require less documentation.

**Formatting**
- Break long lines after 80 characters.
- Delete trailing whitespace.

For Example
```
It is extra spaces (and tabs) at the end of line      
                                                 ^^^^^ here
```
- Don't include spaces after `(`, `[` or before `]`, `)`.

Prefered Way :heavy_check_mark:
```
// Example using Javascript

const array = [1, 2, 3, 4, 5];
```
Not Prefered Way :x:
```
// Example using Javascript

const array = [ 1, 2, 3, 4, 5 ];
```
- Don't misspell.
- Do not leave commented out code within production code.
- If you break up an argument list, keep the arguments on their own lines and closing parenthesis on its own line. [Example 1](https://github.com/andela/code-review-guidelines/tree/master/style/ruby/sample.rb#L2), [Example 2](https://github.com/andela/code-review-guidelines/tree/master/style/ruby/sample.rb#L10).
- If you break up a hash/dictionary/associative array, keep the elements on their own lines and closing curly brace on its own line.
- Indent continued lines two spaces.
- Indent private methods equal to public methods.
- If you break up a chain of method invocations, keep each method invocation on its own line. Place the `.` at the end of each line, except the last. Example.
- Use 2 space indentation (no tabs) or indentation specific to your stack.
- Use an empty line between methods or the required number of spaces specified in the respective style guide.
- Use empty lines around multi-line blocks.
- Use spaces around operators, except for unary operators, such as `!`.
- Use spaces after commas, after colons and semicolons, around `{` and before `}`.
- Use [Unix-style line endings](http://unix.stackexchange.com/questions/23903/should-i-end-my-text-script-files-with-a-newline) (\n).
- [Use uppercase for SQL keywords and lowercase for SQL identifiers](http://www.postgresql.org/docs/9.2/static/sql-syntax-lexical.html#SQL-SYNTAX-IDENTIFIERS).

**Code Organization**
- Ensure to always take advantage of inbuilt language functionality like packages, modules etc. to organise the different parts of your code.
- Order methods so that caller methods are earlier in the file than the methods they call.

Prefered Way :heavy_check_mark:
```
// Example using Javascript

// caller function above called function
function callerFunction() {
    calledFunction();
}

// called function below caller function
function calledFunction() {
    console.log('called function should be below caller function')
}
```
Not Prefered Way :x:
```
// Example using Javascript

// called function above called function
function calledFunction() {
    console.log('called function should be below caller function')
}

// caller function below called function
function callerFunction() {
    calledFunction();
}
```
- Order methods so that methods are as close as possible to other methods they call.
```
// Example using Javascript

// caller and called functions are close to each other in order
function login(email, password) {
    getUser(email, password);
}

function getUser(email, password) {
    return users.find(user => user.email === email);
}
```

For language specific style guides, see below.

**Python**

See [PEP-8 Style Guide](https://www.python.org/dev/peps/pep-0008/).

**JavaScript**

[Airbnb Javascript Style Guide](https://github.com/airbnb/javascript) is preferred. In addition to that, take note of the following general pointers.

- Prefer ES6 classes over prototypes.
- Use strict equality checks (`===` and `!==`) except when comparing against (null or undefined).
- Prefer [arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) `=>`, over the function keyword except when defining classes or methods. 
_Note: ES6 Arrow function does not have its own bindings to `this` or `super` keywords._
```
// this will work using normal function
// but won't work if using ES6 Arrow function
let nodevember = {
  numOfAttendees: 0,
  incrementNumOfAttendees: function() {
    this.numOfAttendees++;
  }
  // other properties
};

$('.add-attendee-btn').on('click', nodevember.incrementNumOfAttendees.bind(nodevember));
```
- Use semicolons at the end of each statement.
- Prefer single quotes.
- Prefer [template strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings) over string concatenation.

Prefered `template strings` :heavy_check_mark:
```
const firstname = 'Marwan';
const lastname = 'Samih';

const fullname = `${firstname} ${lastname}`
console.log(fullname) // 'Marwan Samih'
```
Not Prefered `concatenation` :x:
```
const firstname = 'Marwan';
const lastname = ' Samih';

const fullname = firstname.concat(lastname);
console.log(fullname) // 'Marwan Samih'
```
- Prefer promises over callbacks.
- Prefer array functions like `map` and `forEach` over for loops.
```
const names = ['Marwan', 'Moustafa', 'Mark', 'Abdo'];

// Prefered
names.map(name => console.log(name));
// OR
names.forEach(name => console.log(name));

// Not Prefered 
for(let i = 0; i < names.length; i++){
    console.log(names[i]);
}
```
- Use `const` for declaring variables that will never be re-assigned, and let otherwise.
```
// will never be re-assigned
const PI = 3.14;
PI = 3.20; // Not Allowed Error

// can be re-assigned
let circleArea = 78.54;
circleArea = 100; // Allowed
```
- Avoid `var` to declare variables, use `let` where applicable.

Prefered `let` :heavy_check_mark:
```
let username = "MarShallOwn";
```
Not Prefered `var` :x:
```
// Example using Javascript

var username = "MarShallOwn";
```

**PHP**

We should ensure that there is strict adherence to the [PSR-2 Coding Style Guide](http://www.php-fig.org/psr/psr-2/).

**Java**

We should ensure that all Java Code follows the [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html).
