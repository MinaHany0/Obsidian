- seg fault : always check your pointer allocation, use assert, that you if pass a pointer for the dyn alloc by reference not by value
- - Functions used in ISR must be re-entrant functions if it's to be used on other places in the code
- variadic function says arithmetic operation on void pointer not defined (i put in a pointer to a struct)
- <font color = "yellow">when writing recursive functions  , write recursive part first then condition to break </font>
- If some variable is used in a function by reference and you only need the initial value of the variable, save its value in a local variable in the function
```
(define f  
	(let ([b b])  
		(lambda (x) (* 1 (+ x b)))))
```
here in this racket code: we capture a variable b by reference, so we shadow it by another local variable b , which holds the initial value of the global variable b and keeps the initial value in the function definition.

- there is a rule called "evaluate arguments in advance" that is we always evaluate the arguments of a function before evaluating the body of the function, because the body is evaluated when the function is called.