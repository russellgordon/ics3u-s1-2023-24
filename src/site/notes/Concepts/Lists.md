---
{"dg-publish":true,"permalink":"/concepts/lists/","dgHomeLink":true,"dgShowToc":true}
---


# Lists

## Recap

Early on in this course we learned about  *variables* and *constants*, each of which can hold a single value of a [[Concepts/Data Types\|given data type]]:

```swift
var score = 0			// variable, data type is Int
let acceleration = 9.8	// constant, data type is Double 
```

[[Concepts/Thread 1 Recap#Structures\|Structures]] allow us to describe more interesting data by grouping related individual variables and constants:

```swift
struct TradingCard {
    
    let imageName: String
    let playerName: String
    let homeRunCount: String
    let runsBattedIn: String
    let average: String
    let famousPlay: String
    
}
```

We can then create as many *instances* of a structure as needed:

```swift
let kellyGruber = TradingCard(imageName: "KellyGruber",
                              playerName: "Kelly Gruber",
                              homeRunCount: "117",
                              runsBattedIn: "443",
                              average: ".259",
                              famousPlay: "On April 16, 1989, Gruber was the first Blue Jay in history to hit for the cycle when he got four hits in six at–bats with six RBI and four runs scored. His cycle occurred in the following order: home run, double, triple, and single.")

let joeCarter = TradingCard(imageName: "JoeCarter",
                            playerName: "Joe Carter",
                            homeRunCount: "396",
                            runsBattedIn: "1445",
                            average: ".259",
                            famousPlay: "In 1993, in the World Series, with the Blue Jays leading three games to two, Carter came to bat with one out in the bottom of the ninth inning with the Blue Jays trailing 6–5 and Rickey Henderson and Paul Molitor on base. On a 2–2 count, Carter hit a three-run walk-off home run off Phillies pitcher Mitch Williams.")
```

This in turn allowed us to *apply abstraction* in the **Trading Cards** task.

We presented five different trading cards using just one structure that describes the data – `TradingCard`:

![Screenshot 2023-01-21 at 6.26.34 AM.png](/img/user/Media/Screenshot%202023-01-21%20at%206.26.34%20AM.png)

And one structure to describe the user interface – `DetailView`:

![Screenshot 2024-01-25 at 7.27.01 AM.png](/img/user/Media/Screenshot%202024-01-25%20at%207.27.01%E2%80%AFAM.png)

> [!NOTE]
> 
> Some students will have used helper views to shorten or divide up the code within `DetailView`.

The ability to navigate to the five different cards is provided by the `PlayerListView` structure:

![Screenshot 2023-01-21 at 6.33.50 AM.png](/img/user/Media/Screenshot%202023-01-21%20at%206.33.50%20AM.png)

However, you may have been wondering – aren't we supposed to avoid repeating ourselves?

Recall:

> **D.R.Y.**
> Don't Repeat Yourself!

Look at the code in the final screenshot above, of `PlayerListView`.

It sure looks like we are repeating ourselves – five navigation links – otherwise identical, except for what page they lead to.

The solution to this repetition is another way to store values – that is something called an *array* or *list*.

## What is an array?

Variables and constants store a single value inside them.

An array is another programming language *abstraction* that lets us store many values at once.

We can then refer to those values using just one label, or name.

For example, here is an array that stores some of the house names here at Lakefield College School:

```swift
let houseNames = ["Matthews", "Uplands", "Cooper", "Moodie"]
```

If we used individual constants to store those values, we'd have to do something like this:

```swift
let firstHouse = "Matthews"
let secondHouse = "Uplands"
let thirdHouse = "Cooper"
let fourthHouse = "Moodie"
```

As you will soon learn, putting many instances of data into an array is *far* more flexible and helps us to *manage complexity* in our apps.

## Terminology

Let's take a brief detour to address terminology.

The word *array* means the same thing as *list*.

When referring to a programming language abstraction that holds multiple values – most documentation and tutorials you will find online will use the term *array*.

All AP materials from the College Board – including questions on the Computer Science Principles exam – use the term *list*.

These are the same thing.
 
Finally, note that an array or list is not quite the same thing as the `List` structure in the SwiftUI framework.

An array, or list, in programming language terms lets us store many values but access them via one name.

A `List` structure in SwiftUI lets use *present* many values in a user interface, like we did with the `PlayerListView` structure:

![Screenshot 2023-01-21 at 6.33.50 AM.png](/img/user/Media/Screenshot%202023-01-21%20at%206.33.50%20AM.png)

In this course, you will hear and use both words:

- array
- list

That way, you will be able to understand tutorials you find online, and be prepared for the AP CSP exam.

## Essential knowledge

An array, or list, is an ordered sequence of *elements*.

For example:

```swift
let blackPinkBand = ["Jisoo", "Jennie", "Rosé", "Lisa"]
```

The `blackPinkBand` list has four elements.

An *element* is an individual value in a list that will always be assigned a unique *index*.

In the Swift programming language and nearly every other programming language, a list is *zero-based*.

That means the first element of a list has an index of 0.

The second element of a list has an index of 1.

Overall the `blackPinkBand` list is described this way:

|Index|Element|
|-|-|
|0|Jisoo|
|1|Jennie|
|2|Rosé|
|3|Lisa|

We can access individual elements of a list by their index.

For example, in a [[Tutorials/Creating a Command-Line Project\|command-line app]], we could print the third band member's name using this code:

```swift
print(blackPinkBand[2])
```

In a command-line app, the output looks like this:

![Screenshot 2023-01-21 at 7.47.58 AM.png](/img/user/Media/Screenshot%202023-01-21%20at%207.47.58%20AM.png)

> [!TIP]
> In a command-line app, Xcode tells us that the program ended normally, without any errors, by showing the output:
> 
> `Program ended with exit code: 0`
> 
> So, that will always appear when you run a command-line app. It is not an error but a success message. 🎉

If we try to access an element that does not exist:

```swift
print(blackPinkBand[4])
```

...our app will crash. This is known as an **Index out of range** error.

![Screenshot 2023-01-21 at 7.55.57 AM.png](/img/user/Media/Screenshot%202023-01-21%20at%207.55.57%20AM.png)

Remember, the list in this example has just four elements, which can be accessed using index values from 0 through 3:

|Index|Element|
|-|-|
|0|Jisoo|
|1|Jennie|
|2|Rosé|
|3|Lisa|

We "reached beyond the end of the list" when we tried to access a fifth element by using the index of 4:

```swift
print(blackPinkBand[4])
```

### Exercise 1

> [!EXERCISE]
> 
> 1. Create a new [[Creating a Command Line macOS Project\|command-line macOS app]] named `TopTenList` and create a list that has ten elements.
>    
>    For example, you might create a list of ten cities that you would like to visit someday, or your ten favourite ice cream flavours.
>    
>    Then print the first, fifth, and final element of each list, similar to what was shown above.
>    
>    Finally, try printing the eleventh element of your list. 
>    
>    Of course, that does not exist, and your app will crash. It's good to become familiar with common reasons why your app might crash. Going past the end of a list is a very common programming error.

## Iterating over lists

Loops are a natural friend to lists.

We can *iterate* over the values of a list using a loop.

Here is a loop that simply counts from zero to three:

```swift
// Count from 0 to 3
for i in 0...3 {
    print(i)
}
```

The output will be:

```
0
1
2
3
```

We could use a loop like that to iterate over the elements in the `blackPinkBand` list, and print their names on the screen:

![Screenshot 2023-01-21 at 8.08.05 AM.png](/img/user/Media/Screenshot%202023-01-21%20at%208.08.05%20AM.png)

Here is that same code, with the results shown using an animation:

![Stepping Through an Array.gif](/img/user/Media/Stepping%20Through%20an%20Array.gif)

However, this is not the best way to use a loop with a list in Swift.

Manually specifying the range of elements to iterate over, via the indices, like this:

```swift
for i in 0...3 {
```

... is prone to error.

It's very easy to make a mistake and go past the end of the array, by asking for an element using an index that does not exist:

![Screenshot 2023-01-21 at 8.09.53 AM.png](/img/user/Media/Screenshot%202023-01-21%20at%208.09.53%20AM.png)

Here is that same code, with the results shown as an animation:

![Index Out of Range.gif](/img/user/Media/Index%20Out%20of%20Range.gif)

> [!TIP]
> "Index out of range" is one of the *most common* categories of programmer errors.

It is much better to use the following code:

```swift
// Print each band member's name
for bandMember in blackPinkBand {
    print(bandMember)
}
```

With a loop like this, the Swift compiler automatically iterates the correct number of times – four, in this case – since `blackPinkBand` contains four elements.

With each iteration of the loop, the value of `bandMember` is changed to temporarily hold the current element of the list.

Even better: if we are deliberate in how we name a list, the Xcode editor's autocomplete is very helpful – this feature exists because iterating over a list is a *very common task* when developing an app:

![Iterating Over a List.gif](/img/user/Media/Iterating%20Over%20a%20List.gif)

### Exercise 2

> [!EXERCISE]
> 
> 2. Extend your `TopTenList` command-line app.
>    
>    Referring to the examples in the section above, iterate over the values of your list and print them to the screen using two different approaches in code.

## Iterating over lists with SwiftUI

As you know, SwiftUI has a `List` structure.

We used it in our Trading Cards app:

![Screenshot 2023-01-21 at 6.33.50 AM.png](/img/user/Media/Screenshot%202023-01-21%20at%206.33.50%20AM.png)

However, it's *name* – `List` – is not an accident.

The `List` structure is not an array, but it works *with* arrays.

As it turns out: we can take individual instances of a structure, and put them into an array.

This has been done below, on line 66:

![Screenshot 2023-01-21 at 8.44.03 AM.png](/img/user/Media/Screenshot%202023-01-21%20at%208.44.03%20AM.png)

By placing instances of a structure into an array (also known as a list, lowercase "l"), a very nice edit can be made to the `PlayerListView` page:

![Screenshot 2023-01-21 at 8.47.39 AM.png](/img/user/Media/Screenshot%202023-01-21%20at%208.47.39%20AM.png)

Now, the `List` structure on line 13 is accepting the array (or list) named `allPlayers`.

The `List` structure in SwiftUI iterates over the `allPlayers` array, which contains:

|Index|Element|
|-|-|
|0|kellyGruber|
|1|joeCarter|
|2|patBorders|
|3|tonyFernandez|
|4|georgeBell|

With each iteration the next player in the array is temporarily inserted into `currentPlayer` and then used to create a `NavigationLink`.

In turn, that instance of `currentPlayer` (which changes as the loop iterates) is passed along to the `DetailView` to allow each card to be shown.

This is very much like what happened earlier in the example from the command line app:

![Screenshot 2023-01-21 at 8.56.13 AM.png](/img/user/Media/Screenshot%202023-01-21%20at%208.56.13%20AM.png)

Here, the loop on line 14 iterates over the array, and each band member's name is printed to the screen on line 15.

There is *one* final change that must be made, however.

To use an instance of a structure with `List` in SwiftUI, that instance must be uniquely identifiable.

When a structure is used with a `List`, but each instance cannot be uniquely identified, this error will appear:

![Screenshot 2023-01-21 at 8.59.47 AM.png](/img/user/Media/Screenshot%202023-01-21%20at%208.59.47%20AM.png)

To fix this, we declare that our `TradingCard` structure will conform to the `Identifiable` protocol by making the change shown on line 10 – note that the *old* code is shown in dark grey, and the *new* code is shown in dark blue:

![Screenshot 2023-01-21 at 9.14.38 AM.png](/img/user/Media/Screenshot%202023-01-21%20at%209.14.38%20AM.png)

Finally, on line 12, we actually make instances of the `TradingCard` structure uniquely identifiable by adding a stored property named `id` and assigning it a default value of `UUID()`, using the  assignment operator, `=`.

`UUID` is short for "universally unique identifier".

With those minor changes to `TradingCard`, the `List` structure back on the list view is now happy and shows each player in the `allPlayers` array:

![Screenshot 2023-01-21 at 9.17.05 AM.png](/img/user/Media/Screenshot%202023-01-21%20at%209.17.05%20AM.png)

### Exercise 3

> [!EXERCISE]
> 
> 3. Return to your own **Trading Cards** app.
>    
>    Make your structure conform to the `Identifiable` protocol as explained above.
>    
>    Add the instances of your structure to an array, like was shown with `allPlayers` above.
>    
>    Finally, in your app's list view, change the code so that the `List` structure uses your new array.
>    
>    In this way, you can change the list view from having this many lines of code:
>    
>    ![Screenshot 2023-01-21 at 9.28.02 AM.png](/img/user/Media/Screenshot%202023-01-21%20at%209.28.02%20AM.png)
>    
>    ... to this many:
>    
>    ![Screenshot 2023-01-21 at 9.22.55 AM.png](/img/user/Media/Screenshot%202023-01-21%20at%209.22.55%20AM.png)
>    
>    By doing this, you will have *managed complexity* in your app by using an array with a `List` structure to elminate some very repetitive code.
   
   
