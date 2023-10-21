---
{"dg-publish":true,"permalink":"/concepts/abstraction-and-binary-numbers/","dgHomeLink":true,"dgShowToc":true}
---

# Abstraction and Binary Numbers

Quick, what number is this?

$$101$$

If you thought:

> That is clearly one-hundred-and-one...

... then that would be entirely reasonable!

However, those three symbols:

$$101$$

... can also represent the number *five*.

Why is this?

The answer lays in what *number system* is assumed.

## Number systems

A number system is an example of an abstraction.

Most people would look at $101$ and see one-hundred-and-one.

That is because, way back in elementary school, they learned the concept of place value, and the *base 10* number system was used.
### Base 10

Each digit in $101$ has a value, according to it's position or *place*.

In base 10, those values are:

Value expressed as a power|$10^2$|$10^1$|$10^0$
-|-|-|-
Value expressed in standard form|$100$|$10$|$1$

The value of each place is a *power* with a *base* of 10.

The *exponent* of the power increases as you move from right to left.

So when we are reading $101$ we are filling in the digits in the chart like so:

Value expressed as a power|$10^2$|$10^1$|$10^0$
-|-|-|-
Value expressed in standard form|$100$|$10$|$1$
&nbsp;|$1$|$0$|$1$

... and in expanded form, we know that:

$$
\begin{aligned}
&= 100\times1 + 10\times0 + 1\times1 \\
&= 100 + 0 + 1 \\
&= 101
\end{aligned}
$$

You've probably not thought of $101$ in quite that detailed a manner in a long time. 

Going forward in this course, when we are writing numeric values, we must be careful to annotate the number system.

We do this by appending a subscript. When we write $101$ and mean *one-hundred-and-one* – that is, we are using base 10 – we should write it like this instead:

$$101_{10}$$

### Base 2

In base 2, $101$ has a value of *five*.

To indicate that we are expressing a value in base 2, we write it like this: 

$$101_{2}$$

So how does $101_{2}$ have a value of five?

It's all about the *base* of the power assigned to each place:

Value expressed as a power|$2^2$|$2^1$|$2^0$
-|-|-|-
Value expressed in standard form|$4$|$2$|$1$
&nbsp;|$1$|$0$|$1$

In expanded form:

$$
\begin{aligned}
&= 4\times1 + 2\times0 + 1\times1 \\
&= 4 + 0 + 1 \\
&= 5
\end{aligned}
$$

So, this is how we know that $101$ in base 2 has a value of five in base 10.

Expressed using symbols, that is: $101_2=5_{10}$

#### Another example

It is true that:

$$1001_2=9_{10}$$

How?

Value expressed as a power|$2^3$|$2^2$|$2^1$|$2^0$
-|-|-|-|-
Value expressed in standard form|$8$|$4$|$2$|$1$
&nbsp;|$1$|$0$|$0$|$1$

In expanded form:

$$
\begin{aligned}
&= 8\times1 + 4\times0 + 2\times0 + 1\times1 \\
&= 8 + 0 + 0 + 1 \\
&= 9
\end{aligned}
$$

### Exercises

Try doing the following conversions in your graph paper notebook:

1. $1011_2=\phantom{answer}_{10}$
2. $0011_2=\phantom{answer}_{10}$
3. $1111_2=\phantom{answer}_{10}$
4. $14_{10}=\phantom{answer}_{2}$
5. $13_{10}=\phantom{answer}_{2}$
6. $12_{10}=\phantom{answer}_{2}$




