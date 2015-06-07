---
series: 'electronics'
number: 2
title: "Fancy Lights"
icon: 'lightbulb-o'
desc: "Using your RGB LED & the 7-segment display"
---
# Fancy Lights

## RGB LED

You kit also contains an RGB LED - it's the one with 4 pins.  It works just like the regular single color LEDs, except they've all been jammed together into the same package so the colors blend together.  Just like the regular LEDs, the long pin gets connected to power through a 330 ohm resistor.  To turn on a color, you connect one of the pins to ground.  See this diagram to see which colors go with which pins:

![RGB LED Diagram](/img/rgb-led.jpg)

<div class="panel panel-danger">
<div class="panel-heading">Sidebar: <strong>Your art teachers have been lying to you forever</strong></div>
  <div class="panel-body" markdown="1">

There's a reason the LED has red, green, and blue components: they're what we call the **additive primary colors** because those 3 colors of light can be mixed together in various proportions to create pretty much any color you can think of, and mixing them all together prefectly equally creates white.

On the other hand, paint and ink are **subtractive** - mixing in more colors gets you closer to black.  This is the part your art teachers have been lying to you about - red, yellow, and blue are not the best primary colors!  You're much better off working with cyan, magenta, and yellow.  See [the wikipedia article](http://en.wikipedia.org/wiki/Primary_color) for more information.

</div>
</div>

Let's hook this thing up:

![RGB LED Diagram](/img/06-rgb.png)

You can disconnect & reconnect the ground wires to change the color.  

<div class="panel panel-primary">
<div class="panel-heading">Before you continue, show this to one of the adult-y people</div>
  <div class="panel-body" markdown="1">

Build a circuit that uses your 3 buttons to turn each individual color in your RGB LED on and off.

</div>
</div>

## 7-segment LED display

Your kit also comes with a 7-segment numeric display for displaying a number.  It works just like the RGB LED - 1 pin gets connected to power through a resistor, then you connect the other pins to ground to turn them on or off.

![7-seg Diagram](/img/07-7seg.png)

Experiment to see which connection controls which segment.  Or, you know, just look at this handy reference diagram:

![7-seg LED Diagram](/img/7-seg.png)

<div class="panel panel-primary">
<div class="panel-heading">Before you continue, show this to one of the adult-y people</div>
  <div class="panel-body" markdown="1">

Make your 7-segment display display a 1, then add a button that makes it display a 4 instead.

</div>
</div>
