---
series: 'electronics'
number: 1
title: "Glowy Things"
icon: 'lightbulb-o'
desc: "Let's play with LEDs"
---
# Glowy Things

**LED**s, or *Light Emitting Diodes*, are a simple and common electronic component.  **Diodes** are components that only let electrons flow through in one direction - if you hook it up backwards, it will act like it's not connected at all.  LEDs are special diodes that convert electrical energy into light if the current is flowing in the right direction.  Notice that one leg of the LED is longer than the other - the longer one gets connected to the positive, and the short one is connected to the negative or ground.

Let's light up a simple LED. The picture shows a red LED, but you can use whichever color you want - it's hard to tell which is which since the plastic parts are all clear.  Note that the long leg of the LED - indicated by the bent leg in the diagram (which is kind of hard to see in this one) - is on top.

![Base LED Setup](/img/02-light.png)

Note that we didn't directly connect the LED straight to the power connection with a wire - we used a **resistor** in there instead.  A resistor resists the flow of electrical current.  Left to their own devices, an LED will pull as much power as it is given - enough that it can fry the LED!

Note that you have 2 different kinds of resistors.  Those colored bands around the resistor tell us how much resistance it has, measured in **ohms**.  The one we used for this circuit has a resistance of 330 ohms, which isn't too much - just enough to light the LED, but not enough to burn it out.  The other one, with the black stripe in the middle, has 10,000 ohms of resistance.  If you try that resistor instead, the LED probably won't light up at all.

Let's make this a little more interesting.  Let's add a button that controls whether the light is on or not.  

![Button LED Setup](/img/03-button-light.png)

These pushbuttons are a little weird - the pins that are across from each other are always connected, whether the button is pushed or not.  When you push the button, it connects all the pins together.  Most of the time, we'll connect things through a button like we did in this example - diagonally across from each other.

![Button Diagram](/img/button.png)

<div class="panel panel-primary">
<div class="panel-heading">Before you continue, show this to one of the adult-y people</div>
  <div class="panel-body" markdown="1">

Build a circuit that lights up an LED only while 2 buttons are being pressed.

</div>
</div>

## Series & Parallel Circuits

We can run multiple LEDs at the same time too.  There are 2 ways to do this: *series* and *parallel*.  2 components are in series if the electricity flows from one component into the other.  The buttons you just hooked up were in series with the LED.  Let's try a circuit that has 2 LEDs in series - hook this up and see what happens.

![Series LED Setup](/img/04-series.png)

Did you see what happened?  You probably didn't - because nothing visible happened!  Why didn't this work?

I'll tell you why - there's not enough energy!  When you connect things in series, it divides the voltage equally to each component.  Since we have 3.3 volts going out, each LED gets around 1.7 volts. These LEDs need around 2-2.2 volts to glow, so it's enough to light them up.  So how do we get them to light up?  More voltage!  Move the wire you have from the 3V pin on the Teensy to the 5V pin - 5 volts divided by 2 gives us 2.5 volts, which is enough to get the LEDs to light up a little bit.

![Better series LED Setup](/img/04a-series.png)

Now let's try a parallel circuit.  Parallel components are each independently connected to the voltage source & the ground.  Put this together:

![Parallel LED Setup](/img/05-parallel.png)

You'll note that both LEDs light up.  This time, each component gets the whole 3.3 volts.  However, that means that the circuit is pulling more **amps** - a measurement of the number of electrons moving past a point over time.  If we were powering this with a battery instead of a computer, the battery life would be cut in half.  We don't have to worry about it at this scale, but if you tried powering a lot of LEDs in parallel like this, you might fry your Teensy - it's only able to provide so many amps without burning itself out.

<div class="panel panel-primary">
<div class="panel-heading">Before you continue, show this to one of the adult-y people</div>
  <div class="panel-body" markdown="1">

Build a circuit that lights up 2 parallel LEDs only while a button is pressed.

</div>
</div>
