When [[Parsers|parsing]], in our example of MonkeyLang, a *function literal* is how we define functions: which parameters they have and what the function does. Function literals look this:
```
fn(x, y) {
	return x + y;
}
```
In order to achieve this, we'll need to iterate over our tokens, reading from the keyword `fn` forward to break down into the declaration, list of parameters, function name, and block statement defined within our curly braces.

The abstract structure of our function literal is as so:
`fn <parameters> <block statement>`
Given that we can have multiple parameters, these are essentially just going to be a comma separated list of the previous:
`(<parameter one>, <parameter two>, <parameter three>, ...)`
which can also be empty if a function has no arguments:
```
fn() {
	return foobar + barfoo;
}
```
And as in other languages, using a function literal as an argument to another function is possible too:
```
myFunc(x, y, fn(x, y), {return x > y});
```

parsing the parameters is essentially just peeking tokens one at a time to see if the next one is a comma or right parenthesis, if it is then we know we've build out list of identifiers and can tie things off nicely. empty list is also valid as functions can take no arguments

## Parsing Call Expressions
Call expressions are extremely simple:
`<expression>(<comma seperated expressions>)`
that's it.

Normal expression would be called with something like:
`add(2,3)`
within this example, the *add* is an identifier. Identifiers are expressions. The arguments 2 and 3 are expressions too - integer literals. But they don't have to be, the arguments are just a list of expressions:
`add(2 + 2, 3 * 3 * 3)`
That's valid, too. The first argument is the infix expression 2 + 2 and the second one is 3 * 3 * 3. So far, so good. Looking at the function that's being called, in this case the function is bound to the identifier add. The identifier add returns this function when it's evaluated. That means we could go straight to the source, skip the identifier and replace add with a function literal:
`fn(x, y) { x + y; }(2, 3)`
We can also use function literals as arguments:
`callsFunction(2, 3, fn(x, y) { x + y; });`
Using this we essentially walk across the tokens one after the other from the LPAREN token `(` to loop through while the next token is a `,` and then finish building our list of arguments once we find a RPAREN. If we don't find the right brace we just return out an empty slice nil
