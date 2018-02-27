---
title: MATLAB Tutorial 2
subtitle: Stop "Boolean"" me
---

These notes recap the second MATLAB tutorial I gave, which covered
Boolean algebra and an introduction to vectors and matrices.

Boolean Algebra
---------------

Boolean algebra refers to a branch of mathematical algebra where the
variables are the truth values, *true* or *false*. This is sometimes
referred to as *relations* or *logicals*. Note that "true" and "false" are built into MATLAB. Try typing them in:

```
>> true
>> false
```

Note the corresponding output. A logical "1" corresponds to "true" and a logical "0" corresponds to "false".

-   < and >

MATLAB is able to check if one value is greater than or less than another value. ">" means "greater than" and "<" means "less than". Try these for example:

```
>> 3 < 5
>> 5 > 9
```

The first line is a <b>true</b> relation (3 is indeed less than 5). The output MATLAB gives is a "logical" 1, which means "true". The second line is a <b>false</b> relation. The output MATLAB gives is a "logical" 0, which means "false". You can also use relationals with single letters. Try this:

```
'a' < 'c'
```

This is "true". MATLAB converts letters to their corresponding integer in the alphabet ("a" = 1, "b" = 2, and so on), and performs the same relational test.

-   <= and >=

Just like "<" and ">", MATLAB is also capable of checking whether a value is "greater than or equal to" (>=) than another value, or "less than or equal to" (<=) another value. Note that in *R*, <- is used to assign values to variables. Try these:

```
>> 3 <= 5
>> 5 >= 13
>> 4 <= 4
>> 4 < 4
```

Just like previously, the first line will produce a "True", a logical "1", and the second line will produce a "False", a logical "0". Here, the third line will produce a "True" (4 is less than <b>or equal to</b> 4), whereas the fourth line will produce a "False" (4 is <u>not</u> less than 4).

-   == and ~=

Similarly, MATLAB can check whether two values are equal to each other in a logical test.

```
>> 3 == 3
>> 5 == 9
```

Note here the use of two equal signs. This is primarily because the equal operator is used for assigning variables and expressions.

You can also check if two values are not equal to each other using the "~" operator. Try this:

```
>> 4 ~= 6
>> 'a' ~= 'a'
```

-   && and ||

MATLAB can perform conditional logic tests using two expressions. The "AND" operator (&&) checks both expressions and will only output "True" if both expressions true themselves. Try this:
```
>> 3 < 5 && 4 ~= 7
```

The first expression ("3 is less than 5") is true, and so is the second expression ("4 is not equal to 7") is also true. Since both are true relations, MATLAB outputs a logical "true". However, if one expression is false:

```
>> 2 ~= 5 && 3 > 29
```

MATLAB will output a logical "false" because at least one statement is false (three is not greater than 29). Here is the truth table for the && operator:

|x|y|x && y|
|---|---|---|
|true|true|true|
|true|false|false|
|false|true|false|
|false|false|false|

The OR operator (||) works similarly. If at least one expression is true, then the overall logical expression is true. For example:

```
>> 2 ~= 5 || 3 > 29
```

Even though the second statement is false, this overall logical expression is "true". As long as <b>at least one</b> statement is true, then the OR expression is true. However, an OR expression will be false if both relations are false:

```
>> 2 < 1 || 5 == 10
```

Here is the truth table for the || operator:

|x|y|x || y|
|---|---|---|
|true|true|true|
|true|false|true|
|false|true|true|
|false|false|false|

-   The *xor* function

A useful conditional function is the "exclusive or" function.

```
>> help xor
```

This function takes two statements as arguemnts, and outputs "true" if <b>only one</b> expression is true. Try these commands:

```
>> xor(2 == 5, 3 ~= 4)
>> xor(1 ~= 20, 4 <= 10)
```

The first line outputs a logical "true" because only the seccond statement is true. However, the second line outputs a logical "false" because both statements are true. Here's the truth table for the *xor* function.

|x|y|xor(x,y)|
|---|---|---|
|true|true|false|
|true|false|true|
|false|true|true|
|false|false|false|

Vectors and Matrices
-------

Whilst most programming languages require definitions (i.e. defining the variable as a scalar, vector or string), MATLAB treats most things as matrices by default. A single scalar like "5" or "0.2" is a 1 x 1 matrix for example. Vectors, a 1-dimensional array of numbers, is a 1 x *n* matrix or a *n* x 1 matrix.

-   Creating row vectors

Vectors can be created like this:

```
>> thisVector = [1 2 3 4]
```

This is very different to *R* which uses a *concatenation* function. You can similarly use commas to create a vector:
```
>> anotherVector = [2, 7, 6, 5]
```

You can add row vectors to create a longer vector without a function:

```
>> longVector = [thisVector, anotherVector]
```

Adding vectors together in this way is called *concatenating* vectors.

-   Identifying elements in vectors

To retrieve an element within a vector, use the format *vector_name*(*element_position*). For example:

```
>> anotherVector(3)
```
The above line of code will output a 6, the *third* element of *anotherVector*. You can ask for multiple elements at once by inserting another vector:

```
>> longVector([2 8 5])
```

This will output the second, eighth and fifth elements of *longVector* in order.

You can use this indexing to reassign values to specific positions in the vector. For example:

```
>> anotherVector(2) = 4
```

The above line will reassign the *second* element in *anotherVector* to the value of 4. 

-   Creating column vectors

Column vectors (a 1-dimensional array of numbers going down) can be created by using semicolons (;) to define the end of each row:

```
>> columnVector = [3; 7; 5; 10]
```

Column vectors can also be created by transposing row vectors (and vice versa) using an apostrophe ('):

```
>> thisVector'
```

-   The : operator, linspace and logspace

The colon operator (:) is a useful way of generating vectors. For example:

```
>> 3:10
```

This creates a vector of all the integers between 3 and 10. You can also specify the size of the increments between the two limits. For example, to define a vector of all the odd numbers between 1 and 100:

```
>> oddNumbers = 1:2:100
```

You can also specify the increment to be a decimal:

```
>> 1:.5:30
```
-   Creating matrices

Creating a matrix is simply a combination of row and column vectors. You can explicitly enter values into matrix like so:

```
>> myMatrix = [2 9 3; 6 7 2]
```

This will create a "2 x 3" matrix. MATLAB defines 2-dimensional matrices first by rows then column. Also, matrices must be a complete rectangle; if there is a mismatch between the lengths of vectors being concatenated into a 2-dimensional matrix, an error will occur:

```
>> mat = [3 9 1; 2 8]
```

Running the previous line of code will produce this error:
```
Error using vertcat
Dimensions of matrices being concatenated are not consistent.
```

You can use the : operator and previously defined vectors to create matrices as well:

```
>> newMatrix = [thisVector; anotherVector]
>> anotherMatrix = [3:7,5:9]
```

-   Linear indexing

Identifying elements in a matrix is a little different to vectors. Try these:
```
>> myMatrix
>> myMatrix(1)
>> myMatrix(2)
>> myMatrix(3)
```

*myMatrix* is a 2 x 3 matrix we created earlier. You'll notice that MATLAB will process the matrix by going down the columns, such that the second element is in the <b>first column, second row</b> rather than second column, first row. This is called *linear indexing*.

-   Subscript indexing

To avoid confusion with linear indexing, it is best to use *subscript indexing*, where the row and column is specfied. For example:

```
>> myMatrix(1,2)
```

This will output the element that is in the *first* row, and the *second* column of *myMatrix*, a "9".






