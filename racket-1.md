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
  
## Tail Position, Tail Calls and Tail Recursion

``` 
(define (add-up n)
  (if (positive? n)
      (+ n
         ; This recursive call is not in tail position w.r.t. the addition.
         (add-up (sub1 n)))
      0))
```
The above algorithm, whether executes as algebraic manipulation of expressions or a call stack, takes O(n) space.   

(add-up 10) Builds up the expression (+ 10 (+ 9 (+ ...))), or 10 call frames.  

The algorithm below, except for the logarithmically growing numeric result, requires only O(1) space. The recursive
calls are in "tail position" wrt the function.  

Definition: an expression e₁ inside an expression e₂ is in tail position
  w.r.t. e₂ iff evaluating e₁ [assuming e₁ is evaluated] always produces the
  value of e₂ without having to examine the value of e₁.  
  
In other words, if e1 is evaluated then the rest of the expression can be removed first. In terms of a call stack
and a function call in tail posiition wrt a function body: the call frame representing the state of the function 
and waiting return can be replaced with the called function's stack frame instead of stacking it.  

```
(define (add-up′ n accumulator)
  
  (if
   
   ; The condition expression is not in tail position w.r.t. the whole conditional
   ;  expression [which is the function body]. The conditional is waiting to react
   ;  to the result of this expression.
   (positive? n)

   ; The branches of a conditional expression are in tail position w.r.t. the
   ;  conditional expression.
   ; In the Algebraic Stepper you can literally see the surrounding expression
   ;  disappear before this expression is evaluated.
   
   (add-up′
    ; The argument expressions are not tail position w.r.t. the function call to
    ;  ‘add-up′’. The function call operation is waiting for their values.
    ; Waiting after ‘(sub1 n)’: evaluation of the next argument expression.
    ; Waiting after ‘(+ n accumulator)’: passing argument values to ‘add-up′’.
    (sub1 n)
    (+ n accumulator))
   
   accumulator))
```  

Language implementations that don't consume extra memory for tail position evaluation are said to have "tail
call optimization." A recursive function where al recursice calls are in tail position wrt the function are
called tail recursive. 

```
(or #true 324)
```

The #true is not in tail position wrt the disjunction expression because its value still needs to be examined to
determine that it should be the value of the whole expression (i.e the context that it's in a disjunction)
vs e.g a conjunction needs to be remembered.  
The 324 is in tail position wrt the disjunction expression.  

If the compiler determines that the expression is equivalent to #true, so that the result of the #true doesn't
need to be examined at run-time, then the disjunction expression dissappears at compile time and the question 
of whether the #true is in tail position w.r.t to it dissappears as well. 
