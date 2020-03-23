---
layout: post
title: Work, Vectors, Forces and Energy - Some math behind it all
description: A sequel to our first intuition about Energy. This one delves into the elementary mathematical aspects (a bit).
mathjax: true
series: true
seriesname: Energy
part: 2
modified: 
tags:
- energy
- energy 101
- physics
- science
- work
- kinetic energy
- potential energy
- mechanical energy
- power
- conservation of energy
image:
  path: "images/Energy/Essence/header1.jpg"
  background: Energy/Essence/bg1.jpg
  feature: Energy/Essence/header1.jpg
  credit: NASA
  creditlink: https://unsplash.com/@nasa
date: 2020-03-19 11:28 -0400
---
There was once a time when I was bragging that I had no time, but now after the outbreak of this thingy, it seems that I have so much time that I cannot think of what to do with it. I was pretty much bored. I was in a state that is very non-descriptive. I wanted to do things, but I didn't want to do them as well. It was as if I was thinking about tasks, and at the same instant, also thinking of the reasons I should avoid them.

That, my friends, sums all of me up. I am bored, but at the same time, I am not willing to do a thing. This post is very unexpected, to be frank. I had different plans, my *tests* were going to end, and I was going to learn and share different things.

None of that happened. I do have the time to learn, but I don't want to. Well, I probably will (maybe). Anyways, as it is that I have the time to share, so here it is - a sequel to the Energy *Series*.

Shall we? You first!

So we start with work. This time we are going to deal with some of its mathematical aspects. What's work? Well, we defined work as the energy used to do something. How did it come about? I think I said something on the lines of a force. That's where we start.

Now whatever I am going to talk about is based on our arbitrary decision of assigning a particular number to this quantity (and quality) - based on the magnitudes of the forces that it comes from and the output that it produces. What's the output? Well, the body is pushed to a state of motion. So, we say that the work done by a force is nothing but the force itself times its output. We call this output the displacement.

If you are still taking a very very preliminary course on all of this, you might not have heard of displacement, but distance instead.

The two terms are equivalent (ine one dimension). The problem appears when we think of higher dimensions. Let's just go with 2 for now.

But before all of that, let's represent our thingy ***mathemagically***:

$$W = F \times s$$

Here, $$s$$ stands for the displacement. Why $$s$$? Ask humans (and look up my post on Nomenclature :p). Well, maybe not in this case... I have an answer. The 's' stands for the German word *Strecke* which actually translates to distance, but we use it to represent displacement sometimes. That doesn't mean that it stops **you** from using different letters. Your document or whatever should make the use clear and that's it. But obviously, following a univeral conventions makes it easier for people to go through your points and stuff.

Anyways, if you think of the work done by a particular force, it seems logical that the output of **that** force would just be in that direction. What do I mean by that? This:

<center>
    <img src="/images/Energy/Elem.&#32;Math/mayTheDirBeWithYou.png"><br>
    <sub style="font-family: cursive">May the direction be with you.</sub>
</center>

The thing is that this direction thingy is true for all point-like objects. In most of the basic mechanics, we assume that an object is a point object, or the force's point of application is the center of mass. What is this *center of mass*? Well, that requires a separate talk. For now, think of it as a predefined point in a body which sums up all the movement of the body. You could, theoretically, represent the whole body with its center of mass - if you want to trace net movements and all that jazz. But that's a special talk for later.

Now consider this case - a point object in two dimensions acted by multiple forces. In this case, the net movement would be in some other direction depending on how large the forces are and their directions. Here's an example:

<center>
    <img src="/images/Energy/Elem.&#32;Math/directiondimensions.png"><br>
    <sub style="font-family: cursive">May the direction be IN you.</sub>
</center>

What in this case then? Do we give up? Nope. We try to think of individual cases; try to separate them, and try to see how those forces add up. If you think of the first direction output in the direction of the force $$F_1$$, and the second direction output in the direction of the force $$F_2$$, you can then think of somehow "summing" up these directions to give us a net direction. So, all the stuff remains intact and we don't need to introduce any other thingies - except this summing thingy of course.

We usually refer to these *additions* as *summing vectors* or *the addition of vectors*. What's a vector? Force and displacement are vectors. A person moving north at 40 units (unit based on whatever system you like) per second and at the same time having a horizontal shift with 20 units per second would have a net movement governed by these two *vectors*. So what's a vector? A vector is a mathematical aid. Physically, and more naively, it is a quantity that can have both a *direction* and a *magnitude*. We can think of it as an arrow pointing towards a point in space. This distinction of an arrow pointing towards something in space is necessary. That's because many other quantities also have direction, but an arbitrary one - for example, current just moves into the wire or out of the wire, and that can't point to a specific point in space (kinda, more talks on that later). Vectors are very important *mathemagical* tools - used in Physics, Computer Science, and Math, of course.

I won't bother you with the mathematics for the calculation of the net direction when you have multiple vectors. That requires a different talk altogether, as I don't wanna club in too much information and render the knowledge useless. All you can know for now is that the net direction of two vectors is a triangle forming thingy. What do I mean?

<center>
    <img src="/images/Energy/Elem.&#32;Math/additionOfVecs.png"><br>
    <sub style="font-family: cursive">Sum it up man!</sub>
</center>

Say you have vector $$\vec{a}$$ (we usually write vectors with boldfaces or with arrows on top of 'em) with a direction kinda north, and another vector $$\vec{b}$$ going kinda east. What you do is first make sure the tail of one arrow points to the other vectors head. You cand do this by shifting either of the vectors parallel to the other (if they aren't already lined up obviously). The resultant is the line completing the triangle. It's direction is from one vector's tail to the other vector's head. As in the image, if you shift both of these and try it out, you get a parallelogram. The resultant is one of the diagonals. So, some folks call it the parallelogram law.

Seriously, enough with the fancy *laws*. Don't take it as a rule. Please. I don't want to leave you with nothing, but also don't want to you to cultivate the habit of just learning the rules and nothing else. You will learn the math behind it all and get that juicy intuition, just not in this post.

That's a lot of direction talk. How does all this relate to Work? If a body has multiple forces acting on it, it's resultant direction would be different. If we wanted to find the work done by just one force, we would have to isolate the net output (or the displacement) that it produces.

Oh by the way, if you're wondering what the difference between displacement and direction is, it's that displacement is a vector quanitity while distance is not.

So to isolate the displacement caused just by that force, we would need to do some angle play. If the situation was like so:

<center>
    <img src="/images/Energy/Elem.&#32;Math/workDoneDotProd.png"><br>
</center>

Then what we would have to take the net displacement and resolve it into "its components" (separate magnitudes along different directions... You could think of this as trying to get the vectors, along the direction of our force and perpendicular to it, that added up to give us the net displacement) along the direction of our force. Turns out, this situation is always a right triangle situation. If the angle between the net direction and the force is $$\theta$$, then the net displacement **by our force** turns out to be $$s \cdot cos(\theta)$$ (the displacement times the cosine of the angle $$\theta$$).

So our previous one-dimensional expression for work becomes this new thing:

  $$W = F \cdot s \cdot cos(\theta)$$

If you try to write it in terms of vectors, you get a simplified expression:

  $$W = \vec{F}\cdot\vec{s}$$

The dot ( $$\cdot$$ ) and the arrows matter. If you see vectors with arrows on top and a dot in between, you can think of the expression as the previous non-vector equation. The dot represents a dot product which quanitatively is equal to the magnitude of the two quantiites multiplied together times the cosine of the angle between them.

One more thing to note here is that Work is not a vector quanitity as per our definition. And by proper intuition it shouldn't be as well. It is a scalar quantity.

Well, there's still a problem. That equation isn't really the complete story. What if the force changes its value with displacement? What if it varies in such a manner that different amounts of forces (of the same force but at different displacemetns) get attributed to different changes in displacements? That, my friends, requires Calculus. If you've been given constant forces, you could easily work with that equation. The problem is with varying forces.

If you've been given constant forces, you could easily work with that equation. The problem is with varying forces.

If you've been given constant forces, you could easily work with that equation. The problem is with varying forces.

***If you've been given constant forces, you could easily work with that equation. The problem is with varying forces.***

***Ease: Constant Forces. Problem: It's varying with displacement.***

How do we make it non-varying? We obviously can't do anything to the force itself. So let's change our perspective. If the change in the displacement is very teensy weensy bit of a thingy - like super super super super super super super tiny (almost zero), the change in the force for that change of displacement would be almost zero. Well, to be frank it depends on the scale. The more you zoom in, the less varying the force becomes. At one instant after zomming in a lot, it becomes constant. That we could use. Here's our new equation:

$$dW = \vec{F}\cdot d\vec{s}$$

What's with all those *'d'*s? They signify that the thingy is zoomed in so very much that the change almost tends to zero. You take the angle as the angle between that displacement and the unvarying force over that tending to zero change. One thing to note here is that this is just one part of the whole work done. You would need to do this for all displacements and then sum all the works up. That can be done by integrating stuff. Here's how you write this sum (the initial and final displacement are $$0$$ and $$s$$ in this case... But it could be anything depending on the requirement):

$$W = \int_{0}^{W}{dW} = \int_{0}^{s}{\vec{F}\cdot d\vec{s}} $$

Integration is again a part of calculus and it's a huge topic. I didn't want to leave this bit for people who were interested. You can check out hundreds of resources on Calc or wait for me to post something up. However, one thing you should take from here is this:

> ***The definite integral usually represents an area under a curve (or a line, or whatever... A curve kinda    generalizes it a bit). So, if you have a plot of the force versus the displacement, you could find the total work done by finding the area under thingy, given that the force acts along the same line as the displacement (otherwise the $$cos\theta$$ will bother you).***

The above equation is the most fundamental equation we can get from our intuition. That's work.

If the angle between the force and the net displacement is $$90$$ degrees, the cosine turns out to be $$0$$ and the work done thus becomes $$0$$ - so, no work. Does that make sense to you? Well, obviously the math makes sense, but let's make the sure the intuition's there by a daily life example. When you lift your books (or whatever) in your hands, hold them still and move forward, their net direction is forward and the force by your hands is upwards. So you do no work in the process (or technically the force exerted by you does no work).

But that's just half of the picture - what process?. Let's go in deep. When you lift the book, the work done ***by the upward force*** exerted by you ***to move the books in the forward direction*** is zero. That makes sense. That force obviously can't direct something to a direction perpendicular to it.

Your next question ***should*** be, *Where's the energy going then?*. Surely, I feel stressed after lifting super heavy things. That energy just can't vanish away. That energy you talk about goes into some work. It goes into the work done by the upward force to keep the stack of books (or whatever) from falling. There's also the gravitational force acting on it. This force tries to produce a displacement downwards. Your force tries to produce a displacement in the upward direction and it so happens that when things are steady, these displacements cancel out. (If the vectors are in completely opposite directions and have equal magnitudes, their resultant would be nothing. If they are opposite but their magnitudes aren't equal, the resultant would be in the direction of the one with more of the *umph* - the magnitude).

This is a good example of a situation where you do indeed do work, but the displacement isn't visible (kinda). That doesn't mean it isn't there. It just happened to be equal and opposite to the one that the gravitational force is producing. So there's no work by that force to move the things forward, but for sure it does work to keep the books on your hands and not on the ground.

That's all for this talk. And to be real frank, I enjoyed a lot typing this one. We have just touched the brim. Plus, we haven't even talked about the mathematical aspects and the types of energies. That all will surely be in the sequel. Stay tuned!
