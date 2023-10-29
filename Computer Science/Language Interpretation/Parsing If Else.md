In our example of MonkeyLang, to facilitate [[Parsers|parsing]] an if/else condition, we essentially break this up into a fairly simple struct, at which point we can peek one tokens at a time to see what's coming next in order to decide what exactly we need to construct. This becomes clearer when viewing the following struct of the If/Else expression from our AST:
```go
type IfExpression struct {
	Token        token.Token  // The "if" token
	Condition    Expression
	Consequence  *BlockStatement
	Alternative  *BlockStatement
}
```
