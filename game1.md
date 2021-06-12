```template
let x = 0
let y = 0
basic.forever(function () {
    basic.pause(100)
    led.unplot(x, y)
    basic.pause(100)
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

First, we need to create a counter variable. Initially it should be set to 0. Each time we hit the target, we'll add one to it, and when we reach 7, we stop. To create the variable, go to the ``||Variables:Variables||`` tray, then make a new variable named ``||Variables:counter||``. Use a ``||Basic:on start||`` block to initialize ``||Variables:counter||`` to 0.

```blocks
let counter = 0
```

## Step 3

At the start of each round, we're going to need to select a random ``||Variables:targetX||`` and a random ``||Variables:targetY||``. Create both of these variables and set them both initially to -1 (since we haven't selected anything yet). We're also going to want to take a pause between each round, show the checkmark, and then start the new round. We don't want to show our ball while we're between rounds. So we need a variable to keep track of whether we're actively playing or not. So create a new variable ``||Variables:playing||``, and set its initial value to ``||Logic:false||``. 

```blocks
let targetX = -1
let targetY = -1
let playing = false
let counter = 0
```

## Step 4

As we said in the previous step, we're only going to want to show and move the ball with the accelerometer when we're actively ``||Variables:playing||``. Wrap the entire insides of the ``||Basic:forever||`` block in an ``||Logic:if||`` condition that only runs when ``||Variables:playing||`` is ``||Logic:true||`` and the ``||Variables:counter||`` is less than 7.

```blocks
basic.forever(function () {
    if (playing == true) {
        basic.pause(100)
        led.unplot(x, y)
        basic.pause(100)
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
    }
})
```

## Step 5

All that's left now is to handle the individual rounds. To do this, we'll use a second ``||Basic:forever||`` block. If the ``||Variables:playing||`` variable is ``||Logic:false||`` and the ``||Variables:counter||`` is less than 7, then we select a new random target pixel (i.e., random values for ``||Variables:targetX||`` and ``||Variables:targetY||``). You can find the random number generator in the ``||Math:Math||`` tray. Once we've selected these targets, we can set ``||Variables:playing||`` true ``||Logic:true||``.

```blocks
basic.forever(function () {
    if (playing == false && counter < 7) {
        targetX = randint(0, 4)
        targetY = randint(0, 4)
        led.plot(targetX, targetY)
        playing = true
    }
})
```

## Step 6 

Finally, we need to check to see if the ball has hit the target. Add an else block that is an alternative to the ``||Logic:if||`` in your new ``||Basic:forever||`` block. Within this, if ``||Variables:x||`` is equal to ``||Variables:targetX||`` and ``||Variables:y||`` is equal to ``||Variables:targetY||``, then we'll pause the game (by setting ``||Variables:playing||`` to ``||Logic:false||``), increment the ``||Variables:counter||`` variable, show a checkmark (but we'll want to show it upside down), set the targets to -1, wait for a couple of seconds, then clear the screen. Because ``||Variables:playing||`` will be ``||Logic:false||``, the next iteration will reset the targets and start the next round.

```blocks
basic.forever(function () {
    if (playing == false && counter < 7) {
        targetX = randint(0, 4)
        targetY = randint(0, 4)
        led.plot(targetX, targetY)
        playing = true
    } else {
        if (targetX == x && targetY == y) {
            playing = false
            basic.showLeds(`
                . . . # .
                . . # . #
                . # . . .
                # . . . .
                . . . . .
                `)
            targetX = -1
            targetY = -1
            basic.pause(2000)
            basic.clearScreen()
        }
    }
})
```
