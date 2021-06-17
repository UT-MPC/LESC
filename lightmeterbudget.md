```template
input.onButtonPressed(Button.A, function () {
    basic.showNumber(totalTime)
})
let totalTime = 0
let timing = false
let startTime = 0
totalTime = 0
let threshold = 100
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
basic.forever(function () {
    if (input.lightLevel() < threshold) {
        if (timing == true) {
            timing = false
            totalTime = (input.runningTime() - startTime) / 1000
        }
    } else {
        if (timing == false) {
            timing = true
            startTime = input.runningTime()
        }
    }
})

```

# LESC Light Meter with Budget

## Step 1

What you created to address requirements 1 through 3 is shown below. We need to add a budget variable and flash the LEDs when the user's budget has run out.

## Step 2

First, create a new ``||Variable:Variable||`` called ``||Variable:budget||``. Set its initial value to some reasonable number of seconds (something you're willing to test with). Here, we'll use 10 seconds, even though that's an unreasonable budget.

```blocks
let totalTime = 0
let timing = false
let startTime = 0
let threshold = 100
let budget = 10
```

## Step 3

The only other thing we need to change is what we display to the LEDs. So we'll change the ``||Basic:forever||`` block that contains the LED display code. We'll need to add an ``||Logic:if... then... else||`` block inside this ``||Basic:forever||`` block. We want to do what we were doing before *if* the budget is not expired. If the budget is expired, then we want to do something different.

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

That's all folks!
