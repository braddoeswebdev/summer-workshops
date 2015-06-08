---
series: 'electronics'
number: 3
title: "Blinking Lights"
icon: 'flash'
desc: "Let's write some code to control a light!"
---
# Blinking Light

So far, we've just been using 2 pins on our Teensy - the power and the ground.  Let's give one of the other pins a shot.  Hook up an LED to pin 13 (through a resistor) and ground, as shown:

![Blinking LED](/img/08-blink.png)

The LED you hooked up should now be turning on and off in sync with the LED on the Teensy!  Just as a test to make sure it's working correctly, the Teensys come with a program loaded on them already that just turns whatever is connected to pin 13 on and off.  Here's a trick: let's see what happens if we flip it around.  Connect the positive side of the LED to power and the negative side to pin 13.  Now it's backwards - when the Teensy LED is off, ours is on, and vice versa.  Why is that?  When we "turn on" a pin, it connects to the 3V pin and pushes a charge out.  When it gets  "turned off", it connects to the GND pin.

<div class="panel panel-primary">
<div class="panel-heading">Before you continue, show this to one of the adult-y people</div>
  <div class="panel-body" markdown="1">

Hook up 2 LEDs - one that does the same thing as the Teensy LED, and another that's doing the opposite.

</div>
</div>

## Programming the Teensy

So this is all well and good, but what if we don't want to use pin 13 to make an LED blink?  Or what if we want it blinking faster or slower?  Looks like we need to write our own program!  Start up the **Arduino** program on your computer.

![Arduino Software](/img/arduino.png)

The first thing we need to do is make sure it knows we're going to be programming on a Teensy and not another kind of microcontroller.  Under the *Tools* menu, open the *Board* list and choose the **Teensy LC**.

Now let's look at the template the software gave us to start our program with:

~~~~
void setup() {
  // put your setup code here, to run once:

}

void loop() {
  // put your main code here, to run repeatedly:

}
~~~~

There are 2 **functions** defined here: `setup` and `loop`.  The lines beginnning with `//`s are called **comments** - little notes that you can leave for yourself in your program.  The comments in the template tell us what these functions do:  the `setup` function runs once when your Teensy starts to get your program ready to run, then the `loop` functions will run over and over again.  Let's fill in these functions with some code to make our LED blink.  We're going to use 3 different functions in our code: `pinMode`, `digitalWrite`, and `delay`.  Let's look at what each of those do:

* `pinMode(pin, mode)`: tells a pin what it's going to be doing in our program.  In our case, we want pin 13 to be an output pin that we can turn on and off.
* `digitalWrite(pin, value)`: tells a pin to turn on (`HIGH`) or off (`LOW`).
* `delay(ms)`: tells the Teensy to wait for the specified number of miliseconds before continuing.

No copying & pasting - type this in yourself!  Here's the code:

~~~~
void setup() {
  pinMode(13, OUTPUT);
}

void loop() {
  digitalWrite(13, HIGH);  
  delay(1000);
  digitalWrite(13, LOW);
  delay(1000);
}
~~~~

Our `setup` function just tells the Teensy to use pin 13 for output.  The `loop` function tells it to turn pin 13 on, wait a second, turn it off, and wait a second - then the `loop` function starts again, turns pin 13 on, waits a second... on and on until we unplug it.  Make sure you have the semicolons - the `;`s at the end of the lines that need them! Save your code somewhere, then hit the checkmark button in the upper-left to make sure your code is OK, and then hit the arrow button to push your code to your Teensy.

<div class="panel panel-primary">
<div class="panel-heading">Before you continue, show this to one of the adult-y people</div>
  <div class="panel-body" markdown="1">

Change your program to use a different pin, and make it blink faster.

</div>
</div>

## Input Programming

Now let's try to get one of our pushbuttons hooked up to the Teensy & have it control the LED.  Leave your LED hooked up with the negative end connected to the Teensy, and add this stuff to your breadboard:

![Teensy + Button](/img/09-button.png)

And here's the code:

~~~~
void setup() {
  // initialize the digital pin as an output.
  pinMode(13, OUTPUT);
  pinMode(12, INPUT);
}

// the loop routine runs over and over again forever:
void loop() {
  if(digitalRead(12) == HIGH) {
    digitalWrite(13, LOW);
  }else{
    digitalWrite(13, HIGH);
  }
}
~~~~

So... something's not right here.  When the button is pressed, it behaves as expected - the Teensy LED goes of and ours gets brighter.  When the button isn't pressed, both the Teensy LED & our other LED are lit up - that shouldn't be happening!  The problem is that the Teensy isn't sure what it's seeing on pin 12 when the button isn't pressed - it's not connected to power, but it's not connected to ground either... so it just picks one randomly!  Because it's switching so fast, your brain can't process that it's turning on and off - we just see it as being dimmer than usual.  You might have seen this when you were experimenting with the blinking program if you tried it with a delay of less than 10ms (remember that fact - we're going to use it later).  

Anyway, how do we fix this?  Basically, we need a way to connect the pin to ground when the button isn't being pressed.  What we want to do is connect the pin to ground through something with a lot of resistance, like one of those 10,000 ohm resistors in your kit.  Because it has a lot of resistance, the current won't flow through it unless it has to - like when the button isn't pressed.  When we push the button, it opens up a path with less resistance - through the Teensy - so the current will go that way instead.  

![Better Teensy + Button](/img/09a-button.png)

## Back to the Code...

So now that we see that the code works, let's look at it in a little more detail.  There are 4 new things in the last program - `if` and it's friend `else`, `digitalRead`, and `==`.  The `digitalRead` function is just the opposite of `digitalWrite`: it returns whether a pin is connected to power (`HIGH`) or ground (`LOW`).  The `==` lets us compare things - in this case, whether or not the value on pin 12 is `HIGH`.  `if` lets us make decisions inside the code, so the program only does certain things (enclosed in {}'s) if a condition is true.  `else` lets us say what happens when that condition is false (again, in another set of {}'s).  Note that an `else` has to come with an `if`.


<div class="panel panel-primary">
<div class="panel-heading">Before you continue, show this to one of the adult-y people</div>
  <div class="panel-body" markdown="1">

Show us your working LED & button setup.

</div>
</div>
