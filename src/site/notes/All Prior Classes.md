---
{"dg-publish":true,"permalink":"/all-prior-classes/","dgHomeLink":true}
---

# All Prior Classes

## Table of Contents

### Thread 1

- [[All Prior Classes#Thread 1, Day 8 - Monday, October 30, 2023\|Day 8 - Monday, October 30, 2023]]
- [[All Prior Classes#Thread 1, Day 7 - Friday, October 27, 2023\|Day 7 - Friday, October 27, 2023]]
- [[All Prior Classes#Thread 1, Day 6 - Wednesday, October 25, 2023\|Day 6 - Wednesday, October 25, 2023]]
- [[All Prior Classes#Thread 1, Day 5 - Tuesday, October 24, 2023\|Day 5 - Tuesday, October 24, 2023]]
- [[All Prior Classes#Thread 1, Day 4 - Monday, October 23, 2023\|Day 4 - Monday, October 23, 2023]]
- [[All Prior Classes#Thread 1, Day 3 - Friday, October 20, 2023\|Day 3 - Friday, October 20, 2023]]
- [[All Prior Classes#Thread 1, Day 2 - Wednesday, October 18, 2023\|Day 2 - Wednesday, October 18, 2023]]
- [[All Prior Classes#Thread 1, Day 1 - Tuesday, October 17, 2023\|Day 1 - Tuesday, October 17, 2023]]


<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/thread-1/day-8/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">




### Thread 1, Day 8 - Monday, October 30, 2023
#### Agenda
1. Discussion: Create a "Bento-Box" Design
	- Reviewing some strategies to help complete the exercise assigned in our last class.
	- Time to work on this task in class, as needed.
1. Activity: [[Tutorials/Reproducing the Stopwatch\|Reproducing the Stopwatch]]
	- Learn how to reproduce the interface of a real iOS app.
1. Portfolios: Mid-module Portfolio Reviews
	- Major skills learned to date:
		- authoring structures to model data
		- creating user interfaces
	- Meet privately with Mr. Gordon to review your portfolio and propose a current level of achievement for the skills list above, based on the evidence currently in your portfolio.
###### Things to do before our next class
- [ ] Take half an hour to make further progress on either the Bento Box task or the [[Tutorials/Reproducing the Stopwatch\|Stopwatch activity]].


</div></div>

<small>[[All Prior Classes#Thread 1\|Back to top of thread 1 ⬆]]</small>

<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/thread-1/day-7/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">




### Thread 1, Day 7 - Friday, October 27, 2023
#### Agenda
1. Productivity: [Negative app](https://apps.apple.com/ca/app/negative/id1378123825?mt=12)
	- Dark mode makes using most parts of our computers comfortable after sundown.
	- PDFs have long been a problem – they still show with a white background.
	- Negative solves this – optionally, try it out.
1. Discussion: [Rubber Duck Debugging](https://rubberduckdebugging.com)
	- Solving logical errors and syntax errors can be frustrating, but everyone deals with it, even experienced programmers.
	- Pairing with a friend to describe what you are trying to do with your code, line by line, can be helpful.
		- Often during this process, you will realize the source of the problem you are having.
	- When a friend is not nearby, [use your duck](https://rubberduckdebugging.com)! 🦆
1. Setup: [SF Symbols App](https://developer.apple.com/sf-symbols/)
	- Not all software developers have graphic design skills.
	- Platform owners like Apple want their users to have a consistent experience when using apps written by different people.
	- One of the ways Apple helps their developers provide that consistent look and feel is by offering a wide variety of built-in images that can be used in apps.
	- Please [download and install](https://devimages-cdn.apple.com/design/resources/download/SF-Symbols-5.dmg) the SF Symbols app now. 
	  > [!TIP]
	  > To use an SF Symbol within a SwiftUI layout, try the following code:
	  > ```swift
	  >   Image(systemName: "bolt")
	  >       .resizable()
	  >       .scaledToFit()
	  >       .frame(width: 20)
	  > ```
1. Setup: [[Tutorials/Creating a New macOS Project with a GUI\|Creating a New macOS Project with a GUI]]
	- Please follow these steps to create a new project for the Bento-Box exercise below.
1. Tutorial: Saving Revisions of Your Work
	- Xcode automatically saves your code as you type.
	- However, it is additionally useful to have "save points" while you author code.
	- Mr. Gordon will explain how to *stage* and *commit* your work to save revisions locally.
	  > [!IMPORTANT]
	  >  As you go forward in this course, *always* commit your work frequently with descriptive messages.
	  >  
	  >  This serves as a form of note-taking, makes it easier to debug problems, and if necessary, makes it possible for you to return to a prior version of your code.
1. Exercise: Create a "Bento-Box" Design
	- Marketing teams must be able to convey new features in a concise manner to an audience.
	- In recent years, Apple has used "Bento-Box" graphics to do so.
	- Try to [[Media/Bento Box Example\|reproduce this image]] using SwiftUI, or use it as inspiration to design a bento-box themed view related to something you care about.
	- Mr. Gordon will demonstrate how to add images into your project.
	- Use [[Media/SwiftUI Views Mastery\|SwiftUI Views Mastery]] as a reference.
	- Here is the [starter code discussed in class](https://gist.github.com/lcs-rgordon/3e9812b1dfd2a776137a807bed860db4) and a [[Media/Bento Box Starter Code\|screenshot of what it looks like]].
	  > [!HINT]
	  > Some keywords to look for examples of:
	  > - foregroundStyle
	  > - cornerRadius
	  > - gradient
	  > - Image
	  >   
	  > **Also:** the keyboard shortcut `Option-Shift-K` produces the Apple logo.

###### Things to do before our next class
- [ ] Complete the exercise on layout as described above, then write about what you learned in a portfolio entry on [Notion](https://notion.so).
- [ ] ==Review your portfolio==
	- We will be doing mid-module portfolio reviews early next week.
	- You will have a short private conversation with Mr. Gordon, and:
		- describe what you have done well by using the evidence in your portfolio
		- identify what you might do to improve
		- categorize your current level of achievement as one of these levels:
			- approaching expectations
			- meeting expectations
			- exceeding expectations

</div></div>

<small>[[All Prior Classes#Thread 1\|Back to top of thread 1 ⬆]]</small>

<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/thread-1/day-6/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">




### Thread 1, Day 6 - Wednesday, October 25, 2023
#### Agenda
1. Exercise: Create a Wireframe Layout
	- Select at least five layouts [from these examples](https://russellgordon.ca/lcs/2023-24/ics3u/wireframes.pdf).
	- Consult SwiftUI Views Mastery as a reference.
	- Recommend that [you use this playground](https://russellgordon.ca/lcs/2023-24/ics3u/Blueprints.playground.zip) to make your wireframes.
	- Use the same concepts we have just looked at to wireframe the layouts you selected.
###### Things to do before our next class
- [ ] Complete the exercise on layout as described above, then write about what you learned in a portfolio entry on [Notion](https://notion.so).

</div></div>

<small>[[All Prior Classes#Thread 1\|Back to top of thread 1 ⬆]]</small>

<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/thread-1/day-5/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">




### Thread 1, Day 5 - Tuesday, October 24, 2023
#### Agenda
1. Activity: Modelling a Report Card
	- Create a [[Tutorials/Creating an Xcode Playground\|new Xcode playground]] named **Report Card Exercise**.
	- Work with your partner to author a structure that could efficiently store the data shown [[Media/Report Card Example\|in this report card]].
	- Remember: <span style="color:green">**D**on't **R**epeat **Y**ourself</span>
		- Use [strategies we have discussed](https://gist.github.com/russellgordon/a9be1f533e43085c184428bce46d947b) to avoid repeatedly defining similar fields.
1. Setup: Obtain Digital Copies of Your Books
	- Follow the instructions given in class to obtain your digital copies of *SwiftUI Views Mastery* and *Working with Data in SwiftUI*.
1. Concept: [[Concepts/Introduction to Layout\|Introduction to Layout]]
	- Learn how to create basic page layouts in SwiftUI.
	- Please continue to use screenshots to show the *results* of code being run.
1. Exercise: Create a Wireframe Layout
	- Select at least two layouts [from these examples](https://russellgordon.ca/lcs/2023-24/ics3u/wireframes.pdf).
	- Use the same concepts we have just looked at to wireframe the layouts you selected.

###### Things to do before our next class
- [ ] Complete the exercise on layout as described above, then write about what you learned in a portfolio entry on [Notion](https://notion.so).

</div></div>

<small>[[All Prior Classes#Thread 1\|Back to top of thread 1 ⬆]]</small>

<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/thread-1/day-4/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">




### Thread 1, Day 4 - Monday, October 23, 2023
#### Agenda
1. Discussion: Don't Repeat Yourself
	- How to keep your code tidy.
	- Capitalization conventions when authoring Swift code.
	- Vocabulary review.
	- Reviewing various solutions to the exercise from yesterday's class.
	> [!TIP]
	>  Here is [code that exemplifies the idea of embedding one structure inside another](https://gist.github.com/russellgordon/a9be1f533e43085c184428bce46d947b), and here is a [[Media/Nested Structures Example\|screenshot comparing that code to the cards]] themselves.
2. Portfolio: [[Portfolios/Sharing Long Blocks of Code\|Sharing Long Blocks of Code]]
	- Share code, not screenshots of code.
	- Please continue to use screenshots to show the *results* of code being run.
3. Portfolio: [[Portfolios/Handling Comments on Posts\|Handling Comments on Posts]]
	- Do not mark comments as resolved in Notion so that the record of our conversation is preserved and easy to see at a glance.
4. Concept: Computed Properties
	- Structures can do more than just store values - they can calculate values as well.
	> [!TIP]
	>  Here is [the code we developed and discussed](https://gist.github.com/russellgordon/df50e7fadd13aec68c5e30a840c9796f) in class, and here is a [[Media/Computed Properties Example\|screenshot showing the results]] when the code is run.
5. Exercise: Describing 2D and 3D Figures
	- You have been randomly assigned [a 2D or 3D figure to work with](https://www.eqao.com/wp-content/uploads/g9-formula-sheet-academic.pdf).
	- Create a [[Tutorials/Creating an Xcode Playground\|new Xcode playground]] named **Computed Properties Exercise**.
	- Write a structure that models the figure you have been assigned.
		- The structure should use stored properties and computed properties.
	- Make several instances of the structure and test your work.

###### Things to do before our next class
- [ ] Complete the exercise on structures as described above, then write about what you learned in a portfolio entry on [Notion](https://notion.so).

</div></div>

<small>[[All Prior Classes#Thread 1\|Back to top of thread 1 ⬆]]</small>

<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/thread-1/day-3/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">




### Thread 1, Day 3 - Friday, October 20, 2023
#### Agenda
1. Concept: [[Concepts/Abstraction and Binary Numbers\|Abstraction and Binary Numbers]]
	- Read this mini-lesson to get a very brief introduction to how computers store numeric data.
1. Tutorial: [[Tutorials/Creating an Xcode Playground\|Creating an Xcode Playground]]
	- Please follow the steps described in this tutorial to create a playground named **Data Types and Structures**.
1. Concept: [[Concepts/Data Types\|Data Types]]
	- Use the playground you just created to try out the examples given in this mini-lesson.
	- Take notes in your black hardcover notebook, or in your portfolio entry for today in [Notion](https://notion.so).
1. Concept: [Structures](https://russellgordon.ca/lcs/2023-24/ics3u/structures.pdf)
	- Try out the examples described in this mini-lesson in the same playground you already have open.
1. Exercise: Model Hockey Cards Data Using Structures
	- Here is a [close-up of a retro-style hockey card for an imaginary player](https://russellgordon.ca/lcs/2023-24/ics3u/retro-75-hockey-card-template.jpg).
	- Here is an image of [several similar cards](https://russellgordon.ca/lcs/2023-24/ics3u/album-of-retro-75-custom-hockey-cards.jpg).
	- Write structure(s) in your playground to describe the data shown in the hockey cards.
	- Then create *instances* of your structure for at least three hockey cards. 

###### Things to do before our next class
- [ ] Complete the exercise on structures as described above, then write about what you learned in a portfolio entry on [Notion](https://notion.so).

</div></div>

<small>[[All Prior Classes#Thread 1\|Back to top of thread 1 ⬆]]</small>

<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/thread-1/day-2/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">




### Thread 1, Day 2 - Wednesday, October 18, 2023
#### Agenda
1. Portfolio: [[Portfolios/Creating a Notion Account\|Creating a Notion Account]]
	- Get started with using Notion.
2. Tutorial: [[Tutorials/Creating Bookmarks\|Creating Bookmarks]] 
	- Please be sure you make a bookmark for your Notion portfolio page.
3. Portfolio: [[Portfolios/First Post\|First Post]]
	- Learn more about what makes for good evidence of understanding when posting in your portfolio.
4. Install [[Setup/Xcodes\|Xcodes]]
	- Xcodes makes it easy to manage the installation of *Xcode*, which is the programming environment we will use this year.
	  > [!NOTE]
	  > Check your email for an invitation to join the Apple Developer program via Lakefield College School.
	  > 
	  > **Please create a new Apple ID using your LCS email address to accept the invitation.**
	  > 
	  > When creating your Apple ID, use the school's street address, but your own phone number. The complete address for LCS is:
	  > 
	  >  `4391 County Road 29`
	  >  `Lakefield College School`
	  >  `Lakefield ON K0L2H0`
	  >  `Canada`
5. Install Xcode 15
	- Use [[Setup/Xcodes\|Xcodes]] to install Xcode 15.
	  > [!TIP]
	  > Do not install Xcode via the App Store, as using this method means that it will automatically get upgraded when a new version is released (which is not always ideal).
6. [[Activities/Programming with Purpose\|Programming with Purpose]]
	- Please watch the video and respond to the prompts provided.
###### Things to do before our next class
- [ ] Be sure that you have installed Xcodes and Xcode, as described above.
- [ ] Write your [[Activities/Programming with Purpose#Reflection\|reflection]] after watching Programming with Purpose.

</div></div>

<small>[[All Prior Classes#Thread 1\|Back to top of thread 1 ⬆]]</small>

<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/thread-1/day-1/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">




### Thread 1, Day 1 - Tuesday, October 17, 2023
#### Agenda
1. [Computer Studies at LCS](https://drive.google.com/file/d/1moFeJKPkoIbtV_4aXU0EiVfD_iudTmlG/view?usp=sharing)
	- Ultimately, Computer Studies is about talking to people to understand problems that you can help them solve using technology.
2. [Course Outline](https://bit.ly/lcscs23-g11-sco)
3. Activity: [[Activities/Parsing Instructions\|Parsing Instructions]]
4. Setup: [[Setup/Installing Playgrounds\|Installing Playgrounds]]
5. Setup: [[Setup/Subscribe to Turtle Sketches\|Subscribe to Turtle Sketches]]
6. Activity: [[Activities/Name Plate\|Name Plate]]
###### Things to do before our next class
- [ ] Be sure that [you have upgraded your computer to macOS Sonoma](https://teaching.russellgordon.ca/software-setup/mac-os-sonoma/).
- [ ] Make progress on [[Activities/Name Plate\|drawing an initial version of your name using the turtle drawing metaphor]].

</div></div>

<small>[[All Prior Classes#Thread 1\|Back to top of thread 1 ⬆]]</small>
