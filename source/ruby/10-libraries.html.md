---
series: 'ruby'
number: 10
title: "Libraries"
icon: 'book'
desc: "Using code that other people have written"
---
# Libraries

Bill Gates once said "I choose a lazy person to do a hard job because a lazy person will find an easy way to do it."  You've already seen a couple of ways to be a "lazy" programmer and save yourself some time, effort, and repetition: variables, using methods, writing methods of your own, using arrays & iterators to do things over and over again... but you haven't seen the pinnacle of laziness yet: using someone else's code.

Let's start with a simple scenario.  You've been at this programming thing for a while now.  You've probably got a collection of code you might like to use in other programs - some of the classes & methods you've made may be useful as you continue working on other things.  For example, you wrote a die class at the end of the last lesson.  That might be a useful class to have around. But how do you get it into your new program?  You could copy & paste it... but that sounds like work.  Plus, if you wanted to use that class again on another project, you'd have to copy & paste the whole thing again.  And what happens if you improve the class in one program - wouldn't it be nice to be able to have 1 die sitting somewhere that you can just pull into any program?

## Requiring Files

As it so happens, you can do just that.  Put your die class in a file all by itself & save it as `die.rb`.  Then create this new program in the same folder:

~~~~ ruby
require './die.rb'

d = Die.new 6
e = Die.new 20

puts d.showing
e.cheat 8
puts e.showing
~~~~

The `require` method goes and looks for a file & throws whatever it finds into your program.  I told it to look for our `die.rb` file in the same folder that this program is in - the `./` is a shortcut to the folder you're in right now.

## Gems

Great, so you can reuse bits of code that you've already written in other programs.  But what about code that someone else wrote?  We could go out on the Internet, find some code, and copy & paste it into a file... but that sounds like a lot of work.  Fortunately for us, Ruby comes with a nice, easy way to pull in bunches of code called RubyGems.  RubyGems is a set of tools that downloads, organizes, and helps our programs find "gems" - bundles of code that other people wrote & published for the world to use.  

You can't install gems for yourself here - you have to be an administrator to add new gems.  I've already installed a couple of fun ones for you to play with though. You include a gem into your code just like you would with a file you made: use `require` and the name of the gem.

*On your computer at home, you can install a gem by running `gem install ` and the name of a gem in a command line*

### colored

`colored` is a gem that gives your programs color.  When you `require colored` it adds a bunch of methods to the string class that change the color of the string when it gets printed to the screen.

- `"string".color` just turns the text the color you specify
- `"string".on_color` leaves the text alone, but changes the background color
- `"string".bold` makes the colors brighter (don't ask - it's a long story).

And here are the colors you can use:

- <span style="color: white; background-color: black">White</span> and <span style="color: white; background-color: black">Bright White</span> (they're the same thing, usually)
- <span style="color: black; background-color: white">Black</span> and <span style="color: #888; background-color: white">Bright Black</span>
- <span style="color: #800; background-color: white">Red</span> and <span style="color: #f00; background-color: black">Bright Red</span>
- <span style="color: #880; background-color: white">Yellow</span> and <span style="color: #ff0; background-color: black">Bright Yellow</span>
- <span style="color: #080; background-color: white">Green</span> and <span style="color: #0f0; background-color: black">Bright Green</span>
- <span style="color: #088; background-color: white">Cyan</span> and <span style="color: #0ff; background-color: black">Bright Cyan</span>
- <span style="color: #008; background-color: white">Blue</span> and <span style="color: #00f; background-color: black">Bright Blue</span>
- <span style="color: #808; background-color: white">Magenta</span> and <span style="color: #f0f; background-color: black">Bright Magenta</span>

~~~~ ruby
require 'colored'

puts "I'm green!".green
puts "Hey, I'm bright green!".green.bold
puts "Ew, I'm ugly! and hard to read!".red._on_blue
~~~~

As you can see from the example, you can use multiple methods on the same string to give it multiple effects.

<div class="panel panel-primary">
<div class="panel-heading">Before you continue, show this to one of the adult-y people</div>
  <div class="panel-body" markdown="1">

Write a short story that uses some colorful text for effect.  

</div>
</div>

### green_shoes

If you've made it this far, you're probably getting a little tired of boring little text-based programs with no pictures or buttons or anything.  `green_shoes` is another gem that lets you escape the command line & make some graphical programs.  

~~~~ ruby
require 'green_shoes'

Shoes.app do
  button "Push Me!" do
    alert "Hey, you can read!"
  end
end
~~~~

Instead of rambling on forever about all the things Green Shoes can do, I'm just going to send you over to the [Shoes Walkthrough](http://shoesrb.com/walkthrough/) to look at some simple programs that you can experiment with.  You might also want to look over the [Green Shoes Manual](http://ashbb.github.io/green_shoes/Hello!.html) for more detailed instructions.

This is the end of the Ruby lessons.  Have fun & make awesome stuff!
