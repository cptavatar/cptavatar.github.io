---
author: admin
comments: true
date: 2009-08-03 22:41:52+00:00
layout: post
slug: my-first-scala-program
title: My First Scala Program
wordpress_id: 167
categories:
- Tech
tags:
- Java
---

A while back for my birthday, I got the Odersky [Programming in Scala](http://www.amazon.com/Programming-Scala-Comprehensive-Step-step/dp/0981531601/ref=sr_1_1?ie=UTF8&s=books&qid=1249338643&sr=8-1) book and today I finally got a chance to crack it and play around. I had been interested in trying to pick up one of the new wave of dynamic [JVM langagues](http://en.wikipedia.org/wiki/List_of_JVM_languages) like [Groovy](http://groovy.codehaus.org/), [JRuby](http://jruby.codehaus.org/), or [Jython](http://www.jython.org/) and had settled on [Scala](http://www.scala-lang.org/). I had read a suggestion that [Project Euler](http://projecteuler.net/) would make for a fertile playground of test problems to learn on, and having already done the first several in Java that rang true for me. So, here is my overly complicated solution to the simple first problem..


 


     //If we list all the natural numbers below 10 that are multiples of 3
     //or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.
     //Find the sum of all the multiples of 3 or 5 below 1000.
 
     import scala.actors._
    
    
     object Adder extends Actor {
    
    	var sum = 0
    	def act() = {
    		react {
    			case (num: Int) =>
    				sum += num
    				act()
    				case "REPORT" =>
    				Console.println("Total = " + sum);
    		}
    	}
    }
    
    object ProblemOneRunner {
    	def main(args: Array[String]): Unit = {
    		Adder.start
    		for(i <- 1 to 999) {
    		if(i % 3 == 0 || i % 5 == 0 ) {
    			Adder ! i
    		}
    	}
    		Adder ! "REPORT"
    	}
    }
    


It starts out looking something like a Java program with an import statement, although Scala uses the _ notation to import everything instead of * since * is an identifier. Scala supports a lot of flexibility in its import statements, they can show up anywhere and you can use them to remap names or set up exclusion filters - but lets not get to far astray.

Next, you'll notice that my program has two objects and no classes. Its not that Scala doesn't have classes, its just that Scala classes don't have the Java concept of static - if you want a singleton object, you use the _object_ keyword. The solution I have above uses one singleton as the main program entry point and another Adder singleton that extends Actor. This is just so I could play with Scala's built in multithreading and message passing support - obviously this problem doesn't really require it but I thought I'd try it out anyway for fun.

The Adder has its own sum variable it uses to keep track of the numbers it will add up - Scala uses the _var_ keyword for variables that can be reset and _val_ for ones that can't. You'll notice the lack of any type declaration here, its not that Scala variables are not typed, its just that it uses type inference to figure out what they are. Also, Java users will notice the lack of semicolons - semicolons are optional in Scala in most cases. The Adder overrides the _act_ method, the entry point for threads, and then calls _react_ which will look for a message in the actor's inbox and if it doesn't find one, put the actor to sleep. Unlike some of the other constructs Scala provides for Actors like _receive_, the thread will die at the end of _react_ instead of looping so we have to put a call to _act_() at the end of the int message we send it to keep it alive.

In the main method, we start up our Actor thread, then loop through 1 through 999 looking for numbers divisible by 3 or 5 to send to our Adder, then once we are done we send a message to the thread to report and finish its loop. Again, Java users will notice the easy condensed for loop and the ! message passing syntax.

I've barely scratched the surface of Scala here, I'll try to get a couple more problems done and posted that likewise abuse language features as I get time.
