2.1  In each line of the following table we've left out one piece of information. Fill in the missing details.

| function | arg 1 | arg 2 | result |
| -------- | ----- | ----- | ------ |
| word | now | here | nowhere |
| sentence | now | here | (now here) |
| first | (blackbird) | | blackbird |
| + | 3 | 4 | 7 |
| every | butfirst | (thank you girl) | (hank ou irl) |
| member? | e | aardvark | #f |
| member? | the | (the) | #t |
| keep | vowel? | (i will) | (i) |
| keep | vowel? | eieiosssss | eieio |
| last | () | none | error |
| every | last | (honey pie) | (y e) |


2.2   What is the domain of the vowel? function?

Every possible character

2.3  One of the functions you can use is called appearances. Experiment with it, and then describe fully its domain and range, and what it does. (Make sure to try lots of cases. Hint: Think about its name.)

The domain is any character, word, or sentence. The range is any positive integer or zero. The function counts the number of instances of argument 1 in argument 2.

2.4  One of the functions you can use is called item. Experiment with it, and then describe fully its domain and range, and what it does.

The domain is any positive integer and any character, word, or sentence. The range is a character, word, or sentence. The function accepts two arguments, where the first is an index in the second. The function returns the item in the second argument at the index defined by the first argument.

The following exercises ask for functions that meet certain criteria. For your convenience, here are the functions in this chapter: +, -, /, <=, <, =, >=, >, and, appearances, butfirst, butlast, cos, count, equal?, every, even?, expt, first, if, item, keep, last, max, member?, not, number?, number-of-arguments, odd?, or, quotient, random, remainder, round, sentence, sqrt, vowel?, and word.

2.5   List the one-argument functions in this chapter for which the type of the return value is always different from the type of the argument.

even?, number?, number-of-arguments, odd?, vowel?, first, last

2.6   List the one-argument functions in this chapter for which the type of the return value is sometimes different from the type of the argument.

round, sqrt, cos

2.7   Mathematicians sometimes use the term "operator" to mean a function of two arguments, both of the same type, that returns a result of the same type. Which of the functions you've seen in this chapter satisfy that definition?

+, -, word, quotient, remainder, expt, max

2.8  An operator f is commutative if f(a,b)=f(b,a) for all possible arguments A and B. For example, + is commutative, but word isn't. Which of the operators from Exercise 2.7 are commutative?

Any one arg function is commutative. Also:
+, =, max

2.9  An operator f is associative if f(f(a,b),c)=f(a,f(f(b,c)) for all possible arguments A, B, and C. For example, * is associative, but not /. Which of the operators from Exercise 2.7 are associative? 

+, max, =