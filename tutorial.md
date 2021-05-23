# LESC Light Meter Tutorial -- Activity 1.1

## Step 1

This tutorial will be our first introduction to the MakeCode programming platform. We will create a simple program that will use a sensor on the @boardname@ to detect the level of ambient light.

## Step 2

On your screen, you see two blue *blocks*. They say ``||Basic:on start||`` and ``||Basic:forever||``. 

## Step 3

The ``||Basic:forever||`` block tells the program to do something, repeatedly, forever. In this program, we don't need the ``||Basic:forever||`` block, so click on it and then press the delete key on your keyboard.

## Step 4

The ``||Basic:on start||`` block tells the program what to do when it first starts.  We don't need it either. Delete it, too.

## Step 5

Instead, we want to measure the light level every time the user presses button A and display it every time they press button B.

## Step 5

The first thing we need to do is to create a *variable* we will use to store the light level. Click on ``||Variables||`` and select *Make a Variable*. We should name our new variable *light* so type that in the  window that pops up, then click OK. You will see more options appear in the ``||Variables||`` tray.

## Step 7

Next, we want to set the value of the *light* variable any time the user presses the A button. First we need activate an action when the button is pressed. Choose ``||Input:on Button Pressed||`` from the ``||Input:Input||`` tray. 

```blocks
input.onButtonPressed(Button.A, function () {
})
```

## Step 8

Choose ``||Variables:set light to||`` and drag the block inside the ``||Input:on Button Pressed||`` block.

```blocks
input.onButtonPressed(Button.A, function () {
    light = input.lightLevel()
})
```

## Step 9

Now, instead of the value of the light being 0, we want to get the value from the light sensor. You can find this sensor value in the ``||Input||`` tray; it's called ``||Input:lightLevel||``. Drag ``||Input:lightlevel||`` to replace the 0.

```blocks
light = input.lightLevel()
```

## Step 10

At this point, your program is successfully retrieving the light value. But you don't know what it is! We need to display it on the @boardname@'s LEDs. To do this, select ``||Basic:show number||`` from the ``||Basic||`` tray, drag it after the ``||Variables:set light to||`` block, and replace the 0 with your variable's name.
```blocks
input.onButtonPressed(Button.A, function () {
    light = input.lightLevel()
    basic.showNumber(light)
})
```

## Step 11

Now, on the simulated @boardname@ on your screen, you should see the light value in the upper left corner (it says 128). When the program starts, it will sense this fictitious light level and display it as a scroll on the screen.

## Step 12

Next, try it on your own device. Download the code to your computer, drop it on your @boardname@, and see if you can observe the light reading when the program starts.
