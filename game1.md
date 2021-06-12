```template
let x = 0
let y = 0
basic.forever(function () {
    led.unplot(x, y)
    if (input.acceleration(Dimension.X) < -600) {
        x = 0
    } else if (input.acceleration(Dimension.X) < -200) {
        x = 1
    } else if (input.acceleration(Dimension.X) < 200) {
        x = 2
    } else if (input.acceleration(Dimension.X) < 600) {
        x = 3
    } else {
        x = 4
    }
    if (input.acceleration(Dimension.Y) < -600) {
        y = 0
    } else if (input.acceleration(Dimension.Y) < -200) {
        y = 1
    } else if (input.acceleration(Dimension.Y) < 200) {
        y = 2
    } else if (input.acceleration(Dimension.Y) < 600) {
        y = 3
    } else {
        y = 4
    }
    led.plot(x, y)
})
```

# LESC Ball Game Tutorial

## Step 1

What you created as part of the basic accelerometer example is shown below. We're going to change it so that when we're "playing", we are trying to hit a randomly selected target. Each time we successfully "hit" the target, we'll display a check mark, then select a new target. We do this seven times in a row, then the program ends.

## Step 2

First, we need to create a counter variable. Initially it should be set to 0. Each time we hit the target, we'll add one to it, and when we reach 7, we stop. To create the variable, go to the ``||Variables:Variables||`` tray, then make a new variable named ``||Variables:counter||``. Use a ``||Basic:on start||`` block to initialize ``||Variables:counter||`` to ``||Logic:true||``.

```blocks
let counter = 0
let x = 0
let y = 0
```
