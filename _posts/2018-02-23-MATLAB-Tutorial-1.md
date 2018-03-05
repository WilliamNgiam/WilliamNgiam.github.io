These notes recap the first MATLAB tutorial in which I introduced the MATLAB interface and some basics.

Console
-------

The console contains

-   Command Window

-   Workspace

This is where the variables that are created will be saved

-   Current Folder

This is where MATLAB is currently working. We'll learn more about
*paths* and *present working directory* later.

-   Command History

This is all the past commands and functions you've run in this session.
You can scroll through here and click on these to re-run a function

-   Prompts

This is where you run console commands.

Variables
---------

-   Initializing variables

Creating a variable saves the results of an equation or expression. It
uses the format *variablename = expression*.

    >> myNumber = 3 + 5

This creates the variable "myNumber" and saves it to the workspace. You
should see that myNumber has been saved with the value of 8, not the
expression.

-   Incrementing variables

Incrementing variables changes the value of the initialized variable, by
using the variable in the expression.

    >> myNumber = myNumber + 2

"myNumber" should appear in the workspace now with the value of 10 (i.e.
the variable "myNumber" has been updated). This will be useful later in
writing experimental code for trial loops or counters.

-   Variable names

Variable names can be made up of alphanumeric characters and
underscores, but must start with a letter. You can run into problems
with underscores in variable names so programmers usually use mixed
cases. Examples of variable names:

    this1thing
    thisVariable
    my_number
    my_number1

Types
-----

Unlike most programming languages, such as Python or R, MATLAB has four
types of objects and often do not require definition. You can run into
some problems with functions and variables mismatching in the required
types.

-   Double

Stands for double precision, usually just big numbers.

-   Single

Stands for single precision, smaller numbers. You won't encounter these
often.

-   Char

A bunch of characters, somtimes referred to as a "string". Defined using
inverted commas

    >> myName = 'William'

-   Logical

A true or false result.

To find the class of an object, you can use the function *class*.

    >> class(myNumber);
    >> class(myName);

Note that:

    >> class myNumber

produces a different result. This is because it treats *myNumber* here
as a string (it will appear in purple when you type it in the console).

Functions
---------

-   Calling functions

Functions can be used in prompts or writing scripts. The format is
*function\_name(arguments)*. For example:

    >> abs(-3)

Here, *abs* is the function being called, the absolute value function.
-3 is the argument for the function. The *abs* function takes the
argument and turns it into the positive value, 3 in this case!

-   Arguments

Different functions require different numbers of arguments (or none at
all!). Use the *help* function to figure out what arguments are required
for the function, and what order the arguments need to be input!

    >> help abs

Random Number Generating
------------------------

MATLAB isn't capable of being truly random. It relies on something
called a *seed*, which is a number that generates MATLAB's next random
events. Try this:

    >> rng('Shuffle')
    >> rand

This will generate a random decimal number between 0 and 1.

Now run this:

    >> rng(0)
    >> rand

I can predict you got 0.8147! Despite it being "random", I was able to
predict your result. This is because it relies on the seed number you
entered ("0" in this case) to generate the random sequence of results.
This is known as *pseudorandomness*. Reset the randomness by running:

    >> rng('Shuffle')

This will reset the seed to a different number.
