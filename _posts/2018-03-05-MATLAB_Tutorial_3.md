---
title: MATLAB Tutorial 3
---

These notes recap my third MATLAB tutorial which further explore
matrices.

2-Dimensional Matrices
----------------------

Let's start by creating a matrix of random numbers:

    >> myMatrix = rand(4)

This will create a 4 by 4 matrix of randomly generated numbers between 0
and 1 and save it as `myMatrix`.

-   Indexing

We can call a specific value from a matrix in two different ways.
Firstly, we can use *linear indexing*:

    >> myMatrix(5)

This will output the 5th element of `myMatrix`. Remember that MATLAB
'counts' down the columns from left to right. This means that in our 4
by 4 matrix, the 5th element will be the first element in the second
column. A more nuanced way of indexing is *subscript indexing*:

    >> myMatrix(1,3)

This will output the element that is in the first row, third column of
`myMatrix`. Remember that the first argument corresponds to which row,
and the second argument corresponds to which column.

An example of the way we used matrices in cognitive research is to
record participant's data. Let's imagine `myMatrix` corresponds to the
percentage correct of each participant in each block. Each row is a
different participant, each column is a different block.

    >> myMatrix = myMatrix*100

We have just converted the numbers in `myMatrix` to percentages out of
100. Imagine if we wanted to plot only the second participant's data. A
useful way to pull out that data as a vector is using the colon operator
(`:`):

    >> participantTwo = myMatrix(2,:)

This will output all the values of the second row of `myMatrix`. In our
example, this would be the percentage correct for all four blocks
(columns) for our second participant. Similarly, we can pull out a
column vector from our matrix:

    >> thirdBlock = myMatrix(:,3)

The corresponding column vector is the third column of `myMatrix`. In
our example, this would be the percetange correct for all our
participants on the third block.

Matrices as arguments for functions
-----------------------------------

Let's look at some useful functions and how they handle vectors and
matrices. Earlier, I've saved `participantTwo` and `thirdBlock` as a row
vector and column vector respectively, as well as `myMatrix`, which is
serving as our data matrix.

-   `max` function

The `max` function returns the largest value. Let's find out what the
highest percentage correct our second participant got:

    >> max(participantTwo)

This should return the largest value in that vector! What if we wanted
to find the highest percentage correct by any participant in any block?

    >> max(myMatrix)

Notice here that this will output a vector of four values. This is
because this function (and most other basic functions) examine the
matrix by columns rather than all values. The resulting output is the
largest value for each of our (four) columns from `myMatrix`. To get the
largest of these values, we can just run the `max` function again,

    >> max(max(myMatrix))

The `min` function works similarly. Can you find what the smallest
percentage correct of all our participants was?

-   `mean` function

The `mean` function returns the average value and work similarly to the
`max` function we just used. Let's say we wanted to find mean
performance in the third block.

    >> mean(thirdBlock)

This will return the average performance of all our participants in the
third block! Now, what if we input the matrix as the argument rather
than a vector. It works similarly to the `max` function, such that it
will give the mean of each column in the matrix (the mean percentage
correct in each block!):

    >> mean(myMatrix)

What if we wanted to find the average performance of each participant,
rather than mean performance in each block? We can take advantage of the
fact that these functions evaluate columns of matrices and transpose our
matrix:

    >> mean(myMatrix')

Our matrix is transposed and now our participants are the columns, and
the blocks are the rows!

Another useful function is the `sum` function, which adds up all the
values. Can you figure out how to find the block with the largest sum of
percentage correct? You could do it like this:

    >> max(sum(myMatrix))

Some special matrices
---------------------

There are some special functions that are useful in generating matrices:

-   The `zeros` matrix

<!-- -->

    >> zeros(4)

The zeros matrix is commonly used to create "empty" data structures to
save to. Values can be added to the matrix in each cell, or a value can
be rewritten into the matrix. The above line of code creates a 4 by 4
matrix of zeros.

-   The `ones` matrix

<!-- -->

    >> ones(4)

`ones` is another useful function in generating matrices. The above line
of code creates a 4 by 4 matrix of ones.

-   The `NaN` matrix

<!-- -->

    >> NaN(4)

`NaN` stands for *not a number* and the above line of code creates a 4
by 4 matrix of NaNs. This kind of matrix is extremely useful for
preallocating values for something like the trials of a block, or
recording data. It's preferred over a zero matrix because a zero may be
a valid value for the matrix (such as a participant response on a scale
or a participant getting every trial response wrong). Also, it is easier
to spot a missing value in a NaN matrix. For example, if a participant
doesn't complete a block, the remaining unfilled matrix will be kept as
NaNs, rather than as zeros.

Matrix operations
-----------------

Above, we converted randomly generated decimals to percentage correct by
multiplying the matrix by 100. Similarly, we can divide the elements in
our data matrix by integers (scalars). Multiplying and dividing matrices
by scalars is fairly straightforward in MATLAB:

    >> myMatrix*3
    >> myMatrix/40

However, multiplying matrices by each other is different. Try the
following:

    >> myMatrix*ones(4)

Remember that `ones(4)` produces a 4 x 4 matrix of ones. The result you
get when multiplying a matrix of ones by `myMatrix` might be surprising
to you if you were expecting it to produce exactly the same matrix
(where each element is multiplied by one). This doesn't happen because
of *matrix algebra*, and is a potential pitfall in data analysis because
it spits output and doesn't look like an error! As long as the number of
rows in your matrix (or vector) matches the number of columns in your
second matrix (or vector), the operation will function. You should be
wary of this when working with *square matrices* like we are here.

When you want to multiply corresponding elements in two of the
same-sized matrices, use a `.` in front of the operation.

    >> myMatrix.*ones(4)
    >> myMatrix./ones(4)

This will multiply and divide the corresponding elements. Since we
multiply and divide by one, we get the same matrix out.

Try executing these lines to see this similarly with vectors:

    >> vectorOne = 2:5
    >> vectorTwo = randperm(20,4)
    >> vectorOne*vectorTwo
    >> vectorOne.*vectorTwo
    >> vectorOne./vectorTwo

Dividing and multiplying vectors and matrices is useful in experimental
psychology when you might have random conditions with different number
of trials and conditions in each, such that you might have to divide
corresponding elements in vectors or matrices.

3-D Matrices
------------

Matrices can go beyond the two-dimensions of rows and columns. For 3
dimensional matrices, I like to refer to the third dimension as
'layers'.

    >> my3Dmatrix = randi(100,2,3,4)

This will produce a 3-D matrix of 2 rows, 3 columns and 4 "layers" (a 2
x 3 x 4 matrix) containing random integers from 1 to 100. This might
occur if you have for example, two conditions with three different
stimuli and four blocks.

A useful function is `size`, which will give you the length of all the
dimension of your vector or matrix, no matter how many dimensions it
contains.

    >> size(myMatrix)
    >> size(my3Dmatrix)

The same operations apply to 3-D matrices as they do to 2-D matrices.
