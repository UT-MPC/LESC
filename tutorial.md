# LESC Light Meter Tutorial -- Activity 1.1

## Step 1

This tutorial will be our first introduction to the MakeCode programming platform. We will create a simple program that will use a sensor on the @boardname@ to detect the level of ambient light. We will then display the level of ambient light using a plot on the @boardname@'s LEDs.

## Step 2

On your screen, you see two blue *blocks*. They say ``||Basic:on start||`` and ``||Basic:forever||``. 

## Step 3

The ``||Basic:forever||`` block tells the program to do something, repeatedly, forever. The ``||Basic:on start||`` block tells the program what to do when it first starts.  In this program, we don't need the ``||Basic:on start||`` block, so click on it and then press the delete key on your keyboard.

## Step 4

Within the ``||Basic:forever||`` block, we want to continuously measure the ambient light level then use the LEDs to display a plot of the changing light level.

## Step 5

The first thing we need to do is to create a *variable* we will use to store the light level. Click on ``||Variables||`` and select *Make a Variable*. We need to give our new variable a name (for example, *reading*). Type the name in the  window that pops up, then click OK. You will see more options appear in the ``||Variables||`` tray.

## Step 6

Next, we want to set the value of the *reading* variable to be the value that the @boardname@'s light sensors detect in the surroundings. Choose ``||Variables:set reading to||`` and drag the block inside the ``||Basic:forever||`` block.

```blocks
basic.forever(function () {
    reading = 0
})
```

## Step 7

Now, instead of the value of the light being 0, we want to get the value from the light sensor. You can find this sensor value in the ``||Input||`` tray; it's called ``||Input:lightLevel||``. Drag ``||Input:lightlevel||`` to replace the 0.

```blocks
basic.forever(function () {
    reading = input.lightLevel()
})
```

## Step 8

At this point, your program is successfully retrieving the light value. But you don't know what it is! We need to display it on the @boardname@'s LEDs. To do this, select ``||Led:plot bar graph||`` from the ``||Led:led||`` tray, drag it after the ``||Variables:set light to||`` block You need to replace the first 0 with your variable's name and the second 0 with the max value of the light reading (i.e., 255).

```blocks
basic.forever(function () {
    reading = input.lightLevel()
    led.plotBarGraph(
    reading,
    255
    )
})
```

## Step 9

Now, on the simulated @boardname@ on your screen, you should see the light value in the upper left corner (it says 128). When the program starts, it will sense this fictitious light level and display it as a scroll on the screen. You can drag the line between yellow and gray to adjust the fictional light value and see how your display plot changes.

## Step 10

Next, try it on your own device. Download the code to your @boardname@, and see if you can observe the plotted value changing as the ambient light level changes. Click Finish in the orange box to the right. The browser will take you to the primary makecode window and show you your program.
