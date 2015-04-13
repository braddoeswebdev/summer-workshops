---
series: 'ruby'
number: 7
title: "Writing Methods"
icon: 'pencil'
desc: "Write your own methods to save yourself some time & typing"
---
# Writing Methods

As we've seen, loops and iterators allow us to do the same thing (run the same code) over and over again. However, sometimes we want to do the same thing a number of times, but from different places in the program. For example, let's say we were writing a questionnaire program for a psychology student. From the psychology students I have known and the questionnaires they have given me, it would probably go something like this:

~~~~ ruby
puts 'Hello, and thank you for taking the time to'
puts 'help me with this experiment.  My experiment'
puts 'has to do with the way people feel about'
puts 'Mexican food.  Just think about Mexican food'
puts 'and try to answer every question honestly,'
puts 'with either a "yes" or a "no".  My experiment'
puts 'has nothing to do with bed-wetting.'
puts

# We ask these questions, but we ignore their answers.

goodAnswer = false
while (not goodAnswer)
  puts 'Do you like eating tacos?'
  answer = gets.chomp.downcase
  if (answer == 'yes' or answer == 'no')
    goodAnswer = true
  else
    puts 'Please answer "yes" or "no".'
  end
end

goodAnswer = false
while (not goodAnswer)
  puts 'Do you like eating burritos?'
  answer = gets.chomp.downcase
  if (answer == 'yes' or answer == 'no')
    goodAnswer = true
  else
    puts 'Please answer "yes" or "no".'
  end
end

# We pay attention to *this* answer, though.
goodAnswer = false
while (not goodAnswer)
  puts 'Do you wet the bed?'
  answer = gets.chomp.downcase
  if (answer == 'yes' or answer == 'no')
    goodAnswer = true
    if answer == 'yes'
      wetsBed = true
    else
      wetsBed = false
    end
  else
    puts 'Please answer "yes" or "no".'
  end
end

goodAnswer = false
while (not goodAnswer)
  puts 'Do you like eating chimichangas?'
  answer = gets.chomp.downcase
  if (answer == 'yes' or answer == 'no')
    goodAnswer = true
  else
    puts 'Please answer "yes" or "no".'
  end
end

puts 'Just a few more questions...'

goodAnswer = false
while (not goodAnswer)
  puts 'Do you like eating sopapillas?'
  answer = gets.chomp.downcase
  if (answer == 'yes' or answer == 'no')
    goodAnswer = true
  else
    puts 'Please answer "yes" or "no".'
  end
end

# Ask lots of other questions about Mexican food.

puts
puts 'DEBRIEFING:'
puts 'Thank you for taking the time to help with'
puts 'this experiment.  In fact, this experiment'
puts 'has nothing to do with Mexican food.  It is'
puts 'an experiment about bed-wetting.  The Mexican'
puts 'food was just there to catch you off guard'
puts 'in the hopes that you would answer more'
puts 'honestly.  Thanks again.'
puts
puts wetsBed
~~~~

~~~~ text
Hello, and thank you for taking the time to
help me with this experiment.  My experiment
has to do with the way people feel about
Mexican food.  Just think about Mexican food
and try to answer every question honestly,
with either a "yes" or a "no".  My experiment
has nothing to do with bed-wetting.

Do you like eating tacos?
>> yes
Do you like eating burritos?
>> yes
Do you wet the bed?
>> no way!
Please answer "yes" or "no".
Do you wet the bed?
>> NO
Do you like eating chimichangas?
>> yes
Just a few more questions...
Do you like eating sopapillas?
>> yes

DEBRIEFING:
Thank you for taking the time to help with
this experiment.  In fact, this experiment
has nothing to do with Mexican food.  It is
an experiment about bed-wetting.  The Mexican
food was just there to catch you off guard
in the hopes that you would answer more
honestly.  Thanks again.

false
~~~~

That was a pretty long program, with lots of repetition. (All of the sections of code around the questions about Mexican food were identical, and the bed-wetting question was only slightly different.) Repetition is a bad thing. Still, we can't make it into a big loop or iterator, because sometimes we have things we want to do between questions. In situations like these, it's best to write a method. Here's how:

~~~~ ruby
def sayMoo
  puts 'mooooooo...'
end
~~~~

~~~~ text

~~~~

Uh... our program didn't sayMoo. Why not? Because we didn't tell it to. We told it how to sayMoo, but we never actually said to do it. Let's give it another shot:

~~~~ ruby
def sayMoo
  puts 'mooooooo...'
end

sayMoo
sayMoo
puts 'coin-coin'
sayMoo
sayMoo
~~~~

~~~~ text
mooooooo...
mooooooo...
coin-coin
mooooooo...
mooooooo...
~~~~

Ahhh, much better. (Just in case you don't speak French, that was a French duck in the middle of the program. In France, ducks say "coin-coin".)

So we defined the method sayMoo. (Method names, like variable names, start with a lowercase letter. There are a few exceptions, though, like + or ==.) But don't methods always have to be associated with objects? Well, yes they do, and in this case (as with  puts and gets), the method is just associated with the object representing the whole program. In the next chapter we'll see how to add methods to other objects. But first...

## Method Parameters

You may have noticed that some methods (like  gets, to_s, reverse...) you can just call on an object. However, other methods (like +, -, puts...) take parameters to tell the object how to do the method. For example, you wouldn't just say  5+, right? You're telling 5 to add, but you aren't telling it what to add.

To add a parameter to sayMoo (let's say, the number of moos), we would do this:

~~~~ ruby
def sayMoo numberOfMoos
  puts 'mooooooo...'*numberOfMoos
end

sayMoo 3
puts 'oink-oink'
sayMoo  # This should give an error because the parameter is missing.
~~~~

~~~~ text
mooooooo...mooooooo...mooooooo...
oink-oink
#<ArgumentError: wrong number of arguments (0 for 1)>
~~~~

numberOfMoos is a variable which points to the parameter passed in. I'll say that again, but it's a little confusing:  numberOfMoos is a variable which points to the parameter passed in. So if I type in  sayMoo 3, then the parameter is 3, and the variable numberOfMoos points to 3.

As you can see, the parameter is now required. After all, what is sayMoo supposed to multiply  'mooooooo...' by if you don't give it a parameter? Your poor computer has no idea.

If objects in Ruby are like nouns in English, and methods are like verbs, then you can think of parameters as adverbs (like with sayMoo, where the parameter told us how to sayMoo) or sometimes as direct objects (like with puts, where the parameter is what gets putsed).

## Local Variables

In the following program, there are two variables:

~~~~ ruby
def doubleThis num
  numTimes2 = num*2
  puts num.to_s+' doubled is '+numTimes2.to_s
end

doubleThis 44
~~~~

~~~~ text
44 doubled is 88
~~~~

The variables are num and numTimes2. They both sit inside the method doubleThis. These (and all of the variables you have seen so far) are local variables. This means that they live inside the method, and they cannot leave. If you try, you will get an error:

~~~~ ruby
def doubleThis num
  numTimes2 = num*2
  puts num.to_s+' doubled is '+numTimes2.to_s
end

doubleThis 44
puts numTimes2.to_s
~~~~

~~~~ text
44 doubled is 88
#<NameError: undefined local variable or method `numTimes2' for #<StringIO:0x007f837203e1f0>>
~~~~

Undefined local variable... In fact, we did define that local variable, but it isn't local to where we tried to use it; it's local to the method.

This might seem inconvenient, but it actually quite nice. While it does mean that you have no access to variables inside methods, it also means that they have no access to your variables, and thus can't screw them up:

~~~~ ruby
def littlePest var
  var = 0
  puts 'HAHA!  I ruined your variable!'
end

var = 'You can\'t even touch my variable!'
littlePest var
puts var
~~~~

~~~~ text
HAHA!  I ruined your variable!
You can't even touch my variable!
~~~~

There are actually two variables in that little program named var: one inside littlePest, and one outside of it. When we called littlePest var, we really just passed the string from one var to the other, so that both were pointing to the same string. Then littlePest pointed its own local  var to 0, but that did nothing to the  var outside the method.

## Return Values

You may have noticed that some methods give you something back when you call them. For example, gets returns a string (the string you typed in), and the + method in 5+3, (which is really 5.+(3)) returns 8. The arithmetic methods for numbers return numbers, and the arithmetic methods for strings return strings.

It's important to understand the difference between methods returning a value to where the method was called, and your program outputting information to your screen, like  puts does. Notice that 5+3 returns  8; it does not output  8.

So what does puts return? We never cared before, but let's look at it now:

~~~~ ruby
returnVal = puts 'This puts returned:'
puts returnVal
~~~~

~~~~ text
This puts returned:
~~~~

The first puts didn't seem to return anything, and in a way it didn't; it returned nil.  Sometimes,you can ask the computer for something and the answer is nothing. How do we talk about... nothing?  The answer is nil: Ruby's way of saying "nothing".  nil is a special object which basically means "not any other object." And when you  puts nil, it prints out nothing. (Just a new line.) Though we didn't test it, the second puts did, too;  puts always returns nil. Every method has to return something, even if it's just nil.

Take a quick break and write a program to find out what sayMoo returned.

Were you surprised? Well, here's how it works: the value returned from a method is simply the last line of the method. In the case of sayMoo, this means it returns puts 'mooooooo...'\*numberOfMoos, which is just  nil since puts always returns  nil. If we wanted all of our methods to return the string 'yellow submarine', we would just need to put that at the end of them:

~~~~ ruby
def sayMoo numberOfMoos
  puts 'mooooooo...'*numberOfMoos
  'yellow submarine'
end

x = sayMoo 2
puts x
~~~~

~~~~ text
mooooooo...mooooooo...
yellow submarine
~~~~

So, let's try that psychology experiment again, but this time we'll write a method to ask the questions for us. It will need to take the question as a parameter, and return  true if they answered yes and  false if they answered no. (Even though most of the time we just ignore the answer, it's still a good idea for our method to return the answer. This way we can use it for the bed-wetting question, too.) I'm also going to shorten the greeting and the debriefing, just so this is easier to read:

~~~~ ruby
def ask question
  goodAnswer = false
  while (not goodAnswer)
    puts question
    reply = gets.chomp.downcase

    if (reply == 'yes' or reply == 'no')
      goodAnswer = true
      if reply == 'yes'
        answer = true
      else
        answer = false
      end
    else
      puts 'Please answer "yes" or "no".'
    end
  end

  answer  # This is what we return (true or false).
end

puts 'Hello, and thank you for...'
puts

ask 'Do you like eating tacos?'      # We ignore this return value.
ask 'Do you like eating burritos?'
wetsBed = ask 'Do you wet the bed?'  # We save this return value.
ask 'Do you like eating chimichangas?'
ask 'Do you like eating sopapillas?'
ask 'Do you like eating tamales?'
puts 'Just a few more questions...'
ask 'Do you like drinking horchata?'
ask 'Do you like eating flautas?'

puts
puts 'DEBRIEFING:'
puts 'Thank you for...'
puts
puts wetsBed
~~~~

~~~~ text
Hello, and thank you for...

Do you like eating tacos?
>> yes
Do you like eating burritos?
>> yes
Do you wet the bed?
>> no way!
Please answer "yes" or "no".
Do you wet the bed?
>> NO
Do you like eating chimichangas?
>> yes
Do you like eating sopapillas?
>> yes
Do you like eating tamales?
>> yes
Just a few more questions...
Do you like drinking horchata?
>> yes
Do you like eating flautas?
>> yes

DEBRIEFING:
Thank you for...

false
~~~~

Not bad, huh? We were able to add more questions (and adding questions is easy now), but our program is still quite a bit shorter! It's a big improvement — a lazy programmer's dream.
