# LESC Scoreboard Tutorial

## Step 1

In this tutorial, we will create a program that uses our scoreboard circuit to keep track of scored goals and buzz everytime a goal is scored

## Step 2

Our first step is to deal with our first requirement: when the program starts, display an initial score of 0. We'll need a score variable to keep our score, so in ``||Variables:Variables||``, create a new variable named ``||Variables:score||``

## Step 3

In the ``||Basic:on start||`` block, set the value of the ``||Variables:score||`` variable to 0. Then, to give yourself some time to set up your goal after the program starts, add a pause of one second before any goals are scored. Then display the score.

```blocks
let score = 0
basic.pause(1000)
basic.showNumber(score)
```

## Step 4

When the value of pin P0 is high (1), we want to count a scored goal. We will create a variable ``||Variables:goal||`` that aims to continuously store the value of P0 (i.e., the value of ``||Variables:goal||`` is 1 if pin P0 is high, and 0 otherwise). In the ``||Basic:forever||`` block, set the value of ``||Variables:goal||`` to the value of ``||Pins:digital read pin P0||``.

```blocks
basic.forever(function () {
    goal = pins.digitalReadPin(DigitalPin.P0)
})
```

## Step 5

If the value of ``||Variables:goal||`` is 1, then we want to score a goal. Create an ``||Logic:if true then||`` block in the ``||Basic:forever||`` block, and change the condition to check whether the value of the ``||Variables:goal||`` variable is 1. If it is, increment the value of the ``||Variables:score||`` variable by 1.

```blocks
basic.forever(function () {
    goal = pins.digitalReadPin(DigitalPin.P0)
    if (goal == 1) {
        score = score + 1
    }
})
```

## Step 6

When the score is incremented, we also want to cause the buzzer to make a sound. To do this, we need to send a high (1) signal to pin P2. As long as the signal is high, the buzzer will vibrate, so we also need to stop the sound. We'll play it for a second. So use the ``||Pins:digital write pin P2||`` block to set the value to 1. Pause for a second (``||Basic:pause(ms) 1000||``), then set pin P2 to 0.

```blocks
basic.forever(function () {
    goal = pins.digitalReadPin(DigitalPin.P0)
    if (goal == 1) {
        score = score + 1
        pins.digitalWritePin(DigitalPin.P2, 1)
        basic.showNumber(score)
        basic.pause(1000)
        pins.digitalWritePin(DigitalPin.P2, 0)
    }
})
```
