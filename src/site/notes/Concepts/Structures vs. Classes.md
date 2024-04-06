---
{"dg-publish":true,"permalink":"/concepts/structures-vs-classes/","dgHomeLink":true,"dgShowToc":true}
---

# Structures vs. Classes

This lesson is really about *value types* and how they differ from *reference types*.

To explore this concept, please create a [[Tutorials/Creating an Xcode Playground\|new Xcode playground]] named `StructuresAndClasses`.
## Value types

What is a value type?

Let's imagine that we all live on a Cartesian plane and our locations can be described by an ordered pair $(x, y)$.

Now, have you ever seen this sweater around the Lakefield campus?

![Screenshot 2024-01-17 at 10.36.04 AM.png|500](/img/user/Media/Screenshot%202024-01-17%20at%2010.36.04%E2%80%AFAM.png)

Thinking of that, please type the following into your new playground:

![Screenshot 2024-01-17 at 10.40.40 AM.png|325](/img/user/Media/Screenshot%202024-01-17%20at%2010.40.40%E2%80%AFAM.png)

Run the playground using the **Command-Shift-Return** keyboard shortcut and review the results at right in the sidebar:

![Screenshot 2024-01-17 at 10.41.41 AM.png|650](/img/user/Media/Screenshot%202024-01-17%20at%2010.41.41%E2%80%AFAM.png)

Are the values what you thought they would be?

Now add the following additional lines of code:

![Screenshot 2024-01-17 at 9.50.55 AM.png|325](/img/user/Media/Screenshot%202024-01-17%20at%209.50.55%E2%80%AFAM.png)

Then re-run the entire playground and inspect the results in the sidebar at right again:

![Screenshot 2024-01-17 at 10.43.52 AM.png|650](/img/user/Media/Screenshot%202024-01-17%20at%2010.43.52%E2%80%AFAM.png)

Are the values what you thought they would be?

Examine the code (probably on line 10 in your playground) carefully:

```swift
var home = school
```

Based on the results you have seen when running the playground – what can you conclude about what happened when the `home` variable was created?
## Reference types

Now, on line 3, change the `struct` keyword so that it says `class` instead:

![Pasted image 20240117105009.png|650](/img/user/Media/Pasted%20image%2020240117105009.png)

We are now definining a *class* named `Location` rather than a *structure*. 

They are similar in most ways, but a class is a *reference type*, whereas a structure is a *value type*.

What does that mean? Let's find out.

First, shortly after you made the change on line 3, Xcode presented an error message:

![Pasted image 20240117100029.png|650](/img/user/Media/Pasted%20image%2020240117100029.png)

It is a requirement of the Swift compiler that a class be defined with a special function known as an *initializer*.

An initializer is used when an instance of a class is created, or initialized. The purpose of an initializer is to set the value of each stored property in the class.

Fortunately, we do not need to write the initializer for a class manually – Xcode will do it for us. Make edits to your code as follows:

![Adding an Initializer.gif|650](/img/user/Media/Adding%20an%20Initializer.gif)

### How initializers work

When an instance of a class is created, the arguments for a given parameter are passed to the initializer:

![Screenshot 2024-01-17 at 10.51.57 AM.png|650](/img/user/Media/Screenshot%202024-01-17%20at%2010.51.57%E2%80%AFAM.png)

The keyword `self` refers to the instance of the class being initialized.

`self.x` refers to the stored property named `x`.

`self.y` refers to the stored property named `y`.

In this initializer, the values passed to the initializer are simply assigned to each stored property.

Depending on your goals as a programmer, you may sometimes add logic to an initializer to check that provided values meet certain requirements. That is not happening here.

> [!TIP]
> 
> Structures actually have initializers as well. However, the Swift compiler automatically generates an initializer for a structure. As a result we rarely have to think about initializers when using structures.
> 
> That might lead you to ask – why does Swift not just automatically generate an initializer for a class as well? The answer goes beyond the scope of this lesson – but essentially it's because classes can be used to build upon other classes – a concept known as *inheritance*. If you're curious about this, you can [read a bit more about it here, in a short example](https://www.hackingwithswift.com/quick-start/beginners/how-to-add-initializers-for-classes), but this is not required.

### Examining the results

With the conversation about initializers out of the way, please run the playground with `Location` defined as a class:

![Screenshot 2024-01-17 at 11.05.34 AM.png|650](/img/user/Media/Screenshot%202024-01-17%20at%2011.05.34%E2%80%AFAM.png)

Again, how are those results different as compared to when `Location` is defined as a structure?

Try changing `Location` from a structure to a class and back again, and really take a close look at the results:

![Struct to Class and Back Again.gif|650](/img/user/Media/Struct%20to%20Class%20and%20Back%20Again.gif)

## Summary

How closely have you been paying attention? 😅

Add the following to your notes, completing each sentence.

1. A structure is a &#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f; type.
   <br/>
2. A class is a &#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f; type.
   <br/>
3. In the code example above, when `Location` is defined as a structure, `home` is a &#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f; of `school` and occupies a &#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f; region of memory in the computer.<br/>
   So, when `home` changes, `school`  &#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f; &#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;.
   <br/>
4. In the code example above, when `Location` is defined as a class, `home` is simply a &#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f; to `school` and occupies the &#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f; region of memory in the computer.<br/>
    So, when `home` changes, `school`  &#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;&#x5f;.
   <br/>




