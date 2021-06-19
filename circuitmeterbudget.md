```template
input.onButtonPressed(Button.A, function () {
    basic.showNumber(totalTime)
})
let totalTime = 0
let timing = false
let startTime = 0
totalTime = 0
let threshold = 100
let budget = 10
basic.forever(function () {
    if (timing == true) {
        totalTime = totalTime + (input.runningTime() - startTime) / 1000
        basic.pause(100)
        startTime = input.runningTime()
    }
    if (budget - totalTime > 0) {
        if (timing == true) {
            basic.showLeds(`
                # # # # #
                # # # # #
                # # # # #
                # # # # #
                # # # # #
                `)
        } else {
            basic.showLeds(`
                . . . . .
                . . . . .
                . . # . .
                . . . . .
                . . . . .
                `)
        }
    } else {
        basic.showLeds(`
            # # # # #
            # # # # #
            # # # # #
            # # # # #
            # # # # #
            `)
        basic.showLeds(`
            . . . . .
            . . . . .
            . . . . .
            . . . . .
            . . . . .
            `)
    }
})
basic.forever(function () {
    if (input.lightLevel() < threshold) {
        if (timing == true) {
            timing = false
        }
    } else {
        if (timing == false) {
            timing = true
            startTime = input.runningTime()
        }
    }
})
```

# LESC Circuit Meter with Budget

## Step 1
One example solution for Design Challenge #1 is shown below. We'll use this as a starting point for the second design challenge. We don't have to make a lot of changes, though. The only real difference is that, instead of using the light sensor, we'll measure whether pin P0 is pressed. All we really need to look at is the ``||Basic:forever||`` block that sets the ``||Variables:timing||`` variable to ``||Logic:true||`` and ``||Logic:false||``.

## Step 2

First, instead of comparing ``||Input:light level||`` to the ``||Variables:threshold||`` variable, we want to check if pin P0 is pressed. Change the condition on the ``||Logic:if||`` block.

```blocks
basic.forever(function () {
    if (input.pinIsPressed(TouchPin.P0)) {
        if (timing == true) {
            timing = false
        }
    } else {
        if (timing == false) {
            timing = true
            startTime = input.runningTime()
        }
    }
})
```

## Step 3

But now the two conditions are backwards. We want ``||Variables:timing||`` to be ``||Logic:true||`` when pin P0 is pressed and ``||Logic:false||`` when it is *not* pressed. To fix this, we just need to swap the two ``||Logic:if||`` blocks that are inside the outer ``||Logic:if||`` block.

```blocks
basic.forever(function () {
    if (input.pinIsPressed(TouchPin.P0)) {
        if (timing == false) {
            timing = true
            startTime = input.runningTime()
        }
    } else {
        if (timing == true) {
            timing = false
        }
    }
})
```

## Step 4

That should be everything we need! You can try this out on the simulated @boardname@ by using your mouse to "press" pin P0. But it's much more fun on the real @boardname@ using whatever you were using for a switch in the previous activity.
