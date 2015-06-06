---
series: 'electronics'
number: 1
title: "Glowy Things"
icon: 'lightbulb-o'
desc: "Let's play with LEDs"
---
# Glowy Things

**LED**s, or *Light Emitting Diodes*, are a simple and common electronic component.  **Diodes** are components that only let electrons flow through in one direction - if you hook it up backwards, it will act like it's not connected at all.  LEDs are special diodes that convert electrical energy into light if the current is flowing in the right direction.  

Let's light up a simple LED. The picture shows a red LED, but you can use whichever color you want - it's hard to tell which is which since the plastic parts are all clear.

![Base LED Setup](/img/02-light.png)

Note that we didn't directly connect the LED straight to the power connection with a wire - we used a **resistor** in there instead.  A resistor resists the flow of electrical current.  Left to their own devices, an LED will pull as much power as it is given - enough that it can fry the LED!

Note that you have 2 different kinds of resistors.  Those colored bands around the resistor tell us how much resistance it has, measured in **ohms**.  The one we used for this circuit has a resistance of 330 ohms, which isn't too much - just enough to light the LED, but not enough to burn it out.  The other one, with the black stripe in the middle, has 10,000 ohms of resistance.  If you try that resistor instead, the LED probably won't light up at all.

Let's make this a little more interesting.  Let's add a button that controls whether the light is on or not.  

![Button LED Setup](/img/03-button-light.png)

These pushbuttons are what we call a **normally open switch**, meaning that when the button isn't pushed, the circuit isn't closed, so no current will flow.  When the button is pushed, it connects all the pins together so current can flow.  


## 

<div class="panel panel-primary">
<div class="panel-heading">Before you continue, show this to one of the adult-y people</div>
  <div class="panel-body" markdown="1">

Build a circuit that lights up an LED only while 2 buttons are being pressed.

</div>
