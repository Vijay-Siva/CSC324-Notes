# Racket  

Function call: 
  (<function> <argument> ...)
  
arity: the number of arguments that a function takes 
  - unary
  - binary
  - ternary
  ...
  
map: unary-function list -> list  
Applies the function f on each argument, and returns the result of each function call in a list.  
Reduction rule:  
  * (map \<f\> (list \<a\> \<b\> \<c\> ...))
  * -> (list (\<f\> \<a\>) (\<f\> \<b\>) (\<f\> \<c\>) ...)

apply: function list -> any   
Applies the function f on the given list where each element in the list is passed into f as a parameter in the given order.   
Reduction rule:
  * (apply f (list a b c ...))
  * -> (f a b c)
  
### Semantics versus Syntax  

In a principles of programming languagses course we care about how programming languages
behave, which is called the semantics (meaning), not how they look, which is called syntax.

## Semantics of Function Calls in Python, Java and Racket  

In these languages function calls are "eager" and "by value"  

Eager: \*All\* the argument expressions are evaluated from left to right. This happens before
the function starts.  

Example: Can f be defines so f(1/0) is not an error? No because 1/0 will always be evaluated before anything about f matters.  

* if, and or are not functions
  - they don't require that we evaluate each expression, for example if the first expression 
  is false in an and statement, the other expressions are not evaluated. A function always 
  evaluates 
  
