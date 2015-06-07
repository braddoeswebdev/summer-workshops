---
series: 'electronics'
number: 4
title: "Building a Light Switch"
icon: 'lightbulb-o'
desc: "Learning more basic programming concepts in order to turn your light on and off... again"
---
# Building a Light Switch

Right now, your light is on while your button is pressed down, and goes off while the button isn't pressed.  Let's make this a little more useful - when you push the button, the light switches on or off (i.e. off - *push button* - on - *push button* - off).  Change your circuit from the last lesson around a little bit:

![Switch circuit](/img/10-switch.png)

There's nothing new about the circuit - but the code needs a few new things.  Most importantly, we need a way to keep track of whether the light is on or not, so we know whether to turn it on or off the next time the button gets pressed.

## Variables

You can think of variables like little labelled boxes into which we can put data.  We can look and see what's in the box, or we can put something else in the box.  In our case, we'll need a variable to keep track of the status of the light.  Let's look at some code that uses a variable:

~~~~
int light = HIGH;

void setup() {
  pinMode(13, OUTPUT);
  pinMode(12, INPUT);
}

void loop() {
  if(digitalRead(12) == HIGH) {
    if(light == HIGH) {
      light = LOW;
    }else{
      light = HIGH;
    }
  }
  digitalWrite(13, light);

}
~~~~

The first line creates a new variable called `light` and puts `HIGH` in it.  The `int` at the beginning of the line tells the Teensy what kind of data this box will hold - in this case, an integer, or whole number.  Because we made it outside the `setup` and `loop` functions, we can use it inside both of them.  If we made it inside one of the functions, it would only be accessible inside that function - and if we made it inside `loop`, we'd get a new box each time it ran - not all that useful, most of the time.

If you look further down, you see we use the `light` variable in an `if` statement to determine if the light is already on - if it is, we turn it off, `else` we turn it on.  We use the `light` variable again at the end to actually turn the light on or off.

Run this & try pushing the button a few times.  It doesn't work great, right?  Not that we'll see this much **noise** at this scale, but it might just turn on or off on it's own due to random electrical signals floating around.  What happens if you hold down the button?  That should give you a clue as to what's happening here.  The LED dims when you hold the button down because it's turning on and off really really fast.  What can we do?

Let's try adding a delay after you push the button.  How long should we delay?  Experiment with some different values & see what you think.

~~~~
if(digitalRead(12) == HIGH) {
    if(light == HIGH) {
      light = LOW;
    }else{
      light = HIGH;
    }
    delay(50);
  }
~~~~

You can experiment as long as you want - you're not going to find a perfect number.  Too small, and it's going to turn on and off while you're pushing the button.  Too large, and it won't work if you push the button too fast.  And either way, it still switches on and off while you're holding the button down.  We're going to have to try something a little more complex...

We'll need a couple more variables - the current state of the button (`reading`), the state of the button the last time `loop` ran (`last`), the minimum time that the button has to be pressed for it to count (`bounce`), and how long the button has been pressed (`bounceTime`).

~~~~
int light = HIGH;
int reading = LOW;
int last = LOW;
int bounce = 100;
int bounceTime = 0;

void setup() {
  pinMode(13, OUTPUT);
  pinMode(12, INPUT);
}

void loop() {
  reading = digitalRead(12);

  if(reading != last) {
    if(bounceTime > bounce) {
      if(reading == LOW) {
        bounceTime = 0;
        if(light == HIGH) {
          light = LOW;
        }else{
          light = HIGH;
        }
      }
    }
  }else{
    bounceTime = bounceTime + 1;
  }

  digitalWrite(13, light);
  last = reading;
}
~~~~

3 completely new things here. First is the `!=`: read it as **not equal to** - it does the opposite of `==`.  The next line uses an `>` in the `if` - it returns true if the first thing is bigger than the second.  So, if the button changes, and the button has been pressed for long enough, and we take our finger off the button so it's not pressed anymore, then we reset the counter and switch the light.

The other new thing is the `+` - the Teensy is a computer, so it's capable of doing simple arithmetic as well as turning LEDs on and off.  In addition to `+`, we have `-`, `*` for multiplication, and `/` for division.

This is a little complicated, so read over the code a time or 2 and make sure you understand what's going on before continuing.

## Not!

That last program was kind of long & unpleasant.  Let's learn a trick to make it shorter.  Look at this:

~~~~
if(light == HIGH) {
  light = LOW;
}else{
  light = HIGH;
}
~~~~

That's kind of a lot of code to switch a variable back and forth.  Since `HIGH` and `LOW` are opposites, wouldn't it be nice if there was a way to just say something like `light = the opposite of light`?  In fact, there is something that does that - the `!`.  You can read the `!` as **not**, and just like `!=` is 'not equal', `!HIGH` would be 'not `HIGH`', which is `LOW`.  That means we can replace those 5 lines with 1 - `light = !light;`!  Here's the shorter program:

~~~~
int light = HIGH;
int reading = LOW;
int last = LOW;
int bounce = 100;
int bounceTime = 0;


void setup() {
  pinMode(13, OUTPUT);
  pinMode(12, INPUT);
}

void loop() {
  reading = digitalRead(12);

  if(reading != last) {
    if(bounceTime > bounce) {
      if(reading == LOW) {
        bounceTime = 0;
        light = !light;
      }
    }
  }else{
    bounceTime = bounceTime + 1;
  }

  digitalWrite(13, light);
  last = reading;
}
~~~~

<div class="panel panel-primary">
<div class="panel-heading">Before you continue, show this to one of the adult-y people</div>
  <div class="panel-body" markdown="1">

Wire up another LED on another pin.  Make it do the opposite of the LED that's already there.

</div>
</div>
