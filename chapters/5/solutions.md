5.1  What values are printed when you type these expressions to Scheme? (Figure it out in your head before you try it on the computer.)

(sentence 'I '(me mine))

(I me mine)

(sentence '() '(is empty))

(is empty)

(word '23 '45)

2345

(se '23 '45)

(23 45)

(bf 'a)

""

(bf '(aye))

()

(count (first '(maggie mae)))

6

(se "" '() "" '())

("" "")

(count (se "" '() "" '()))

2

5.2  For each of the following examples, write a procedure of two arguments that, when applied to the sample arguments, returns the sample result. Your procedures may not include any quoted data.

> (f1 '(a b c) '(d e f))
(B C D E)

(define (f1 sent1 sent2)
  (se (bf sent1) (bl sent2))
)

> (f2 '(a b c) '(d e f))
(B C D E AF)

(define (f2 sent1 sent2)
  (se (bf sent1) (bl sent2) (word (first sent1) (last sent2)))
)

> (f3 '(a b c) '(d e f))
(A B C A B C)

(define (f3 sent1 sent2)
  (se sent1 sent1)
)

> (f4 '(a b c) '(d e f))
BE

(define (f4 sent1 sent2)
  (word (item 2 sent1) (item 2 sent2))
)

5.3  Explain the difference in meaning between (first 'mezzanine) and (first '(mezzanine)).

(first 'mezzanine) -> get first letter of word
(first '(mezzanine)) -> get first word of sentence

5.4  Explain the difference between the two expressions (first (square 7)) and (first '(square 7)).

(first (square 7)) - first letter of word created by function
(first '(square 7)) - first word in sentence "square 7"

5.5  Explain the difference between (word 'a 'b 'c) and (se 'a 'b 'c).

'abc
(a b c)

5.6  Explain the difference between (bf 'zabadak) and (butfirst 'zabadak).

nothing


5.7  Explain the difference between (bf 'x) and (butfirst '(x)).

one operates on a word and one on a sentence. "" and ().

5.8  Which of the following are legal Scheme sentences?

(here, there and everywhere) - no
(help!) - yes
(all i've got to do) - no
(you know my name (look up the number)) - no

5.9  Figure out what values each of the following will return before you try them on the computer:

(se (word (bl (bl (first '(make a))))
          (bf (bf (last '(baseball mitt)))))
    (word (first 'with) (bl (bl (bl (bl 'rigidly))))
          (first 'held) (first (bf 'stitches))))


(se 'matt 'wright)

(se (word (bl (bl 'bring)) 'a (last 'clean))
    (word (bl (last '(baseball hat))) (last 'for) (bl (bl 'very))
	  (last (first '(sunny days)))))

     (se 'brian 'harvey)

5.10  What kinds of argument can you give butfirst so that it returns a word? A sentence?

word -> word
sentence -> sentence

5.11  What kinds of argument can you give last so that it returns a word? A sentence?

word -> word, sentence
sentence -> sentence

5.12  Which of the functions first, last, butfirst, and butlast can return an empty word? For what arguments? What about returning an empty sentence?

empty word

(first '("" 'a 'b))
(last '('a 'b ""))
(bf 'a)
(bl 'a)

empty sentence

(bf '(a))
(bl '(a))

Real Exercises

5.13  What does ' 'banana stand for?

quote

What is (first ' 'banana) and why?

"" because that is the first item passed in

5.14  Write a procedure third that selects the third letter of a word (or the third word of a sentence).

(define (third target) (item 3 target))

5.15   Write a procedure first-two that takes a word as its argument, returning a two-letter word containing the first two letters of the argument.

> (first-two 'ambulatory)
AM

(define (first-two wd) (word (first wd) (first (bf wd))))

5.16  Write a procedure two-first that takes two words as arguments, returning a two-letter word containing the first letters of the two arguments.

> (two-first 'brian 'epstein)
BE

(define (two-first wd1 wd2) (word (first wd1) (first wd2)))


Now write a procedure two-first-sent that takes a two-word sentence as argument, returning a two-letter word containing the first letters of the two words.

> (two-first-sent '(brian epstein))
BE

(define (two-first-sent sent) (word (first (first sent)) (first (item 2 sent)) ))

5.17  Write a procedure knight that takes a person's name as its argument and returns the name with "Sir" in front of it.

> (knight '(david wessel))
(SIR DAVID WESSEL)

(define (knight sent) (se 'sir sent))

5.18  Try the following and explain the result:

(define (ends word)
  (word (first word) (last word)))

> (ends 'john)

(john (first 'john) (last 'john))

5.19  Write a procedure insert-and that takes a sentence of items and returns a new sentence with an "and" in the right place:

> (insert-and '(john bill wayne fred joey))
(JOHN BILL WAYNE FRED AND JOEY)

5.20  Define a procedure to find somebody's middle names:

> (middle-names '(james paul mccartney))
(PAUL)

> (middle-names '(john ronald raoul tolkien))
(RONALD RAOUL)

> (middle-names '(bugs bunny))
()

> (middle-names '(peter blair denis bernard noone))
(BLAIR DENIS BERNARD)


(define (middle-names fullname)
(bl (bf fullname))
)

5.21  Write a procedure query that turns a statement into a question by swapping the first two words and adding a question mark to the last word:

> (query '(you are experienced))
(ARE YOU EXPERIENCED?)

> (query '(i should have known better))
(SHOULD I HAVE KNOWN BETTER?)

(define (query sent)

(sentence 
(first (bf sent))
(first sent)
(bf (bl sent))
(word (last sent) '?))

)