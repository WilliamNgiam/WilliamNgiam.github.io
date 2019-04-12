---
title: MATLAB Tutorial 7
---

These notes recap an introduction session to using PsychToolbox, a MATLAB toolbox commonly used in conducting experiments for stimulus display and recording responses. This first introduction includes a demo of drawing text and colours, teaching concepts of windows, rects and flips.

## Initializing the PsychToolbox window

When running an experiment using PsychToolbox (PTB), there are a few initial lines of code that help set up stimulus display.

```
AssertOpenGL;       % 
```

screenID = max(Sreen('Screens'));   % Returns the screen number to display monitor
Screen('Preference','SkipSyncTests',1); % Set to 1 to skip any sync tests
```
[ptbWindow, winRect] = PsychImaging('OpenWindow', screenID, [], [], [], [], [], 6); 
```

```
[screenWidth, screenheight] = RectSize(winRect);
screenCentreX = round(screenWidth/2);
screenCentreY = round(screenHeight/2);
flipInterval = Screen('GetFlipInterval', ptbWindow);
```

## Drawing text (`DrawFormattedText`)

In an experiment, text is often required when conducting an experiment, especially for instructions at the beginning, or when asking the participant for a response or informing the participant of a break. Firstly, let's define the desired text to be shown:

```
text = ['Hello world!'];
```

To draw text, we simply use the `DrawFormattedText` function.