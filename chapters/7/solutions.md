Boring Exercises

7.1  The following procedure does some redundant computation.

(define (gertrude wd)
  (se (if (vowel? (first wd)) 'an 'a)
      wd
      'is
      (if (vowel? (first wd)) 'an 'a)
      wd
      'is
      (if (vowel? (first wd)) 'an 'a)
      wd))

> (gertrude 'rose)
(A ROSE IS A ROSE IS A ROSE)

> (gertrude 'iguana)
(AN IGUANA IS AN IGUANA IS AN IGUANA)

Use let to avoid the redundant work.



(define (gertrude wd)
  (let ((article 'ben))
  (se article
      wd
      'is
      article
      wd
      'is
      article
      wd))
)


(define (vowel? c)
  (member? c 'aeiou))

(define (gertrude wd)
  (let ((article 
  
  (if (vowel? (first wd)) 'an 'a) 
  
  ))
  (se article
      wd
      'is
      article
      wd
      'is
      article
      wd))
)


7.2  Put in the missing parentheses:

> (let pi 3.14159
       pie 'lemon meringue
    se 'pi is pi 'but pie is pie)
(PI IS 3.14159 BUT PIE IS LEMON MERINGUE)

> (let ((pi 3.14159)
       (pie '(lemon meringue)))
    (se 'pi 'is pi 'but 'pie 'is pie))
(PI IS 3.14159 BUT PIE IS LEMON MERINGUE)

Real Exercises

7.3  The following program doesn't work. Why not? Fix it.

(define (superlative adjective word)
  (se (word adjective 'est) word))

It's supposed to work like this:

> (superlative 'dumb 'exercise)
(DUMBEST EXERCISE)

"exercise" gets substituted in for both words, including the word procedure. To fix, change word to:

```
(define (superlative adjective wd)
  (se (word adjective 'est) wd))
```



7.4  What does this procedure do? Explain how it manages to work.

(define (sum-square a b)
  (let ((+ *)
        (* +))
    (* (+ a a) (+ b b))))


big chalkboard defines the procedures "+" and "*." We'll define them as b+ and b*.
Within the scope of the function, we create local variables "+" and "*." We'll call them l+ and l*.
So the let maps l+ to b* and l* to b+.

The function resolves to (b+ (b* a a) (b* b b))