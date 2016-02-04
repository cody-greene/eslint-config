### Usage
This package offers two [eslint config][] files:
- [lax.yml](lax.yml) only includes rules that help catch errors while promoting best practices
- [strict.yml](strict.yml) extends `lax.yml` by adding opinionated styling rules

> When installing this module manually: be sure to use `npm install cody-greene/eslint-config#vXXX`

To configure a project, add something like this to `package.json`:
```json
{
  "eslintConfig": {
    "root": true,
    "extends": "./node_modules/eslint-config/strict.yml",
    "env": {"browser": true, "commonjs": true, "es6": true},
    "ecmaFeatures": {
      "experimentalObjectRestSpread": true
    }
  },
  "devDependencies": {
    "eslint-config": "cody-greene/eslint-config#v1.0.0"
  }
}
```

> Once the project is configured, make sure the appropriate [eslint plugin][] is installed.

### Auto formatting
`eslint --fix <file>` will automatically fix several issues from the `strict.yml` ruleset, including:
```
array-bracket-spacing
eqeqeq
indent
no-multi-spaces
no-spaced-func
object-curly-spacing
quotes
semi
space-after-keywords
space-before-function-paren
space-return-throw-case
space-unary-ops
```

### Style rules
- [no-trailing-spaces](#no-trailing-spaces)<a name='no-trailing-spaces'></a> Remove any trailing whitespace (configure your editor to do this automatically)

- [eol-last](#eol-last)<a name='eol-last'></a> End files with a single newline character (configure your editor to do this automatically)

- [indent](#indent)<a name='indent'></a> Use soft tabs set to 2 spaces (editor config). And try to limit lines to 100 columns
> Why? Same line-length & indentation when looking at the editor, the terminal, or github

- [semi](#semi)<a name='semi'></a> Never use semicolons

- [quotes](#quotes)<a name='quotes'></a> Use `'single-quotes'` except when avoiding escape sequences e.g. an apostrophe

- [space-before-function-paren](#space-before-function-paren)<a name='space-before-function-paren'></a> Place 1 space before the arguments list of anonymous functions
```javascript
// bad
doSomething(function(err, res) {
  console.log(err, res)
})

// good
doSometing(function (err, res) {
  console.log(err, res)
})
```

- [no-space-func](#no-space-func)<a name='no-spaced-func'></a> Place no space between a function name the the arguments list

- [keyword-spacing](#keyword-spacing)<a name='keyword-spacing'></a> Place 1 space before the opening parenthesis in control statements.
```javascript
// bad
if(isJedi) {
  fight ()
}

// good
if (isJedi) {
  fight()
}
```

- [brace-style](#brace-style)<a name='brace-style'></a> Place 1 space before the leading brace. `else` & `if-else` should not be next to a closing brace.
```javascript
// bad
if (foo){
  bar()
}else
{
  baz()
}

// good
if (foo) {
  bar()
}
else {
  baz()
}

// exception: one-liners (good)
function test(){ return 'test' }
if (foo) bar()
else baz()
```

- [block-spacing](#block-spacing) <a name='block-spacing'></a> Do not pad your blocks with blank lines
```javascript
// bad
function bar() {

  console.log(foo)

}

// good
if (baz) {
  console.log(qux)
} else {
  console.log(foo)
}
```

- [space-in-parens](#space-in-parens) <a name='space-in-parens'></a> Do not add spaces inside parentheses
```javascript
// bad
function bar( foo ) {
  return foo + baz( qux )
}

// good
if (foo) {
  console.log(foo)
}
```

- [array-bracket-spacing](#array-bracket-spacing) <a name='array-bracket-spacing'></a> Do not add spaces inside brackets
```javascript
// bad
const foo = [ 1, 2, 3 ]
console.log(foo[ 0 ])

// good
const foo = [1, 2, 3]
console.log(foo[0])
```

- [operator-linebreak](#operator-linebreak)<a name='operator-linebreak'></a> When a statement is too long to fit on a single line, insert line breaks before operators
```javascript
// bad
if (someCondition ||
  otherCondition) {
}

// good
if (someCondition
  || otherCondition) {
}
```

- [func-style](#func-style)<a name='func-style'></a> Use function declarations instead of function expressions
```javascript
// bad
const test = function (){ return 'hello' }

// good
function test(){ return 'hello' }

// exception: arrow-functions
const test = () => 'hello'
```

- [no-sequences](#no-sequences)<a name='no-sequences'></a> Use one `var/let/const` declaration per variable
> Why? It's easier to add/remove variables without messing with commas

```javascript
// bad
const foo = 867
  , bar = 53
  , baz = 0.9

// good
const foo = 867
const bar = 53
const baz = 0.9
```

- [comments](#comments)<a name='comments'></a> Use `/** ... */` for multi-line jsdoc style comments
```javascript
/**
 * Post a new job for an active worker to execute
 * @example
 *   let redis = require('redis').createClient()
 *   // You may want to partially bind this:
 *   // enqueue = enqueue.bind(null, redis)
 *   enqueue(redis, {queue:'low', type:'ping'}, console.log)
 *   enqueue(redis, {queue:'hi', type:'ping', params: {
 *     foo: true,
 *     bar: 'baz'
 *   }}, console.log)
 * @param {RedisClient} redis
 * @param {string} opt.queue e.g. critical, high, low
 * @param {string} opt.type Name of the job handler
 * @param {object?} opt.params e.g. userid: '123' (may be null)
 * @param {number?} opt.time Delay the job until: epoch-time in milliseconds (default: no delay)
 * @param {function} done(err, id) Receives a unique job id if successful
 * @returns {boolean} false if redis command was added to offline queue
 */
function enqueue(redis, opt, done) {}
```

- [todo](#todo)<a name='todo'></a> Use `TODO` & `FIXME` to annotate problems
```javascript
class Calculator extends Abacus {
  constructor() {
    super()

    // TODO: total should be configurable by an options param
    this.total = 0
  }
}
```

- [naming](#naming)<a name='naming'></a> Avoid single letter variables. Be descriptive. Use PascalCase for classes and camelCase for everything else
```javascript
// bad
for (let i = 0; i < list.length; ++i) {
  let e = list[i]
  console.log(i, e)
}

// good
for (let index = 0; index < attendeeList.length; ++index) {
  let person = attendeeList[index]
  console.log(index, person)
}
```

[eslint config]: http://eslint.org/docs/rules
[eslint plugin]: http://eslint.org/docs/user-guide/integrations