Boring Exercises

6.1  What values are printed when you type these expressions to Scheme? (Figure it out in your head before you try it on the computer.)

(cond ((= 3 4) '(this boy))
      ((< 2 5) '(nowhere man))
      (else '(two of us)))
(nowhere man)

(cond (empty? 3)
      (square 7)
      (else 9))

error?

(define (third-person-singular verb)
  (cond ((equal? verb 'be) 'is)
        ((equal? (last verb) 'o) (word verb 'es))
        (else (word verb 's))))

(third-person-singular 'go)

goes

6.2  What values are printed when you type these expressions to Scheme? (Figure it out in your head before you try it on the computer.)

(or #f #f #f #t)

#t

(and #f #f #f #t)

#f

(or (= 2 3) (= 4 3))

#f

(not #f)

#t

(or (not (= 2 3)) (= 4 3))

#t

(or (and (= 2 3) (= 3 3)) (and (< 2 3) (< 3 4)))

#t

6.3  Rewrite the following procedure using a cond instead of the ifs:

(define (sign number)
  (if (< number 0)
      'negative
      (if (= number 0)
	  'zero
	  'positive)))


(define (sign number)
  (cond 
   ((< number 0) 'negative)
   ((= number 0) 'zero)
   (else 'positive))
)


6.4  Rewrite the following procedure using an if instead of the cond:

(define (utensil meal)
  (cond ((equal? meal 'chinese) 'chopsticks)
	(else 'fork)))

Real Exercises

Note: Writing helper procedures may be useful in solving some of these problems.

6.5  Write a procedure european-time to convert a time from American AM/PM notation into European 24-hour notation. Also write american-time, which does the opposite:

> (european-time '(8 am))
8

> (european-time '(4 pm))
16

> (american-time 21)
(9 PM)

> (american-time 12)
(12 PM)

> (european-time '(12 am))
24

Getting noon and midnight right is tricky.

(define (is-am? sent)
  (equal? (last sent) 'am)
)

(define (is-midnight? sent)
  (and (is-am? sent) (equal? (first sent) '12))
)

(define (is-noon? sent)
  (and (not (is-am? sent)) (equal? (first sent) '12))
)

(define (european-time sent)
(cond 
  ((is-midnight? sent) '24)
  ((is-noon? sent) '12)
  ((not (is-am? sent)) (+ (first sent) 12))
  (else (first sent))
)
)

(define (american-time wd)
(cond 
  ((equal? wd '24) '(12 am))
  ((equal? wd '12) '(12 pm))
  (( > wd 12) (se (- wd 12) 'pm))
  (else (se wd 'am))
)
)

6.6  Write a predicate teen? that returns true if its argument is between 13 and 19.

(define (teen? age)
(and (> age 12) (< age 20))
)

6.7  Write a procedure type-of that takes anything as its argument and returns one of the words word, sentence, number, or boolean:

> (type-of '(getting better))
SENTENCE

> (type-of 'revolution)
WORD

> (type-of (= 3 3))
BOOLEAN

(Even though numbers are words, your procedure should return number if its argument is a number.)

Feel free to check for more specific types, such as "positive integer," if you are so inclined.

(define (type-of arg)
(cond 
  ((sentence? arg) 'SENTENCE)
  ((number? arg) 'NUMBER)
  ((boolean? arg) 'BOOLEAN)
  (else 'WORD)
)
)

6.8  Write a procedure indef-article that works like this:

> (indef-article 'beatle)
(A BEATLE)

> (indef-article 'album)
(AN ALBUM)

Don't worry about silent initial consonants like the h in hour.

(define (indef-article wd)

(if (member? (first wd) '(a e i o u))
    (se 'an wd)
    (se 'a wd)
)
)


6.9  Sometimes you must choose the singular or the plural of a word: 1 book but 2 books. Write a procedure thismany that takes two arguments, a number and a singular noun, and combines them appropriately:

> (thismany 1 'partridge)
(1 PARTRIDGE)

> (thismany 3 'french-hen)
(3 FRENCH-HENS)

(define (thismany num noun)
  (if (= num 1)
    (se num noun)
    (se num (word noun 's))
  )
)

6.10  Write a procedure sort2 that takes as its argument a sentence containing two numbers. It should return a sentence containing the same two numbers, but in ascending order:

> (sort2 '(5 7))
(5 7)

> (sort2 '(7 5))
(5 7)

(define (sort2 sent)
  (if (< (first sent) (last sent))
    sent
    (se (last sent) (first sent))
  )
)

6.11  Write a predicate valid-date? that takes three numbers as arguments, representing a month, a day of the month, and a year. Your procedure should return #t if the numbers represent a valid date (e.g., it isn't the 31st of September). February has 29 days if the year is divisible by 4, except that if the year is divisible by 100 it must also be divisible by 400.

> (valid-date? 10 4 1949)
#T

> (valid-date? 20 4 1776)
#F

> (valid-date? 5 0 1992)
#F

> (valid-date? 2 29 1900)
#F

> (valid-date? 2 29 2000)
#T


and ( (eq? 0 (remainder year 100) (eq? 0 (remainder year 400)

(define (max-day month year)
  (cond 
    ((member? month '(1 3 5 7 8 10 12)) 31)
    ((member? month '(4 6 9 11)) 30)
    ((= 2 month)
      (if (and (= (remainder year 4) 0) (= 0 (remainder year 100) (remainder year 400)))
        29
        28
      )
    )
    (else 0)
  )
)

(define (valid-date? month day year)
  (cond
    ((< year 0) #f)
    ((<= day 0) #f)
    ((> day (max-day month year)) #f)
    (else #t)    
  )
)

6.12  Make plural handle correctly words that end in y but have a vowel before the y, such as boy. Then teach it about words that end in x (box). What other special cases can you find?

(define (plural wd)  
  (cond
    ((and (equal? 'y (last wd)) (member? (last (bl wd)) '(a e i o u))) (word wd 's))
    ((equal? 'y (last wd)) (word (bl wd) 'ies))
    ((equal? 'x (last wd)) (word wd 'es))
    (else (word wd 's))
  )
)


### okay, i'm done with this chapter. i get the idea

6.13  Write a better greet procedure that understands as many different kinds of names as you can think of:

> (greet '(john lennon))
(HELLO JOHN)

> (greet '(dr marie curie))
(HELLO DR CURIE)

> (greet '(dr martin luther king jr))
(HELLO DR KING)

> (greet '(queen elizabeth))
(HELLO YOUR MAJESTY)

> (greet '(david livingstone))
(DR LIVINGSTONE I PRESUME?)

6.14  Write a procedure describe-time that takes a number of seconds as its argument and returns a more useful description of that amount of time:

> (describe-time 45)
(45 SECONDS)

> (describe-time 930)
(15.5 MINUTES)

> (describe-time 30000000000)
(9.506426344208686 CENTURIES)
