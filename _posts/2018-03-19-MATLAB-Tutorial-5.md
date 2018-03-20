---
title: MATLAB Tutorial 5
---

These notes build on writing `if` loops and `for` loops and introduces plotting in MATLAB. 

## Revisiting loops to generate data

Consider the following equation:

![Equation 1](http://www.sciweavers.org/upload/Tex2Img_1521351948/eqn.png)

We're going to generate these values from *-5 < x < 5* so we can plot the function later. For each value of x, we need to calculate the appropriate value (we'll call them *y*) according to the function above. The end goal of our code is to have a vector of *y* values. I'll also be writing this code in a way that makes things a little easier to change later on.

To generate a line plot, we (usually) need two vectors: one for our x-coordinates, and one for our corresponding y-coordinates. We need to write code to calculate what the appropriate y-values will be for our chosen x-values:

```
lowerBound = -5;    % The minimum bound of x values
upperBound = 5;     % The maximum bound of x values

xValues = lowerBound:upperBound;        % Generate a vector of x values
numPoints = numel(xValues);             % Number of x values

for thisPoint = 1:numPoints

    thisX = xValues(thisPoint);
    
    if thisX < 0

        thisY = 0;

    elseif  thisX >=0 && thisX <= 2

        thisY = thisX*2;

    else

        thisY = thisX^2;

    end

    yValues(thisPoint) = thisY;

end
```

At the top of the code, the `lowerBound` and `upperBound` are defined allowing this to be easily changed. This is better than writing `for x = -5:5` for a few reasons here. It is a good habit to define variables at the top of the code instead of hard coding it into the `for` loop, especially in situations when we might reuse that variable. Changing the value is easier than searching for the `for` loop and rewriting the values into the code.

Below that, I've created a vector for our `xValues` and found the number of points in this vector using the `numel` functions. I did this because we're not starting from a straightforward value like 1 in this case. So the number of points will vary.

The `for` loop iterates for the number of points I have in my x-values vector (`numPoints`). With each iteration, it retrieves a x-value and checks if `thisX < 0`. If so, the y-value is 0. If not, it *then* checks if this x-value is greater than or equal to zero and less than or equal to two. **Note** how I have defined the condition in the `elseif` section of the loop. The following condition does not quite work:

```
0 <= thisX <= 2
```

This won't work because the left hand side of the condition (`0 <= thisX`) will be evaluated first. Because we've already defined in our `if` condition something for when `thisX` is less than zero, this will always be true, and spit out a logical 1 value! Then the right hand side of the condition is evaluated, whether our logical 1 value is less than two, which is always true! Therefore, this `elseif` condition will always be met and not what we want.

Lastly, the `else` section is for the rest of our x-values that we have left over.

Check your vectors by typing their variables names into the command window:

```
xValues
yValues
```

## Plotting in MATLAB (using the `plot` function)

Welcome to our first data analysis/visualisation in our tutorials! We'll plot the values we generated above so we can visualise the function. This might be similar to plotting your experimental data.

The general format of the plot functions is simply `plot(x,y)`, where `x` and `y` are vectors for the x-coordinates and y-coordinates respectively. They have to be matched, so the vectors have to be the same length.

Let's quickly plot our values from above:

```
figure;     % Opens a new figure window
plot(xValues,yValues);
```

Hopefully, you'll see three noticeable different sections to this line plot, for three of the different sections in our function. You'll notice that the right-most section of the function (where `x` on the horizontal axis is greater than 2) does not quite look like a parabola. We haven't defined enough values to shape the function. Let's revisit the data we have generated and create a finer-grained line:

```
% Generate data
lowerBound = -5;    % The minimum bound of x values
upperBound = 5;     % The maximum bound of x values

xValues = lowerBound:.1:upperBound;        % Generate a vector of x values
numPoints = numel(xValues);             % Number of x values

for thisPoint = 1:numPoints

    thisX = xValues(thisPoint);
    
    if thisX < 0

        thisY = 0;

    elseif  thisX >=0 && thisX <= 2

        thisY = thisX*2;

    else

        thisY = thisX^2;

    end

    yValues(thisPoint) = thisY;

end

% Plot data
figure;
plot(xValues,yValues);
```

I've changed the `xValues` to be a vector between -5 and 5 but with steps of .1 rather than the default 1. We now have 110 points rather than the 11 points we generated earlier. I've included the plotting code to the bottom of our script.

## Improving the look of our plot

By default, the line plot will be a blue line that is typically unappealing and inappropriate for figures in manuscripts. Let's spruce it up!

### The line characteristics

The plot function accepts an argument to change the look of the line. For example:

```
plot(xValues,yValues,'kx');
```

This will plot the co-ordinates in black (the 'k' part of the 'kx' argument) and as crosses (the 'x' part of the 'kx' argument). Try the following arguments: `'ro'`, `'bs'`, `'g.`.

Other *line specifications* require two additional arguments: what the specification is, and a value for that specification. For example, we can manipulate the line width:

```
plot(xValues,yValues,'k-','LineWidth',3);
```

The size of the markers:

```
plot(xValues,yValues,'k.','MarkerSize',10);
plot(xValues,yValues,'k.','MarkerSize',20);
```

The color of the marker face:

```
plot(xValues,yValues,'ks','MarkerFaceColor','w');
plot(xValues,yValues,'ko','MarkerFaceColor','r');
```

The color of the marker edge:

```
plot(xValues,yValues,'s','MarkerEdgeColor','r');
```

Or all at once:

```
plot(xValues,yalues,'o','LineWidth',2,'MarkerSize',15, ...
'MarkerFaceColor','k','MarkerEdgeColor','y');
```

### Label the azes

Labelling our axes is very simple using the `xlabel` and `ylabel` functions:

```
figure;
plot(xValues,yValues,'k-');
xlabel('X');
ylabel('Y');
```

You can change the arguments for `xlabel` and `ylabel` to any string (remember to write them inside `''`).

### Change the axes

At the moment, it's hard to see the function for *x* is less than zero because it lies right on the axis edge. To change the axes, simply write `axis([XMIN XMAX YMIN YMAX])`, inputting the appropriate values inside our square brackets. For our plot, let's move the *y*-axis up a little:

```
figure;
plot(xValues,yValues,'k-');
xlabel('X');
ylabel('Y');
axis([-5 5 -20 20]);
```

### Some other things I like to change

I like to change the tick direction so that they're facing outwards rather than inwards. One useful function to manipulate the figure is `set`. The first argument for the `set` function can be the figure handle or `gca`. `gca` stands for *get current axes* and will manipulate the current figure you're working on.

Here's an example using the figure handle:
```
figureHandle = figure;
plot(xValues,yValues,'k-');
xlabel('X');
ylabel('Y');
axis([-5 5 -20 20]);
set(figureHandle,'TickDir','out');
```

And using `gca`:
```
figure;
plot(xValues,yValues,'k-');
xlabel('X');
ylabel('Y');
axis([-5 5 -20 20]);
set(gca,'TickDir','out');
```

There are many more options for manipulating figures and plots which are best learnt on an "as-needed" basis. The most common things I edit in the figure include `XTick`, `XTickLabel`, `XMinorTick`, `YTick`, `YMinorTick`, `TickLength`, `FontName`, `FontSize`. I also use the `box off` command to remove the box edge on the outside.

Saving the MATLAB figure as an .eps file lets you open it in Adobe Illustrator for further edits.

## Simulating data and plotting multiple functions

Let's plot multiple lines on the same figure axes! To generate the new data, I'm going to simulate the Rescorla-Wagner equation, a model of classical conditioning:

![Rescorla-Wagner DeltaV](https://wikimedia.org/api/rest_v1/media/math/render/svg/1a108fadc091ae8ac948090320d0a87b9317b724)

and

![Rescorla-Wagner V](https://wikimedia.org/api/rest_v1/media/math/render/svg/ba1eb2aed8d43f984a00348aa02c9e005b59c19c)

These equations were taken from the Wikipedia page on [Rescorla-Wagner](https://en.wikipedia.org/wiki/Rescorla%E2%80%93Wagner_model) which you can explore to further understand the parameters. Here, I'll generate two lines for two alpha parameter values:

```
beta = .2;      % Rate parameter
lambda = 1;     % Maximum conditioning
Vinitial = 0;   % Initial associative strength
numTrials = 100;

numPlots = 2;   % Let's have two plots, one for each alpha
allV = NaN(numPlots,numTrials);

for thisPlot = 1:numPlots

    if thisPlot == 1

        alpha = .2;

    elseif thisPlot == 2

        alpha = .8;

    end

    for thisTrial = 1:numTrials

        if thisTrial == 1

            V = Vinitial;

        end

        deltaV = alpha*beta*(lambda-V);
        V = V+deltaV;
        allV(thisPlot,thisTrial) = V;

    end

end
```

In the first row of the `allV` matrix, we've saved the associative strength across 100 trials with an `alpha` of .2, and the same thing in the second row with an `alpha` of .8. Plotting these is fairly straightforward with the `plot` function:

```
figure;
plot(allV');
end
```

We have to transpose the allV matrix here because it defaults to plotting by column rather than by row. This is a little tricky to edit each plot specifically so it might be preferable to plot in this way:

```
figure;
for thisPlot = 1:numPlots

    plot(allV(thisPlot,:));
    hold on;

end

alphaLabels = num2str([.2; .8]);
legend(alphaLabels,'Location','SouthEast');
```



