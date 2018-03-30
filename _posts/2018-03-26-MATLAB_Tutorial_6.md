---
title: MATLAB Tutorial 6
---
These notes recap a 'live coding' session of a Rescorla-Wagner simulation, going through the use of a `while` loop.

## `While` loops

A while loop is useful when needing to reach a criterion or an event, but the number of loop iterations required to do so is unknown. The format for a `while` loop works like this:

```
while expression

    bunch of code

end
```

While the expression is true, the code within the `while` loop will be excuted. Once the expression is not met, then the code will not be executed and the loop is ended. For example:

```
x = 1;

while x < 10
    
    x = x + 1;

end
```

On each iteration of the `while` loop, the scalar variable `x` has one added to it. After enough iterations, `x` will eventually exceed 10, making the `x < 10` condition that defines the `while` loop false. This will end the while loop. In a way, the `x` variable here is a 'counter', which will be useful for our simulation later.

Another way of using `while` loops is to have a "switch" that turns on or off, depending on when we want the while loop to be iterated. Here's an example:

```
disp('Let us flip a coin until it shows tails')
mySwitch = true;

while mySwitch
    
    flip = randi(2);

    if flip == 1

        disp('Heads!');

    else

        disp('Tails!');
        mySwitch = false;

    end

end
```

In the above code, we have defined a switch called `mySwitch`, which we set to "on" or `true`. When mySwitch is true, the while loop gets iterated. It flips randomly a number between one and two, displayed `Heads!` for when it flips 1 and `Tails!` when it flips 2. When it does flip `Tails`, it turns the switch off by changing `mySwitch` to `false`, and the while loop gets terminated.

## Rescorla-Wagner Simulation

The Rescorla-Wagner model predicts the amount of learning from classical conditioning between a unconditioned stimulus and a conditioned stimulus. It uses the following equation to model learning:

![Rescorla Wagner Equation 1](https://wikimedia.org/api/rest_v1/media/math/render/svg/1a108fadc091ae8ac948090320d0a87b9317b724)

and

![Rescorla Wagner Equation 2](https://wikimedia.org/api/rest_v1/media/math/render/svg/ba1eb2aed8d43f984a00348aa02c9e005b59c19c)

where alpha is the salience of a cue (between 0 and 1), beta is the rate parameters (between 0 and 1), lambda is the maximum amount of conditioning, V is the associative strength.

Using this model, we will simulate how the rate of learning occurs over time when varying both alpha and beta at the same time. To do this, we will be looking at the number of trials required to reach a certain threshold, with different values of alpha and beta. I'll write my thought process as I go through the code.

### Setting up initial parameters

In any simulation or experimental code, the first things that should be defined are the parameters that you are working with. For this exercise, this means defining the alpha and beta values we want to use for our simulation, and what the values for the other parts of the Rescorla-Wagner equation will be.

```
% Initial parameters
threshold = .75;        % Required threshold for learning
lambda = 1;             % Setting maximum learning to 1
initialV = 0;           % Starting value for learning         

% Alpha values

minAlpha = 0.1;         % Minimum value for alpha
maxAlpha = 0.8;         % Maximum value for alpha
alphaIncrements = 0.01; % Size of increment that alpha changes at

allAlphas = minAlpha:alphaIncrements:maxAlpha;      % Vector containing all alphas
numAlphas = length(allAlphas);                      % The number of alphas to be tested

% Beta values

minBeta = 0.1;          % Minimum value for alpha
maxBeta = 0.8;          % Maximum value for alpha
betaIncrements = 0.01;  % Size of increment that alpha changes at

allBetas = minBeta:betaIncrements:maxBeta;         % Vector containing all betas
numBetas = length(allBetas);                        % The number of betas to be tested

% Save the number of trials for each combination of alpha and beta
allData = NaN(numAlphas,numBetas);
```

I've defined the `threshold`, `lambda` and `intialV` starting values for our simulation. Below that, I define a minimum and maximum value for alpha and beta, and also the size of step I want them to increase by. This allows me to easily change and define my vector of alpha and beta values (`allAlphas` and `allBetas`), if I choose to simulate different ranges of values. I've also asked for the number of alphas and betas I'm simulating (`numAlphas` and `numBetas`), knowing that I will have to save the number of trials for each combination of alpha and beta into a matrix. 

### Writing the simulation

Now to write the simulation. I've set up two `for` loops to select alpha and beta values to run the simulation. Once these values are selected, the changes to `V`, the metric for amount of learning, will occur within the `while` loop. The `while` loop is iterated when the condition is met, that the amount of learning is less than the required threshold (`V < threshold`). We have also set up a counter, simulating each trial, called `numTrials`. With each iteration of the `while` loop, this counter adds one (`numTrials = numTrials + 1`). When learning has reached the required threshold, the `while` loop no longer gets iterated, and the number of trials is then saved into our `allData` matrix.

```
for thisAlpha = 1:numAlphas

    alpha = allAlphas(thisAlpha);   % Alpha for each iteration of the for loop

    for thisBeta = 1:numBetas

        beta = allBetas(thisBeta);  % Beta for each iteration of the for loop

        V = initialV;
        numTrials = 0;

        while V < threshold

            numTrials = numTrials + 1;
            V = V + alpha*beta*(lambda-V);

        end

        allData(thisAlpha,thisBeta) = numTrials;

    end

end
```

### Visualising the results of our simulation

Let's visualise the number of trials it takes to reach the threshold for learning for each combination of alpha and beta:

```
image(allData);
ylabel('Alpha');
set(gca,'YTick',1:10:numAlphas);    % Changing y-axis ticks to appear at intervals of 10
set(gca,'YTickLabel',allAlphas(1:10:numAlphas));
xlabel('Beta');
set(gca,'XTick',1:10:numBetas,'XTickLabel',allBetas(1:10:numBetas));    % Changing x-axis tick labels
c = colorbar;       % Creating a colorbar for the image
c.Label.String = 'Number of trials to reach threshold of learning'  % Labelling the colorbar
```

A new figure should appear that is bright yellow in the top left corner getting gradually bluer towards the bottom right corner. The colorbar to the right of the screen shows the corresponding number of trials for the colour. Here, we can see that when alpha and beta are lower, the number of trials required to reach the threshold of learning is higher.

## Rescorla-Wagner Simulation - Simulating changing alpha, beta and lambda

Before scrolling further, try to write a simulation that finds the number of trials to reach a learning threshold for each combination of alpha, beta and lambda.

```
% Rescorla-Wagner Simulation

% Initialise required parameters

threshold = .75;    % End threshold for learning
initialV = 0;

minLambda = threshold+.01;    % Set min lambda above threshold to ensure condition is met
maxLambda = 1;
lambdaIncrements = 0.01;
allLambdas = minLambda:lambdaIncrements:maxLambda;
numLambdas = length(allLambdas);

minAlpha = 0.1;
maxAlpha = 0.8;
alphaIncrements = 0.01;  % Size of increment that alpha changes
allAlphas = minAlpha:alphaIncrements:maxAlpha;
numAlphas = length(allAlphas); % length(.1:.1:.8)

minBeta = 0.1;
maxBeta = 0.8;
betaIncrements = 0.01;  % Size of increment that beta changes
allBetas = minBeta:betaIncrements:maxBeta;
numBetas = length(allBetas);

% Save number of trials for each combination of alpha and beta
allData = NaN(numAlphas,numBetas,numLambdas);

% Run simulation

for thisAlpha = 1:numAlphas
    
    alpha = allAlphas(thisAlpha);
    
    for thisBeta = 1:numBetas
    
        beta = allBetas(thisBeta);
        
        for thisLambda = 1:numLambdas
            
            lambda = allLambdas(thisLambda);

            V = initialV;
            numTrials = 0;

            while V < threshold

                numTrials = numTrials + 1;
                V = V + alpha*beta*(lambda-V);

            end

            allData(thisAlpha,thisBeta,thisLambda) = numTrials;
            
        end
        
    end
    
end        

```

To visualise the data another way, you can use the `surf` function, which produces a 3-D surface plot. It's not often very useful in behavioural psychology to plot data in this way (at least that I've come across) but it does produce a cool visualisation of the data.

```
figure;
for ii = 1:numel(allData(1,1,:))
surf(allData(:,:,ii));
shading INTERP
hold on;
end
```




