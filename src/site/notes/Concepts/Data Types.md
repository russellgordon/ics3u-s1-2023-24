---
{"dg-publish":true,"permalink":"/concepts/data-types/","dgHomeLink":true,"dgShowToc":true}
---

# Data Types

At the level of hardware and electricity, a computer only understands *high voltage* and *low voltage*.

High voltage, or *on*, corresponds to a 1.

Low voltage, or *off*, corresponds to a 0.

Computers use the [[Concepts/Abstraction and Binary Numbers\|abstraction of binary numbers]] to represent numeric values.

How these 1's and 0's are stored at a physical level varies depending on the storage medium.

For example, in a [compact disc](https://duckduckgo.com/?q=compact+disc&iax=images&ia=images#) pits and lands are [used to register 1's or 0's](https://ecomputernotes.com/fundamental/input-output-and-memory/what-are-pits-and-lands-in-cds).

## Bits

A *bit* is a single piece of information – literally a 1 or a 0.

As we just learned, we can use the abstraction of the base 2 number system to represent numbers in base 10.

Four bits can represent a *minimum* of zero:

Value expressed as a power|$2^3$|$2^2$|$2^1$|$2^0$
-|-|-|-|-
Value expressed in standard form|$8$|$4$|$2$|$1$
&nbsp;|$0$|$0$|$0$|$0$

$$
\begin{aligned}
&= 8\times0 + 4\times0 + 2\times0 + 1\times0 \\
&= 0 + 0 + 0 + 0 \\
&= 0
\end{aligned}
$$

So, $0000_2=0_{10}$

Four bits can represent a *maximum* of fifteen:

Value expressed as a power|$2^3$|$2^2$|$2^1$|$2^0$
-|-|-|-|-
Value expressed in standard form|$8$|$4$|$2$|$1$
&nbsp;|$1$|$1$|$1$|$1$

$$
\begin{aligned}
&= 8\times1 + 4\times1 + 2\times1 + 1\times1 \\
&= 8 + 4 + 2 + 1 \\
&= 15
\end{aligned}
$$

So, $1111_2=15_{10}$

## Variables, Constants, Data Types

In your playground, the default code provided is:

![Screenshot 2023-10-21 at 8.47.37 AM.png](/img/user/Media/Screenshot%202023-10-21%20at%208.47.37%E2%80%AFAM.png)

Run your playground by clicking the button in the lower left corner, or by pressing **Command-Shift-Return** on your keyboard.

![Screenshot 2023-10-21 at 8.44.33 AM.png|200](/img/user/Media/Screenshot%202023-10-21%20at%208.44.33%E2%80%AFAM.png)

After a few seconds – it takes a bit longer the first time you run a playground – you will see results appear in the sidebar:

![Screenshot 2023-10-21 at 8.45.45 AM.png](/img/user/Media/Screenshot%202023-10-21%20at%208.45.45%E2%80%AFAM.png)

This code creates a *variable* named `greeting`.

A variable can hold a *single value at a time*.

The variable named `greeting` holds the value `Hello, playground`.

Now hold down the **Option** key on your keyboard.

Position your cursor over the `greeting` text.

You will see a question mark appear.

Click the trackpad or your mouse button.

Xcode will tell you the *data type* of the `greeting` variable is a *string*:

![Screenshot 2023-10-21 at 8.55.39 AM.png](/img/user/Media/Screenshot%202023-10-21%20at%208.55.39%E2%80%AFAM.png)

A *string* is a programming term for a data type that holds text.

In Swift, strings are always surrounded by quotes – they must begin and end with a `"`.

Add the following code to your playground to express your age – my age will be a little greater than yours:

```swift
let age = 46
```

This creates a *constant* named `age`.

**Option**-click the `age` constant.

Swift reports the data type as an integer, or `Int`:

![Screenshot 2023-10-21 at 8.59.35 AM.png](/img/user/Media/Screenshot%202023-10-21%20at%208.59.35%E2%80%AFAM.png)

In Swift, on modern computers, an `Int` is [stored using *sixty-four* bits](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics/#Int)!

One bit is used to store the *sign* – that is, whether the number is positive or negative. 

That leaves sixty-three bits to represent a range of values from  `-2,147,483,648` and `2,147,483,647`.

To be clear, an `Int` in Swift is stored this using the [[Concepts/Abstraction and Binary Numbers\|very same system of abstraction for binary numbers that we just explored]]. The only difference is that one bit is used to store the sign to mark a value as being positive or negative.

Try celebrating a birthday by adding one to the age constant:

```swift
let age = 46
age += 1
```

Does this work? It does not, because we cannot change a constant value:

![Screenshot 2023-10-21 at 9.09.23 AM.png](/img/user/Media/Screenshot%202023-10-21%20at%209.09.23%E2%80%AFAM.png)

You can comment out the code that tries to change the age like this:

```swift
let age = 46
//age += 1
```

Now the code is still there for us to read, but the computer will ignore it.

Finally, add the following code to your playground to represent an imaginary bank balance:

```swift
var balance = 1_000_000.49
```

Run your code and **Option**-click it to find it's data type:

![Screenshot 2023-10-21 at 9.11.10 AM.png](/img/user/Media/Screenshot%202023-10-21%20at%209.11.10%E2%80%AFAM.png)

The `Double` data type stores numeric values that contain decimals. More on [how this works later in the course](https://wizardzines.com/zines/integers-floats/).

> [!SUMMARY]
> A *variable* is a place to store a single value that is allowed to change in the future.
> 
> A *constant* is a place to store a single value that is not allowed to change in the future in our code.
> 
> The three main data types we will use, at first, are: `Int`, `Double`, and `String`.
