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

## Modeling Booleans 

```
(define True (λ (x y) x))
#;(define (True x y) x)
(define False (λ (x y) y))
#;(define (False x y) y)
```

The main defining property of booleans is how conditional expressions react
to them.  
(define (If condition consequent alternative) ???)

```
We want this
(If True (λ (x) x) (λ (y) (y y)))
 to reduce to
(λ (x) x)
and this
(If False (λ (x) x) (λ (y) (y y)))
to reduce to
(λ (y) (y y))
```

So we can define 'If: by:
``` (define If (λ (condition consequent alternative)
                (condition consequent alternative))) 
```

## Modeling Natural Numbers 

One useful model of natural numbers in computation is to be able to express doing something
n times. 

Our model of a number will be a funcion that takes a unary function and composes it 
n times. i.e ``` (n f) = f∘f∘···∘f  ``` n times 

The identity operation for composition:f⁽⁰⁾ = I, where I ∘ g = g = g ∘ I.  
```
(define Zero (λ (f) (λ (x) x)))

; f⁽¹⁾ = f.
(define One (λ (f) (λ (x) (f x)))) ; Written this way for symmetry.

; f⁽²⁾ = f ∘ f.
(define Two (λ (f) (λ (x) (f (f x)))))
```





