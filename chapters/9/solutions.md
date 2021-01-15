Real Exercises
9.4  The following program doesn't work. Why not? Fix it.

(define (who sent)
  (every describe '(pete roger john keith)))

(define (describe person)
  (se person sent))
It's supposed to work like this:

> (who '(sells out))
(pete sells out roger sells out john sells out keith sells out)

```
(define (who sent)
  (every (lambda (wd) (se wd sent)) '(pete roger john keith))
)
```

In each of the following exercises, write the procedure in terms of lambda and higher-order functions. Do not use named helper procedures. If you've read Part IV, don't use recursion, either.

9.5  Write prepend-every:

> (prepend-every 's '(he aid he aid))
(SHE SAID SHE SAID)

> (prepend-every 'anti '(dote pasto gone body))
(ANTIDOTE ANTIPASTO ANTIGONE ANTIBODY)

```
(define (prepend-every prefix sent)
    (every (lambda (wd) (word prefix wd)) sent)
)
```

9.6  Write a procedure sentence-version that takes a function f as its argument and returns a function g. f should take a single word as argument. g should take a sentence as argument and return the sentence formed by applying f to each word of that argument.

> ((sentence-version first) '(if i fell))
(I I F)

> ((sentence-version square) '(8 2 4 6))
(64 4 16 36)

(define (square num)
    (* num num)
)

```
(define (sentence-version f)
    (lambda (sent) (every f sent))
)
```

9.7  Write a procedure called letterwords that takes as its arguments a letter and a sentence. It returns a sentence containing only those words from the argument sentence that contain the argument letter:

> (letterwords 'o '(got to get you into my life))
(GOT TO YOU INTO)

```
(define (letterwords letter sent)
    (keep (lambda (wd) (member? letter wd)) sent)
)
```

9.8  Suppose we're writing a program to play hangman. In this game one player has to guess a secret word chosen by the other player, one letter at a time. You're going to write just one small part of this program: a procedure that takes as arguments the secret word and the letters guessed so far, returning the word in which the guessing progress is displayed by including all the guessed letters along with underscores for the not-yet-guessed ones:

> (hang 'potsticker 'etaoi)
_OT_TI__E_
Hint: You'll find it helpful to use the following procedure that determines how to display a single letter:

(define (hang-letter letter guesses)
  (if (member? letter guesses)
      letter
      '_)
)

```
(define (hang wd guesses)
    (every (lambda (letter) (hang-letter letter guesses)) wd)
)
```


9.9  Write a procedure common-words that takes two sentences as arguments and returns a sentence containing only those words that appear both in the first sentence and in the second sentence.

```
(define (common-words sent1 sent2)
    (keep (lambda (wd) (member? wd sent2)) sent1)
)
```


9.10  In Chapter 2 we used a function called appearances that returns the number of times its first argument appears as a member of its second argument. Implement appearances.

```
(define (appearances arg1 arg2)
    (accumulate +
        (every (lambda (item) 1)
            (keep (lambda (item2) (equal? arg1 item2)) arg2)
        )
    )
)
```

9.11  Write a procedure unabbrev that takes two sentences as arguments. It should return a sentence that's the same as the first sentence, except that any numbers in the original sentence should be replaced with words from the second sentence. A number 2 in the first sentence should be replaced with the second word of the second sentence, a 6 with the sixth word, and so on.

> (unabbrev '(john 1 wayne fred 4) '(bill hank kermit joey))
(JOHN BILL WAYNE FRED JOEY)

> (unabbrev '(i 3 4 tell 2) '(do you want to know a secret?))
(I WANT TO TELL YOU)

```
(define (unabbrev se1 se2)
    (every 
        (lambda (wd) 
            (if (number? wd)
             (item wd se2)
             wd
        )) 
    se1)
)
```

9.12  Write a procedure first-last whose argument will be a sentence. It should return a sentence containing only those words in the argument sentence whose first and last letters are the same:

> (first-last '(california ohio nebraska alabama alaska massachusetts))
(OHIO ALABAMA ALASKA)

```
(define (first-last se)
    (filter 
        (lambda (wd) (equal? (first wd) (last wd)))
    se)
)
```

9.13  Write a procedure compose that takes two functions f and g as arguments. It should return a new function, the composition of its input functions, which computes f(g(x)) when passed the argument x.

> ((compose sqrt abs) -25)
5

> (define second (compose first bf))

> (second '(higher order function))
ORDER

```
(define (compose f g)
  (lambda (x) (f (g x)))
)
```

9.14  Write a procedure substitute that takes three arguments, two words and a sentence. It should return a version of the sentence, but with every instance of the second word replaced with the first word:

> (substitute 'maybe 'yeah '(she loves you yeah yeah yeah))
(SHE LOVES YOU MAYBE MAYBE MAYBE)

```
(define (substitute wd1 wd2 se)
        (every 
            (lambda (wd) (if (equal? wd wd2) (word wd1) wd))
        se)
)
```

9.15  Many functions are applicable only to arguments in a certain domain and result in error messages if given arguments outside that domain. For example, sqrt may require a nonnegative argument in a version of Scheme that doesn't include complex numbers. (In any version of Scheme, sqrt will complain if its argument isn't a number at all!) Once a program gets an error message, it's impossible for that program to continue the computation.

Write a procedure type-check that takes as arguments a one-argument procedure f and a one-argument predicate procedure pred. Type-check should return a one-argument procedure that first applies pred to its argument; if that result is true, the procedure should return the value computed by applying f to the argument; if pred returns false, the new procedure should also return #f:

> (define safe-sqrt (type-check sqrt number?))

> (safe-sqrt 16)
4

> (safe-sqrt 'sarsaparilla)
#F

(define (type-check f pred)
    (lambda (x) (if (pred x) (f x) #f))
)

9.16  In the language APL, most arithmetic functions can be applied either to a number, with the usual result, or to a vector—the APL name for a sentence of numbers—in which case the result is a new vector in which each element is the result of applying the function to the corresponding element of the argument. For example, the function sqrt applied to 16 returns 4 as in Scheme, but sqrt can also be applied to a sentence such as (16 49) and it returns (4 7).

Write a procedure aplize that takes as its argument a one-argument procedure whose domain is numbers or words. It should return an APLized procedure that also accepts sentences:

> (define apl-sqrt (aplize sqrt))

> (apl-sqrt 36)
6

> (apl-sqrt '(1 100 25 16))
(1 10 5 4)

```
(define (aplize f)
    (lambda (se)
        (if (number? se)
            (f se)
            (every f se)
        )
    )
)
```

9.17  Write keep in terms of every and accumulate.

```
(define (keep3 f sent)

    (accumulate
        sentence
        (every (lambda (wd) (if (f wd) (word wd) '())) sent)
    )
)
```