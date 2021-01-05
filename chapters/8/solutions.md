Boring Exercises

8.1  What does Scheme return as the value of each of the following expressions? Figure it out for yourself before you try it on the computer.

> (every last '(algebra purple spaghetti tomato gnu))

'(a e i o u)

> (keep number? '(one two three four))

()

> (accumulate * '(6 7 13 0 9 42 17))

0

> (member? 'h (keep vowel? '(t h r o a t)))

#f

> (every square (keep even? '(87 4 7 12 0 5)))

(16 144)

> (accumulate word (keep vowel? (every first '(and i love her))))

ai

> ((repeated square 0) 25)

25

> (every (repeated bl 2) '(good day sunshine))

(go d sunshi)

8.2  Fill in the blanks in the following Scheme interactions:

> (______ vowel? 'birthday)
IA

keep

> (______ first '(golden slumbers))
(G S)

keep

> (______ '(golden slumbers))
GOLDEN

every

> (______ ______ '(little child))
(E D)

every last

> (______ ______ (______ ______ '(little child)))
ED

(accumulate word (every last '(little child)))

> (______ + '(2 3 4 5))
(2 3 4 5)

every

> (______ + '(2 3 4 5))
14

accumulate

8.3  Describe each of the following functions in English. Make sure to include a description of the domain and range of each function. Be as precise as possible; for example, "the argument must be a function of one numeric argument" is better than "the argument must be a function."

(define (f a)
  (keep even? a))

description: extracts only the even numbers and returns them as a word
domain: a word or a function that returns a word, where the word only contains numbers
range: a word that contains only even numbers or is empty

(define (g b)
  (every b '(blue jay way)))

description: applies the provided function to sentence '(blue jay way)
domain: a function that accepts a word as an argument
range: a sentence

(define (h c d)
  (c (c d)))

description: applies function "c" on "d" twice
domain: a function that accepts one or more paramters and a piece of data that is acceptable as a paramter to the function
range: any

(define (i e)
  (/ (accumulate + e) (count e)))

description: adds contents of sentence together and divides by number of items in the sentence
domain: a sentence of numbers
range: a number

accumulate

description: applies a function to a sentence, reducing down to a single value
domain: a function and a sentence. function takes two args and returns one value
range: any reduced value (ex. sentence -> word, word -> letter)

sqrt

description: performs square root math function on a number
domain: any number
range: any number

repeated

description: repeats a specified procedure a defined number of times
domain: a procedure and number of times to repeat that procedure
range: a procedure

(repeated sqrt 3)

description: a procedure that takes the square root of a number 3 times
domain: a number
range: a number

(repeated even? 2)

description: this is an error cuz even? accepts an integer and returns a bool, but if you apply it twice, your passing a bool into it when it expects an int
domain: 
range:

(repeated first 2)

description: applies first twice
domain: a sentence of words
range: a letter

(repeated (repeated bf 3) 2)

description: takes butfirst 6 times
domain: a word or sentence
range: a word or sentence

Real Exercises

Note: Writing helper procedures may be useful in solving some of these problems. If you read Part IV before this, do not use recursion in solving these problems; use higher order functions instead.

8.4  Write a procedure choose-beatles that takes a predicate function as its argument and returns a sentence of just those Beatles (John, Paul, George, and Ringo) that satisfy the predicate. For example:

(define (ends-vowel? wd) (vowel? (last wd)))

(define (even-count? wd) (even? (count wd)))

(define (choose-beatles predicate)
    (keep predicate '(John Paul George Ringo))
)

> (choose-beatles ends-vowel?)
(GEORGE RINGO)

> (choose-beatles even-count?)
(JOHN PAUL GEORGE)

8.5  Write a procedure transform-beatles that takes a procedure as an argument, applies it to each of the Beatles, and returns the results in a sentence:

(define (amazify name)
  (word 'the-amazing- name))

  (define (transform-beatles transformer)
    (every transformer '(John Paul George Ringo))
)

> (transform-beatles amazify)
(THE-AMAZING-JOHN THE-AMAZING-PAUL THE-AMAZING-GEORGE
 THE-AMAZING-RINGO)

> (transform-beatles butfirst)
(OHN AUL EORGE INGO)

8.6  When you're talking to someone over a noisy radio connection, you sometimes have to spell out a word in order to get the other person to understand it. But names of letters aren't that easy to understand either, so there's a standard code in which each letter is represented by a particular word that starts with the letter. For example, instead of "B" you say "bravo."

Write a procedure words that takes a word as its argument and returns a sentence of the names of the letters in the word:

> (words 'cab)
(CHARLIE ALPHA BRAVO)

(You may make up your own names for the letters or look up the standard ones if you want.)

Hint: Start by writing a helper procedure that figures out the name for a single letter.

(define (code-letter letter)
  (cond 
    ((equal? letter 'a) 'adam)
    ((equal? letter 'b) 'ben)
    ((equal? letter 'c) 'carrot)
    ((equal? letter 'd) 'duplex)
    ((equal? letter 'e) 'error)
    ((equal? letter 'f) 'function)
    ((equal? letter 'g) 'garbage)
    ((equal? letter 'h) 'harry)
    ((equal? letter 'i) 'indigo)
    ((equal? letter 'j) 'jackfruit)
    ((equal? letter 'k) 'ketamine)
    ((equal? letter 'l) 'logo)
    ((equal? letter 'm) 'mom)
    ((equal? letter 'n) 'nope)
    ((equal? letter 'o) 'ocelot)
    ((equal? letter 'p) 'purple)
    ((equal? letter 'q) 'quartet)
    ((equal? letter 'r) 'right)
    ((equal? letter 's) 'soldier)
    ((equal? letter 't) 'to)
    ((equal? letter 'u) 'undo)
    ((equal? letter 'v) 'veranda)
    ((equal? letter 'w) 'wax)
    ((equal? letter 'x) 'xanax)
    ((equal? letter 'y) 'yellow)
    ((equal? letter 'z) 'zoo)
  )
)

(define (words wd)
  (every code-letter wd)
)

8.7  [14.5][9] Write a procedure letter-count that takes a sentence as its argument and returns the total number of letters in the sentence:

> (letter-count '(fixing a hole))
11

(define (letter-count sent)
  (accumulate + (every count sent))
)

8.8  [12.5] Write an exaggerate procedure which exaggerates sentences:

> (exaggerate '(i ate 3 potstickers))
(I ATE 6 POTSTICKERS)

> (exaggerate '(the chow fun is good here))
(THE CHOW FUN IS GREAT HERE)

It should double all the numbers in the sentence, and it should replace "good" with "great," "bad" with "terrible," and anything else you can think of.

(define (swap wd)
  (cond 
    ((equal? wd 'good) 'great)
    ((equal? wd 'bad) 'terrible)
    ((number? wd) (* 2 wd))
    (else wd)
  )
)

(define (exaggerate sent)
    (every swap sent)
)

8.9  What procedure can you use as the first argument to every so that for any sentence used as the second argument, every returns that sentence?

identity

What procedure can you use as the first argument to keep so that for any sentence used as the second argument, keep returns that sentence?

(= 1 1)

What procedure can you use as the first argument to accumulate so that for any sentence used as the second argument, accumulate returns that sentence?

(define (assent x y)
  (se x y)
)

(accumulate assent '(ben is ben hello))

8.10  Write a predicate true-for-all? that takes two arguments, a predicate procedure and a sentence. It should return #t if the predicate argument returns true for every word in the sentence.

> (true-for-all? even? '(2 4 6 8))
#T

> (true-for-all? even? '(2 6 3 4))
#F

(define (always-one arg)
  1)

(define (count sent)
  (accumulate + (every always-one sent)))

(define (true-for-all? pred sent)
    (= (count sent)(count (keep pred sent))
))

8.11  [12.6] Write a GPA procedure. It should take a sentence of grades as its argument and return the corresponding grade point average:

> (gpa '(A A+ B+ B))
3.67

Hint: write a helper procedure base-grade that takes a grade as argument and returns 0, 1, 2, 3, or 4, and another helper procedure grade-modifier that returns −.33, 0, or .33, depending on whether the grade has a minus, a plus, or neither.

(define (gp grade)
  (cond ((equal? (first grade) 'A) 4)
    ((equal? (first grade) 'B) 3)
    ((equal? (first grade) 'C) 2)
    ((equal? (first grade) 'D) 1)
    (else 0)
  )
)

# Should ignore modifier for F, but meh
(define (gp-mod grade)
  (cond ((equal? (last grade) '-) -.33)
    ((equal? (last grade) '+) .33)
    (else 0)
  )
)

(define (gp-total grade)
 (+ (gp grade) (gp-mod grade))
)

(define (gpa grades)
(/ (accumulate + (every gp-total grades)) (count grades))
)

8.12  [11.2] When you teach a class, people will get distracted if you say "um" too many times. Write a count-ums that counts the number of times "um" appears in a sentence:

> (count-ums '(today um we are going to um talk about functional um programming))
3

(define (is-um? wd)
(eq? wd 'um)
)

(define (count-ums sent)

(count (keep is-um? sent))

)

8.13  [11.3] Write a procedure phone-unspell that takes a spelled version of a phone number, such as POPCORN, and returns the real phone number, in this case 7672676. You will need to write a helper procedure that uses an 8-way cond expression to translate a single letter into a digit.

8.14  Write the procedure subword that takes three arguments: a word, a starting position number, and an ending position number. It should return the subword containing only the letters between the specified positions:

> (subword 'polythene 5 8)
THEN
