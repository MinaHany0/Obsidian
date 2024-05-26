
### 1- write the input and output in its type format
	int -> int
### 2- write the description of the function
	function takes number and return double the value
### 3- Function Stub
	a syntatically correct function call with a dummy result at the end
	its purpose is to enable the test checks to run
	---> I as mina on't see much value in stub right now
### 4-define examples
	in BSL->	;;(double 0) should return 0
			;;(double 1) should return 2
	in Cpp	//double(3) should return 6 
			//double(6) should return 12
	Use generic test function to test the function
	like check_expect() or check_equal() or make any generic function to use
### 5-Template
	the template shows you the raw material the function is dealing with
	ex: (define (double n)
		(...n))		----> here it tells that it deals with n and outputs some calc of n

## Code Coverage for a test concept
The test cases need to cover all paths available in the code
also make a matrix for all possible changes of input with regards to each other (combination of different inputs together)
	ex: checking that rectangle 1 is bigger than rectangle 2
			you have multiple combination of length and width of rectangle 1 with combination of length and width for rectangle 2
		Goof practice is having test cases as many as there are enumeration values

## Commit Ready Concept
the code should be well commented and well structured (neat and tidy)
the code should have been tested already
the code should have all the elements of design (HTDF Principles)