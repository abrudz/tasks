# Day9 Summary and Tasks
Multiline functions, recursion, control structures, tracing

All of this information, and more, can be found on:
- http://course.dyalog.com/autumn2021/Loops/
- http://course.dyalog.com/autumn2021/Ufns/
- https://mastering.dyalog.com/User-Defined-Functions.html
- https://www.dyalog.com/uploads/documents/MasteringDyalogAPL.pdf#%5B%7B%22num%22%3A529%2C%22gen%22%3A0%7D%2C%7B%22name%22%3A%22XYZ%22%7D%2C40%2C640%2C0%5D

When asked to make a diagram, you can either:  
- Use pen and paper
- Create a text variable in your workspace. For example:

```
      diagram←''
      )ED diagram
```

## Setting up
Please do `)CLEAR` your workspace and save it with the name "your_name_tasks6.dws"

## The editor
Edit character vectors and matrices directly
View any array
Edit dfns (curly brace functions) and tradfns (traditional functions using explicit names)

)ED
⎕ED
Shift+Enter

Press Esc to close the editor and save your changes
Press Shift+Esc to close the editor without saving changes

## Multiline and traditional functions
The syntax is given here: http://course.dyalog.com/autumn2021/Ufns/#traditional-functions

More details notes here:
https://mastering.dyalog.com/User-Defined-Functions.html

### Key shortcuts
Ctrl-Enter (trace function)
Shift+Enter (Edit name)

## Tasks

### 1
Explain at least 4 of the following expressions:

1. Describe the transformation of the data from one step to the next
2. Describe the overall effect and/or purpose of the expression
3. Re-write the funciton as a multi-line function with comments

`¯3 1.5 {⍺[1]+⍺[2]×¯1+⍳⍵} 10`

`{+/(1↓⍵)=¯1↓⍵}¨'orange' 'apple' 'teenager' 'mississippi' 'bookkeeper'`

`{i/⍳⍴i←2=+⌿0=∘.|⍨⍳⍵}20`

`{⍵↓⍨¯1+i/⍳⍴i←<\⍵='⍝'}'3+2×⍳6   ⍝ Odd numbers from 5 to 15'`

`{⍵↓⍨¯1+⍵⍳'⍝'}'3+2×⍳6   ⍝ Odd numbers from 5 to 15'`

`10 18 {(3 7⍴'early  on timelate   ')[1++/⍵∘.<⍺;]} 4 6 12 14 16 20 23`

`{+/⍵=⌈\⍵} 1 3 5 4 5 2 6 7 3 8 9`

`0 40 60 70 90{(2,⍴⍵)⍴('FDCBA'[+⌿⍺∘.≤⍵]),⍵}?10⍴100`

### 2
In https://abrudz.github.io/tasks/tasks5.pdf

Tasks 14, 15 and 16 can be written as single line dfns. However, they are probably better written as multi-line functions with comments.

For example, "exploding" a single line function to add comments:

```
WhoAteMost ← {
                                        ⌿ names   ⍝ Names of people
    (total=⌈/                                     ⍝   who ate the most
             total←+/+/                           ⍝   of total eaten
                            fruits⍳⍵              ⍝   of fruits specified in ⍵
                       ate[;        ;])           ⍝   selected from data about fruits eaten in the week
                                                }
```

The same function as a true multi-line dfn:

```
 WhoAteMost←{
⍝ Who ate the most fruits specified in character matrix ⍵
⍝ --- Define constants ---
     fruits←4 7⍴'Apples MangoesOrangesBananas'
     days←7 3⍴'SunMonTueWedThuFriSat'
     names←3 7⍴'Adam   RodrigoRich   '
     ⎕RL←42 1 ⋄ ate←?3 4 7⍴3
⍝ --- Algorithm ---
     specified←ate[;fruits⍳⍵;]   ⍝ Amount of each of those fruits specified in ⍵ eaten by anyone all week
     total←+/+/specified         ⍝ Total fruit, of those specified, eaten by each person
     names⌿⍨total=⌈/total        ⍝ Names of those who are the most fruit
 }
```

Solve tasks 15 and 16, defining the solutions as multi-line dfns with full comments, as above.

### 3-A
A basic treatment of recursion in dfns: http://course.dyalog.com/autumn2021/Loops/

The structure of a "loop" is to perform several actions in a list of actions before returning to the first.

1. Start
2. Do something
3. Do something else
4. Do one last thing
5. Return to start

As a diagram, it might look like this:

```
   Start --------> Do something
      ↑                 |
      |                 |
      |                 |
  Last thing            |         
      ↑                 |
      |                 ↓
      ∘---------Do something else   
```

Explicit loops are not used as frequently in APL as they might be in other conventional programming languages. One exception might be in "functional" programming languages.

Often, one of the actions in a loop will modify some state, so that the next time the loop iterates there is some incremental effect.

```
   Start --------> Modify something
      ↑                 |
      |                 |
      |                 |
  One last change       |         
      ↑                 |
      |                 ↓
      ∘---------Modify something else    
```

**Task:** Express the following diagram as a traditional function using control structures.

```
Initialise the result as an empty numeric list
For each of the characters 'ABCDEF':
   Find the index into the alphabet --------> Multiply by five
      ↑                                             |
      |                                             |
      |                                             |
  Catenate to the result                            |
      ↑                                             |
      |                                             ↓
      ∘--------------------------------- Add one, if the index value is even
```

**Task:** Express the following traditional function's control structure (between `:For` and `:EndFor`) using a diagram similar to those above.

```
 mask←term FindIn text;letter
 mask←0⍴⍨⍴term
 :For letter :In text
     :If letter∊term
         mask+←term∊letter
     :EndIf
 :EndFor
```

### 3-B
Recursion can be used for similar effect as iteration (looping), but the main feature is that a recursive function will call itself with some modification of its argument.

1. Take some input as data
2. Test a condition
         If TRUE                               if FALSE
3.  Quit and return result         Call same function with modified data


```
   Start arg
      |
      |
      |
      ↓
  If condition ---→ Quit and return result
     Else
      |
      |
      ↓
  Start again with returned result 
```

**Task:** Write a diagram similar to the one above which describes the Fac function:  
```
 Fac←{
     ⍵≤1:1
     ⍵×∇ ⍵-1
 }
```

**Task:** Experiment with the function to find out what it does. Remember:  
- Use F1 with the cursor to the immediate right of a symbol to get help for it.
- Trace through the funciton with Ctrl+Enter or Action → Trace in the top menu. Inspect the values of ⍵ as the function runs.

**Task:**
2. Write Fac2 as a reduction. That is a function which uses the reduction operator. For example, {+/⍵} is a reduction. You Fac2 should behave identically to Fac above.

3. Find the primitive function equivalent to Fac and Fac2.

### 4
Write the function HashCount, as described here: http://course.dyalog.com/autumn2021/Loops/#hash-counting-string

### 5
If you have time, read [the page on Loops](http://course.dyalog.com/autumn2021/Loops) and then try to solve the other problems in Problem Set 8:

http://course.dyalog.com/autumn2021/Loops/#problem-set-8

### Side effects
When a function accepts arguments, applies functions to the values of those arguments and returns results, without affecting any other external change, this is sometimes known as "functional programming" or "programming in the functional style".

This has many benefits over other styles of programming that rely on "side effects". As an example of a function with side effects, see this "Update" function:

```
    ∇  animal Update number;index    
[1]    index←animals_seen[;⍳3]⍳animal
[2]    animals_seen[index;4]+←number 
    ∇   
```

Begin by initialising the global variable "animals_seen":

```
      animals_seen←3 4⍴'CAT',0,'DOG',0,'COW',0
```

**Task:** Run the update function with some different arguments to see if you can update the "animals_seen" table. 

We want to run the "Update" function until "animals_seen" has the following value:

```
      animals_seen
CAT  3
DOG 12
COW 55
```

1. How can you call the function a single time (starting with 0s in the 4th column) to end up in this state?

2. How can you call the function a single time (starting with 0s in the 4th column) to end up in this state?

3. 
	a. Set "index" to the value 42 in the workspace
	b. Run the Update function with any valid arguments of your choosing
	c. Verify that the value of "index" is still 42
	d. Remove ";index" from the header?
	e. Run the Update function
	f. Verify that the value of "index" has changed

## Notes on side effects and scope
It is important to localise variables inside traditional functions so that they do not overwrite values in other calling functions.

Remember:  

- A local variable is visible to functions called from this function.
- A local variable "shadows" the name, so global variables of the same name are no longer visible from within that function.

## Tracing, printing and stop bits
Read, and make sure to define the test-marking TradFn based on the psuedocode given on this page: http://course.dyalog.com/autumn2021/Ufns/#marking-tests

Compare runtimes between 3 versions of the test marking function:

- one using outer product and reduction
- one using interval-index
- one as a traditional function using control structures

The glyph for interval-index is not available in Dyalog Classic. You will need to define:

```
      IntervalIndex ← {⍺ ⎕U2378 ⍵}
```

Now you should experiment with tracing and stop bits. Use http://course.dyalog.com/autumn2021/Errors/#suspend-your-disbelief and https://mastering.dyalog.com/First-Aid-Kit.html to revise and learn new information.

Each of those has some activities you can try. Try the following first:

### Tracing
Tracing a function is a useful way to see what is happening. There are 3 main modes of tracing.

Firstly, you can step through the function line-by-line and inspect the values of variables at different points. Use Ctrl+Enter to step in, then press Enter to execute each line in turn.

Secondly, you can insert "print" or "output" statements in key lines of your program code to output the results of those expressions to the session log.

Thirdly, you can use ⎕TRACE to make the interpreter output the results of key expressions on particular lines for you without having to insert and delete print statements.

Try all three of of these methods with your Grade2 traditional function.

### Suspending a function
Sometimes it is useful to set a certain place in a function for execution to stop. This is usually because you know that a large amount of code works correctly, and you want to pause execution just before the place in your code where you think an error occurs. 

Try the following with your Grade2 traditional funciton:

- Use the editor to set a stop bit (click in the left column so that a red dot appears) on a line which you know will be executed.
- Run the function and verify that it stops
- Continue execution
- Use the editor to clear the stop bit (remove the red dot by clicking)

- Step into the function (Ctrl+Enter) and use the tracer to set a stop bit
- Verify the stop bit works and remove it

- Use ⎕STOP to set the stop bit
- Verify the stop bit works
- Use ⎕STOP to clear the stop bit

## Configuration parameters
We briefly mentioned configuration parameters. It is unlikely you will need to modify these for existing applications, but it is important to know what they are.

http://course.dyalog.com/autumn2021/Interpreter-internals/#configuration-parameters

## Getting Help
Right now, while you are relatively new to APL, you are mostly going to be concerned with "what does this do?" type questions: http://course.dyalog.com/autumn2021/Help/#what-does-this-thing-do

Of course, you will be very interested in "How do I do this?"-style questions, but the discovery of those answers is a bit of a longer process. Never be afraid to ask for help.

### Versions of Dyalog
In your work, you may be required to use versions of Dyalog which are not the latest. You can find some of the key features added in the APL Wiki. The course page on [getting help](http://course.dyalog.com/autumn2021/Help) contains links to documentation you may find relevant.