```template
let reading = 0
basic.forever(function () {
    reading = input.lightLevel()
    led.plotBarGraph(
    reading,
    255
    )
})
```

# LESC Light Detector Part 2

## Step 1

What you created as part of the first light detector step is shown below. We're going to change it so that we continuously sense the value of the light level and store it in the reading variable. When the user presses the A button, we'll print the value of the reading variable to the LEDs, and when the user presses the B button, we'll plot the bar graph of the light level for the next five seconds then clear the screen.

## Step 2

First, drag a ``||Input:on button A pressed||`` block from the ``||Input:Input||`` onto your workspace. When we press the A button, we want to display the light level. Use a ``||Basic:show number||`` block, along with your ``||Variables:reading||`` variable to do this.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.showNumber(reading)
})
```

## Step 3

Next, we want to plot the bar graph only when the user presses the B button and not continuously. Drag a ``||Input: on button A pressed||`` block from ``||Input:Input||`` onto your workspace. Change the A to a B. Move the ``||Led:plot bar graph of reading||`` block from the ``||Basic:forever||`` block and into the ``||Input:on button B pressed||`` block.

```blocks
input.onButtonPressed(Button.B, function () {
    led.plotBarGraph(
    reading,
    255
    )
})
basic.forever(function () {
    reading = input.lightLevel()
})
```

## Step 4

Now, though, the bar graph still stays on the screen. We want to make it disappear after 5 seconds. Drag a ``||Basic:pause||`` block into the ``||Input: on button B pressed||`` block after the ``||Led:plot bar graph of reading||`` block. Change the time to 5 seconds. Then place a ``||Basic:clear screen||`` block at the end.

```blocks
input.onButtonPressed(Button.B, function () {
    led.plotBarGraph(
    reading,
    255
    )
    basic.pause(5000)
    basic.clearScreen()
})
```

## Step 5

That's it! Try it out in the simulated @boardname@ and download it to your device to see if it works.
