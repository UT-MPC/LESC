```template
let y = 0
let x = 0
let playing = false
let targetY = -1
let targetX = -1
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
basic.forever(function () {
    if (playing == false) {
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
# LESC Wrist Game Tutorial

## Step 1

What you see below is the result of the game program before we attached the @boardname@ to the glove (or sock). All we need to do is to add in the control of the neopixel as part of the game. First, becuase we want to play exactly seven rounds of the game, the first thing we need to do is create a counter variable that starts at 0. Click on the ``||Variables||`` tray and make a new variable named counter.

## Step 2

At the beginning, we also need to set up our neopixel the way we did in the practice exercise. We do this in the ``||Basic:on start||`` block. If you need a hint, click the light bulb on the right.

```blocks
let counter = 0
let playing = false
let targetY = -1
let targetX = -1
let ring: neopixel.Strip = null
ring = neopixel.create(DigitalPin.P2, 7, NeoPixelMode.RGB)
for (let index = 0; index <= 6; index++) {
    ring.setPixelColor(index, neopixel.rgb(16, 16, 16))
    ring.show()
}
```

## Step 3

Next, we want to change our ``||Basic:forever||`` block that detects whether we have finished a round or not (whether the ball found the target). Instead of always starting a new round, we only want to start a new round if the counter hasn't reached 7 yet. We also want to increment the counter each time we win a round. Wrap the entire ``||Basic:forever||`` block in an ``||Logic:if||`` block that only runs if ``||Variables:counter||`` is less than 7, and add one to ``||Variables:counter||`` each time we win a round.

```blocks
basic.forever(function () {
    if (counter < 7) {
        if (playing == false) {
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
                counter += 1
                targetX = -1
                targetY = -1
                basic.pause(2000)
                basic.clearScreen()
            }
        }
    }
})
```

## Step 4

The last step is to light up the neopixel, one LED at a time. Since there are seven LEDs on the neopixel, we can use the ``||Variables:counter||`` variable as the index of the LED we should light up. Add this into the same ``||Basic:forever||`` block, just after you display the check for finding the target.

```blocks
basic.forever(function () {
    if (counter < 7) {
        if (playing == false) {
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
                ring.setPixelColor(counter, neopixel.colors(NeoPixelColors.Blue))
                ring.show()
                counter += 1
                targetX = -1
                targetY = -1
                basic.pause(2000)
                basic.clearScreen()
            }
        }
    }
})
```
