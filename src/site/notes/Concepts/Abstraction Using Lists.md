---
{"dg-publish":true,"permalink":"/concepts/abstraction-using-lists/","dgHomeLink":true,"dgShowToc":true}
---

# Abstraction Using Lists and Structures

## Introduction

Many of us have been fortunate enough to travel at least a little bit, whether that be locally within Ontario or in more far-flung locations around the world.

Say that you wish to author an app named *Landmarks* to keep track of the notable locations you have personally travelled to and want to remember:

![Screenshot 2024-01-26 at 9.09.10 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.09.10%E2%80%AFPM.png)

Landmarks might be places you want to visit again, or places you want to avoid because they were not enjoyable for some reason.

This lesson will walk you through the process of authoring this app from start to finish, recapping how we can use a list (also known as an array) and the concept of *separation of concerns* to keep the views – the user interface code – distinct from the model – the data kept within our app.

In this way, we avoid repeating ourselves. Remember:

> **D.R.Y.**
> Don't Repeat Yourself!

Additionally, to spruce the app up a bit, you will learn how to use a `LazyVGrid` to create a more interesting scrollable gallery of landmarks.

## Create the project

Let's get started by [[Tutorials/Creating a New iOS Project\|creating a new iOS project]] named *Landmarks*.

As soon as you have created the project, remember to create a remote:

![Screenshot 2024-01-26 at 9.03.32 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.03.32%E2%80%AFPM.png)

![Screenshot 2024-01-26 at 9.04.10 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.04.10%E2%80%AFPM.png)

## Build the detail view

When you navigate down a level in an app to read more about something, app developers commonly refer to the interface you arrive at as a *detail view*:

![Pasted image 20240126211025.png|300](/img/user/Media/Pasted%20image%2020240126211025.png)

Let's build this view out now.

### Organize

We'll begin by organizing the project. 

First delete `ContentView`. This is a generic name and using this within our projects should be avoided going forward:

![Screenshot 2024-01-26 at 9.12.44 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.12.44%E2%80%AFPM.png)

Next create a group named `Views`:

![Screenshot 2024-01-26 at 9.13.27 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.13.27%E2%80%AFPM.png)

... like this:

![Screenshot 2024-01-26 at 9.14.16 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.14.16%E2%80%AFPM.png)

Then create a new **SwiftUI View** file named `DetailView` inside the `Views` group:

![Screenshot 2024-01-26 at 9.15.43 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.15.43%E2%80%AFPM.png)

Finally, in the app entry point file:

![Screenshot 2024-01-26 at 9.16.29 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.16.29%E2%80%AFPM.png)

... have an instance of `DetailView` be created instead:

![Screenshot 2024-01-26 at 9.17.06 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.17.06%E2%80%AFPM.png)

This resolves the error we created when deleting `ContentView`.

Commit and push your work at this point with the message:

```
Created detail view and organized project by creating Views group.
```

### Build

The interface we want to create can be achieved using a `ScrollView`, which acts like a `VStack` but provides infinite vertical space for things like a large amount of text:

![Pasted image 20240126212325.png|300](/img/user/Media/Pasted%20image%2020240126212325.png)

When you first build an interface, a good place to start is simply with a static layout – where you *hard-code* values inside *string literals*:

![Screenshot 2024-01-26 at 9.28.23 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.28.23%E2%80%AFPM.png)

> [!NOTE]
> Everything you see that is highlighted in red in the screenshot above is a string literal.

The focus of this lesson is not to practice building interfaces from scratch – you've had plenty of practice with that – so please feel free to copy and paste this code into your `DetailView` file:

```swift
import SwiftUI

struct DetailView: View {
    
    var body: some View {
        ScrollView {
            Image("SudburyNickel")
                .resizable()
                .scaledToFit()
            
            HStack {
                Image(systemName: "hand.thumbsdown")
                    .resizable()
                    .scaledToFit()
                    .frame(height: 20)
                    .padding(5)
                
                Spacer()
            }
            .padding(.horizontal)
            
            Text("""
                Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. A pellentesque sit amet porttitor eget. Tempor commodo ullamcorper a lacus vestibulum sed arcu non. Eget duis at tellus at urna condimentum. Sapien et ligula ullamcorper malesuada proin libero nunc consequat. Urna nunc id cursus metus aliquam. Eget felis eget nunc lobortis mattis aliquam. Pharetra convallis posuere morbi leo urna molestie. Lacus laoreet non curabitur gravida arcu ac tortor dignissim convallis. Sit amet mattis vulputate enim.

                Sit amet facilisis magna etiam tempor orci. Quis eleifend quam adipiscing vitae proin sagittis. Mollis nunc sed id semper risus in. Pellentesque dignissim enim sit amet venenatis. Laoreet suspendisse interdum consectetur libero id faucibus nisl tincidunt eget. Eu volutpat odio facilisis mauris. Purus gravida quis blandit turpis cursus in hac habitasse platea. Nibh tortor id aliquet lectus proin nibh nisl condimentum. Fringilla ut morbi tincidunt augue interdum velit euismod. Sed ullamcorper morbi tincidunt ornare massa eget egestas.
                """)
            .padding(.horizontal)
        }
        .navigationTitle("Sudbury Nickel")
    }
}

#Preview {
    NavigationStack {
        DetailView()
    }
}
```

To see the same results, you will need to download this image to your computer:

![SudburyNickel.png|700](/img/user/Media/SudburyNickel.png)

... and then add the image to your **Assets** catalog in Xcode:

![Screenshot 2024-01-26 at 9.31.19 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.31.19%E2%80%AFPM.png)

A couple of observations:

1. `DetailView` within the preview is created within a `NavigationStack`.
2. We do this so that we can see the navigation title within the preview.

![Screenshot 2024-01-26 at 9.28.23 PM copy 1.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.28.23%E2%80%AFPM%20copy%201.png)

Commit and push your work at this point with the message:

```
Finished detail view by providing static values using string literals.
```

## Build the model

Of course, we want to show many landmarks, not just one.

It would be extremely inefficient to make a copy of `DetailView` for each landmark we want to keep track of in our app.

So, we must build a model to keep track of the data within our app.

This will allow us to apply abstraction to `DetailView` so that it can display any landmark, not just the information we have currently hard-coded into it.

What we must do is imagine a second location that we want to keep track of:

![Screenshot 2024-01-26 at 9.41.48 PM.png|600](/img/user/Media/Screenshot%202024-01-26%20at%209.41.48%E2%80%AFPM.png)

Now, between these two screenshots, we can identify four pieces of information that will change from one landmark to the next:

- the landmark name
- the image
- whether we like the landmark or not
- the description

> [!NOTE]
> 
> In the screenshot above, we are using placeholder text for each landmark. In a real app, we would have something different to say about each landmark we are keeping track of.

So, our next step is to create another group within our project named `Model` (singular):

![Screenshot 2024-01-26 at 9.44.16 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.44.16%E2%80%AFPM.png)

... like this:

![Screenshot 2024-01-26 at 9.44.56 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.44.56%E2%80%AFPM.png)

Inside the `Model` group, please create a new **Swift** file named `Landmark`:

![Screenshot 2024-01-26 at 9.45.40 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.45.40%E2%80%AFPM.png)

And once again, the purpose of this tutorial at the moment is not to have you spend time typing – so please feel free to [copy this code](https://gist.githubusercontent.com/lcs-rgordon/9f3906ff846c3241d3c79a6733ea9006/raw/e64f82707af9c192b4230a8d11f19d57681bc200/Landmark.swift) into your new `Landmark` file, so your file looks like this:

![Screenshot 2024-01-26 at 9.47.58 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.47.58%E2%80%AFPM.png)

After code-folding the parts of the file where instances of the structure are created, your file would look like this:

![Screenshot 2024-01-26 at 9.49.54 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.49.54%E2%80%AFPM.png)

Let's examine what we see here.

1. We define a structure named `Landmark`. It contains four stored properties that we need to provide values for when creating instances of `Landmark`. It contains one property, `id`, which is automatically populated with a universally unique identifier. We make `Landmark` conform to the `Identifiable` protocol so that [[Concepts/Lists#Iterating over lists with SwiftUI\|we can use instances of this structure in a scrollable list]].
2. We create several instances – six, in this case – of the structure. This holds the data we will display within our app. We can create as many instances as we wish.
3. We add all the instances of the `Landmark` structure into an array named `allLandmarks`. This will let us build a scrollable list, and later, a scrollable gallery, without having repetitive code.

Commit and push your work now with this message:

```
Added a model to the app to describe landmarks.
```

## Apply abstraction to the detail view

Now we should return to our detail view:

![Screenshot 2024-01-26 at 9.59.38 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%209.59.38%E2%80%AFPM.png)

We want to make this work with any of the data we have just added to our model.

So, make the following initial edits:

![Screenshot 2024-01-26 at 10.00.35 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.00.35%E2%80%AFPM.png)

By making these edits, we tell Swift that in order to create an instance of `DetailView` and show the user interface, an instance of the `Landmark` structure we just defined must be provided.

Of course, this creates an error, because our preview is currently trying to create `DetailView` without providing an instance of `Landmark`:

![Screenshot 2024-01-26 at 10.02.04 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.02.04%E2%80%AFPM.png)

Correct this by making the following edit:

![Screenshot 2024-01-26 at 10.02.43 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.02.43%E2%80%AFPM.png)

We will also need to update the app entry point file:

![Screenshot 2024-01-26 at 10.05.07 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.05.07%E2%80%AFPM.png)

... by making this edit:

![Screenshot 2024-01-26 at 10.05.39 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.05.39%E2%80%AFPM.png)

For the next part of this lesson to work for you, please download this image to your computer:

![ROM.png|700](/img/user/Media/ROM.png)

Then add it to the **Assets** catalog in Xcode:

![Screenshot 2024-01-26 at 10.04.45 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.04.45%E2%80%AFPM.png)

Now return to `DetailView`:

![Screenshot 2024-01-26 at 10.06.09 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.06.09%E2%80%AFPM.png)

At the moment, `DetailView` still uses hard-coded values in the form of string literals.

> [!IMPORTANT]
> 
> We literally apply abstraction at this point by replacing the hard-coded values with references to the stored properties of the instance of `Landmark` that is being provided to `DetailView`. 

Here is the first edit – note that *old code is in dark grey* and *new code is in dark blue* below:

![Screenshot 2024-01-26 at 10.08.10 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.08.10%E2%80%AFPM.png)

We have changed a hard-coded string literal reference:

```swift
Image("SudburyNickel")
```

... to a reference that is dynamic, using whatever is in the `image` property of `item` instead:

```swift
Image(item.image)
```

Note how the image in the preview has changed to show the Royal Ontario Museum:

![Screenshot 2024-01-26 at 10.08.10 PM 1.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.08.10%E2%80%AFPM%201.png)

Next make the edit to change the navigation title:

![Screenshot 2024-01-26 at 10.13.48 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.13.48%E2%80%AFPM.png)

Then make the edit to change the landmark description from a string literal:

![Screenshot 2024-01-26 at 10.14.33 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.14.33%E2%80%AFPM.png)

... to use the `description` property of `item` instead:

![Screenshot 2024-01-26 at 10.15.04 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.15.04%E2%80%AFPM.png)

Finally, we need to make use of the `isRecommended` property.

Here is where we need to be a little fancy – and make a decision about what SF Symbol to show.

When the landmark is something we liked, we want to show a "thumbs up" image.

When the landmark is something we did not like, we want to show a "thumbs down" image.

We can do this here using something called a *ternary conditional operator*. 

Quoting an explanation originally given in the [Develop in Swift tutorials](https://developer.apple.com/tutorials/develop-in-swift-tutorials), a ternary conditional operator comes in three parts:

1. First is a Boolean (true or false) expression, followed by a question mark.
1. Next is a value to use when the expression is true, followed by a colon.
1. Finally, there's the value to use when the expression is false.

The ternary operator is a compact way to change what shows in a view based on an either/or condition.

So, please make this edit, changing:

```swift
Image(systemName: "hand.thumbsdown")
```

To:

```swift
Image(systemName: item.isRecommended == true ? "hand.thumbsup.fill" : "hand.thumbsdown")
```

... like this, shown on line 23:

![Screenshot 2024-01-26 at 10.24.07 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.24.07%E2%80%AFPM.png)

We are evaluating the expression  `item.isRecommended == true` .

When the item has been recommended, we show the `hand.thumbsup.fill` symbol.

Otherwise, we show the `hand.thumbsdown` symbol.

We can test this out by scrolling down to the previews section of this view:

![Screenshot 2024-01-26 at 10.25.45 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.25.45%E2%80%AFPM.png)

Currently, we have just one preview showing, beginning on line 40:

![Screenshot 2024-01-26 at 10.26.10 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.26.10%E2%80%AFPM.png)

However, there is no reason we cannot show a second preview, so add this code below the existing preview:

```swift
#Preview {
    NavigationStack {
        DetailView(item: sudburyNickel)
    }
}
```

... like this:

![Screenshot 2024-01-26 at 10.27.08 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.27.08%E2%80%AFPM.png)

Notice how there are now two preview buttons:

![Screenshot 2024-01-26 at 10.27.08 PM copy 1.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.27.08%E2%80%AFPM%20copy%201.png)

You can click between those two previews, and you will see abstraction in action – the contents of the detail view shown will differ – because in each case we are passing a different instance of the `Landmark` structure to be shown in `DetailView`.

This is big progress, so commit and push your work now with this message:

```
Applied abstraction to make detail view show properties of an instance of the Landmark structure.
```

## Create the list view

### Static list view

Now we need a list so that we can navigate down to each of the landmarks we want to see.

In the `Views` group create a new **SwiftUI View** named `ListView`:

![Screenshot 2024-01-26 at 10.33.37 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.33.37%E2%80%AFPM.png)

... like this:

![Screenshot 2024-01-26 at 10.34.24 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.34.24%E2%80%AFPM.png)

For this next part of the tutorial to work, you will need to download the following four images to your computer, and then add them all to your **Assets** catalog:

![NiagaraFalls.png|700](/img/user/Media/NiagaraFalls.png)

![Wonderland.png|700](/img/user/Media/Wonderland.png)

![StoneyLake.png|700](/img/user/Media/StoneyLake.png)

![CNTower.png|700](/img/user/Media/CNTower.png)

... like this:

![Screenshot 2024-01-26 at 10.38.36 PM.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.38.36%E2%80%AFPM.png)

Now again, the purpose of this lesson is not to practice typing.

So, fee free to [copy this code](https://gist.githubusercontent.com/lcs-rgordon/96f7be6184af3820035d95f5a83885f8/raw/b2aa7d7eb964f532bdae10b4b0e4ca8ccf9c5ac0/ListView.swift) into your `ListView` file, like this:

![Screenshot 2024-01-26 at 10.41.56 PM 1.png|700](/img/user/Media/Screenshot%202024-01-26%20at%2010.41.56%E2%80%AFPM%201.png)

You can now navigate down to the detail view for each landmark. Try this out.

Commit and push with this message:

```
Created the list view, but our code is currently repetitive.
```

### Apply abstraction

Of course, we know now that we can do better by applying abstraction to the list view.

Recall that we defined an array that contains all the landmarks we care about keeping track of:

![Screenshot 2024-01-27 at 7.31.32 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%207.31.32%E2%80%AFAM.png)

Highlight the `List` structure and everything it contains, and replace it with this code:

```swift
List(allLandmarks) { currentLandmark in
	
	NavigationLink {
		DetailView(item: currentLandmark)
	} label: {
		Text(currentLandmark.name)
	}
	
}
.navigationTitle("Landmarks")
```

... like this:

![Screenshot 2024-01-27 at 7.37.41 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%207.37.41%E2%80%AFAM.png)

The visual result is identical.

However, the code is much shorter.

The contents of the `allLandmarks` array:

|Index|Element|
|-|-|
|0|Sudbury data|
|1|Niagara Falls data|
|2|CN Tower data|
|3|ROM data|
|4|Canada's Wonderland data|
|5|Kawarthas data|

... is now iterated over by the `List`.

One by one, an instance of the `Landmark` model is placed in `currentLandmark`.

The `List` iterates six times because there are six elements in the `allLandmarks` array.

Importantly, if we now add more instances of `Landmark` to the `allLandmarks` array, we will automatically see more items in our scrollable list here.

Let's do that now to illustrate the point. 

Download the following image to your computer and then add it to the **Assets** in Xcode:

![BlueMountain.png|700](/img/user/Media/BlueMountain.png)

... like this:

![Screenshot 2024-01-27 at 7.55.16 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%207.55.16%E2%80%AFAM.png)

Then, open the `Landmark` file in the `Model` group add the following code to create a seventh instance of the `Landmark` structure:

```swift
let blueMountain = Landmark(
    name: "Blue Mountain",
    image: "BlueMountain",
    isRecommended: true,
    description: """
                Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. A pellentesque sit amet porttitor eget. Tempor commodo ullamcorper a lacus vestibulum sed arcu non. Eget duis at tellus at urna condimentum. Sapien et ligula ullamcorper malesuada proin libero nunc consequat. Urna nunc id cursus metus aliquam. Eget felis eget nunc lobortis mattis aliquam. Pharetra convallis posuere morbi leo urna molestie. Lacus laoreet non curabitur gravida arcu ac tortor dignissim convallis. Sit amet mattis vulputate enim.

                Sit amet facilisis magna etiam tempor orci. Quis eleifend quam adipiscing vitae proin sagittis. Mollis nunc sed id semper risus in. Pellentesque dignissim enim sit amet venenatis. Laoreet suspendisse interdum consectetur libero id faucibus nisl tincidunt eget. Eu volutpat odio facilisis mauris. Purus gravida quis blandit turpis cursus in hac habitasse platea. Nibh tortor id aliquet lectus proin nibh nisl condimentum. Fringilla ut morbi tincidunt augue interdum velit euismod. Sed ullamcorper morbi tincidunt ornare massa eget egestas.
                """
)
```

... like this:

![Screenshot 2024-01-27 at 7.56.55 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%207.56.55%E2%80%AFAM.png)

Finally, be sure to add the `blueMountain` instance to the `allLandmarks` array:

![Screenshot 2024-01-27 at 7.57.45 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%207.57.45%E2%80%AFAM.png)

Now return to the preview of `ListView`, and you will see the new item in our scrollable list:

![Screenshot 2024-01-27 at 7.58.24 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%207.58.24%E2%80%AFAM.png)

We can, of course, navigate down to the detail view for the new entry:

![Screenshot 2024-01-27 at 7.58.49 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%207.58.49%E2%80%AFAM.png)

This is amazing progress, so please commit and push your work now with this message:

```
Applied abstraction to the scrollable List structure so it reads the array containing all the landmarks.
```

## Improve the list item view

At this point in the lesson you have completed the primary objective – you have practiced applying abstraction twice.

You have transformed a static detail view that used string literals so that it accepts and uses an instance of the `Landmark` structure instead.

You have modified a scrollable `List` so that instead of using six copy-pasted `NavigationLinks`, the `List` reads an array containing landmarks.

Now, we can continue making use of abstraction to create a more attractive version of this app.

### Update app entry point

Now that our list is working the way we want it to, we should probably update the app entry point so that it shows the list, rather than the detail view.

Make this edit to the `LandmarksApp` file – the old code is above, and the new code is below:

![Screenshot 2024-01-27 at 8.06.31 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.06.31%E2%80%AFAM.png)

Now if we run the app in the Simulator, or on a real device, the list will be shown:

![Screenshot 2024-01-27 at 8.07.35 AM.png|300](/img/user/Media/Screenshot%202024-01-27%20at%208.07.35%E2%80%AFAM.png)

Commit and push your work with this message:

```
Made the app entry point open the list view.
```

### Add the list item view

We can do better than the plain scrollable list that we have now.

Add a new **SwiftUI View** named `ListItemView` to the `Views` group:

![Screenshot 2024-01-27 at 8.15.21 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.15.21%E2%80%AFAM.png)

... like this:

![Screenshot 2024-01-27 at 8.16.21 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.16.21%E2%80%AFAM.png)

You can [copy this code](https://gist.githubusercontent.com/lcs-rgordon/a7301e4f1a2d3d9eb715f73b318bdc67/raw/8973beee2d74b6450e1275f6849f7ec4cda01613/ListItemView.swift) into `ListItemView`, so the file looks like this:

![Screenshot 2024-01-27 at 8.17.22 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.17.22%E2%80%AFAM.png)

Now we have a nicer way to see the name, image, and recommendation status of a landmark.

> [!IMPORTANT]
> Note how `ListItemView` accepts an instance of `Landmark` on line 11.
> 
> We then make use of that instance's properties on lines 16, 25, and 31. 
> 
> This is abstraction in action!

### Use the list item view

Let's make use of this new structure by making one edit to `ListView`.

Replace the code here:

```swift
Text(currentLandmark.name)
```

... with this instead:

```swift
ListItemView(item: currentLandmark)
```

... like this:

![Screenshot 2024-01-27 at 8.18.48 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.18.48%E2%80%AFAM.png)

This is a big improvement, so please commit and push your work with this message:

```
Made the scrollable list look nicer and display more information by using a helper view.
```

## Improving the landing view

Generally speaking, the view that is presented when an app first opens can be referred to as the *landing view*.

Our new scrollable list that serves as our landing view is *nice*, but it could be *better*.

If you cast a critical eye at the interface:

![Screenshot 2024-01-27 at 8.18.48 AM 1.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.18.48%E2%80%AFAM%201.png)

... notice how much empty space there is in each list item view.

On a device like a phone, with a small screen, this is a lost opportunity to display more information.

Let's make a better landing view for our app now, in the form of a scrollable gallery.

This gallery will take the form of a grid that can be scrolled and navigated from.

### Add another helper view

Add a new **SwiftUI View** file to the `Views` group named `GalleryItemView`:

![Screenshot 2024-01-27 at 8.29.51 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.29.51%E2%80%AFAM.png)

Then [copy this code](https://gist.githubusercontent.com/lcs-rgordon/625099f1e7a7236f865ad311c91d1ee7/raw/bccd1c30189527eb7e7258f34d5e30340e35af14/GalleryItemView.swift) into the new file, so it looks like this:

![Screenshot 2024-01-27 at 8.37.57 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.37.57%E2%80%AFAM.png)

The layout of this new helper view is not especially interesting – just several items arranged in `VStack`.

The code for the preview is worth a bit of discussion:

![Screenshot 2024-01-27 at 8.39.09 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.39.09%E2%80%AFAM.png)

Examining that code:

1. We create two instances of `GalleryItemView` inside an `HStack` so we can get a better sense of how this helper view will look inside of a grid (which is what we are going to create next).
2. We use a `.frame` modifier to limit the vertical height of each `GalleryItemView`, again, to better simulate the space they will have inside a grid.

Try commenting out the `.frame` modifiers. You will see the preview then looks a bit strange, with a large gap:

![Screenshot 2024-01-27 at 8.41.40 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.41.40%E2%80%AFAM.png)

That is because of the `Spacer` view on line 30. That `Spacer` exists to  align the thumbs up/down images.

Try commenting out the `Spacer` as well:

![Screenshot 2024-01-27 at 8.42.56 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.42.56%E2%80%AFAM.png)

Notice how the items are misaligned.

Remove the comments from the `.frame` modifiers and the `Spacer` again:

![Screenshot 2024-01-27 at 8.43.48 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.43.48%E2%80%AFAM.png)

This is good progress, so please commit and push your work with this message:

```
Added a gallery item view to use later inside a scrolling grid.
```

### Create a scrolling grid

Now, let's create the scrolling grid, or gallery, of landmarks.

Please add a new **SwiftUI View** file named `GalleryView` to the `Views` group, like this:

![Screenshot 2024-01-27 at 8.45.53 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.45.53%E2%80%AFAM.png)

Now [copy this code](https://gist.githubusercontent.com/lcs-rgordon/f8a2f05c2517208d1e795f502241b1df/raw/a373f975424d3e2fc8822f41ed93821d5aebfde8/GalleryView.swift) into the new file, like this:

![Screenshot 2024-01-27 at 8.49.31 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.49.31%E2%80%AFAM.png)

If you look closely at the code, you will notice it's identical to the code in the `ListView` file, except instead of using `ListItemView` as the label for the `NavigationLink`, it is using our new `GalleryItemView`.

This does not look good, because `GalleryItemView` is not designed to be used in a `List`.

Although our work is not finish, it will be easier to see remaining edits if you commit your work now, with this message: 

```
Using the new gallery item view inside a scrolling list, temporarily.
```

We are going to use it inside of a layout structure that we have not formally examined before – the `LazyVGrid`.

Here is how Mark Moeykens describes this structure, which you can find on or near page 137 in **SwiftUI Views Mastery**:

![Screenshot 2024-01-27 at 8.51.43 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.51.43%E2%80%AFAM.png)

Take some time to look through the examples in **SwiftUI Views Mastery**.

We are going to build out a grid together now. Note that there are many ways to use a `LazyVGrid`.

First, we cannot use a `List` any more. 

Change this to a `ForEach` structure instead, like this – note that old code is on top, and new code is shown below:

![Screenshot 2024-01-27 at 8.56.34 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.56.34%E2%80%AFAM.png)

The preview is going to look a little strange, but that is fine for now:

![Screenshot 2024-01-27 at 8.57.02 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%208.57.02%E2%80%AFAM.png)

A `ForEach` structure is designed to iterate over an array. It iterates over an array the same way the `List` structure does, but it does not create a list with individual items. It just repeatedly builds the views it contains.

In our code currently, we use the `ForEach` to iterate over the `allLandmarks` array and create a new `NavigationLink` for each instance of the `Landmark` structure that we defined in our model.

Our next step is to wrap the `ForEach` structure in a `LazyVGrid` structure, like this:

![Screenshot 2024-01-27 at 9.00.01 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%209.00.01%E2%80%AFAM.png)

Notice that we immediately get an error.

This is because the `LazyVGrid` structure needs to know how many columns we want in our grid.

Although our code is not yet working, again it will be easier to see the remaining few edits if we commit and push now.

Please do so with this message:

```
Almost finished adding our LazyVGrid to GalleryView.
```

We will specify how many columns we want by adding a stored property named `twoColumns` to the `GalleryView` structure:

```swift
// MARK: Stored properties
let twoColumns = [
	GridItem(.adaptive(minimum: 100, maximum: 200), alignment: .top),
	GridItem(.adaptive(minimum: 100, maximum: 200), alignment: .top),
]
	
// MARK: Computed properties
```

... like this:

![Screenshot 2024-01-27 at 9.03.00 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%209.03.00%E2%80%AFAM.png)

Now we need to use the new stored property with our `LazyVGrid`.

Add the parameter named `columns` to the `LazyVGrid` and provide the argument `twoColumns`, using the stored property we just created, as shown on line 23:

![Screenshot 2024-01-27 at 9.04.19 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%209.04.19%E2%80%AFAM.png)

In short, we have told the `LazyVGrid` that we want two columns, and that it can automatically adjust the size of the columns, between a minimum width of 100 points and a maximum width of 200 points.

You could try adding a third column by adjusting the stored property:

![Screenshot 2024-01-27 at 9.05.48 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%209.05.48%E2%80%AFAM.png)

... but this looks a bit crowded. So, leave it as just two columns:

![Screenshot 2024-01-27 at 9.06.11 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%209.06.11%E2%80%AFAM.png)

We have two more small edits to make.

First, we need to be able to scroll the `LazyVGrid`.

Wrap the `LazyVGrid` in a `ScrollView` structure, like this:

![Screenshot 2024-01-27 at 9.07.17 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%209.07.17%E2%80%AFAM.png)

Now the layout looks the way we intend.

A final touch – items in a grid automatically inherit the default *accent color* for an iOS app, which is a bright blue.

This doesn't look great, so, let's override that accent colour.

Attach the following view modifier to the `NavigationLink`:

```swift
.tint(.primary)
```

And you will see the following:

![Screenshot 2024-01-27 at 9.09.04 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%209.09.04%E2%80%AFAM.png)

At this point, you can scroll the grid, and select items to navigate to the detail view.

This is nicer than the scrolling list, so please adjust the app entry point file to use this new view instead – old code is on top, new code is below:

![Screenshot 2024-01-27 at 9.10.22 AM.png|700](/img/user/Media/Screenshot%202024-01-27%20at%209.10.22%E2%80%AFAM.png)

We are done! Please commit and push your work with this message:

```
Finished adding a gallery in the form of a scrollable grid to our new landing view.
```

## Exercises

1. If you look closely at the following three files:
	- `DetailView`
	- `ListItemView`
	- `GalleryItemView`
	  
	  ... you will see some repetitive code.
	  
	  Add a helper view named `RecommendationView` that will replace this repeated code. It will need a stored property named `item` of type `Landmark`.

2. Replace the landmarks listed with several landmarks of your own, from your own experience in life. Instead of placeholder text, write a couple of paragraphs of actual text, explaining why you enjoyed or did not enjoy visiting a particular landmark. 
