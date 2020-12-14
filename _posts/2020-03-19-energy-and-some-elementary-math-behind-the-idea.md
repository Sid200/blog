---
layout: post
title: Work, Vectors, Forces and Energy - Some math behind it all
description: A sequel to our first intuition about Energy. This one delves into the elementary mathematical aspects (a bit).
mathjax: true
series: true
seriesname: Energy
part: 2
modified: 2020-12-14
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
date: 2020-03-19
---
There was once a time when I was bragging that I had no time, but now after the outbreak of this thingy, I seem to have plenty of time to spare. This state is very succinct, and I have no words to describe it -  I want to do things, but I still don't want to do them.

> Future Sid: Ahoy matey! That state lasted for no longer than some days... So yeah.

I wasn't expecting to write this post at all, but here we are. Let's make the most of this time with a sequel to our Energy Series!

## How (do you) Work?

So we start with work. This time we are going to deal with some of its mathematical aspects. What's work? Well, we defined work as the energy used to do something. How did it come about? I think I said something along the lines of a force. That's where we start.

Whatever we're going to talk about is based on our arbitrary decision of assigning a particular number to this quantity (and quality) based on the magnitudes of the forces that it comes from and the output that it produces. What's the output? Well, the body is pushed to a state of motion and it moves from its initial position. So, we say that the work done by a force is nothing but the force itself times its output. We call this output *the displacement*.

If you are still taking a very very preliminary course on all of this, you might not have heard of displacement, but distance instead.

The two terms are equivalent in one dimension (well not really, and we'll see why). The problem appears when we think of higher dimensions. Let's just go with 2 for now.

But before all of that, let's represent the work thing ***mathemagically***:

$$W = F \times s$$

Here, $$s$$ denotes the displacement. Why $$s$$? Ask humans (and look up my post on Nomenclature; thank me for the best self-advertisement transition later :P). You don't have to leave now though, there's an answer; the 's' stands for the German word *Strecke* which actually translates to distance, but we use it to represent displacement. That doesn't mean that it stops **you** from using different letters. Your document or whatever should make the use clear and that's it. But obviously, following a universal convention makes it easier for people to read through your stuff.

Anyhow, let's continue. If you think of the work done by a particular force, it seems logical that the output of **that** force would just be in it's direction. What do I mean by that? This:

<center>
    <img src="/blog/images/Energy/ElemMath/mayTheDirBeWithYou.svg" style="background-color: #1e1e1eff; height: 450px"><br>
    <sub style="font-family: cursive">May the direction be with you.</sub>
</center>

The thing is that this direction thingy is true for all point-like objects. In most of basic mechanics, we assume that an object is a point object, or that the force's point of application is the object's center of mass. What is the *center of mass*? Well, that requires a separate talk. For now, think of it as a predefined point in a body which sums up all the movement of the body. You can easily replace the whole body with its center of mass for some type of calculations. Anyhow, we'll delve into this later.

### Hello, multiple forces!

Now consider a point object in two dimensions acted on by multiple forces. In this case, the net movement would be in some other direction depending on how large the forces are and their directions. Here's an example:

<center>
    <img src="/blog/images/Energy/ElemMath/directiondimensions.svg" style="background-color: #1e1e1eff; height: 450px"><br>
    <sub style="font-family: cursive">May the direction be IN you.</sub>
</center>

#### Vector Addition

What in this case then? Do we give up? Nah. Let's think of individual cases; we'll deal with each force and it's output separately. The displacement's direction caused due to force $$F_1$$ is in it's direction, and the same goes for $$F_2$$'s displacement; we can maybe somehow *add* these to give us a net (resultant) displacement.

We usually refer to these *additions* as *the addition of vectors*. What's a vector? Force and displacement are vectors. A person moving north at 40 units (unit based on whatever system you like) per second (please let me be happy with a unit of my choice) and at the same time having a horizontal shift with 20 units per second would have a net movement governed by these two *vectors*. So what's a vector? A vector is a mathematical aid. Physically, and more naively, it is a quantity that can have both a *direction* and a *magnitude*. We can think of it as an arrow pointing towards a point in space. This distinction of an arrow pointing towards something in space is necessary. That's because many other quantities also have direction, but an arbitrary one - for example, current just moves into the wire or out of the wire, and that can't point to a specific point in space (kinda, more talks on this later). Vectors are very important *mathemagical* tools - used in Physics, Computer Science, and Math, of course.

> While I keep on using *mathemagical*, that in no way is a proper word (Unless we make it one?)

I won't bother you with the mathematics for the calculation of the net direction when you have multiple vectors. I could put it all in here, but then this post might get very long and too much information at once while helpful, can sometimes be unhelpful.

> When I say that it can get long, I genuinely mean it; Many of my initial drafts are gigantic solely because I like having all information in a single post (which isn't too good for a blog).

What you can do know for now is that the resultant vector for the addition of two vectors can be found out using a triangle forming thingy. Here's how:

<center>
    <img src="/blog/images/Energy/ElemMath/additionOfVecs.png"><br>
    <sub style="font-family: cursive">Sum it up man!</sub>
</center>

Say you have vector $$\vec{a}$$ (we usually write vectors with boldfaces as in $$\mathbf{a}$$, or with arrows on top of 'em) with a direction kinda north, and another vector $$\vec{b}$$ going kinda east. We make sure the tail of one arrow points to the other vectors head. This can be done by shifting either of the vectors parallel to the other (if they aren't already lined up obviously). The resultant is the line completing the triangle. It's direction is from one vector's tail to the other vector's head. As in the image, if you shift both of these and try it out, you get a parallelogram. The resultant is one of the diagonals. So, some folks call it the parallelogram law.

Seriously, enough with the fancy *laws*. Please don't cultivate the habit of rote memorization. You will learn about all the math behind it and get that satiating intuition - just not in this post.

That's a lot of direction talk. How does all this relate to Work? If a body has multiple forces acting on it, it's resultant direction would be different. Each force produces some displacement in some direction, and then resultant direction we see is the vector sum of all these individual displacements. If we wanted to find the work done by just one force, we would have to isolate the net output (or the displacement) that it produces. We would have to do something opposite to adding.

> Oh by the way, if you're still wondering what the difference between displacement and direction is, it's that displacement is a vector quantity while distance is not.

#### Let the vectors be resolved!

Imagine this situation:

<center>
    <img src="/blog/images/Energy/ElemMath/workDoneDotProd.png"><br>
</center>

To do what we want to do, we would take the net displacement and resolve it into *its components*. Components are separate magnitudes along different directions. The component along the direction of our force should be it's *output*. The one completely perpendicular to our force shouldn't have resulted due to this force. If the angle between the net direction and the force is $$\theta$$, then the net displacement **by our force** turns out to be $$s \cdot cos(\theta)$$ (the displacement times the cosine of the angle $$\theta$$).

> This process of *breaking* Euclidean Vectors into its *components* along some *basis* vectors is known as decomposition. I think we can have a proper (mathematically rigorous) discussion about vectors soon-ish?

So our previous one-dimensional equation for work becomes this:

  $$W = F \cdot s \cdot cos(\theta)$$

We can simplify what's written above using some vector notation:

  $$W = \vec{F}\cdot\vec{s}$$

The dot ( $$\cdot$$ ) and the arrows matter. If you see vectors with arrows on top and a dot in between, you can think of the expression as the previous non-vector equation. The dot represents a dot product which quantitatively is equal to the magnitude of the two quantities multiplied together times the cosine of the angle between them.

> Future Sid: I have no idea what got in me, but for some reason I made ridiculous spelling mistakes for everything related to *quantity*. *Sigh, hElP mEE!* 

One more thing to note here is that Work is not a vector quantity as per our definition. And by proper intuition it shouldn't be as well. It is a scalar quantity.

> Let's get super-mathy here. A dot product is a specific case of a more general form - an inner product. An inner product is somewhat like a feature of an Inner Product Space* (which is a Vector Space). An inner product between two (abstract) vectors is represented by $$\langle a, b\rangle$$ and it must satisfy certain properties; namely, it should be commutative, linear, distributive, positive-definite, and its "output" must be a scalar.
>
> Phew! Did that scare you? Well, that's Linear Algebra! (and to be fair you don't know what those terms mean. I reckon it won't be as scary once you know what half of the words actually mean, but that's for later...)

### Hello, multiple variable forces? (Disclaimer: Calculus)

Well, there's still a problem - that last equation isn't really the complete story. What if the force varies with displacement? What if the force is a function of the displacement? To solve this problem, my friends, we require some Integral Calculus. If you've been given constant forces, you could easily work with that equation. The problem is with varying forces.

If you've been given constant forces, you could easily work with that equation. The problem is with varying forces.

If you've been given constant forces, you could easily work with that equation. The problem is with varying forces.

***If you've been given constant forces, you could easily work with that equation. The problem is with varying forces.***

> Future Sid: It seems like I was (secretly) reciting some kind of cult's prayer 👀

How do we make it non-varying? We obviously can't do anything to the force itself. So let's change our perspective. If the change in the displacement is very teensy weensy bit of a thingy - like super super super super super super super tiny (almost zero), the change in the force for that change of displacement would be almost zero. Well, to be frank it depends on the scale. The more you zoom in, the less varying the force becomes. At one instant after *zooming in* a lot, it becomes constant. That fact we can use.

> I am sometimes glad I proofread; things like *zomming* would've long possessed my posts.

> That explanation is a very naive interpretation and I miss words like *infinitesimal* that all Calculus folks come across zillion of times 😢. That said, if you already know about integrals and stuff, just skim through quickly.

Here's our new equation:

$$\mathrm{d}W = \vec{F}\cdot \mathrm{d}\vec{s}$$

What's with that $$d$$? It signifies the near-zero change we get when *we zoom in*. You take the angle as the angle between that displacement and the unvarying force over that tending to zero change. One thing to note here is that this is just one part of the whole work done. You would need to do this for all displacements and then sum all the works up. That can be done by integrating stuff. Here's how you write this sum (the initial and final displacement are $$0$$ and $$s$$ in this case... But it could be anything depending on the requirement):

$$W = \int_0^W\mathrm{d}W = \int_\vec{0}^\vec{s}{\vec{F}\cdot \mathrm{d}\vec{s}}$$

> Just to be very technical, this integral is called a *line integral*. There's more to it, but yeah by now you know the drill - later post for the win!

Integration is again a part of calculus and it's a huge topic. I didn't want to leave this bit for people who were interested. You can check out hundreds of resources on Calc or wait for me to post something up. However, one thing you should take from here is this:

> ***The definite integral usually represents an area under a curve (or a line, or whatever... A curve kinda generalizes it a bit). So, if you have a plot of the force versus the displacement, you could find the total work done by finding the area under thingy, given that the force acts along the same line as the displacement (otherwise the $$cos\theta$$ will bother you).***

The above equation is the most fundamental equation we can get from our intuition. That's work.

## Using what we learnt

If the angle between the force and the net displacement is $$90^\circ$$, the cosine turns out to be $$0$$ and the work done thus becomes $$0$$ - so, no work. Does that make sense to you? Well, obviously the math makes sense, but let's make the sure the intuition hasn't been hampered.

Suppose you lift a stack of books with your hands, hold it still, and move forward with constant velocity. The stack's displacement's direction is forward and the force your hands exert to keep the stack in place is in the upwards direction. So you do no work in the process.

But that's just half of the picture - what process?. Let's delve deeper - when you lift the book, the work done ***by the upward force*** exerted by you (which keeps the stack in place) ***to move the books in the forward direction*** is zero. That makes sense; that force can't direct something to a direction perpendicular to it.

Your next question ***should*** be *Where's the energy going then?*. Surely, I feel stressed after lifting super heavy things; that energy can't just vanish away. That energy you talk about does go into some work.

- When you first lift the stack to some height, you're countering gravity and doing some positive work (while gravity is doing negative work of the same magnitude). So there's your first bits of energy gone.

- When you're holding the stack still, realistically speaking, your muscles still somewhat move, you still use chemical energy to keep your muscles in the state they're in. So you also spend some energy there. Ideally though, we consider we're robots and our hands are super still.

> To be VERY VERY realistic, your hand does do some work for the movement in the horizontal direction. It applies some teensy force in the horizontal direction for the initial bits, but once you *reach* that constant velocity we were talking about, there's no force (well you do have some force to negate the other effects like air resistance, but it's so tiny that we forget about it).

So there's no work by that force to move the things forward, but for sure it does work to keep the books on your hands and not on the ground (while lifting them).

> Future Sid: The way I phrased all of this part before was so very inaccurate. SHAME!

That's all for this talk. And to be real frank, I enjoyed typing this one a lot.

> Future Sid: And to be real frank, I enjoyed proofreading this one ***a lot***.

We have just touched the brim. Plus, we haven't even talked about the mathematical aspects and the types of energies. Well, the last scenario did talk about *negative* work from the gravitational force - and that's exactly where we'll start from in the sequel. Stay tuned (for some millennia - thanks to my very regular writing habits).
