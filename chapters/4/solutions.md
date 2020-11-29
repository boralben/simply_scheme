Boring Exercises

4.1  Consider this procedure:

(define (ho-hum x y)
  (+ x (* 2 y)))

Show the substitution that occurs when you evaluate

(ho-hum 8 12)

(+ 8 (* 2 12))

4.2  Given the following procedure:

(define (yawn x)
  (+ 3 (* x 2)))

list all the little people that are involved in evaluating

(yawn (/ 8 2))

Jonathan oversees the whole thing, taking arguments 8 and 2. He hires Janet, to oversee yawn. She hires Jordan to divide of 8 by 2, returning 4. Janet then hires jarvis to oversee addition of 3 and (* 4 2), who hires James to oversee (* 4 2). James returns 8, Jarvis returns 11. Janet returns 11 to Jonathan, who returns 11.

(Give their names, their specialties, their arguments, who hires them, and what they do with their answers.)

4.3  Here are some procedure definitions. For each one, describe the function in English, show a sample invocation, and show the result of that invocation.

(define (f x y) (- y x))

Subtract x from y. 
(f 10 5) -> 5

(define (identity x) x)
Returns the value provided
(identify 4) -> 4

(define (three x) 3)

Retruns 3 no matter what value is provided
(three 4) -> 3

(define (seven) 7)
Takes no arguments, always returns 7
(seven) -> 7

(define (magic n)
  (- (/ (+ (+ (* 3 n)
              13)
           (- n 1))
        4)
     3))

Retruns the value of the argument provided

magic (0) -> 0
magic (7) -> 7
magic (-1) -> -2

Real Exercises

4.4  Each of the following procedure definitions has an error of some kind. Say what's wrong and why, and fix it:

(define (sphere-volume r)
  (* (/ 4 3) 3.141592654)
  (* r r r))

Only the second experssion is run

(define (next x)
  (x + 1))

procedure should be first (+ x 1)

(define (square)
  (* x x))

No argument is declared

(define (triangle-area triangle)
  (* 0.5 base height))

mismatched formal parameters

(define (sum-of-squares (square x) (square y))
  (+ (square x) (square y)))

Don't pass procedures into the definition--only formal paramters, aka names

4.5  Write a procedure to convert a temperature from Fahrenheit to Celsius, and another to convert in the other direction. The two formulas are F=9⁄5C+32 and C=5⁄9(F-32).

(define (f-to-c temp)
  (* (/ 5 9) (- temp 32))
)

(define (c-to-f temp)
  (+ (*(/ 9 5) temp) 32)
)

4.6  Define a procedure fourth that computes the fourth power of its argument. Do this two ways, first using the multiplication function, and then using square and not (directly) using multiplication.

(define (fourth x)
  (* x x x x)
)

(define (fourth x)
 (expt (expt x 2) 2)
)

4.7  Write a procedure that computes the absolute value of its argument by finding the square root of the square of the argument.

(define (absval x)
  (sqrt (expt x 2))
)

4.8  "Scientific notation" is a way to represent very small or very large numbers by combining a medium-sized number with a power of 10. For example, 5×107 represents the number 50000000, while 3.26×10-9 represents 0.00000000326 in scientific notation. Write a procedure scientific that takes two arguments, a number and an exponent of 10, and returns the corresponding value:

(define (scientific n x)
  (* n (expt 10 x))
)

> (scientific 7 3)
7000

> (scientific 42 -5)
0.00042

Some versions of Scheme represent fractions in a/b form, and some use scientific notation, so you might see 21/50000 or 4.2E-4 as the result of the last example instead of 0.00042, but these are the same value.

(A harder problem for hotshots: Can you write procedures that go in the other direction? So you'd have

> (sci-coefficient 7000)
7

> (sci-exponent 7000)
3

You might find the primitive procedures log and floor helpful.)

4.9  Define a procedure discount that takes two arguments: an item's initial price and a percentage discount. It should return the new price:

> (discount 10 5)
9.50

> (discount 29.90 50)
14.95

(define (discount initial percent_off)
  (* initial (* 0.01 (- 100 percent_off)))
)

4.10  Write a procedure to compute the tip you should leave at a restaurant. It should take the total bill as its argument and return the amount of the tip. It should tip by 15%, but it should know to round up so that the total amount of money you leave (tip plus original bill) is a whole number of dollars. (Use the ceiling procedure to round up.)

(define (tip tot)
  (- (ceiling (* tot 1.15)) tot)
)

> (tip 19.98)
3.02

> (tip 29.23)
4.77

> (tip 7.54)
1.46
