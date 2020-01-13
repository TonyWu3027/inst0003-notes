# Pseudocode Cheatsheet

## Comment `//`

```pseudocode
// this is a comment, it will not be processed by the programme. It is used by programmers to explain their code which increases the readability 
```

## Variables

>   Variables are the storage of data to be referenced and manipulated in a comoputer programme.

### Rule for naming:

-   ***Begins*** with a lower-case letter
-   ***Connects*** different words with underscore `__`

```pseudocode
tony // valid varible name
1programme // invalid, shouldn't start with number
programme1 // valid
programme_1 // valid
_pen // invalid, shouldn't start with symbols
this_is_my_value // valid
this is my value // invalid, shuold be connected
IF // invalid, IF is a keyword in Pseudocode, the name of variables should not be keyword
ELSE // invalid, the same reason as above
```

## Name of Programme, Function, and Procedure

-   The name  should start with a ***capital letter***

-   If more than one word is used all words starts with a capital letter and ***no spaces or symbols are used in between words*** 

-   A program ***does not have any variable in input***, these have to be obtained from the user with the command `INPUT`

-   A program ***does not have any output***, these need to be emitted with the command `PRINT`, or `DISPLAY`

## `SET,INIT`

Declaring a variable. Note that: a vairable must be declared before used

```pseudocode
SET x : INT // declare a variable called x of data type integer, note that data type is not covered in this course but we use them in actual programming
INIT y: INT = 1 // declare a variable called y and give it an initilised value of 1
```

## Assignment `:=`

```pseudocode
x := 1 // assign value 1 to variable x
y := 2 // assign value 2 to variable y
z := y // assign the value of variable y to variable z
```

## Comparison `=,!=,<=,>=,<,>`

Returns `True` or` False` of the comparison 

```pseudocode
x = y // returns whether x equals to y
x != y // returns whether x strictly not equals to y, for example if x = 'Tony' and y = 'Toby', x <> y is True
x > y // returns whether x is greater than y
x >= y // returns whether x is greater than or equal to y
x < y // returns whether y is greater than x
x <= y // returns whether y is greater than or equal to x
```

## Arithmetic `+,-,*,/,mod,SUM(),PRODUCT()`

>   Note that, in her slides `SUM()` is denoted by $\sum$ and `PRODUCT()` is denoted by $\prod$, here it is denoted in function notation

```pseudocode
x + y
x - y
x*y // multiplication
x/y
x mod y // returns the remainder of x divided by y
SUM(3*x,y,z) // returns the sum of 3*x, y, and z
PRODUCT(x,y,z) // returns x*y*z
```

## Logical Expression `AND,OR`

```pseudocode
IF x>1 AND x<5 // if x is between 1 and 5 exclusively
	THEN
		y := 1 // y will be 1
	ELSE IF x>10 OR x<-10 THEN // else if x is greater than 10 or x is less than -10
		y := 2 // y will be 2
	ELSE // all other cases
		y := 0 // y will be 0
ENDIF
```

## Functions (She refered as "statements")

```pseudocode
<function_name>(<parameter_1>,<parameter_2>) // the structure for calling a function. The return is the output of the function
<verb>(<variable_1>,<variable_2>) // another approach of understanding functions

// Examples
SUM(3*x,y,z) // returns the sum of 3*x, y, and z
PICK(the_pen_on_the_table) // pick_up the pen on the table
DO_HOMEWORK(info_sys) // do the IS homework
```

## `START,ENDPROGRAM,ENDFUNCTION`

```pseudocode
START // start of a pseudocode programme/snippet or a function
ENDPROGRAME // to end the whole programme
ENDFUNCTION // to end a function

// Example
START DoSomeMaths // start of the programme called "DoSomeMaths"
	START QuadraticFunction(x) // start of the programme called "QuadraticFunction", with x as parameter
	
		result := x*x + 2*x +3 // store the value of x^2 +2x +3 to a varaible called "result", note that here we use assign(:=) rather than equal(=)
		
	ENDFUNCTION result //end the function and return the value of variable "result"
	
ENDPROGRAM // end the whole programme

START UserInfoCollection
	DISPLAY “Enter your name”
	INPUT name
	DISPLAY “Enter your age”
	INPUT age
	DISPLAY ”your name is” name,
	DISPLAY “your age is” age
ENDPROGRAM

// note that: here we use indentation to represent the logic layers. START and END should be on the same layer, the code underlying it should be on the next layer, so indent. Usually, in programming, one indentation = one "Tab"

```

## I/O Operations`INPUT,READ,GET,PRINT,DISPLAY`

```pseudocode
INPUT x // assign the user's keyboard/devide input to variable x

READ myFile.dat,myVal // assign the data read from local file myFile.dat to the variable myVal
GET myFile.dat, myVa; // same as above

PRINT x // show on screen the value of variable x
DISPLAY x // same as above
```

## Boolean Values `TRUE,FALSE`

```pseudocode
x := 1
y := 2
PRINT x=y
>>> FALSE
PRINT x<y
>>> TRUE
PRINT x>y
>>> FALSE

// note that >>> represent what you will see on the screen if you execute the code above
```

## `COMPUTE, CALCULATE, DETERMINE`

Never used them before...

## `INCREMENT, DECREMENT`

```pseudocode
x := 1
INCREMENT x // the equivalent of x := x + 1
PRINT x
>>> 2

y := 1
DECREMENT y // y := y - 1
PRINT y
>>> 0
```

## `IF,ELSE IF, ELSE, ENDIF`

See example in ***Logical Expression*** section above

## `SWITCH,CASE,BREAK`

```pseudocode
// structure
SWITCH (<varibale>) // read the value of <variable>
	CASE <value_1>: // if that value is <value_1>
		<statement_1> // do <statement_1>
	BREAK
	CASE <value_2>: // if that value is <value_2>
		<statement_2> // do <statement_2>
	BREAK
	CASE <value_3>: // if that value is <value_3>
		<statement_3> // do <statement_2>
	BREAK

// Example
SWITCH (colour) // read colour
   CASE red: // if colour is red
		PRINT “Red” // show 'Red'
   BREAK
   CASE blue: 
		PRINT “blue”
   BREAK
   CASE others: 
		PRINT “Please enter a colour”
   BREAK
```

##Pre-Condition Iteration `FOR,ENDFOR`

```pseudocode
// print out the grade of each student, one at a time
FOR (each_student_in_IS_module)
	PRINT each_student_grade
ENDFOR

// count the number of student and print out that number in the end
INIT total_number = 0
FOR (each_student_in_IS_module)
	INCREMENT total_number
ENDFOR
PRINT total_number

// Note that: indentation is used
```

## Post-Condition Iteration `WHILE,ENDWHILE`

```pseudocode
// print out 'hello world' for ten times
INIT counter = 1
WHILE counter <= 10
	PRINT "hello world"
	INCREMENT counter
ENDWHILE

// Note that: indentation is used
```

## Function vs. Procedure

Functions and procedures are the snippets of code or subprogrammes of a programme that can be constantly reused for specific purposes

>   A function has a return value while a procedure doesn't have

```pseudocode
// Example of function
START MyFunction(x,y) // x and y are parameters
	INIT result = 0
	result := (x/y)*x
ENDFUNCTION result // the value of result is returned from the function

INIT value = 0 
value := MyFunction(2,1) // call that function, with x=2,y=1, assign the returned value to variable "value"
PRINT value // print out "value"
>>> 4 

// Example of procedure
START MyProcedure (x,y)
	INIT result = 0
	result := (x/y)*x
ENDFUNCTION // no return value

INIT value = 0 
value := MyFunction(2,1) // call that procedure, with x=2,y=1, assign the returned value to variable "value"
PRINT value // print out "value"
>>> NULL // because nothing is returned from a procedure
```

