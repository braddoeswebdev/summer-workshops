---
series: "ruby"
number: 0
title: "Getting Started"
icon: 'desktop'
desc: "Set up your computer for Ruby programming"
---
# Getting Started

When you program a computer, you have to "speak" in a language your computer understands: a programming language. There are lots and lots of different languages out there, and many of them are excellent. In this tutorial I chose to use my favorite programming language, *Ruby*.

Aside from being my favorite, Ruby is also the easiest programming language I have seen (and I've seen quite a few). In fact, that's the real reason I'm writing this tutorial: I didn't decide to write a tutorial, and then choose Ruby because it's my favorite; instead, I found Ruby to be so easy that I decided there really ought to be a good beginner's tutorial which uses it. It's Ruby's simplicity which prompted this tutorial, not the fact that it's my favorite. (Writing a similar tutorial using another language, like C++ or Java, would have required hundreds and hundreds of pages.) But don't think that Ruby is a beginner's language just because it is easy! It is a powerful, professional-strength programming language if ever there was one.

When you write something in a human language, what is written is called text. When you write something in a computer language, what is written is called code. I have included lots of examples of Ruby code throughout this tutorial, most of them complete programs you can run on your own computer. When you see an example, type it for yourself to try it out.  If you copy and paste the code, you won't learn as much.

## Let's Get Set Up

Throughout these lessons, you're going to be switching back and forth between 3 programs:

* Whatever web browser you opened this lesson in
* Notepad++, a fancy text editor that you'll actually write your code in
* MobaXTerm, a tool that lets you connect to other computers.

If you haven't opened up the other 2 programs yet, go ahead and do it now.  There should be shortcuts on the desktop.

## Writing a Program

Let's start with Notepad++.  Notepad++ works kind of like regular Notepad: it just lets us type text, no fancy formatting or centering or pages or anything like that.  It will do some other things that help us as programmers though, like turning important words different colors & keeping things lined up.  Go ahead and type this into Notepad++.

~~~~ruby
# Hello, world!

puts "Hello, world!"
~~~~

Once you've typed that in, go ahead and save your file to your L drive.  Make sure you name it something simple, with no spaces or symbols, and with a `.rb` at the end.  `hello.rb` would be a good choice.  Once you save it, things should change colors & look kind of like it does here.

## Running a Program

We're going to connect to another computer to actually run your program - doing it this way makes your job slightly more complicated, but it means I don't have to go around and install and set up a bunch of programs on all your computers!  Flip over to MobaXTerm, type this in: `ssh cortex`, and hit enter.  (`ssh` is a way of connecting to another computer, `cortex` is the name of the computer you're connecting to)  It might pop up and ask you if you really want to connect (which you do), and ask you for your password.  You'll have to do that part before you start doing anything else, but you should only have to do it once a day.

Once you've connected to cortex, it's easy to run your program.  Just type `ruby`, a space, and the name of your program that you saved on your L drive, then hit enter to start it.  So if you followed my advice and called your program `hello.rb`, you'd type `ruby hello.rb`.  It should print "Hello, world!" on the screen and then let you type something else in.

Here's a handy little trick: let's say we wanted the computer to tell us hello again.  You could sit there and type `ruby hello.rb` in again... or you could just push the up key.  Pushing the up & down keys scroll through the commands you've already ran.

Now that you've successfully ran a program, let's start learning more!  Click the next link in the lower right to move on to the first real lesson.
