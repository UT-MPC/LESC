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

When the value of pin P0 is high (1), we want to count a scored goal. We will create a variable ``||Variable:goal||`` that aims to continuously store the value of P0 (i.e., the value of ``||Variable:goal||`` is 1 if pin P0 is high, and 0 otherwise). In the ``||Basic:forever||`` block, set the value of ``||Variable:goal||`` to the value of ``||Pins:digital read pin P0||``.

```blocks
basic.forever(function () {
    goal = pins.digitalReadPin(DigitalPin.P0)
})
```
