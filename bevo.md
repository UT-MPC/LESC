# LESC You Belong Here

## Step 1

This tutorial provides a very basic program that uses strings -- sequences of letters.

## Step 2

On your screen, you see two blue *blocks*. They say ``||Basic:on start||`` and ``||Basic:forever||``. 

## Step 3

The ``||Basic:forever||`` block tells the program to do something, repeatedly, forever. The ``||Basic:on start||`` block tells the program what to do when it first starts.  In this program, we don't need the ``||Basic:on start||`` block, so click on it and then press the delete key on your keyboard.

## Step 4

Within the ``||Basic:forever||`` block, we want our program to continuously scroll the message *Bevo - You Belong Here*. Start by dragging a ``||Basic:show string||`` block inside the mouth of the ``||Basic:forever||`` block.

```blocks
basic.forever(function () {
    basic.showString("Hello!")
})
```

## Step 5

Within the string (i.e, "Hello") change the text to "Bevo - You Belong Here".

```blocks
basic.forever(function () {
    basic.showString("Bevo - You Belong Here")
})
```

## Step 6

Now, on the simulated @boardname@ on your screen, you should see your new string continuously scrolling across the LED display.

## Step 7

Next, try it on your own device. Download the code to your @boardname@, and see if it works.
