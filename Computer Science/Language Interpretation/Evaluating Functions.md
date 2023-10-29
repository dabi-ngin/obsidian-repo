Like other language structures, we also need to [[Evaluation|evaluate]] functions in order to meaningful represent the internals and how conditional flow should move in and out of them.

In our case, functions are represented as objects. We begin by looking at the result we got from our abstract syntax tree when [[Parsing Functions|parsing functions]]. 

One of the trickier parts of evaluating functions is ensuring that we don't overwrite the values bound to identifiers that exist outside of the context of the function call. Ignoring reference to pointers for the time being, we can walk around this problem by simply generating a new nested Environment which sits within the global environment that the runtime uses. This allows us to have a small microcosm which neatly encapsulated the values we want to store within our function. 

Depending on language implementation what is done with these values and how this interacts with global runtime environment is a design decision. In our case here, we're creating  LISP-esque language, so when we get around to writing some basic garbage collection we'll drop these values from memory once the context ends and tear down the inner environment itself such that it de-references the pointer towards an outer Environment (our global environment) and frees up the memory for future allocation.

