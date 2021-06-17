```template
input.onButtonPressed(Button.A, function () {
    if (timing == true) {
        totalTime = totalTime + (input.runningTime() - startTime) / 1000
        startTime = input.runningTime()
    }
    basic.showNumber(totalTime)
})
let totalTime = 0
let startTime = 0
let timing = false
timing = false
startTime = 0
totalTime = 0
let threshold = 100
basic.forever(function () {
    if (input.lightLevel() < threshold) {
        if (timing == true) {
            timing = false
            totalTime = totalTime + (input.runningTime() - startTime) / 1000
        }
    } else {
        if (timing == false) {
            timing = true
            startTime = input.runningTime()
        }
    }
})
basic.forever(function () {
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
})
```

# LESC Light Meter with Budget

## Step 1

What you created to address requirements 1 through 3 is shown below. We need to add a budget variable and flash the LEDs when the user's budget has run out. Before, we were being lazy about updating the totalTime variable and only updated it when we needed to see what its value was. Now, since we want to know that our budget has expired as soon as it expires, we'll have to update totalTime continuously.

## Step 2

First, create a new ``||Variable:Variable||`` called ``||Variable:budget||``. Set its initial value to some reasonable number of seconds (something you're willing to test with). Here, we'll use 10 seconds, even though that's an unreasonable budget in the real world.

```blocks
let totalTime = 0
let timing = false
let startTime = 0
let threshold = 100
let budget = 10
```

## Step 3

The next thing we need to change is what we display to the LEDs. So we'll change the ``||Basic:forever||`` block that contains the LED display code. We'll need to add an ``||Logic:if... then... else||`` block inside this ``||Basic:forever||`` block. We want to do what we were doing before *if* the budget is not expired. If the budget is expired, then we want to do something different.

```blocks
basic.forever(function () {
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
```

## Step 4

Finally, we need to deal with the pesky problem that the ``||Variables:totalTime||`` variable needs to be always up to date so we can compare it to our ``||Variables:budget||`` variable. To achieve this, take the ``||Logic:if||`` block that we added to the ``||Input:on button A pressed||`` block, and move the entire thing to the top of the ``||Basic:forever||`` block that we use to run the display.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.showNumber(totalTime)
})
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
```

## Step 5

At this point, our program will work just fine, but there are two small fixes we can make to it. First, we're still updating the ``||Variables:totalTime||`` variable when the light goes on and off, but that's no longer necessary because we're also continuously updating it. You can remove this portion from the ``||Basic:forever||`` block that switches the ``||Variables:timing||`` variable between true and false.

```blocks
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

## Step 6

Finally, in our ``||Basic:forever||`` block, when we update the ``||Variables:totalTime||`` variable, we're doing it *really* fast. We can adjust how fast we do it by inserting a ``||Basic:pause||`` block, which will determine the *resolution* of our timer. For instance, if we add a 100ms pause, our timer resolution will be 0.1 seconds. This seems reasonable.

```blocks
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
```

## Step 7

That's it! Give it a try on your real device!
