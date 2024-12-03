
<font color = "yellow">NOTICE THAT ALL THE SESSIONS HAVE WRITTEN NOTES, THIS IS JUST THE SUMMARY AND LEARNT LESSONS </font>
# Session 1
- <span style="color:rgb(0, 176, 80)">sometimes the problem is in bad software and not hardware speed</span> 
  when you do a recursive function -> take care that they can have exponential effect if written incorrectly
	  -> hardware won't solve this problem no matter how much you upgrade the cpu
- let expression gives you freedom to write local variables
  and for some reason , sometimes a function cannot be interpreted if the variables inside are not in a let expression
- a type in SML is called OPTION is used to indicate if a value is there or not
  SOME: a value is there
  NONE: no value is there
	  -> this is used when you want to return a no value for the sum of an empty list for example 
	  -> this can be used when returning the top value of an empty stack 
- <span style="color:rgb(0, 176, 240)">Finally the inability to mutate variable and that any change to any variable means shadowing the older value and not changing it is a feature of ML that gives security</span> 
	  ->this means that instead of java or C++ returning references for example to a certain value where you shouldn't modify but you <span style="color:rgb(0, 176, 240)">CAN</span>, ML gives this sense of security because you <span style="color:rgb(0, 176, 240)">CAN'T</span> mutate the variables
# Session 2
- the each of type and one of type have very different usage
- one of type can make the code much simpler
  like making a record of a student that has a name only a name if he is new, but has a student ID if he is registered, so we only use student id
  ex :
		  -> datatype id = studentNum of int
						| Name of string
								* ()

### Card Game Problem SML
Issue with card problem was nested child case expression matched wrongly against the case of parent expression so you need to put it in empty let epression to limit its scope
ex:

case parent of
	first => 
	| second => 
		case child of
			A=> 
			B=> <span style="color:rgb(192, 0, 0)">IT WILL MATCH AGAINST THIRD (WRONG SCOPE)</span>
	| third =>
<span style="color:rgb(255, 192, 0)">so we make nested case expression locally</span>
case parent of
	first => 
	| second => 
		let
		in
			case child of
				A=> 
				B=>
		end
	| third =>

### Lexical Scope vs Dynamic scope of a function
- Lexical scope means that the function only sees the environment in which it was created not the one it was called in
- dynamic scope means that the function sees the environment in which it was called not created

### Anonymous functions
- anonymous functions are great for being defined inside another function and can use the local variables of the main functions directly
### Partial Function
means having a function that takes multiple arguments (two  for example) and i want to give the first argument privately and have the client provide the second argument to the said function
- this is done using currying