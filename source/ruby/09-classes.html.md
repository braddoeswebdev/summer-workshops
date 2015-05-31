---
series: 'ruby'
number: 9
title: "Classes"
icon: 'rocket'
desc: "More kinds of objects for your programs"
---
# Classes

So far we've seen several different kinds, or classes, of objects: strings, integers, floats, arrays, and a few special objects (`true`, `false`, and `nil`) which we'll talk about later. In Ruby, these classes are always capitalized:  String,  Integer, Float, Array... etc. In general, if we want to create a new object of a certain class, we use new:

~~~~ ruby
a = Array.new  + [12345]  # Array  addition.
b = String.new + 'hello'  # String addition.
c = Time.new

puts 'a = ' + a.to_s
puts 'b = ' + b.to_s
puts 'c = ' + c.to_s
~~~~

~~~~ text
a = [12345]
b = hello
c = 2014-09-29 13:51:46 -0700
~~~~

Because we can create arrays and strings using  `[...]` and `'...'` respectively, we rarely create them using `new`. (Though it's not really obvious from the above example, `String.new` creates an empty string, and `Array.new` creates an empty array.) Also, numbers are special exceptions: you can't create an integer with `Integer.new`. You just have to write the integer.

## The Time Class

So what's the story with this `Time` class?  Time objects represent moments in time. You can add (or subtract) numbers to (or from) times to get new times: adding 1.5 to a time makes a new time one-and-a-half seconds later:

~~~~ ruby
time  = Time.new   # The moment I generated this web page.
time2 = time + 60  # One minute later.

puts time
puts time2
~~~~

~~~~ text
2014-09-29 13:51:46 -0700
2014-09-29 13:52:46 -0700
~~~~

You can also make a time for a specific moment using  `Time.mktime`:

~~~~ ruby
puts Time.mktime(2000, 1, 1)          # Y2K.
puts Time.mktime(1976, 8, 3, 10, 11)  # When I was born.
~~~~

~~~~ text
2000-01-01 00:00:00 -0800
1976-08-03 10:11:00 -0700
~~~~

Notice: that's when I was born in Pacific Daylight Savings Time (PDT). When Y2K struck, though, it was Pacific Standard Time (PST), at least to us West Coasters. The parentheses are to group the parameters to `mktime` together. The more parameters you add, the more accurate your time becomes.

You can compare times using the comparison methods (an earlier time is less than a later time), and if you subtract one time from another, you'll get the number of seconds between them. Play around with it!

<div class="panel panel-primary">
<div class="panel-heading">Before you continue, show this to one of the adult-y people</div>
  <div class="panel-body" markdown="1">

Write a program that asks what year, month, and day you were born, then figure out many days old you are.

</div>
</div>

## The Hash Class

Another useful class is the Hash class. Hashes are a lot like arrays: they have a bunch of slots which can point to various objects. However, in an array, the slots are lined up in a row, and each one is numbered (starting from zero). In a hash, the slots aren't in a row (they are just sort of jumbled together), and you can use any object to refer to a slot, not just a number. It's good to use hashes when you have a bunch of things you want to keep track of, but they don't really fit into an ordered list. For example, the colors I use for different parts of the code which created this tutorial:

~~~~ ruby
colorArray = []  # same as Array.new
colorHash  = {}  # same as Hash.new

colorArray[0]         = 'red'
colorArray[1]         = 'green'
colorArray[2]         = 'blue'
colorHash['strings']  = 'red'
colorHash['numbers']  = 'green'
colorHash['keywords'] = 'blue'

colorArray.each do |color|
  puts color
end
colorHash.each do |codeType, color|
  puts codeType + ':  ' + color
end
~~~~

~~~~ text
red
green
blue
strings:  red
numbers:  green
keywords:  blue
~~~~

If I use an array, I have to remember that slot 0 is for strings, slot 1 is for numbers, etc. But if I use a hash, it's easy! Slot 'strings' holds the color of the strings, of course. Nothing to remember. You might have noticed that when we used  `each`, the objects in the hash didn't come out in the same order we put them in. Arrays are for keeping things in order, not hashes.

Though people usually use strings to name the slots in a hash, you could use any kind of object, even arrays and other hashes (though I can't think of why you would want to do this...):

~~~~ ruby
weirdHash = Hash.new

weirdHash[12] = 'monkeys'
weirdHash[[]] = 'emptiness'
weirdHash[Time.new] = 'no time like the present'
~~~~

Hashes and arrays are good for different things; it's up to you to decide which one is best for a particular problem.

<div class="panel panel-primary">
<div class="panel-heading">Before you continue, show this to one of the adult-y people</div>
  <div class="panel-body" markdown="1">

Use a hash to make a list of a few teachers & what room they're in, then print it out nicely.

(If you don't have room numbers memorized, just make some up)

</div>
</div>

## Creating Classes

We've seen a number of different classes of objects. However, it's easy to come up with kinds of objects that Ruby doesn't have. Luckily, creating a new class is pretty easy. Let's say we wanted to make some dice in Ruby. Here's how we could make the Die class:

~~~~ ruby
class Die

  def roll
    1 + rand(6)
  end

end

# Let's make a couple of dice...
dice = [Die.new, Die.new]

# ...and roll them.
dice.each do |die|
  puts die.roll
end
~~~~

~~~~ text
4
2
~~~~

And that's it! Objects of our very own.

We can define all sorts of methods for our objects... but there's something missing. Working with these objects feels a lot like programming before we learned about variables. Look at our dice, for example. We can roll them, and each time we do they give us a different number. But if we wanted to hang on to that number, we would have to create a variable to point to the number. It seems like any decent die should be able to have a number, and that rolling the die should change the number. If we keep track of the die, we shouldn't also have to keep track of the number it is showing.

However, if we try to store the number we rolled in a (local) variable in `roll`, it will be gone as soon as  `roll` is finished. We need to store the number in a different kind of variable:

## Instance Variables

Normally when we want to talk about a string, we will just call it a string. However, we could also call it a string object. Sometimes programmers might call it an instance of the class String, but this is just a fancy (and rather long-winded) way of saying string. An instance of a class is just an object of that class.

So instance variables are just an object's variables. A method's local variables last until the method is finished. An object's instance variables, on the other hand, will last as long as the object does. To tell instance variables from local variables, they have `@` in front of their names:

~~~~ ruby
class Die

  def roll
    @numberShowing = 1 + rand(6)
  end

  def showing
    @numberShowing
  end

end

die = Die.new
die.roll
puts die.showing
puts die.showing
die.roll
puts die.showing
puts die.showing
~~~~

~~~~ text
6
6
4
4
~~~~

Very nice! So `roll` rolls the die and  `showing` tells us which number is showing. However, what if we try to look at what's showing before we've rolled the die (before we've set @numberShowing)?

~~~~ ruby
class Die

  def roll
    @numberShowing = 1 + rand(6)
  end

  def showing
    @numberShowing
  end

end

# Since I'm not going to use this die again,
# I don't need to save it in a variable.
puts Die.new.showing
~~~~

~~~~ text

~~~~

Hmmm... well, at least it didn't give us an error. Still, it doesn't really make sense for a die to be "unrolled", or whatever `nil` is supposed to mean here. It would be nice if we could set up our new die object right when it's created. That's what `initialize` is for:

~~~~ ruby
class Die

  def initialize
    # I'll just roll the die, though we
    # could do something else if we wanted
    # to, like setting the die with 6 showing.
    roll
  end

  def roll
    @numberShowing = 1 + rand(6)
  end

  def showing
    @numberShowing
  end

end

puts Die.new.showing
~~~~

~~~~ text
3
~~~~

When an object is created, its `initialize` method (if it has one defined) is always called.

Our dice are just about perfect. The only thing that might be missing is a way to set which side of a die is showing... why don't you write a `cheat` method which does just that! Come back when you're done (and when you tested that it worked, of course). Make sure that someone can't set the die to have a  `7` showing!

<div class="panel panel-primary">
<div class="panel-heading">Before you continue, show this to one of the adult-y people</div>
  <div class="panel-body" markdown="1">

Flesh out your Die class.  First, add a `cheat` method.  Then change some things around so that we can make dice with any number of sides that we want.  Make your `initialize` method take an argument for the number of sides it has, and then change the `roll` and `cheat` methods to match.

</div>
</div>
