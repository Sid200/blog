---
layout: post
title: The Essence of Lambdas in C++
description: Understand Lambdas in C++ like never before, in a beginner friendly manner
modified: 
tags:
- cpp
- c++
- lambdas
- lambda
- functor
- function
- pointers
image:
  path: /images/LambdasInCPP/lambdas-in-cpp.jpg
  background: LambdasInCPP/bg.jpg
  feature: LambdasInCPP/lambdas-in-cpp.jpg
  credit: Myself :P
  creditlink: 
date: 2019-04-10 19:51 +0000
---
# Hello there!

This, well is my first post on this blog. I just want to make sure that you know that setting up this blog took way longer than I thought because I didn't know anything about Kramdown (a superset of Markdown) and the Jekyll(the static site generator) theme that I was using as well, as you may have guessed, using that. Not only that, I didn't know anything about how Ruby, it's "GEMS" worked. And everything was (well maybe still is) foreign to me. So pardon me if anything gets wrong or something, I will fix stuff if that happens.

Anyways, let's get on to the topic of discussion.

## LAMBDAs in C++

Probably a foreign topic to ya? No? Well if you came to read this blog post, you might want to know some stuff about it, right?

Some prerequisite knowledge that you need to need to need to have:

* What pointers really are
* Function Pointers
* How to write and overload operators for classes...

This is how a very basic lambda looks:

```cpp
[](){}  //this is known as an anonymous lambda as it doesn't have a name

//or even a simpler version:
[]{}
```

So it is nothing but a bunch of brackets. No need to be scared of it. We aren't going to talk about them just right now, we need to cover some topics first.

### Functors

First off, you need to know what a <b>functor</b> is.

A Class object which just "acts" like a function is called a functor(basically meaning that it overloads its operator() method):

```cpp
class sub {
private:
	int val;
public:
	sub(int v) : val(v) {

	}
	int operator()(int x) {
		return val - x;
	}
};

//main

	sub subFrom2(2);

	std::cout << subFrom2(3);	//-1

```

The C++ Standard Library has many functions that make use of things known as <b>predicates</b>. Which are nothing but functors. The STL does define some basic functors like <code>std::greater</code> & 
<code>std::sort</code> :

```cpp
#include<iostream>
#include<vector>		//std::vector which is a container class. In simple words, a better array... 
#include<functional>		//std::greater
#include<algorithm>		//std::sort


int main(){

std::vector<int> vec{ 3, 5, 2, 9, 7 };


	std::sort(vec.begin(), vec.end(), std::greater<int>());	//sorts in descending order...

	for (int elem : vec) {
		std::cout << elem;
	}	

	//97532

	std::cin.get();
	return 0;
}

```

<code>std::greater</code> is just a functor with an overloaded <code>operator()</code>. It takes in two parameters and returns a bool depending on whether the first param is greater than the second (true) or not(false):

```cpp

struct myGreater {
	bool operator()(int x, int y) const {
		return x < y;
	}
};

```
>Please do note that I have simplified implementations as I didn't want to overcomplicate stuff with <br>
>templates and related stuff and just get to the point....<br>
>That doesn't mean that I won't be talking about Generic Lambdas (that is at the very end) though...<br>
>If you want to see implementations, I would highly recommend [cppreference](https://www.cppreference.com)
<br>

However, if you are using something unique, you would probably need to use Lambdas...

Consider that you created your own <code>Point2D</code> class. Consider that you had a 
<code>std::vector</code> of some Point2D Objects. How would you sort them (on the basis of their distance from the origin) in ascending order using <code>std::sort</code>?.
<br>Think about using a functor, as I haven't talked about lambdas right now...
<br>
<br>And obviously, <code>std::greater</code> wouldn't work...

<br>Probably something like this?:

```cpp
class Point2D {
public:
	int m_x;
	int m_y;
public:
	Point2D(int a, int b) : m_x(a), m_y(b) {

	}
};

struct ptLesser {
	bool operator()(const Point2D& a, const Point2D& b) {
		return (a.m_x*a.m_x + a.m_y*a.m_y) < (b.m_x*b.m_x + b.m_y*b.m_y);
	}
};

int main(){

	Point2D pt1{ 3,4 };
	Point2D pt2{ 1,2 };
	Point2D pt3{ 0,0 };

	std::vector<Point2D>vec{pt1, pt2, pt3};

	std::sort(vec.begin(), vec.end(), ptLesser());

	std::cin.get();
	return 0;
}
```
<br>

Now just guess that you probably use the sort in only one particular function. Well, what you are basically doing is just making the whole process much cumbersome by writing a whole struct for that one simple task that you probably are gonna use for just once.

<br>

Since C++11, you no longer need to do this. Say hello to the <b>Lambdas</b>(again), allowing us to write
shorter, simpler and easier to maintain code:

```cpp
std::sort(vec.begin(), vec.end(), [](const Point2D& a, const Point2D& b){
	return (a.m_x*a.m_x + a.m_y*a.m_y) < (b.m_x*b.m_x + b.m_y*b.m_y);
	});
```
OR
<br>
```cpp
auto lambda = [](const Point2D& a, const Point2D& b) {
		return (a.m_x*a.m_x + a.m_y*a.m_y) < (b.m_x*b.m_x + b.m_y*b.m_y);
	};

std::sort(vec.begin(), vec.end(),lambda());
```

<br>

and that's it!
<br><br>

For a heads up: Lambdas are very much the same as functors... 
<br>In this case, there is no difference between the lambda and a functor similar to the lambda...
<br>
However, there is a small difference which we will be talking about a little later...

## How to write lambdas!?! What are these brackets!!!?!!!

That was well how I reacted when I was learning about them... It probably is better to look at how to write lambdas and then we will discuss what's going on under the hood...

Alright, so first up is how to write one? A basic lambda declaration to print "Hello World" would be:

```cpp
[]()->void{
	std::cout<<"Hello World";
};
```

What I just showed above is an example of a complete lambda. Let's have a brief overview of each of these parts and then we will discuss whatever is important in deep:

* The <b>[ ]</b>: This thingy represents a capture list. By default, a lambda can't access any variable 
(other than the ones initialized/declared inside it or passed as params). Modifications on the Capture List help us to tell it how to "capture" the variables...

* The <b>( )</b> is nothing but simply a parameter encloser... You write all the parameters inside this which are to be passed when you "call" the lambda... If there are no parameters, you can exclude the parenthesis.

* The <b>->void</b>: It is just a heads up for the compiler as to what the lambda returns when called. In many cases it is obvious or the compiler can deduce it implicitly and need not be provided.

* The <b>{ }</b> refers to the block of code that the lambda will execute.

### Alright, I understand except for what a lambda really is...

That's supposed to happen because that's how I wanted to frame up my talk.<br>
A <b>Lambda</b> is an object which is callable. Just like a function. Lambdas which don't have names are anonymous lambdas. These are inline and provide us the ability to keep relevant code together 
(like in sorting thing, everything related to it was just one line).

### Let's go deep on what actually happens when we write a lambda...

In basic sense, a functor is automatically created as per the lambda written. For example:

```cpp
int main(){
[](){std::cout<<"Hello World!";};

std::cin.get();
return 0;
}
```

<b>CAN BE THOUGHT AS TRANSFORMMING INTO: </b>

```cpp

class _ZZ4mainENKUliE_{	// a compiler generated name...
public:

	void operator()() const {	//note the const
		std::cout<<"Hello World!";
	}

};

int main(){

	_ZZ4mainENKUliE_();

	std::cin.get();
	return 0;
}

```

By default, the operator overload that happens for the class of the lambda is said to be <b><i>const</i></b>
The code above shows how... This means that the lambda cannot modify its object's member variables... <br>
(in this case, there aren't any).

<br>Let's look at another example that shows the use of member variables.

<b>Wait, where to put these member variables?</b>
<br>That's what the Capture List is for. Get it now?

<br>

```cpp
int main(){

int a = 2;

[a](){std::cout<<a;};

std::cin.get();
return 0;
}
```

<b>TURNS TO: </b>

```cpp

class _ZZ4mainENKUliE_{	// a compiler generated name...
private:
int a;

public:

	_ZZ4mainENKUliE_(int _a) : a(_a){

	}

	void operator()() const {	//note the const
		std::cout<<a;
	}

};

int main(){

	_ZZ4mainENKUliE_(2);

	std::cin.get();
	return 0;
}

```

Now, let's say you wanted to modify <code>a</code>. Essentially, you are asking how to remove that
<b><i>const</i></b> from the <code>operator()</code>. There are a couple of ways to do so.. 
<br>The simplest of them is to add <code>mutable</code> after the parantheses.

<br> Adding that basically means whatever you will be "capturing" can be modified...

### Type of a Lambda

A lambda is nothing but <b>"syntactic sugar"</b> for functors. The code of a lambda is converted to that of a functor (in a unique way which we will see by looking at the disassembly). Here's an extract from the standard (you gotta read the docs) :

>"The evaluation of a lambda-expression results in a prvalue temporary. 
>This temporary is called the closure object.
>The type of the lambda-expression (which is also the type of the closure object) 
>is a unique, unnamed nonunion class type — called the closure type.<br>
>The closure type for a non-generic lambda-expression with no lambda-capture has a public non-virtual nonexplicit const conversion function to pointer to function"

<br>
In simple words, you don't know the type of the lambda. Yeah, well that's hard to accept. However, as the last line in the extract suggests, this is possible:<br>

```cpp
auto lambda = [](int a)->void{std::cout<<a;};

void (*fn)(int a) = lambda
```

<b>But this is not: </b>

```cpp
int b;
auto lambda = [b](int a)->void{std::cout<<a;};

void (*fn)(int a) = lambda	//error no implicit conversion exists.
```
<br>

### Capturing Stuff

#### By Value

There are certain ways in which you can capture stuff. As is evident from the conversion to a functor which I just showed, the variable's value got copied:

```cpp
int a = 2;
auto lambda = [a]() {std::cout << a; };	//value of a gets copied
```
<br>
The variable in our "conceptual" functor (that is created due to the lambda), is assigned the value of the variable a. This is a potential overhead. However, just so you know, that's totally possible.
<br>
If you wanted to copy all the variables defined outside, you could just place an <code>=</code> sign inside the capture list:

```cpp
int a = 2;
int b = 2;
int c = 3;
int d = 4;
auto lambda = [=](int k) {std::cout << a << b << c << d; };		//all values are copied
lambda(3);
```
<br>

The "conceptual" functor in this case would be something like:

```cpp
class functor {
private:
	int a, b, c, d;
public:
	functor(int _a, int _b, int _c, int _d) : a(_a), b(_b), c(_c), d(_d) {

	}
	void operator()(int k) const {
		std::cout << a << b << c << d;
	}
};

```
#### By reference

You can easily do this inside lambdas:

```cpp
int a = 2;
auto lambda = [&a](){std::cout<<++a;};	
lambda()	//3
```
<br>
Wait, what? I didn't add <code>mutable</code> to the lambda. How did it change a?!?
<br>
<br>

The reason can be easily understood if we look at the functor for the above lambda:

```cpp
class functor {
private:
	int &m_a;

public:
	functor(int &_a) : m_a(_a) {

	}

	void operator()() const {
		std::cout << ++m_a;
	}
};
```
<br>

For those who understood, nice. For those who didn't, your question might be something like:

<i><b>
"I am changing <code>m_a</code> even though the function is <code>const</code>. How is that possible?"
</b></i>

<br>
Think about it like this, you aren't changing the reference. You are changing the value of what the reference is referring to. 
<br>
Or think about it with a pointer notation. If it were a pointer, you wouldn't be changing what the pointer is pointing to, you are changing the value of the variable that is being pointed to.

<br>

Now if you wanted all of the variables to be captured by reference, you could just do this:

```cpp
	int b = 2;
	auto lambda = [&](){
		b++;
	};
	lambda();
	std::cout << b;	//3
```
<br>
I guess you can now make the functor for this lambda by yourself...

<b>
NOTE: If you don't specify anything inside the capture list, the default action is to provide no access to variables. You can think that it means there will be no member variables in the functor...
</b>

<br>

### Mixed Captures
These are very possible:

```cpp

	int b = 2;
	int a = 3;
	int c = 5;

	auto lambda = [&, b]() {
		//this lambda copies values of every variable except b
	};

	auto lambda2 = [=, &b, &c] {
		//only a is copied
	};

```


### Lambda Init Captures -- C++14

Since C++14 you can initialize the variables of the lambda (the member variables of the 'conceptual' functor) inside the capture list:

```cpp
	auto lambda = [g=2]() {
		std::cout << g;
	};

	lambda();	//2
```

<code>g</code> is initialised to 2 as it can be seen. Another great example for clearing this part out is the one from the standard(I changed it a little):

```cpp
int x = 4;
auto y = [&r = x, x = x+2]()->int {
            r += 2;
            return x+3;
         };

int s = y();
```

Let's disccus, step-by-step, what might have happened here:

* A variable <code>r</code> which is a reference to the actual variable <code>x</code> is created as a member variable of the 'conceptual' functor.
* Another variable <code>x</code> is created as a member variable which has the value of <code>x+2</code> (The <code>x</code> here is the one initialised on the first line..) i.e. 6.
* The reference <code>r</code> changes the value of the real<code>x</code> to <code>x+2</code> i.e. 
<code>4+2 = 6</code>.
* The lambda returns the value of <code>x+3</code>. Here the x is the member variable. Hence the lambda returns 9.
* Now forget about the 'conceptual' functor.
* Hence, <code>s</code> is assigned the value of 9.
* <code>x</code> changes to 6.

### A talk about Globals and Statics

Global and static variables don't need to be captured. They are already available to the lambda. This is totally valid C++:

```cpp
int x = 2;

int main() {

static int y = 9;

	[]() {
		x++;
		y += 2;
	}();

	std::cin.get();
	return 0;
}
```

>A name in the lambda-capture shall be in scope in the context of the lambda expression and shall be <code>this</code> or refer to a local variable or reference with automatic storage duration.

Phew, that was a lot of talk only about captures!
<br>

## Anonymous Lambdas

A Lambda which isn't named is called an anonymous lambda. Calling such Lambdas can be done on the very same line as such:

```cpp
[](){std::cout<<"Hmm";}();
```

<br>

## Understanding why Lambdas are not totally functors.

If I would have to say in a sentence, Lambdas are inline functors. They are inlined in the function they are created. Or more specifically, their 'constructors'...

Let's infer this from some assembly. Don't worry, you don't need to go and understand Assembly... I will explain anything if required...

We will take this sample code:

```cpp

class functor {
private:
	int &m_a;

public:
	functor(int &_a) : m_a(_a) {

	}

	void operator()() const {
		m_a++;
	}
};

int main() {

	int a = 9;

	[&]() {
		a++;
	}();

	functor functor(a);
	functor();

	return 0;
}

```

You can use [Compiler Explorer](https://godbolt.org/) to check the assembly. I am gonna show the demangled code to you (the code where the names of the functions weren't changed by the compiler):

Let's see what we get, part by part.

These are the definitions of the constructor and the operator overload of the functor class respectively:<br>
(Don't worry about the code inside, we won't be talking about registers at all):

```
functor::functor(int&):
        push    rbp
        mov     rbp, rsp
        mov     QWORD PTR [rbp-8], rdi
        mov     QWORD PTR [rbp-16], rsi
        mov     rax, QWORD PTR [rbp-8]
        mov     rdx, QWORD PTR [rbp-16]
        mov     QWORD PTR [rax], rdx
        nop
        pop     rbp
        ret
functor::operator()() const:
        push    rbp
        mov     rbp, rsp
        mov     QWORD PTR [rbp-8], rdi
        mov     rax, QWORD PTR [rbp-8]
        mov     rax, QWORD PTR [rax]
        mov     edx, DWORD PTR [rax]
        add     edx, 1
        mov     DWORD PTR [rax], edx
        nop
        pop     rbp
        ret
```

Coming to the lambda, this is what we get:

```
main::{lambda()#1}::operator()() const:
        push    rbp
        mov     rbp, rsp
        mov     QWORD PTR [rbp-8], rdi
        mov     rax, QWORD PTR [rbp-8]
        mov     rax, QWORD PTR [rax]
        mov     edx, DWORD PTR [rax]
        add     edx, 1
        mov     DWORD PTR [rax], edx
        nop
        pop     rbp
        ret
```

The definition of the lambda call is the same as that of the overload of the functor.

Now, you might ask where is the constructor for it? Let's go to <code>main</code>:

```
	main:
 1       push    rbp
 2       mov     rbp, rsp
 3       sub     rsp, 32
 4       mov     DWORD PTR [rbp-12], 9
 5       lea     rax, [rbp-12]
 6       mov     QWORD PTR [rbp-8], rax
 7       lea     rax, [rbp-8]
 8       mov     rdi, rax
 9       call    main::{lambda()#1}::operator()() const
10       lea     rdx, [rbp-12]
11       lea     rax, [rbp-24]
12       mov     rsi, rdx
13       mov     rdi, rax
14       call    functor::functor(int&)
15       lea     rax, [rbp-24]
16       mov     rdi, rax
17       call    functor::operator()() const
18       mov     eax, 0
19       leave
20       ret
```

Line 5 to Line 8 is where the constructor part gets done for the lambda.
The <code>this</code> pointer for the lambda is the address 0x08.

Lines 10 to 14 get the set up of the functor done. The address of the functor's <code>this</code> is at 0x24.
Also, notice that this involves a call to the functor's constructor as well...

> Do note that the assembly code is unoptimized, I didn't wanna change anything and show you whatever was there... For example, it loads stuff into registers without any reason instead of moving them...

## Generic Lambdas -- C++ 14

The last topic of discussion and I will be done. I am sick of typing and editing so much of text... But I will do it for you : )

The parameters of a lambda, starting from C++14 can be generic. However, this doesn't involve typing 
<code>template &lt;typename T&gt;</code> anywhere. You just place the <code>auto</code> keyword in front of the parameters:

```cpp

auto print = [] (auto a, auto b) { std::cout<<a<<" & "<<b; };

```

It is to be noted that this does transform to a functor somewhat like this:

```cpp
class NameByCompilerrrrrrrr{
public:
    template<typename T1, typename T2>
    T operator () (T1 a, T2 b) const { std::cout<<a<<" & "<<b; }
};
```

>For a generic lambda, the closure type has a public inline function call operator member template whose template-parameter-list consists of one invented type template-parameter for each occurrence of auto in the lambda’s parameter-declaration-clause, in order of appearance.

And with that being said, you now know almost everything about lambdas! Thank you for joining this discussion with me!

<br>
<hr>