---
series: 'electronics'
number: 5
title: "Serial Communication"
icon: 'lightbulb-o'
desc: "Send information to your Teensy and get information back"
---
# Serial Communication

Your next task is to figure out a way to get your computer to talk back and forth with your Teensy.  To do this, we're going to use the *S* in *USB* - Serial.  **Serial communication** is about as simple as it gets for computers talking to each other - it's just sending 1s and 0s up and down a wire.  To experiment with serial communication, let's build a circuit that counts how many times you've pushed a button.  Put this together:

![Counter circuit](/img/11-counter.png)

Those wires connecting the 7 segment display are kind of a mess - it doesn't really matter which pin you connect each segment to, **as long as you keep track of what goes where!**

Let's start by just counting button presses - no serial, no display, no output of any kind.  We'll steal a bunch of code from the last lesson too:

~~~~
int counter = 0;
int reading = LOW;
int last = LOW;
int bounce = 100;
long bounceTime = 0;

int buttonPin = 8;

void setup() {
  pinMode(buttonPin, INPUT);
}

void loop() {
  reading = digitalRead(buttonPin);

  if(reading != last) {
    if(bounceTime > bounce) {
      if(reading == LOW) {
        bounceTime = 0;
        counter = counter + 1;
      }
    }
  }else{
    bounceTime = bounceTime + 1;
  }
  last = reading;
}
~~~~

Nothing really new to see here (nor is there anything at all to see yet!).  The only thing we're doing differently than last time is adding to a counter instead of switching the light on and off.  

This is boring - let's try this serial thing.  We need to do 2 things: call `Serial.begin(9600)` to tell the Teensy to set up the serial connection,  then we can write to the serial stream with the `Serial.println(data)` function.  

~~~~
int counter = 0;
int reading = LOW;
int last = LOW;
int bounce = 120;
long bounceTime = 0;

int buttonPin = 8;

void setup() {
  Serial.begin(9600);
  pinMode(buttonPin, INPUT);
  pinMode(13, OUTPUT);
}

void loop() {
  reading = digitalRead(buttonPin);

  if(reading != last) {
    if(bounceTime > bounce) {
      if(reading == LOW) {
        bounceTime = 0;
        counter = counter + 1;
        Serial.println(counter);
      }
    }
  }else{
    bounceTime = bounceTime + 1;
  }
  last = reading;
}
~~~~

Once your program finishes uploading, pull up the **Serial Monitor** under the *Tools* menu.  Push the button - you should see numbers start appearing in the serial monitor window!  Yay!  (if you don't see anything, flag someone down - there are a couple of things that could be going wrong)

Now, for the fun part... the 7 segment display.  Now, if I hated you all, I'd make you sit down and figure out which segments need to be turned on for each digit... but I don't, so I did it for you.  Copy & paste the following at the top of your code:

~~~~
byte segDigits[10][7] = { { 1,1,1,0,1,1,1 },  // = 0
                          { 0,0,1,0,0,0,1 },  // = 1
                          { 1,1,0,1,0,1,1 },  // = 2
                          { 0,1,1,1,0,1,1 },  // = 3
                          { 0,0,1,1,1,0,1 },  // = 4
                          { 0,1,1,1,1,1,0 },  // = 5
                          { 1,1,1,1,1,1,0 },  // = 6
                          { 0,0,1,0,0,1,1 },  // = 7
                          { 1,1,1,1,1,1,1 },  // = 8
                          { 0,0,1,1,1,1,1 }   // = 9
                         };
byte pinArray[9];
void pinSetup(byte s0, byte s1, byte s2, byte s3, byte s4, byte s5, byte s6, byte dp) {
  pinArray[0] = s0;
  pinArray[1] = s1;
  pinArray[2] = s2;
  pinArray[3] = s3;
  pinArray[4] = s4;
  pinArray[5] = s5;
  pinArray[6] = s6;
  pinArray[8] = dp;
  for(int i=0;i<8;i++) {
    pinMode(pinArray[i], OUTPUT);
  }
}

void writeDot(byte dot) {
  digitalWrite(pinArray[7], !dot);
}

void writeDigit(int digit) {
  for(int i=0;i<7;i++) {
    digitalWrite(pinArray[i], !segDigits[digit][i]);
  }
}
~~~~

That gives you 3 new functions:

- **pinSetup(s0, s1, s3, s5, s6, s8, s9, dp)** sets those pins as `OUTPUT` pins and tells the other functions where each segment is.  Call this in `setup`.
- **writeDot(dot)** turns the dot on and off.
- **writeDigit(digit)** displays the given digit on the display.

You need to know one other piece of information to make this work.  If you try to display a `10` on the display, it's not going to work out well for you.  We need a way to keep just the last digit of a number.  Enter **modulus**, or the remainder after division.  If you divide any number by 10, the remainder will be the last digit of the number.  To calculate the remainder, use the `%` operator - so `27 % 10` would return `7`.

<div class="panel panel-primary">
<div class="panel-heading">Before you continue, show this to one of the adult-y people</div>
  <div class="panel-body" markdown="1">

Modify your program to use the provided code to display the last digit of the counter on your 7 segment display.  Show us that both the display & the serial monitor are displaying the counter.

</div>
</div>
