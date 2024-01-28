---
{"dg-publish":true,"permalink":"/tutorials/air-bn-b-lottie-animations-library/","dgHomeLink":true,"dgShowToc":true}
---

# AirBnB Lottie Animations Library

If you are interested in computer animation and graphics, you may be familiar with [Adobe After Effects](https://www.adobe.com/ca/products/aftereffects.html).

*Lottie* is an open-source project that defines a file format for describing vector-based animations.

After Effects, and other animation software, can save animations created in those programs in the Lottie file format.

[AirBnb](https://www.airbnb.ca) maintains [lottie-ios](https://github.com/airbnb/lottie-ios), an open-source third-party package that allows iOS, macOS, and tvOS apps to natively render vector-based animations made in applications like After Effects.

Fortunately, you don't have to make these animations yourself.

A website known as [LottieFiles](https://lottiefiles.com) makes many of these animations available free of charge.

## Browse available animations

Head over to [LottieFiles](https://lottiefiles.com) and then sign up with your LCS Google account: 

![Screenshot 2023-01-27 at 1.05.19 PM.png](/img/user/Media/Screenshot%202023-01-27%20at%201.05.19%20PM.png)

Afterwards, take a moment to [browse or search for animations](https://lottiefiles.com/featured) that you find entertaining or that you think might be useful in the future within apps that you might write.

In this tutorial, you will learn how to use these Lottie animations within an iOS app by using the AirBnb third-party package.

## Make a new iOS project

In Xcode, create a new project:

![Screenshot 2023-01-27 at 1.09.27 PM.png|400](/img/user/Media/Screenshot%202023-01-27%20at%201.09.27%20PM.png)

It should be an app, for the iOS platform:

![Screenshot 2023-01-27 at 1.10.16 PM.png](/img/user/Media/Screenshot%202023-01-27%20at%201.10.16%20PM.png)

Name the project iOS `LottieAnimationsList`:

![Screenshot 2023-01-27 at 1.10.55 PM.png](/img/user/Media/Screenshot%202023-01-27%20at%201.10.55%20PM.png)

Ensure that source control is enabled and save in a place where you can find this project later on:

![Screenshot 2023-01-27 at 1.11.28 PM.png](/img/user/Media/Screenshot%202023-01-27%20at%201.11.28%20PM.png)

Once the project is open, create a remote:

![Screenshot 2023-01-27 at 1.12.31 PM.png](/img/user/Media/Screenshot%202023-01-27%20at%201.12.31%20PM.png)

## Organize the project

Now, complete the following steps:

1. Delete `ContentView`
2. Create two groups:
	- `Model`
	- `Views`
3. Inside the `Views` group, create a new **SwiftUI View** named `AnimationsListView`.
4. Make the app entry point file create an instance of `AnimationsListView`.

When you are all done, your project should look like this:

![Screenshot 2023-01-27 at 1.16.50 PM.png](/img/user/Media/Screenshot%202023-01-27%20at%201.16.50%20PM.png)

At this point, commit and push your work to your remote, with the message:

```
Organized project and created a list view to show interesting animations.
```

## Add the third-party package

AirBnb's [lottie-ios](https://github.com/airbnb/lottie-ios) package does most of the hard work for us.

	https://github.com/airbnb/lottie-ios

We will now add the package from AirBnb to our project.

Choose **File > Add Package Dependencies...**

![Screenshot 2024-01-28 at 5.51.17 PM.png|300](/img/user/Media/Screenshot%202024-01-28%20at%205.51.17%E2%80%AFPM.png)

In the window that appears, type `lottie-ios` in the top-right corner:

![Screenshot 2023-01-27 at 1.20.28 PM.png](/img/user/Media/Screenshot%202023-01-27%20at%201.20.28%20PM.png)

> [!NOTE]
> If Xcode is unable to locate the `lottie-ios` package, instead of typing `lottie-ios`, copy and paste the [address of the package](https://github.com/airbnb/lottie-ios) into the dialog box:
> ![Screenshot 2023-01-27 at 2.40.30 PM.png](/img/user/Media/Screenshot%202023-01-27%20at%202.40.30%20PM.png)

Then choose the **Add Package** button.

After a moment, another window will appear. Choose **Add Package** a second time:

![Screenshot 2023-01-27 at 1.21.33 PM.png](/img/user/Media/Screenshot%202023-01-27%20at%201.21.33%20PM.png)

If things worked correctly, you should see `Lottie` listed under **Package Dependencies**:

![Screenshot 2023-01-27 at 1.22.12 PM.png|200](/img/user/Media/Screenshot%202023-01-27%20at%201.22.12%20PM.png)

> [!NOTE]
> 
> The exact version number of the package might vary from what you see in the screenshot above.
> 
> For example, the current version of the Lottie package is 4.4.0.

At this point, commit and push your work to your remote, with the message:

```
Added the third-party lottie-ios library.
```

## Add Mr. Gordon's helper view

Mr. Gordon has authored a helper view to make using Lottie animations even easier.

In the `Views`  group, create a new SwiftUI view named `LottieView`:

![Screenshot 2023-01-27 at 1.24.11 PM.png](/img/user/Media/Screenshot%202023-01-27%20at%201.24.11%20PM.png)

Now [visit this web page](https://gist.githubusercontent.com/lcs-rgordon/347c403814015b248a166b7008582735/raw/54cbbfa86e67580d8b1cc6f42737036fbb81c3e1/LottieView.swift), select all the text using **Command-A**, then switch to Xcode, select all the text in `LottieView` using **Command-A**, and paste Mr. Gordon's code in using **Command-V**. When that is done, it should look like this:

![Screenshot 2023-01-27 at 1.26.03 PM.png](/img/user/Media/Screenshot%202023-01-27%20at%201.26.03%20PM.png)

While you are welcome to review this code, it's not necessary for you to know how it works. You may simply use it within your apps.

At this point, commit and push your work to your remote, with the message:

```
Added Mr. Gordon's helper view.
```

## Download an animation

You have already [browsed available animations](https://lottiefiles.com/featured) and  found ones that you like.

Each Lottie animation can be saved as a JSON file, which is just a text file that has a particular format that is used to describe the animation.

Find an animation you like:

![Screenshot 2024-01-28 at 6.01.48 PM.png](/img/user/Media/Screenshot%202024-01-28%20at%206.01.48%E2%80%AFPM.png)

Then click the **Download** button at top-right:

![Screenshot 2024-01-28 at 6.02.08 PM.png](/img/user/Media/Screenshot%202024-01-28%20at%206.02.08%E2%80%AFPM.png)

Click **Save to workspace to download**:

![Screenshot 2024-01-28 at 6.02.32 PM.png](/img/user/Media/Screenshot%202024-01-28%20at%206.02.32%E2%80%AFPM.png)

Once added to your workspace, download the animation in the **Lottie JSON** format:

![Screenshot 2024-01-28 at 6.04.06 PM.png](/img/user/Media/Screenshot%202024-01-28%20at%206.04.06%E2%80%AFPM.png)

Now, make a new group named `Animations` in your Xcode project, then drag and drop the JSON file from your **Downloads** folder into the `Animations` group in Xcode:

![Screenshot 2024-01-28 at 6.06.22 PM.png](/img/user/Media/Screenshot%202024-01-28%20at%206.06.22%E2%80%AFPM.png)

When you drag the item into Xcode, this dialog will appear – you can accept the default options, as shown:

![Screenshot 2024-01-28 at 6.06.52 PM.png](/img/user/Media/Screenshot%202024-01-28%20at%206.06.52%E2%80%AFPM.png)

Repeat this process until you have several animations that you like in your project.

![Screenshot 2024-01-28 at 6.10.44 PM.png|200](/img/user/Media/Screenshot%202024-01-28%20at%206.10.44%E2%80%AFPM.png)

At this point, commit and push your work to your remote, with the message:

```
Added several animations that I like.
```

## Write a structure to describe the animations

Please create a new **Swift** file in the `Model` group named `FavouriteAnimation`.

You are going to write a structure to describe a favourite animation.

The structure will include:

- a unique identifier, so instances can be used by SwiftUI to display a scrolling list
- a place to store the animation's filename
- a place to store a brief description of the animation

You will then create a list that contains instances to describe your favourite animations.

This all might look like this:

![Screenshot 2024-01-28 at 6.15.15 PM.png](/img/user/Media/Screenshot%202024-01-28%20at%206.15.15%E2%80%AFPM.png)

If you wish, you can [use this code](https://gist.githubusercontent.com/lcs-rgordon/710a9765c06fe49530bb563bda6f682e/raw/81e2b8140ffc0285c2be40cad36c5e44d1e6ac42/FavouriteAnimation.swift) as a starting point for your own.

At this point, commit and push your work to your remote, with the message:

```
Added a structure and an array to describe my favourite animations.
```

> [!TIP]
> 
> You might wish to rename animations as you add them into your project, as the random numbers assigned by the LottieFiles website are not very readable.
> 
> ![Screenshot 2024-01-28 at 6.26.58 PM.png](/img/user/Media/Screenshot%202024-01-28%20at%206.26.58%E2%80%AFPM.png)

## Allow for navigation with a list

Back on `AnimationsListView`, create a list that iterates over your array of favourite animations.

Each iteration over an element of the array creates a navigation link whose destination uses `LottieView` to show an animation that you downloaded from LottieFiles. The label shows your description:

![Screenshot 2024-01-28 at 6.18.42 PM.png](/img/user/Media/Screenshot%202024-01-28%20at%206.18.42%E2%80%AFPM.png)

If you run your app, you should now be able to browse animations that you downloaded:

![Screenshot 2023-01-27 at 2.47.23 PM.png](/img/user/Media/Screenshot%202023-01-27%20at%202.47.23%20PM.png)

Keep this app around for future reference!

The selective use of animations are a great addition to almost any app.



