# LESC Light Meter Timer Tutorial

## Step 1

In this tutorial, we will create a program that calculates the total time that a light has been on, since the program has started. 

## Step 2

To do this, we're going to need a boolean variable, one whose value is either TRUE or FALSE. We'll call our variable timing, to indicate the state of whether our program is timing (i.e., the light is on) or not timing (i.e., the light is off). In the ``||Variables:Variables||`` tray, select "Make a variable" and enter the name "timing" in the popup window.

## Step 3

Just like in our previous program, we will also need a totalTime variable and a startTime variable. So create those, too. 

## Step 4

We will also need a threshold variable. That's the last one.

## Step 5

To start off our program, we need to initialize the values of these variables. The timing variable should initially be false, startTime and totalTime should be 0, and threshold should be set to whatever value to experimentally determined to be the difference between light and dark in your space. Grab a ``||Basic:on start||`` block, and put four ``||Variables:set||`` blocks within in, one for each variable.

```blocks
let timing = false
let threshold = 100
let totalTime = 0
let startTime = 0
```
