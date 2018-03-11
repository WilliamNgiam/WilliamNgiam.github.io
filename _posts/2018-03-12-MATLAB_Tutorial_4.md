-----
title: MATLAB Tutorial 4
-----

These notes cover writing `if` loops and `for` loops.

## The `if` statement

The `if` statement is a control statement that chooses whether lines of code are executed or not. The format for writing an `if` loop is this:

```
if condition

    lines of code

end 
```

The condition is an expression that is either true or false, which we covered in [Tutorial 2](https://williamngiam.github.io/MATLAB_Tutorial_2/). If the condition is a logical true, then the "lines of code" will be executed. If the condition is a logical false, then the "lines of code" will be skipped over. The loop stops at the `end`, such that the code is bracketed by the `if` and `end`. The lines of code to be executed if the condition is true is usually indented.

An example of an `if` loop:

```
myNumber = input('Enter a number: ');

if myNumber > 0

    disp('Your number is greater than zero!')

end
```

The above code asks the user to enter a number in the command window and saves it as `myNumber`. If the condition (`myNumber > 0`) is true, then the command will display the text 'Your number is greater than zero!'. If the number input is less than or equal to zero, the function will not execute anything. Try copying the code into your command window and entering a positive and negative value as inputs.

## The `else` statement

You will note that in the above `if` loop that no output is shown when the condition is not met (i.e. false). A second set of code can be specified to run in the situations where the `if` condition is not met, using the `else` statement. The general form for using an `else` statement is this:

```
if condition
    
    first set of code

else

    second set of code

end
```

The `if` condition is evaluated first. If the condition is met (i.e. true), the first set of code is executed. If the condition is not met (i.e. false), the second set of code is executed instead.

Note that the `if`, `else` and `end` statements are kept on the same level of indentation, with the executed code indented. This programming architecture is good practice to make sure that the loops are clearly bracketed, and the executed code is clear. Additionally, certain programming languages such as Python require the loops be indented properly to function!

Adding to our example, we can have the console say that the number input is not greater than zero (when the `if` condition is false):

```
myNumber = input('Enter a number: ');

if myNumber > 0

    disp('Your number is greater than zero!')

else

    disp('Your number is not greater than zero!')

end
```

Try inserting a positive and negative number as inputs. You'll find that inserting a negative number as an input will now generate a response.

The `if else` loop allows choosing to execute one of two sets of code. There are two ways of writing loops to choose from more than two sets of code.

## Nested `if` loops

Nested loops are loops that are written inside another loop. Let's say for our `myNumber` example that when the number input is zero, we want the console to state that! In the `else` section of the loop, we can specify another `if` loop to do that:

```
myNumber = input('Enter a number: ');

if myNumber > 0

    % This will be executed if myNumber is greater than zero
    
    disp('Your number is greater than zero!')

else

    % This section will be executed if myNumber is not greater than zero
    
    if myNumber == 0

        disp('Your number is zero!')

    else

        disp('Your number is less than zero!')

    end

end
```

Try inserting a positive number, a negative  number and zero as your values for `myNumber`.

Starting from the top of the `if` loop, the first condition is checked: is `myNumber` greater than zero? If that is true, it will execute the first section of code. If it is not true, the `else` section of the first `if` loop will be executed.

So, in that case, the nested `if` loop is executed. If `myNumber` equals zero, it will execute `disp('Your number is zero!')` , and if it doesn't, it will execute `disp('Your number is less than zero!')`. 

Note how the second `if` loop has been indented. This helps distinguish it from the overall `if` loop and also allows the second `if` loop to be organised. Also note how both `if` loops have an `end` statement to denote where the loop has finished.

## The `elseif` statement

A more efficient method of choosing between more than two options of code is using the `elseif` statement. It is used following an initial `if` statement in this general form:

```
if condition

    first set of code

elseif second condition

    second set of code

else

    third set of code

end
```

The first `if` condition is evaluated and if it is not satisfied, the second condition (next to `elseif`) is then evaluated. If that condition is  satisfied, the second set of code is executed. If not, it moves on to the `else` section of the loop.

Rewriting the above example of nested `if` loops using the `elseif` is a bit more efficient:

```
myNumber = input('Enter a number: ');

if myNumber > 0

    disp('Your number is greater than zero!')

elseif myNumber == 0

    disp('Your number is equal to zero!')

else

    disp('Your number is less than zero!')

end
```

Note that the elseif statement has no space, which is not the case in other languages such as R and Python. Try inputting a positive number, a negative number and zero as inputs for `myNumber` in this loop. 

## An exercise

Let's say we are trying to write some code that will square root a number that the user inputs. The normal `sqrt()` function will give the imaginary square number but let's make our function say you cannot square a negative number. Open a new script and save it as 'sqrtinput.m' and try to write the loop!

## The `for` loop

We use the `for` loop when we need to repeat lines of code or a function. Every time we repeat the loop is called an *iteration*. We iterate through a *loop variable* for a defined number of times. A `for` loop is usually formatted this way:

```
for loopVariable = range

    function

end
```

The range here is the range of values that the loop variable will iterate the function. Just like `if` loops, `for` loops require an end. Here's an exmaple:

```
for i = 1:3

    fprintf('I will not fall asleep.\n')

end
```

This will output the string `I will not fall asleep` three times, once for each of the times that our loop variable `i` is iterated. Usually for loops contain the loop variable within the code. It is common for programmers to use `i` as their loop variable, but I prefer to use a variable name that is informative. This is helpful when preallocating values to a vector or matrix. Here is an example of using a `for` loop to preallocate values:

```
numTrials = 3;

for thisTrial = 1:numTrials

    myNumberVector(thisTrial) = randi(10);

end

disp(myNumberVector)
```

This code will pick a random integer between 1 and 10, and save it to `myNumberVector`. Following the end of the `for` loop, `myNumberVector` will be displayed in the console.

We define the number of iterations ('trials') before the `for` loop starts (a handy habit to have is to initialise the parameters you'll use such that later code still functions with any changes to the parameter value). Try running this code again but change `numTrials` to a different number above zero. You'll notice the vector corresponds to `numTrials` (i.e. the number of iterations!).

## Combining `for` and `if` loops

We can combine these control statements into the same loop. Let's try write a code that asks the user to input three different numbers and returns if they're even or odd.

A very useful function for this is the `mod` function, short for 'modulus' and similar to a remainder function. It takes two arguments, the number to-be-divided and the number to divide by. Try this and see if you make sense of this:

```
mod(1:10,4)
```

Let's try write a function that takes inputs from the user and returns if the number is even or odd!

```
numTrials = 3;

for thisTrial = 1:numTrials

    myNumber = input('Enter a number: ');

    if mod(myNumber,2) == 0

        disp(Your number is even!)

    else

        disp(Your number is odd!)

    end

end
```

The `if` loop is nested within the `for` loop (note the programming architecture where the `end` statements are level with their beginning control statements). We repeat the `if` loop on each iteration of `thisTrial` and it checks whether `myNumber` is even. If so, it says so! If not, it says the number is not!

## A `for` loop within a `for` loop

Imagine you are running a change detection task with four colours for three blocks of 100 trials. On each trial, one of these four colours changes. You'll predetermine which colour changes on each trial. 

A useful function that will help us do this is the `randi` function, which produces a random integer. Let's try save the output of each iteration to a matrix, where each row is a block, and each column is a trial.

```
numBlocks = 3;      % Number of blocks
numTrials = 100;    % Number of trials

allChanges = NaN(numBlocks,numTrials);      % Creates a matrix to save the changes

for thisBlock = 1:numBlocks

    for thisTrial = 1:numTrials

        allChanges(thisBlock,thisTrial) = randi(4);     % Random integer from 1 to 4

    end

end
```

I have left comments on lines, hopefully explaining what is achieved by each line of code.

Note that this type of preallocation using `randi` does not guarantee that each item from one to four is equally represented in each block or across all the trials. We'll tackle this another time.









