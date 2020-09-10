---
layout: post
title: The Essence of Lambdas in C++
description: Understand C++ lambdas like never before in a beginner friendly manner
modified: 2020-09-11
tags:
- cpp
- c++
- lambdas
- lambda
- functor
- function
- pointers
image:
  path: /images/
  background: prime-bg.jpg
  feature: LambdasInCPP/lambdas-in-cpp.jpg
  credit: Myself :P
  creditlink: 
date: 2019-04-10
---

Heyo!

This is my very first blog post. Here's my note to every reader:

> This is my first post on this blog. I just want to make sure you know that setting up this blog took way longer than I thought because I knew nothing about Ruby, it's *GEMS*, Liquid, Jekyll and suchlike.

Anyway, let’s get on to today's discussion.

> **NOTE:** Hi there! It's Sid from the future. The current post has no faults whatsoever, but I don't think it covers some stuff it should, and I also think that I can explain some stuff even better. This means that a little bit of a change is underway. You can still continue to read the current post and it will probably be fruitful, but just make sure you know changes are in place.

## LAMBDAs in C++

Probably a foreign topic to ya? No? Well, if you came to read this blog post, you might want to know some stuff about it, right?

Some prerequisite knowledge that you need to need to need to have:

* What pointers are (I mean that's simply expected)
* Function Pointers (Not a lot though)
* How to write and overload operators for classes... (A bit would help)

This is what a very basic lambda looks like:

```cpp
[](){}  //this is known as an anonymous lambda as it doesn't have a name

//an even simpler version:
[]{}
```

So it is nothing but a bunch of brackets. No need to fear it. We will not talk about them just right now; we need to cover some topics first.

### Functors

First off, you need to know what a **functor** is.

A Class object which just "acts" like a function is called a functor (basically meaning that it overloads its `operator()` method):

```cpp
class Sub {
private:
    int m_val;
public:
    Sub(int v) : m_val(v) {

    }
    int operator()(int x) {
        return m_val - x;
    }
};

// main

Sub subFrom2(2);
subFrom2(3);    //-1

```

What's cool about functors? Well, the thing I like them most for is that these can contain "states" (the `m_val` in this case).

The C++ Standard Library has many functions that make use of things known as **predicates**. Which are nothing but functors (alright not completely true because a predicate is required to be any 'callable' thing that returns a `bool` which can be tested. You can have a look at _[stackoverflow](https://stackoverflow.com/questions/5921609/what-is-predicate-in-c)_ and _[cppreference](https://en.cppreference.com/w/cpp/named_req/Predicate)_ if you want to dig deep). The STL defines some functors like `std::greater` & `std::less` :

```cpp
#include<iostream>
#include<vector>            //std::vector which is a container.
#include<functional>        //std::greater et al
#include<algorithm>         //std::sort


int main(){

std::vector<int> vec{ 3, 5, 2, 9, 7 };


    std::sort(vec.begin(), vec.end(), std::greater<int>());    //sorts in descending order...

    for (int elem : vec) {
        std::cout << elem;
    }

    //97532

    std::cin.get();
    return 0;
}
```

`std::greater` is just a functor with an overloaded `operator()`. It takes in two params and returns true if the first one is greater than the second one:

```cpp
struct myGreater {
    bool operator()(const int& x, const int& y) const {
        return x > y;
    }
};
```

> Note that I have simplified implementations as I didn’t want to over-complicate stuff with
 templates and related stuff....
 That doesn't mean that I won't be talking about Generic Lambdas (that is at the very end) though...
>
> If you want to see implementations, I highly recommend [cppreference](https://www.cppreference.com)

However, if you are using something unique, you would probably need to use Lambdas...

Consider that you created a `Point2D` class (concerned with points in 2D, obviously) and that you had a `std::vector` of some Point2D Objects. How would you sort them (on the basis of their distance from the origin) in ascending order using `std::sort`?

Think about using a functor, as I haven't talked about lambdas right now...

And obviously, `std::greater` wouldn't work...

Probably something like this?:

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
        return (a.m_x * a.m_x + a.m_y * a.m_y) < (b.m_x * b.m_x + b.m_y * b.m_y);
    }
};

int main() {

    Point2D pt1{ 1,1 };
    Point2D pt2{ 2,2 };
    Point2D pt3{ 0,0 };

    std::vector<Point2D>vec{ pt1, pt2, pt3 };

    std::sort(vec.begin(), vec.end(), ptLesser());

    for (Point2D elem : vec) {
        std::cout << "(" << elem.m_x << ", " << elem.m_y << ")\n";
    }

    /*
    (0, 0)
    (1, 1)
    (2, 2)
    */

    return 0;
}
```

Just assume that you seldom use the sort. In that case, you make the whole process cumbersome by writing a whole struct for that one simple task.

> Yes, you could use a function returning a `bool` and stuff, but the point remains. You will have some irrelevant code hanging here and there which is not used often.

Since C++11, you no longer need to do this. Say hello to the **Lambdas** (again) which allow us to write
shorter, simpler and easier to maintain code:

```cpp
std::sort(vec.begin(), vec.end(), [](const Point2D& a, const Point2D& b){
    return (a.m_x*a.m_x + a.m_y*a.m_y) < (b.m_x*b.m_x + b.m_y*b.m_y);
    });
```

OR

```cpp
auto ptLess = [](const Point2D& a, const Point2D& b) {
        return (a.m_x*a.m_x + a.m_y*a.m_y) < (b.m_x*b.m_x + b.m_y*b.m_y);
    };

std::sort(vec.begin(), vec.end(),ptLess);
```

and that's it!

For a heads up: Lambdas are very much the same as functors...

In this case, there is no difference between the lambda and a functor similar to the lambda...

However, there is a subtle difference which we will be talking about a bit later...

## The meaning of those mundane brackets

It's better to look at how to write lambdas and then we will discuss what's going on under the hood...

A basic lambda to print `Hello World` would be:

```cpp
[]()->void{
    std::cout<<"Hello World";
}();    //the last parentheses represent a call
```

What I just showed above is an example of a 'complete' lambda - full of all kinds of brackets it could have. Let's have a brief overview of each of these parts:

* The `[ ]`: This thingy represents a capture list. By default, a lambda can't access any variable (other than the ones initialized/declared inside it or passed as params). Modifications on the Capture List help us to tell it how to "capture" the variables...

* The `( )` is nothing but simply a parameter encloser... You write all the parameters inside this which are to be passed when you "call" the lambda... If there are no parameters, you can exclude the parenthesis.

* The `->void`: It is just a heads up for the compiler as to what the lambda returns when called. In many cases it is obvious or the compiler can deduce it implicitly and need not be provided.

* The `{ }` refers to the block of code that the lambda will execute.

### Alright, let's go deep

A **Lambda** is a callable object - just like a function. These are *inline* and provide us the ability to keep relevant code together. (like in sorting thing everything related to it was just one line).

### What goes on when we write a lambda

Essentially a functor is automatically created based on the lambda. For example:

```cpp
int main(){

[](){std::cout<<"Hello World!";}();

}
```

**CAN BE THOUGHT AS TRANSFORMMING INTO:**

```cpp
class _ZZ4mainENKUliE_{    // a compiler generated name...
public:

    void operator()() const {    // note the const
        std::cout<<"Hello World!";
    }

};

int main(){

    _ZZ4mainENKUliE_();

}
```

By default, the operator overload that happens for the class of the lambda is `const`, meaning that the lambda cannot modify its object’s member variables (in this case, there aren’t any).

Let's look at another example that shows the use of member variables.

**Wait, where to put these member variables?**

That's what the Capture List is for. Get it now?

```cpp
int main(){

int a = 2;

[a](){std::cout<<a;}();

std::cin.get();
return 0;
}
```

**TURNS TO:**

```cpp
class _ZZ4mainENKUliE_{    // a compiler generated name...
private:
int a;

public:

    _ZZ4mainENKUliE_(int _a) : a(_a){

    }

    void operator()() const {    // note the const
        std::cout<<a;
    }

};

int main(){

    _ZZ4mainENKUliE_(2);

}
```

Now, let's say you wanted to modify `a`. You are asking how to remove that
`const` from the `operator()`. There are a couple of ways to do so..

The simplest of them is to add `mutable` after the parantheses.

Adding that basically means whatever you will be "capturing" can be modified...

### Type of a Lambda

A lambda is nothing but **"syntactic sugar"** for functors. The code of a lambda is converted to that of a functor (in a unique way which we will see by looking at the disassembly). Here's an extract from the standard (you gotta read the docs) :

> "The evaluation of a lambda-expression results in a prvalue temporary.
 This temporary is called the closure object.
 The type of the lambda-expression (which is also the type of the closure object)
 is a unique, unnamed nonunion class type — called the closure type.
 The closure type for a non-generic lambda-expression with no lambda-capture has a public non-virtual nonexplicit const conversion function to pointer to function"

In simple words, you don't know the type of the lambda. Yeah, well that's hard to accept. However, as the last line in the extract suggests, this is possible:

```cpp
auto lambda = [](int a)->void{std::cout<<a;};

void (*fn)(int a) = lambda;
```

**But this is not:**

```cpp
int b;
auto lambda = [b](int a)->void{std::cout<<a;};

void (*fn)(int a) = lambda    // Error: No implicit conversion exists.
```

### Capturing Stuff

#### By Value

There are certain ways in which you can capture stuff. As is evident from the conversion to a functor which I just showed, the variable's value got copied:

```cpp
int a = 2;
auto lambda = [a]() {std::cout << a; };    // value of a gets copied
```

The variable in our "conceptual" functor (that is created due to the lambda) is assigned the value of the variable `a`. This has a potential overhead in cases where you're copying large objects though.

If you wanted to copy all the variables defined outside, you could just place an `=` inside the capture list:

```cpp
int a = 2;
int b = 2;
int c = 3;
int d = 4;
auto lambda = [=](int k) {std::cout << a << b << c << d; };        //all values are copied
lambda(3);
```

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
lambda()    //3
```

Wait, what? I didn't add `mutable` to the lambda. How did it change a?!?

The reason can be easily understood if we look at the functor for the above lambda:

```cpp
class functor {
private:
    int& m_a;

public:
    functor(int& _a) : m_a(_a) {

    }

    void operator()() const {
        std::cout << ++m_a;
    }
};
```

If you're wondering why `m_a` could be changed even when `operator()()` was `const`, it's because you aren't changing what the reference is referring to (cuz you can't anyhow). [You're only changing the value of the thing being referred to.](https://stackoverflow.com/questions/23436836/why-can-reference-members-be-modified-by-const-member-functions)

Or think about it with a pointer notation. If it were a pointer, you wouldn't be changing what the pointer is pointing to, you are changing the value of the variable that is being pointed to.

And another note. ***Don't think that***

```cpp
int a{3};

[a]() mutable {a = 4;};

//is equivalent to

[&a](){a=4;};
```

They aren't equivalent. One of them creates a *personal* copy of `a` and changes that while the other one changes the value it took from the reference. In other words, the first lambda changes a copy while the second one changes the actual variable.

Now if you wanted all of the variables (from the calling scope) to be captured by reference, you could just do this:

```cpp
int b = 2;
auto lambda = [&](){
    b++;
};
lambda();
std::cout << b;    //3
```

> Even though I say you capture *all* of the variables, the compiler is smart enough to look at what you use inside the lambda and the *conceptual functor* contains just those thingies. A better way to convey this would be to say that this makes all of things accessible.

I guess you can now make the functor for this lambda by yourself...

### Mixed Captures

This is very possible:

```cpp
int b = 2;
int a = 3;
int c = 5;

auto lambda = [&, b]() {
    // b is taken by value and the others by reference...
};

auto lambda2 = [=, &b, &c] {
    // only a would be 'copied'
};
```

### Lambda Init Captures -- C++14

Since C++14, you can initialize the variables of the lambda (the member variables of the 'conceptual' functor) inside the capture list:

```cpp
auto lambda = [g=2]() {
    std::cout << g;
};

lambda();    //2
```

`g` is initialised to `2` as it can be seen. Another great example for clearing this part out is the one from the standard(I changed it a little):

```cpp
int x = 4;
auto y = [&r = x, x = x+2]()->int {
            r += 2;
            return x+3;
         };

int s = y();
```

Let's discuss what might have happened here:

* A variable `r` which is a reference to the actual variable `x` is created as a member variable of the 'conceptual' functor.
* Another variable `x` is created as a member variable which has the value of `x+2` (The `x` here is the one initialised on the first line..) i.e. `6`.
* The reference `r` changes the value of the real`x` to `x+2` i.e.
`4+2 = 6`.
* The lambda returns the value of `x+3`. Here the x is the member variable. Hence the lambda returns 9.
* Now forget about the 'conceptual' functor.
* Hence, `s` is assigned the value of `9`.
* `x` changes to `6`.

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

}
```

> A name in the lambda-capture shall be in scope in the context of the lambda expression and shall be `this` or refer to a local variable or reference with automatic storage duration.

Phew, that was a lot of talk only about captures!

## Anonymous Lambdas

A Lambda which isn't named is called an anonymous lambda. You can call it like so:

```cpp
[](){std::cout<<"Hmm, is someone cAlLiNG mE!?";}();
```

## Understanding why Lambdas are not *totally* functors

If I would have to say in a sentence, Lambdas are inline functors. They are inlined in the function they are created. Or more specifically, their 'constructors'...

Let's infer this from some assembly. Don't worry, you don't need to go and understand Assembly... I will explain anything if required...

We will take this sample code:

```cpp
class functor {
private:
    int& m_a;

public:
    functor(int& _a) : m_a(_a) {

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

}
```

You can use [Compiler Explorer](https://godbolt.org/) to check the assembly. I am gonna show the demangled code to you (the code where the names of the functions weren't changed by the compiler):

Let's see what we get...

These are the definitions of the constructor and the operator overload of the functor class respectively (Don't worry about the code inside, we won't be talking about registers and assembly at all):

```armasm
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

```armasm
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

Wondering about its constructor? Let's go to `main`:

{% highlight armasm linenos %}
main:
   push    rbp
   mov     rbp, rsp
   sub     rsp, 32
   mov     DWORD PTR [rbp-12], 9
   lea     rax, [rbp-12]
   mov     QWORD PTR [rbp-8], rax
   lea     rax, [rbp-8]
   mov     rdi, rax
   call    main::{lambda()#1}::operator()() const
   lea     rdx, [rbp-12]
   lea     rax, [rbp-24]
   mov     rsi, rdx
   mov     rdi, rax
   call    functor::functor(int&)
   lea     rax, [rbp-24]
   mov     rdi, rax
   call    functor::operator()() const
   mov     eax, 0
   leave
   ret
{% endhighlight %}

Line 6 to Line 9 is where the constructor part gets done for the lambda.
The `this` pointer for the lambda is the address `0x08`.

Lines 11 to 15 get the set-up of the functor done. The address of the functor's `this` is at `0x24`.
Also, notice that this involves a call to the functor's constructor...

> Do note that the assembly code is unoptimized, I didn't wanna change anything and show you whatever was there... For example, it loads stuff into registers without any reason instead of moving them...

## Generic Lambdas -- C++ 14

The last topic of discussion and I will be done. I am sick of typing and editing so much of text... But I will do it for you :smile:

Starting from C++14, the params of a lambda can be *generic*. However, this doesn't involve typing `template <typename T>` anywhere. You just place the `auto` keyword in front of the parameters:

```cpp
auto print = [] (auto a, auto b) { std::cout<<a<<" & "<<b; };
```

This does transform to some code like this:

```cpp
class NameByCompilerrrrrrrr{
public:
    template<typename T1, typename T2>
    T operator () (T1 a, T2 b) const { std::cout<<a<<" & "<<b; }
};
```

> For a generic lambda, the closure type has a public inline function call operator member template whose template-parameter-list consists of one invented type template-parameter for each occurrence of auto in the lambda’s parameter-declaration-clause, in order of appearance.

And with that being said, you now know almost everything about lambdas! Thank you for joining this discussion with me!
