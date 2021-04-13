---
layout: post
title: Let's talk Unicode 😐
description: It's just us trying to fix a mess we didn't think about beforehand.
mathjax: true
image:
  path: /images/
  background: prime-bg.jpg
  feature: Unicode/feature.jpg
  credit: Bernard Hermant
  creditlink: https://unsplash.com/@bernardhermant
date: 2021-04-11
---

We take many things for granted, and one thing almost everyone takes for granted is how characters are actually represented. You might have heard computers work in binary - `0`s and `1`s (probably a zillion times), but then how do they *store* and *deal* with the characters you're reading now and are familiar with?

That should be pretty simple to answer: we assign a number to each *character* and then that's it - refer to the *number mapping* and then get the corresponding binary (aka `1`s and `0`s) representation.

# To the time machine!

To properly understand everything, let's take a ride on the time machine! This is a time when the internet was relatively new...

> We could go back even further, but meh let's not bring a lot of history aight? *Also, I'm sort of running short on money and I definitely need to pay my bills for the time machine... 😬*

Alright, so we're here now. At a glance, we note that folks don't have access to a lot of computer memory like we do (heh). That goes to say that most of these *number mappings* utilize just 1 byte.

> A byte is unit of memory and is composed of 8 bits (so 8 places to put our `1`s and `0`s in). On most computer architectures, it is the smallest addressable unit of memory. Ironically, the reason it is the smallest addressable unit of memory is because it was used to encode a single character...

Notice that I said *mappings* instead of *mapping*. Yep, there are multiple mappings available and different computers work with different ones...

Before we dive even deeper, let's just make sure how this number mapping works. Instead of calling these things **number maps**, I am gonna call them **character sets**. We're gonna stick to the American Standard Code for Information Interchange (welp that's a mouthful, but the name makes sense right?) or **ASCII**.

---

> I am gonna assume you're familiar with binary and hexadecimal stuff all throughout the post. If you aren't, here's a short reference:

<details>
<summary>Number Systems 101</summary>

<div markdown="1">
If I were to say "My name is Person" in French, I would say "Je m'appelle Person". The meaning remains the same, but the way it's written and spoken changes. Some languages are used more often than others, some are standardized for official work in some places, and whatnot - you get the point.

The same goes for the numbers we understand. There's no *correct* representation, but some are of course used more than others.

The one we most commonly use is the decimal number system. It's named so because there are 10 symbols -  `0`, `1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`.

A number $$ABC$$ in decimal can also be written as $$A\times 100 + B\times 10 + C$$ or $$A\times 10^2 + B\times 10^1 + C\times 10^0$$. Likewise, if we switch to another base, to convert the number to our beloved decimal system we would multiply the digits by powers of the base and then add these up.

For example, in binary we have 2 symbols - `0` and `1`. So the base is 2. Hence something like `0b10` - oh wait, what's that? What's the `0b`? Well to not always go with the phrase "`x` in binary/hexadecimal" we prefix the thing with `0a` where `a` can be these:

- `b`: Binary
- `x`: Hexadecimal

We can also specify the base using a subscript - $$(111)_2$$

Alrighty, let's continue. So yeah something like `0b10` would be $$1\times 2^1 + 0\times 2^0 = 2$$.

In the hexadecimal system there are 16 symbols. We ran out of *number-like symbols that look like a single entity*, so we use alphabets after 9 - `0`, `1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`, `a`, `b`, `c`, `d`, `e`, `f`.

So `0x3f` would be $$3\times 16 + f = 48 + 10 = 59$$ where we just replace the hexadecimal digit `f` to its *value* - 10.

That's all cool, and we're mostly done; I just don't want to omit one cool thing about the relationship between hexadecimal numbers and binary numbers: you see, each binary digit (or bit) can take 2 values. On the other hand, each hexadecimal digit can take any of the 16 values. 16 happens to be a power of 2. More precisely, it's the fourth power of 2: $$2^4 = 16$$. This means that it takes a total of 4 bits to represent any hexadecimal digit. How? well consider the number

$$(abcd)_2$$

Each of `a`, `b`, `c` and `d` is a bit, so each of them can take 2 values. For each of the 2 values of `a`, there can be 2 values of `b`, and for each of those 2 values of `b`, there can be 2 values of `c`, Aaand for each of THOOOSE 2 values of `c`, there can be a total of 2 values for `d`. So we can ***mathify*** this and get the total number of values 4 bits can represent:

$$\underset{\text{For each of the values of } \verb|a|}{2}\cdot \underset{\text{For each of the values of } \verb|b|}{2}\cdot \underset{\text{For each of the values of } \verb|c|}{2}\cdot \underset{\text{For each of the values of } \verb|d|}{2} = 2^4 = 16$$

What this means is that each hexadecimal digit has a unique 4 bit representation. Hence a number in hexadecimal can be easily converted to binary by decomposing each of the hexadecimal digits to it's 4 bit representation:

$$(\underbrace{3}_{\verb|0011|}\quad\underbrace{F}_{1111})_{16} = (0101 1111)_2$$

We can also go the other way and convert binary to hexadecimal by making groups of 4:

$$(\underbrace{1001}_{9}\quad\underbrace{1010}_A)_2 = (9A)_{16}$$

A byte, which is made of 8 bits can hence be represented by just 2 hexadecimal digits. This shortens down the representation a lot, and is pretty cool! We use this fact to shorten down binary when needed. An example would be memory addresses. Another very awesome example would be color representation - in ***RGB*** notation we specify a decimal value from 0 to 255 for each of the placeholders R (red), G (green) and B (blue). That's 256 total values and can be represented by 8 bits. This means that we can represent this thingy in hexadecimal form by replacing the decimal with its two (hexadecimal) digit equivalent:

$$\mathrm{RGB}(34, 34, 34) = \#\underbrace{22}_\mathrm{R}\underbrace{22}_\mathrm{G}\underbrace{22}_\mathrm{B}$$

Awesome! I think that's enough for a short 101. Onto the main topic!

</div>

</details>

---

Let's say we wanted to represent the text `Hello!` using ASCII. Hmm, let's include numbers as well? Aight, so let's say we wanna represent this:

{% highlight txt %}
Hello! 2+2=4
{% endhighlight %}

Seems cool. You can pick up any *ASCII-Table* and see what each character maps to. Here's a short table that we can use:

<center>
    <img src="/blog/images/Unicode/ascii-demo.svg" data-zoomable>
</center>

> I ***definitely did not*** skip most of characters that weren't necessary for my example...

Alright, with that information here's our text, but in binary:

{% highlight txt %}
01001000 01100101 01101100 01101100 01101111 00100001 00100000 00110010 00101011 00110010 00111101 00110100
{% endhighlight %}

That's how your text is represented by a computer (considering the thing is ASCII encoded), and you got to say that looks beautiful (or maybe it's just the codeblock's styles that I worked hard on 😛) Now that we understand how these mappings work, let's continue.

## jsnkd漢jfnnfs d片smkd s.d;[;waskaas]仮s;s

Everything seems to work fine with this system; where's the problem? Well what about other languages and other weird symbols? Ah well we can just incorporate them depending on the location the computer is gonna work with... That works nice, but let's just fast forward to a time where the internet becomes a bit more common. People can now *share data* over the internet and they do so primarily via text. What if we were to send a string of data from a computer that followed some local encoding to a person with a computer following a different encoding? Well, we expect to end up with random mumbo jumbo. This happened quite often that it got a name - *mojibake*. It's a Japanese word which translates to "unintelligible sequence of characters".

On top of that, most of the times it was difficult to even know which encoding the thing was in.

For most of the encodings, we would need some sort of statical analysis to guess the encoding. ASCII is kinda special in this regard, however. If you stick with normal ASCII, it makes use of only 7 bits instead of 8 bits (extended ASCII makes use of 8 bits). So we could guess that the encoding is in ASCII if the 8th bit is always set to 0.

Also the "we'll deal with the other language problem depending on the location" has a problem. Many languages contain a ton of symbols. Trying to map each one of them consumes a serious amount of memory, and if we use the characters on the top of the mapping thingy most of the times, we're wasting a lot of memory.

> Altogether there are over 50,000 characters in Chinese!

So trying to make an even larger mapping to incorporate every symbol on Earth isn't that feasible... Well, not really - what if we go introduce variable lengths for each character's binary representation? Onto Unicode Encodings! (Minus UTF32 because that's not a variable-length encoding)

> Unicode Encodings like UTF-8 and UTF-16 aren't the only variable-length encodings though. This post concerns Unicode, so it gets the limelight here...

Diving right into encodings like UTF-8 (my favorite!) is going to be weird, so let's first talk about Unicode and the encodings in general.

# Hey Unicode!

## What are you?

Unicode is a standard. This standard defines a *code space*. What's a codespace? It's the space or the list of all the numerical values assigned to characters. This is nothing but the number mapping thing we were dealing with! Each numerical value is called a code point. So a codespace is the list of all possible mappings from a code point to it's corresponding *character*.

When we move to character representation, the term *character* itself becomes vague. It can mean may things which are sometimes decipherable based on the context... A character could refer to a

- *Grapheme*. This might or might not be the actual character in question and there's a tad bit of ambiguity sprinkled over this term too (don't worry we'll get that clarified).
- *Abstract Character*. This is the what we perceive as a viewable, representable character/symbol. Some also call this a *glyph*, but be aware that a *glyph* is like a pictorial representation of a character and it can change it's appearance (but not the general agreed upon layout/format of the character) depending on the font...
- *Code point*. Yeah the terms aren't really interchangeable, but you get the point...

We need to refine the definition of the Unicode codespace to better make sense of graphemes:

> ***The Unicode codespace is a mapping from code points to characters (these can either be abstract characters and/or graphemes).***

> Unicode even has notational stuff in place for the code points. Use hex to represent the number/code point in question. If that is less than 4 digits, prefix it with zeros to make it equal to 4 digits. Prefix the thing with `U+`. So the code point $$(65)_{10}$$ is essentially `U+0041`.

Graphemes are entities in the codespace that have their own code point based representation... (Abstract) characters can essentially be represented by one or more graphemes in Unicode. We'll take two examples to understand this better:

- Consider *H*. This has the code point $$(72)_{10}$$ or `U+0048`. It's a grapheme and an abstract character.

- Now consider *Ç*. This abstract character actually has two representations in Unicode: *Ç* as a whole with code point `U+00C7` and the letter C (`U+0043`) followed by the *Combining Cedilla* ◌̧ (`U+0327`). Both representations produce the same results and refer to the same abstract character, but the latter is composed of two different code points or graphemes. `U+0327` doesn't mean anything in itself in terms of being an abstract character, but when combined with another grapheme, it can give us a meaningful character. This representation using a combination or *cluster* of graphemes is also called a *grapheme cluster*.

All that goes to say that code points map to graphemes which might or might not be abstract characters. All abstract characters which have a single code point representation are graphemes, but not all graphemes are abstract characters. The codespace assigns code points to graphemes which can also be the abstract character in question.

Phew! That was a mouthful, but I hope I was able to get the point across...

## Representation and the basic unit

We can represent the code point in question in several different ways. Each of these ways makes use of an encoding to give us a digital representation. The representation can be broken down to one (or more) units called *code units*. A *code unit* is the smallest identifiable sequence of bits in that encoding. For example, each code unit in *ASCII* is 7 bits long. If you consider *Extended ASCII*, each code unit is 8 bits long. For *UTF-32* on the other hand, each code unit is **32 bits** long!

Consider the character ϕ (`U+03D5`). It has the following representations in the following encodings:

- UTF-32: `0x000003D5` or `00000000000000000000001111010101`
- UTF-16: `0x03D5` or `0000001111010101`
- UTF-8: `0xCF` `0x95` or `11001111` `10010101`

Before we dive any deeper into the aforementioned encodings, I would like to describe the Unicode code space even better (a bit math involved, but if you don't care about the specifications and don't care about this section, you can skip this):

The codespace contains codepoints from `0x0` to `0x10FFFF`. This is divided into 17 *planes* (planes 0 through 16) each with $$2^{16}$$ or 65536 codepoints. Much as the same way that there are $$5+1=6$$ numbers from $$0$$ to $$5$$ (inclusive), there are a total of $$\mathrm{(10FFFF)}_{16} + 1 = 1114111 + 1 = 1114112$$ code points (which agrees with $$17\cdot 65536 = (16+1)\cdot 2^{16} = (2^4+1)\cdot 2^{16} = 2^{20} + 2^{16} = 1114112$$).

> Another way to end up with the same count from $$\mathrm{(10FFFF)}_{16}+1$$ is to use hex math: $$\mathrm{(10FFFF)}_{16} + 1 = (110000)_{16} = 1\cdot 16^5 + 1\cdot 16^4 + 0 + 0 + 0 + 0 = 2^{20} + 2^{16}$$

A bit of a catch though[^1]:

> Of these $$2^{16} + 2^{20}$$ defined code points, the code points from `U+D800` through `U+DFFF`, which are used to encode surrogate pairs in UTF-16 (more on that in a bit), are reserved by the Standard and may not be used to encode valid characters, resulting in a net total of $$2^{16} + 2^{20} − 2^{11} = 1,112,064$$ (there are $$\mathrm{(DFFF)}_{16} - \mathrm{(D800)}_{16} + 1 = \mathrm{(7FF)}_{16} + 1 = (800)_{16} = 8\cdot 16^2 = 2^{11}$$ total characters in the surrogate range thingy) possible code points corresponding to valid Unicode characters. Not all of these code points necessarily correspond to visible characters; several, for example, are assigned to control codes such as carriage return.

There's more to it with blocks, categories, characters for private use and whatnot, but I'll let you use the art of Google-fu to explore those... Onto the encodings!

## UTF-32

This is simplest encoding of all with characters mapped directly to the codepoint value. As we previously saw, there are 1,112,064 code points we need to work with from the code space. Since we're representing stuff in bits, we need to consider powers of 2 to get the number of bits enough to work with the Unicode standard. As it turns out, the smallest upper bound (as a power of 2) to that number is $$2^{21} = 2,097,152$$.

Technically speaking, we can use 21 bits to represent all Unicode characters. UTF-32, however, uses 32-bit code units to represent characters. The main reason to use 32 instead of a number like 21 is because computers don't work well with those kinds of numbers (it takes more instructions and/or cycles to carry out operations; see [this](https://stackoverflow.com/questions/6339756/why-utf-32-exists-whereas-only-21-bits-are-necessary-to-encode-every-character#comment-116659202)).

You could also argue that another reason is because this allows for room for expansion - this isn't really likely as the standard has [restricted itself](https://en.wikipedia.org/wiki/UTF-32#History) to `U+10FFFF` as the maximum code point to remain compatible with UTF-16 because the latter cannot encode code points greater than `U+10FFFF`.

Why do we require UTF-32 then? The main advantage to this encoding is that many operations are then constant time because we have a fixed with encoding. There's not much to it other than that...

From Wiki[^2]:
> The main use of UTF-32 is in internal APIs where the data is single code points or glyphs, rather than strings of characters. For instance, in modern text rendering, it is common that the last step is to build a list of structures each containing coordinates (x,y), attributes, and a single UTF-32 code point identifying the glyph to draw. Often non-Unicode information is stored in the "unused" 11 bits of each word.

UTF-32 is very inefficient in the aspect of memory usage. Each code point requires 4 bytes, and it turns out that characters beyond *Plane 0* (also called the *Basic Multilingual Plane*) are relatively uncommon. To represent all characters in *Plane 0* we require 16 bits, so most of the other bits usually go unused. Imagine how many bits we'd waste if we were to only use stuff from ASCII!

> I haven't mentioned this yet, but the Unicode codespace is backwards compatible with *ASCII* - the first 128 characters in the mapping are the same as that of the usual *ASCII*!

## UTF-16

As we saw, most text contains characters from BMP which requires 16 bits most of the time. So we might as well create an encoding where a code unit is 16 bits long. And thus we end up with UTF-16. Here's how you encode something in UTF-16:

1. Take the code point's numerical value.
2. If the value can fit in 16-bits (that is to say it's ≤ `U+FFFF`)*, just convert the thing to it's 16-bit equivalent and we're done.
3. If not, then the value lies in [`U+10000`, `U+10FFFF`] (an inclusive interval). We encode these code points in two 16-bit code unit pairs known as *surrogate pairs*. What you essentially need to do is subtract `0x10000` from the code point. This gives you a value in [`U+00000`, `U+FFFFF`]:
    - The high ten bits (in `[0x000, 0x3FF]`) are added to `0xD800` to give the first 16-bit code unit aka the *high surrogate* (in [`0xD800`, `0xDBFF`]).
    - The low ten bits (in `[0x000, 0x3FF]`) are added to `0xDC00` to give the second 16-bit code unit aka the *low surrogate* (in [`0xDC00`, `0xDFFF`]).

Notice the asterisk in the third point. It's there because not all things less than `0xFFFF` are viable code points:
> Things from `U+D800` through `U+DFFF` are used to encode surrogate pairs in UTF-16 (as we just saw) and are reserved by the standard and may not be used to encode valid characters.

To explain the third point better, let's encode an emoji - 💩 `U+1F4A9`:

- The code point is `0x1F4A9`. Subtract `0x10000` from it to get `0xF4A9` which is `1111 0100 1010 1001` in binary. So the high ten bits are `0000111101` or `0x3D` and the low ten bits are `0010101001` or `0xA9`.
- The high surrogate will thus be `0xD800` + `0x3D` = `0xD83D`.
- The low surrogate will thus be `0xDC00` + `0xA9` = `0xDCA9`.

So, the UTF-16 code units are `0xD83D` and `0xDCA9`.

### Endianness Considerations

The astute and informed readers will note that both UTF-16 and UTF-32 are dependent on the *endianness* of the computer. *Endianness* refers to the order in which the bytes of some data are stored in memory. Computers store things in bytes. A byte is the lowest unit of memory that is addressable, so *the order* essentially relates to the way what byte is assigned what address. If we follow the big-endian system, the most significant byte (the leftmost byte) is assigned the lowest memory address and the least significant byte (the rightmost byte) is assigned the highest memory address. Little-endian does the exact opposite:

<center>
    <img src="/blog/images/Unicode/endianness.svg" data-zoomable>
</center>

So if we were to represent 💩 in UTF-16 (code units: `0xD83D`, `0xDCA9`) in memory in bytes, it would be different depending on what endianness we're following:

- Big-endian (UTF-16BE): `0xD8` `0x3D` `0xDC` `0xA9`
- Little-endian (UTF-16LE): `0x3D` `0xD8` `0xA9` `0xDC`

UTF-32 has the same problem; it's representation is endianness dependent. To avoid confusion when we're sharing data, these encodings necessitate the use of a thing called *BOM*. The *BOM* or the *Byte Order Mark* (`U+FEFF`) is nothing but a code point prepended to the data with the same encoding format so as to provide a way to tell what the endianness of the encoding is and how to expect data:

> If the endian architecture of the decoder matches that of the encoder, the decoder detects the `U+FEFF` value, but an opposite-endian decoder interprets the BOM as the non-character value `U+FFFE` reserved for this purpose. This incorrect result provides a hint to perform byte-swapping for the remaining values.

The next encoding we're about to dive into doesn't have this problem at all, and we'll see just how!

## UTF-8

This encoding right here takes all kinds of things all kinds of higher levels and gets rid of all unwanted things. As the name suggests, each code unit is 8 bits or 1 byte long. [We previously saw](#utf-32) that we require about 21 bits to represent all code points in the Unicode code space, so 4 code units at max should suffice for UTF-8. This is also a variable length encoding, but the variability is taken to the next level with this.

Unlike UTF-16, there's no subtracting jibber-jabber going on - you take the codepoint, then put the bits as required into some bytes, convert it to it's binary format, put the bits in placeholders of a defined layout which depends on the range in which the code point lies:

| Codepoint Range | Byte 1 | Byte 2 | Byte 3 | Byte 4 |
| :---: | :---: | :---: | :---: | :---: |
| `U+0000` to `U+007F`| `0xxxxxxx`|
|`U+0080` to `U+07FF`| `110xxxxx` | `10xxxxxx` |
|`U+0800` to `U+FFFF`| `1110xxxx` | `10xxxxxx` | `10xxxxxx` |
|`U+10000` to `U+10FFFF`| `11110xxx` | `10xxxxxx` | `10xxxxxx` | `10xxxxxx` |

The cool thing about this is that the first byte in the encoding actually tells you how many bytes are about to follow. The bytes that follow are called *continuation bytes*. Continuation bytes are always of the form  `10xxxxxx`.

In addition to that, UTF-8 doesn't depend on the endianness of the architecture at all because it already specifies the expected order of the code units.

Aaaand what's on top is that this is easily backwards compatible with ASCII so anything ASCII is implicitly UTF-8! How? Well we already saw that the Unicode code space is technically backwards compatible with ASCII. UTF-8 uses 8 bytes just the way ASCII does and just like ASCII the leftmost bit is always 0 for a 1 code unit long encoding. Hence, we'll expect the same encoding if all you have is ASCII!

UTF-8 is clearly memory efficient (at a cost of a tad bit of performance), is endianness independent and ASCII compatible. What else could you even want?

> As it stands, about 95% of the web uses UTF-8 for text encoding!

All of this without any problem seems too unreal to be true, so yeah there's one small catch if you're testifying that a thing is properly encoded in UTF-8: *Overlong Encodings*.

### Overlong encodings

Let's look at `U+0024` or `00100100` (in binary). That in itself just requires one byte and could be written as `00100100` in UTF-8. However, nothing's really stopping me from prepending extra 0s: I could write it like `00000 100100` and then fit it into the 2 byte format giving me `11000000 10100100` as the encoding in UTF-8. This thing right there is called an *overlong* encoding. The standard gets rid of them by well, getting rid of them:

> The standard specifies that the correct encoding of a code point uses only the minimum number of bytes required to hold the significant bits of the code point. Longer encodings are called overlong and are not valid UTF-8 representations of the code point. This rule maintains a one-to-one correspondence between code points and their valid encodings, so that there is a unique valid encoding for each code point. This ensures that string comparisons and searches are well-defined.

## PHEW! Where to next?

This one took me a stupendous amount of time and effort. I wanted to make sure this post was as clear and enjoyable as possible (a well spent 20 min read!). There's still ***A LOT*** of stuff that I didn't cover - different forms, normalization, character categories, other encodings, and whatnot; the list is never-ending, but yeah I hold faith in you to explore those if you really want to!

For now, I'll give my fingers some rest. Until next time!

---

[^1]: [Wiki](https://en.wikipedia.org/wiki/Unicode#Architecture_and_terminology)
[^2]: [UTF-32 and how it's used in practical scenarios](https://en.wikipedia.org/wiki/UTF-32#Use)
