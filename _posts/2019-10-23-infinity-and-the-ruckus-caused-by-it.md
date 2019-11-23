---
layout: post
title: Infinity and the ruckus caused by it
description: Ever wondered what infinity is? Is it a number? Does it even have existence? Let's wonder together!

date: 2019-10-23 09:05 -0400

mathjax: true
series: true
part: 1
image:
  background: prime-bg.jpg
  feature: Infinity/feature.jpg
  credit: Sid Verma
  creditlink: https://unsplash.com/@sidverma
tags:
- infinity
- math
- mathematics
- large
- sets
- set
---

*Two things are infinite: the universe and human stupidity; and I'm not sure about the universe.* - **Albert Einstein**

Hey there! I didn't really upload for a real long time primarily because I wasn't getting a topic I could talk about with all my heart and dedication and plus of that, I didn't have **time**. Doesn't matter though, I am back.

So, it came to my mind that I boast off being a Science Enthusiast on this blog but well I haven't had a single talk come up about one of the very awesomest, logical and cool topics I can think of - Mathematics

I thought and thought. At the end what came into my mind was talking about infinity. It is as abstract as it can be - probably more than Energy (remember the $$E_p$$ talk?). I don't really know what to tell or discuss but first this thing:

> Infinity is not a number. For all the programmers out there, it is NaN (yeah, not a number)

People have several misconceptions about it. Something that is really large, something that is "something that can't be defined" or basically undefined and yeah it is really not defined.

Instead of directly going into mathematical proofs or total into-the-notation talks, let us frame this thing bit by bit.
I don't really know where to start. Infinity or $$\infty$$ (got mathjax :grin:) is used in a lot of places - starting from calculus (I have talks scheduled on that) to well, almost everything (yeah).

If it isn't a number, what is it? Here's what **I** would define it in a *naive* manner:

We humans like boundaries. We don't like staying in unknown situations for very long - thanks to our curiosity. So let's just name something that is large - infinity.

Here's what I plan:

- **Part - 1, 2** will go into the math side of the thing.
- **Part - 2, 3** will go into the Physics side of the thing.
- **Part - 4** will go into the computer side of the thing.


## Alright, let's start...

Let's start with a question: 

*Which has more number of elements - the set of all positive integers or the set of all kinds of integers (positive or negative).*

**Math people:** *Which has more elements - $$\mathbb{Z}^{+}$$ or $$\mathbb{Z}$$? ($$\mathbb{Z}$$ represents integers and $$\mathbb{Z}^{+}$$ represents positive integers)*

---

If you are a **Math Guy (or a girl)**, you would probably know the answer (or even might have discovered the flaw in the question). Why not shut up? (heh I am joking don't worry I believe there will be something for you in the Physics Section?)

In non-technical terms, the answer would be both have the same number of elements. Seems **absurd** right? That's the power of $$\infty$$. It makes your head wobble.

I obviously am not gonna leave anyone without the proof for the same, the awesome proper mathematical notations we might use and some terminology (which if you remember from the Computer Bugs talk, we humans love a lot)

---

### Let's answer this - **What is a Set?**

This is what the naive definition would be:

> A set is a collection of elements, or thingies. These thingies can be anything and depending on that, we define the set. These so called "thingies" can even be sets themselves.

Remember $$\mathbb{Z}$$ that I had written for the Math people? Turns out, it wants to meet you. Let's define it:

**Simple en**: $$\mathbb{Z}$$ is the set of all integers. psst! An integer is a number that isn't a decimal number (or the floating point or a fractional number). It can be negative, zero or positive.

**mAtHAmAGic 1**: $$\mathbb{Z} = \{..., -3, -2, -1, 0, 1, 2, 3, 4, ....\}$$

**mAtHAmAGic 2**: $$\mathbb{Z} = \{x \mid x = \pm p \verb!,! p \in \mathbb{N} \cup \{0\} \}$$

Don't worry if you didn't understand the second one. What am I typing for?

So the first one is called the **Roster Notation**. In this, you just list out the stuff and if it just goes on, ellipses are your friends.

The second one is what any person who understands what the symols mean would choose. I do, so yeah I probably like it more.

---
Here is some stuff that will help:

- You use curly braces- $$\{ \}$$ to denote a set.

- $$\mathbb{N}$$ just like $$\mathbb{Z}$$, is a set. It is a set of all natural numbers. Starting from 1 and going all the way to that thing we are actually talking about.

- $$\in$$ means "belongs to". An elements is in a set if it belongs to the set right? $$\notin$$ similarly would mean "doesn't belong to" or "not in". $$\mid$$ means "such that"
  
- $$\{0\}$$ is again another set. As I said, you use $$\{ \}$$ to denote a set, this would stand as a set consisiting of only 1 element - 0. Similarly, $$\{1,2\}$$ consists of 2 elements - 1 and 2.

- $$\cup$$, you could say is an operation, known by the name of *union*. You perform it on two sets. It is like addition. Just like addition of two numbers gives us a number, the **union** of two **sets** gives a set. Let's use the set builder form for the union:
  $$A \cup B = \{x \mid x \in A$$ or $$x \in B \}$$. This reads 
  **A** union **B** is a set of elements such that if an element *x* is chosen from it, it can either belong to the set A or the set **B**

---

That didn't really answer the stuff and yeah I got diverted again but it is through these small yet long talks I want people to know stuff. Anyways, let's continue.

## The Bijection

Umm okay. Let's see. How do I explain this? Well, let's get back to our question: *Which has more elements - $$\mathbb{Z}^{+}$$ or $$\mathbb{Z}$$.*

Let's try to make up another simple question, the answer to which is already known to us. Hmmm.... Here is what came first to my mind (or third, the others were well, :poop:):

*Does a normal, average human being have more nails or fingers?* 
Well, the obvious answer is they both are equal in amount. How? Well we know that all fingers *have* nails. The nails are already *linked* to the fingers. Each finger has a *corresponding* nail. In other words, there is a *one-to-one correspondence* between the sets of fingers in a human being and sets of nails in a human.

A bijection is a function (a function is like a string which connects the input and output values which belong to two different sets - the domain and the range) that exhibits this *one-to-one correspondence*. There is some additional stuff the next part would deal with.

### Didn't get functions?
Say we had set $$A$$ consisting of the names of some people and set $$B$$ consisting of ice-creams. We could then define a function, let's name that $$f$$ (cuz obvious reasons) which links $$A$$ to $$B$$ or, goes from $$A$$ to $$B$$ such that whatever name we fed into the function, we would be given or linked to an element in $$B$$ which is an ice-cream that the person hates the most. Mathe*magically*:

$$f : A \to B $$
<br>
$$f(x) = m \mid m \in B \text{ and } x \text{ hates } m \text{ the most. Provided, } x \in A$$

***OK. Now back to our nail example thingy***

What if we could find a bijection between $$\mathbb{Z}^{+}$$ and $$\mathbb{Z}$$? That would work right?
Also, $$\mathbb{Z}^{+}$$ and $$\mathbb{N}$$ are just the same, so I am gonna use $$\mathbb{N}$$ cuz it is stuff smaller to type...

Back to finding a bijection. How do we do that? Let's list the numbers from $$\mathbb{Z}$$ and $$\mathbb{N}$$:

$$\mathbb{N}$$: 1, 2, 3, 4, 5, ..., $$\infty$$
<br>
$$\mathbb{Z}$$: $$-\infty$$ ..., -3, -2, -1, 0, 1, 2, 3 ..., $$+\infty$$

How do we come up with a bijection? (We would also need to prove that it is a bijection btw, I will do it don't worry!)

A bijection, requires things to correspond to each other. In other words, there has to be some kind of a part of a whole, within which the elements have same properties. Like for our nail example, all fingers are well, fingers. In this case, the part *is* the whole. What about $$\mathbb{N}$$ and $$\mathbb{Z}$$ ?

$$\mathbb{N}$$ 
seems a little hard for now, so let's concentrate on $$\mathbb{Z}$$ a little. Proper inspection will result in us concluding that there is one way we can divide $$\mathbb{Z}$$ into two things: the positive numbers and the negative numbers.

Since we found two classes of numbers in $$\mathbb{Z}$$, what if we did something similar (and we would need to find some other two classes to prove a one-one correspondence)

What about *even* and *odd* numbers? That should work right? Ok, so how do we relate these two parts through a function?

Well, let's list the numbers again but this time, the odd numbers from $$\mathbb{N}$$ first and negative numbers from $$\mathbb{Z}$$:

---
$$\mathbb{N}$$: 1, 3, 5, 7, ..., $$\infty$$ (Only Odd)
<br>
$$\mathbb{Z}$$: -1, -2, -3, -4, ..., $$-\infty$$ (Only negative)

---

---
$$\mathbb{N}$$: 2, 4, 6, 8, ..., $$\infty$$ (Only Even)
<br>
$$\mathbb{Z}$$: 1, 2, 3, 4 ..., $$-\infty$$ (Only positive)
---

A little bit of math inspection and inegenuity would result in the following definition for this above represented relation:

$$
f(x) = \begin{cases}
  x/2 & x\text{ is even }
  \\ -(x+1)/2 & x\text{ is odd }
\end{cases} 
$$

Now the question is whether the function is a bijection. First, what should we require for one-to-one correspondence? Well, firstly, there should be unique correspondence which is quite obvious - A nail can't belong to two fingers.

Are we missing any other cases? Hmm "Each finger having a unique nail"... What about a finger not having a nail!
What else, no I can't think of anything else. The first case, in mathemagic terms would say - "The function is *injective*" (Each element of the input set links to a unique elements to the output set.)

The second one would be the function is *surjective*. (All of the elements of the output set have been linked to)

How do we prove something is injective? Well, we would need to prove that if two outputs are the same, they need to have the same inputs:

$$f(x_1) = f(x_2) \implies x_1 = x_2$$

The second one is kind of non-intuitive. We would need to prove that the set of outputs (*mathemagically* called the *Range*) is equal to the set which is being linked to actually - the set of outputs (the *Co-Domain*). The set of inputs is called the *Domain* for the curious you...

Let's try to prove (or fail to prove) that the function we defined is bijective:

### Injectivity:
Let, $$x_1$$ and $$x_2$$ belong to $$N$$
Suppose
$$f(x_1) = f(x_2)$$
Three cases arise:
1. $$x_1 , x_2$$ are both odd.
2. $$x_1 , x_2$$ are both even.
3. $$x_1$$ is odd and $$x_2$$ is even (and vice versa, which is the same case)

For 1, 
$$f(x_1) = f(x_2)$$
$$\implies -(x_1 + 1)/2 = -(x_2 + 1)/2$$
$$\implies x_1 = x_2$$

We get the same result for 2 as well.

3 is special. Let's see:
$$f(x_1) = f(x_2)$$
$$\implies -(x_1 + 1)/2 = x_2/2$$
$$\implies -x_1 + 1 = x_2$$
$$\implies -x_1 = x_2 - 1$$

Aww man, we couldn't prove that $$x_1 = x_2$$ for all cases. Well, then this blog post was all usele - Wait!

We stated this:- 
> Let, $$x_1$$ and $$x_2$$ belong to $$N$$

This means that $$x_2 - 1$$ can't be negative or zero. But the 3rd case results in just that. How is that possible? Well, it is not. Hence, the 3rd case doesn't exist at all.

Hence, from the first and the second case, we get that $$f$$ is indeed injective.

What about, surjectivity?

### Surjectivity

Well, $$x/2$$ when x is an even natural number always results in an integer, isn't it? Okay, positive integer.
Also, $$-(x+1)/2$$ when x is an odd natural number always results in a negative intger.

As our function relates to both of the different parts of $$Z$$ (negative and positive) from both these sub-parts of the input set (odd and even), it has to be that the *Co-Domain* and the *Range* are both $$Z$$. Hence, our function is indeed surjective.

### Hmm, that's a bijection!

Yup, we proved that $$f$$ is bijective. That means there is the same *number* of integers as there are *natural numbers*. The math proves it (kinda). Every element links to a unique element totally and all of these elements together encompass the set of integers.

### Where's infinity in all this?

You should actually be asking this question now. We didn't really come across any ruckus caused by infinity. Well, that's because of a reason you will find in the next post. But still, I want to give you a kind of intro question, mind boggling idea which will probably make you contemplate about your existence (maybe?)

## Russell's Paradox

Consider a set $$A$$ defined as such:

$$A = \{x \mid x \notin x\}$$

The question that arises is: *Does $$A$$ contain itself or not? Think about it.*
That's where I am going to leave the talk (part-1). (By the way, if you are reading this, it has probably been a month since I first wrote this thing and then just gave up on blogging for sometime. I am back however, but it is gonna be a very irregular schedule probably.)
