One of the critical portions of [[Evaluation|evaluation]] is the binding of values to identifiers. This is what actually allows variables to be used rather than just having a stateless machine that evaluates expressions

Suppose we've evaluated the following piece of code:
`let x = 5 * 5;`

Only adding support for evaluation isn't enough, we also need to ensure that x evaluates to 25 after the line is interpreted. 

binding is actually a pretty simple part of the evaluation cycle. All that really needs to be done at this point is evaluating expressions that would typically return a value, but when prefixed with a `let` statement we can then store this value in what is essentially a [[Hashmap|hashmap]] we just pass around in local memory [[Garbage Collection|garbage collection]] be damned.

Well, not actually, that's a very important topic in programming languages, but not for this note.

