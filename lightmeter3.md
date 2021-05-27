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

To start off our program, we need to initialize the values of these variables. The timing variable should initially be false, startTime and totalTime should be 0, and threshold should be set to whatever value to experimentally determined to be the difference between light and dark in your space. Grab a ``||Basic:on start||`` block, and put four ``||Variables:set||`` blocks within in, one for each variable. (You'll find the ``||Logic:false||`` value inside the ``||Logic:Logic||`` tray.


## Step 6

Recall our pseudocode:

forever
    if the light level is below the threshold
        if we were timing, stop timing, and add to the total time
    if the light level is above the threshold
        if we were not timing, start timing
        
## Step 7

We need a forever block, so grab a ``||Basic:forever||`` block from the ``||Basic:Basic||`` tray. Within the forever block, we need to implement some *conditional logic*. To do this, we'll use an if ... else statement. Locate it in the ``||Logic:Logic||`` tray and drag it inside the ``||Basic:forever||`` block.

## Step 8

Within the if statement, the condition is currently set to ``||Logic:true||``. Instead, we want it to test whether the value of the light level is below the threshold (i.e., the light is off). Look again in the ``||Logic:Logic||`` tray for the less than comparison block. Drag it into the ``||Logic:if||`` block to replace the ``||Logic:true||``. Replace the first 0 with ``||Input:lightlevel||`` and the second 0 with ``||Variable:threshold||``.


## Step 9 

Now the program will enter the if part of the condition block if the light level is less than the threshold. If the light level is greater than the threshold, the program will enter the else part of the block.

## Step 10

If the light is off (i.e., within the if part of the conditional), if we're currently timing, we need to stop timing, and add the elapsed time to the total time. To do this, we use another ``||Logic:if||`` block, but this time we check the value of the ``||Variables:timing||`` variable to see if it is ``||Logic:true||``. If so, we set it to ``||Logic:false||``, and add the elapsed time (i.e., ``||Input:running time||`` - ``||Variables:startTime||`` divided by 1000) to the ``||Variables:totalTime||``. 

## Step 11

The next step is to fill in what the program does when the light level is greater than the threshold (i.e., what happens in the else part of the block). In this case, the light is on. If we're not timing, we need to start timing. This means we need to set the ``||Variables:timing||`` variable to ``||Logic:true||`` and set the ``||Variables:startTime||`` to the current value of ``||Input:running time||``.

## Step 12

All that remains now are the display functions. First, when the user presses button A, we want to display the value of ``||Variables:totalTime||``.


## Step 13

The other display function just helps us tell that our program is working correctly. When the value of ``||Variables:timing||`` is ``||Logic::true||`` (i.e., the light is on), let's light up all 25 LEDs. When the value of ``||Variables:timing||`` is ``||Logic::false||`` (i.e., the light is on), let's light up just the center LED. To do this, we can actually create *another* ``||Basic:forever||`` block with an ``||Logic:if else||`` condition within it.

