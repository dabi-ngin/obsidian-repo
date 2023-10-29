Our implementation of MonkeyLang will include a rudimentary form of tree walking interpretation. This can be expressed as pseudo code like this:

```Go
func eval(node astNode) {
	if node is integerLiteral {
		return node.integerValue
	} else if node is booleanLiteral {
		return node.booleanValue
	} else if node is infixExpression {
		leftEvaluated := eval(node.left)
		rightEvaluated := eval(node.right)
		
		if node.Operator == "+" {
			return leftEvaluated + rightEvaluated
		} else if node.Operator == "-" {
			return leftEvaluated - rightEvaluated
		}
	}
}
```

As is shown here, our func `eval` is recursive over each left/right sub-node where they exist and returns out simple values where they are just values

When looking at out this causes us to evaluate prefix operators, the logic becomes wonderfully simple. We essentially just begin from the known position of sitting on a prefixExpression as our parser has already told us, and then can decide to evaluate the rightNode of our expression (whatever follows the prefixIdentifier) and apply some logical operation to it to return out the value based on whatever the right expression type is. 

e.g.
if our prefix is a bang `!` and our rightNode is an ast.BooleanExpression `false` 