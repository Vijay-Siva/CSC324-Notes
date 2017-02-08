# Lambda Calculus

The following are equivalent  

```
((λ (x) x)(λ (y) y))
   (λ (y) y)
   (λ (z) z)
   (λ (x) x)
   ((λ (y) y)(λ (y) y))
   ((λ (y) (λ (x) x)) (λ (y) (y y))
```

Another example: ```(λ (x) (f x)) ≡ f)```

The Lambda Calculus has only unary lambda terms and no 'define' form,
but we will start with a slightly extended language of terms [and come back
and restrict ourselves more later]

The expressions in our language are defined by Structural Induction/Recursion:

* <identifier>
* (λ (<identifier> ...) <expression>)
* (<closure-expression> <argument-expression> ...)
* (define <identifier> <expression>)

The word identifier is the PL word for a "name". Names are things we can
compare, asking whether they are equal, but have no other properties. 

