---
{"dg-publish":true,"permalink":"/tutorials/creating-a-to-do-list-app-part-5/","dgHomeLink":true,"dgShowToc":true}
---


# Creating a To-do List App, Part 5

In [[Tutorials/Creating a To-do List App, Part 4\|part four]] of this task, you improved the to-do list app so that you could use Xcode Previews again. You could test a single view in Xcode Previews, and data would not be persisted. You could run your app in the Simulator or on a physical device, and data *would* be persisted – saved to a database file – by the SwiftData framework.

Using SwiftData to persist data is a good choice when the user of your app is the only person who will ever need to see that data. Data is persisted directly on the user's device, so it is kept very secure. Moreover, there is virtually no latency, as writing data to an SSD is very fast.

However, there are situations where the data created by one user in an app needs to be seen by another user of that app.

In these situations, we can persist data within a database stored "in the cloud", and configure our database to share data between users, as needed.

By the way – the term "cloud computing" just means that somewhere, a computer kept in a facility referred to as a "server farm" is running the database software.

A server farm is a building that contains many computers, usually all connected to the Internet.

Here is a photo of a rack of servers, kept within a server farm:

![massimo-botturi-zFYUsLk_50Y-unsplash.jpg|400](/img/user/Media/massimo-botturi-zFYUsLk_50Y-unsplash.jpg)
<small><div class="o2HfV xP9Y2"><span class="U665a FEdrY EZz41">Photo by <a href="https://unsplash.com/@wildmax?utm_content=creditCopyText&amp;utm_medium=referral&amp;utm_source=unsplash">Massimo Botturi</a> on <a href="https://unsplash.com/photos/electronic-wire-lot-zFYUsLk_50Y?utm_content=creditCopyText&amp;utm_medium=referral&amp;utm_source=unsplash">Unsplash</a>
  </span></div></small>

As app developers, by using frameworks, or third-party libraries, we can make use of cloud-hosted databases relatively easily.

In this tutorial, you will begin to learn how to use [Supabase](https://supabase.com) within an iOS project to store data in a cloud-hosted database.

## Obtain the starting point project

Rather than make further changes to the version of your to-do list app that writes data to a local database using SwiftData, it will be easier to return to the version of the app that kept to-do items in memory, and then edit the code from that point.

So, you can [download this file](https://www.russellgordon.ca/lcs/2023-24/ics3u/Todo-CloudDatabase.zip).

Once downloaded, you may need to double-click the `zip` file to de-compress it:

![Screenshot 2024-04-14 at 4.57.03 PM.png|400](/img/user/Media/Screenshot%202024-04-14%20at%204.57.03%E2%80%AFPM.png)

Then open the `Todo-CloudDatabase` folder, and double-click the blue `.xcodeproj` file:

![Screenshot 2024-04-14 at 4.57.13 PM.png|400](/img/user/Media/Screenshot%202024-04-14%20at%204.57.13%E2%80%AFPM.png)

Xcode will open, and you should see something like this:

![Screenshot 2024-05-21 at 12.33.47 PM.png](/img/user/Media/Screenshot%202024-05-21%20at%2012.33.47%E2%80%AFPM.png)

Before you try out the app, you must set a *bundle identifier*. This uniquely identifies your app to the Simulator device or physical device that you run the app on. To set the bundle identifier, first select the blue project file at top-left, then select the **Signing & Capabilities** tab:

![Screenshot 2024-05-21 at 12.26.47 PM.png](/img/user/Media/Screenshot%202024-05-21%20at%2012.26.47%E2%80%AFPM.png)

In the **Bundle Identifier** field, replace this value:

```
replace.with.your.reverse.domain.name.TodoList
```

... with something like this (for example, if your name is Sophia Chen):

```
ca.chen.sophia.TodoList
```

... like this:

![Screenshot 2024-05-21 at 12.28.57 PM.png](/img/user/Media/Screenshot%202024-05-21%20at%2012.28.57%E2%80%AFPM.png)

Now try out the app in the Simulator:

![Screenshot 2024-05-21 at 12.29.54 PM.png](/img/user/Media/Screenshot%202024-05-21%20at%2012.29.54%E2%80%AFPM.png)

You should see that you can add to-do items, edit them, delete them, and toggle their completion status. 

### Create a local repository

Before continuing, it's important to enable source control.

If you open the **Source Control** navigator, then click on **Repositories** tab, you will notice that there is no local repository:

![Screenshot 2024-04-14 at 5.02.01 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%205.02.01%E2%80%AFPM.png)

To fix this, select the menu sequence **Integrate > New Git Repository...**:

![Screenshot 2024-04-14 at 5.03.34 PM.png|350](/img/user/Media/Screenshot%202024-04-14%20at%205.03.34%E2%80%AFPM.png)

Then click the **Create** button:

![Screenshot 2024-04-14 at 5.04.11 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%205.04.11%E2%80%AFPM.png)

### Create the remote repository

Once that is done:

1. Expand the disclosure triangle for the `Todo-CloudDatabase` local repository. 
2. Expand the disclosure triangle for the `Remotes` folder.
3. Two-finger tap or right-click and choose the option to create a new remote.

Like this:

![Screenshot 2024-04-14 at 5.04.45 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%205.04.45%E2%80%AFPM.png)

When the next dialog appears, you can leave the default options, then press the **Create** button:

![Screenshot 2024-04-14 at 5.08.22 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%205.08.22%E2%80%AFPM.png)

You should see that the remote has been created:

![Screenshot 2024-04-14 at 5.09.11 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%205.09.11%E2%80%AFPM.png)

## Separation of Concerns

We have previously learned that it is ideal to keep [[Concepts/Separation of Concerns\|model code separated from view code]].

A **view** is anything a user sees within an app and interacts with – it's job is to *present* data.

A **model** is a representation of the data your app needs to work with.

However... at present, in almost every program we have written so far, the *state* of model data – how many to-do items there are, how many landmarks are shown in a list – has lived within the view.

When we want to perform a CRUD operation (create, read, update, or delete some data) the *code to make that happen is in the view*.

As our programs grow in size, that can become a problem. It can lead to:

- overly long views (too many lines of code)
- duplication of code (when modifying an instance of a data type, the code to do this in different views might look practically identical)

### The MVVM design pattern

So, there is a *software design pattern* known as MVVM, which stands for **Model-View-ViewModel**.

Model and view code work exactly as you already understand them to.

When we introduce a **view model**, it takes over the job of managing the *state* of the data that is described by our model. The view model also manages the actual work of creating, reading, updating, or deleting data on behalf of views within an app.

A single view model might be used by many views within an app.

Visually, and in general, that looks like this:

```mermaid
flowchart LR

id1["<b>Model</b>\nDescribes data"] --> id2["<b>View Model</b>\nManages the state of data"]
id2 --> id3["<b>View(s)</b>\nPresent data"]
id3 --> id2

```

If necessary, the view model creates an initial, empty instance of whatever data structures are described by the model. Or the view model might load existing instances of data (for example, from a database).

The view model provides instances of data to view(s) in an app. As needed, views call upon the view model to create, read, update, or delete data on their behalf.

A view model's job is very similar to the job that the [[Tutorials/Creating a To-do List App, Part 3#The context\|model context performs when using SwiftData]].

Let's look at how this can be applied within the to-do list app we have been developing.

### Create the view model

First, create a group named `ViewModel` in your project:

![Screenshot 2024-04-14 at 6.05.56 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%206.05.56%E2%80%AFPM.png)

Then create a new Swift file named `TodoListViewModel` inside that group:

![Screenshot 2024-04-14 at 6.06.54 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%206.06.54%E2%80%AFPM.png)

> [!TIP]
> 
> Take care to match the spelling and capitalization shown in these examples. It will make it easier to read your code later on.

Now press this button to add another editor on the right side of your Xcode window:

![Screenshot 2024-04-14 at 6.07.04 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%206.07.04%E2%80%AFPM.png)

Then arrange the windows such that `LandingView` is open on the right, and `TodoListViewModel`  is open on the left:

![Split Screen.gif](/img/user/Media/Split%20Screen.gif)

Copy and paste the following code into `TodoListViewModel`:

```swift
import Foundation

@Observable
class TodoListViewModel {
    
    // MARK: Stored properties
    // The list of to-do items
    var todos: [TodoItem]
    
    // MARK: Initializer(s)
    init(todos: [TodoItem] = []) {
        self.todos = todos
    }
    
    // MARK: Functions
    func createToDo(withTitle title: String) {
        
        // Create the new to-do item instance
        let todo = TodoItem(
            title: title,
            done: false
        )
        
        // Append to the array
        todos.append(todo)
        
    }
    
    func delete(_ todo: TodoItem) {
        
        // Remove the provided to-do item from the array
        todos.removeAll { currentItem in
            currentItem.id == todo.id
        }
        
    }
    
}
```

... like this:

![Screenshot 2024-04-14 at 6.20.09 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%206.20.09%E2%80%AFPM.png)

Big picture, this places all of the code related to tracking the state of to-do items, and any code connected to modifying to-do items data, into the `TodoListViewModel` class.

Let's briefly examine a few key lines of code in more detail:

![Screenshot 2024-04-14 at 6.22.17 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%206.22.17%E2%80%AFPM.png)

1. The `@Observable` keyword indicates that SwiftUI should watch any instances of the view model, so that when data changes, the user interface is updated.
2. The list (array) of to-do items, `todos`, is moved inside the view model.
3. `TodoListViewModel` is a class, so it must have an initializer.
4. The functions to create and delete a to-do item are copied directly from what is currently in the `LandingView` file.

Our next job is to remove the code that manages data from the *view*, and instead make use of the *view model* to do that work.

This is important progress, so be sure to commit and push your work at this point using the following message: 

```
Added a view model to manage state within the app, and handle CRUD (create, read, update, delete) operations.
```

### Use the view model

Now we will make modest edits to use the view model within the `LandingView` view.

First, where the `todos` array is currently created:

```swift
// The list of to-do items
@State var todos: [TodoItem] = exampleItems
```

...instead create an instance of `TodoListViewModel`:

```swift
// The view model
@State var viewModel = TodoListViewModel()
```

... like this:

![Screenshot 2024-04-14 at 7.45.19 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%207.45.19%E2%80%AFPM.png)

On line 21 in `LandingView`, the source of truth for data within the app – an instance of the view model – is now created.  This means the initializer function – on lines 18 to 20 in `TodoListViewModel` – is run. In turn, the initializer of the view model creates an empty array of to-do items.

We will fix the error on line 29 in `LandingView` in a moment.

First, scroll down to the functions that still exist in `LandingView`:

![Screenshot 2024-04-14 at 7.49.09 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%207.49.09%E2%80%AFPM.png)

Highlight both functions:

![Screenshot 2024-04-14 at 7.49.32 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%207.49.32%E2%80%AFPM.png)

... and delete them:

![Screenshot 2024-04-14 at 7.50.49 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%207.50.49%E2%80%AFPM.png)

This is all OK, because earlier, we moved the functions over to the view model:

![Screenshot 2024-04-14 at 7.51.35 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%207.51.35%E2%80%AFPM.png)

Now, all we need to do is make the code in the view actually use the instance of the view model that we created a moment ago.

Scroll up in `LandingView` to around line 29:

![Screenshot 2024-04-14 at 7.53.21 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%207.53.21%E2%80%AFPM.png)

Change the code:

```swift
List($todos) { $todo in
```

... to:

```swift
List($viewModel.todos) { $todo in
```

... like this:

![Screenshot 2024-04-14 at 7.54.20 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%207.54.20%E2%80%AFPM.png)

That causes the `List` structure to use the `todos` array that is now inside the view model, instead of trying to use the `todos` array that was previously part of `LandingView` directly (recall we deleted it a moment ago).

Finally, scroll down a bit further to where the the `delete` function and `createToDo` functions are invoked:

![Screenshot 2024-04-14 at 7.56.52 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%207.56.52%E2%80%AFPM.png)

Since those functions are part of the view model, we can access them by simply prepending `viewModel.` in front of the function names, like this:

![Screenshot 2024-04-14 at 7.57.14 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%207.57.14%E2%80%AFPM.png)

... and this:

![Screenshot 2024-04-14 at 7.58.30 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%207.58.30%E2%80%AFPM.png)

Now, try out the app again. You should see that as before, you should see that you can add to-do items, edit them, delete them, and toggle their completion status:

![Trying out the app.gif](/img/user/Media/Trying%20out%20the%20app.gif)

Now, you might be wondering – nothing in the way the app works has changed! This was a waste of time! Not so – the number of lines of code in the view has been reduced by nearly 40%.

Additionally, making use of a view model sets us up to keep the code that communicates with the cloud-hosted database entirely separate from the code that creates our user interface – the views. We are separating the major pieces of functionality within our app, and this a Good Thing.

Be sure to now commit and push your code, using this message:

```
Made use of the view model within our view to manage state.
```

## Supabase

Supabase is a company that offers cloud-hosted databases that can be integrated within apps developed on a wide variety of platforms – not just iOS.

### Create an account

To begin using this service, you must first create an account. This is a one-time-only requirement, and you can make use of your existing account on GitHub to use Supabase.

So, first, [follow this link to sign in to GitHub](https://github.com/login) using your existing account.

Then, [sign in at Supabase](https://supabase.com/dashboard).

You should see an interface something like this:

![Screenshot 2024-04-14 at 8.24.25 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.24.25%E2%80%AFPM.png)

Select **Continue with GitHub**.

You will then see this:

![Screenshot 2024-04-14 at 8.25.23 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.25.23%E2%80%AFPM.png)

Select the green **Authorize supabase** button.

After a moment, you will be logged in to Supabase, and presented with this screen:

![Screenshot 2024-04-14 at 8.26.15 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.26.15%E2%80%AFPM.png)

> [!TIP]
> 
> Do not worry if you briefly see a message at top right that says `Failed to create your profile.` That will go away after a moment, and does *not* impact your ability to use the service, in any case.

### Create a new project

Begin by clicking either one of the green **New Project** buttons:

![Screenshot 2024-04-14 at 8.27.24 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.27.24%E2%80%AFPM.png)

The first time you create a project, you will be prompted to create an organization:

![Screenshot 2024-04-14 at 8.29.32 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.29.32%E2%80%AFPM.png)

Type `Lakefield College School` for the **Name** field and then select `Educational` for the **Type of organization** dropdown, then click **Create organization**:

![Screenshot 2024-04-14 at 8.30.35 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.30.35%E2%80%AFPM.png)

After a moment, you will be brought to this screen to create a new project:

![Screenshot 2024-04-14 at 8.32.44 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.32.44%E2%80%AFPM.png)

Make the following selections – and – **very important** – be sure to copy and save the database password in a safe place on your own computer – you **must** be able to find this password later on:

![Screenshot 2024-04-14 at 8.33.34 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.33.34%E2%80%AFPM.png)

You will then see something like this screen – it may take a few minutes to set up your project:

![Screenshot 2024-04-14 at 8.37.14 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.37.14%E2%80%AFPM.png)

After a little while, the screen will change to the following:

![Screenshot 2024-04-14 at 8.38.35 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.38.35%E2%80%AFPM.png)

You are ready to create a table in your cloud-hosted database!

### Create a table

Select **Table Editor** button:

![Screenshot 2024-04-14 at 8.39.43 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.39.43%E2%80%AFPM.png)

Then press the green **Create a new table** button:

![Screenshot 2024-04-14 at 8.40.44 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.40.44%E2%80%AFPM.png)

Name the table `todos`:

![Screenshot 2024-04-14 at 8.41.18 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.41.18%E2%80%AFPM.png)

Add a description of `Holds all the to-do items saved by users in my app`:

![Screenshot 2024-04-14 at 8.41.57 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.41.57%E2%80%AFPM.png)

Then select the checkbox to *disable* row-level security:

![Screenshot 2024-04-14 at 8.42.10 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.42.10%E2%80%AFPM.png)

You will get a pretty stern warning about this choice – do not worry – this is only temporary, while we are learning – so go ahead and select the green **Confirm** button:

![Screenshot 2024-04-14 at 8.46.02 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.46.02%E2%80%AFPM.png)

You will then see the following:

![Screenshot 2024-04-14 at 8.46.29 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.46.29%E2%80%AFPM.png)

Scroll down a bit to the **Columns** section:

![Screenshot 2024-04-14 at 8.47.32 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.47.32%E2%80%AFPM.png)

You are going to add columns that match the properties of the `TodoItem` structure in your Xcode project:

![Screenshot 2024-04-14 at 8.48.24 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.48.24%E2%80%AFPM.png)

So, first, delete the `created_at` column:

![Screenshot 2024-04-14 at 8.48.48 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.48.48%E2%80%AFPM.png)

Leave the `id` column as is.

Add a `title` column:

![Screenshot 2024-04-14 at 8.50.29 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.50.29%E2%80%AFPM.png)

Then add a `done` column:

![Screenshot 2024-04-14 at 8.51.03 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.51.03%E2%80%AFPM.png)

Make sure the spelling of the column name, and the related data type, match what is shown above.

Then click the green **Save** button.

You should see an interface like the following:

![Screenshot 2024-04-14 at 8.52.20 PM.png](/img/user/Media/Screenshot%202024-04-14%20at%208.52.20%E2%80%AFPM.png)

You are all set to begin creating data in this table.

### Add data to the table

Using the green **Insert** button, add three rows of data to the table:

![Screenshot 2024-04-15 at 7.38.02 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%207.38.02%E2%80%AFAM.png)

For the data:

- let the database automatically generate the `id` value
- select a title for the to-do item
- set the `done` value to `false`

... then press the green **Save** button:

![Screenshot 2024-04-15 at 7.38.27 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%207.38.27%E2%80%AFAM.png)

The to-do items don't need to be exactly as shown, but please don't spend time adding dozens of to-do items right now:

![Screenshot 2024-04-15 at 7.40.44 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%207.40.44%E2%80%AFAM.png)

### Modifying a table's structure

You might have noticed that when adding data, `NULL` was an option. You can think of `NULL` in a database as equivalent to `nil` in a Swift program.

Both the `title` of a to-do item and it's completion status, `done`, should always have a value.

Therefore, let's learn how to modify the structure of a table and correct this.

Click the three dots `•••` beside the table name and then **Edit Table**:

![Screenshot 2024-04-15 at 7.42.27 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%207.42.27%E2%80%AFAM.png)

Next to the definition of the `title` column, click the gear icon, `⛭` and then de-select the **Is Nullable** option:

![Screenshot 2024-04-15 at 7.44.51 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%207.44.51%E2%80%AFAM.png)

... so it looks like this:

![Screenshot 2024-04-15 at 7.45.44 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%207.45.44%E2%80%AFAM.png)

Then do the same for the `done` column.

After adjusting both columns, press the green **Save** button:

![Screenshot 2024-04-15 at 7.46.03 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%207.46.03%E2%80%AFAM.png)

So, now the table is set up the way we need it to be, for now.

How do we get the data out of this table, and into our app?

## The Web

The Internet, it's related technologies, and particularly the World Wide Web, or "the Web" for short, are at the core of many things we do in a day.

This is a brief sidebar to explain a bit about how information is sent between computers using the Web.

### Headers

First, try visiting this page in your web browser:

[https://www.russellgordon.ca/lcs/hello.html](https://www.russellgordon.ca/lcs/hello.html)

The content of that web page, when Mr. Gordon added it to his website, looked like this:

```html
<html>
	<head>
		<title>A very small web page</title>
	</head>
	<body>
		Hello, world!
	</body>
</html>
```

A web browser (on your computer) interprets the HTML – which stands for *hypertext markup language* – sent by a web server (a computer somewhere else in the world) and shows the content.

Often, there are other files that control the appearance of the page (CSS – *cascading style sheets*) and behaviour of the page (JS – *JavaScript*).

However, there is other information that is sent by the web server when a web browser makes a request – these are called *headers* – and they provide additional information about the content being sent.

Open the **Terminal** app on your computer, using the Spotlight feature to find it:

![Pasted image 20240415075648.png|400](/img/user/Media/Pasted%20image%2020240415075648.png)

At the prompt that appears, type this command, then press **Return**:

```bash
curl -i https://www.russellgordon.ca/lcs/hello.html
```

In general, `curl` is "a tool for transferring data from or to a server using URLs".

The command above asks a program named `curl` to fetch the web page and show us the contents of the requested file, along with any headers that the server provides for that document.

You should see output similar to the following:

![Screenshot 2024-04-15 at 8.03.28 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%208.03.28%E2%80%AFAM.png)

In a similar way, we are now going to use `curl` to fetch the data from our database table hosted by Supabase.

### Obtaining project details

Every project in Supabase has a *URL* that it is accessed from, and a *key* that ensures the user accessing the project is allowed to do so.

> [!NOTE]
> 
> There are other layers of authentication involved, but we are omitting those for the time being.

Open the **Project Settings** page:

![Screenshot 2024-04-15 at 8.04.21 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%208.04.21%E2%80%AFAM.png)

Then select the **API** option (this stands for *application programming interface*):

![Screenshot 2024-04-15 at 8.05.03 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%208.05.03%E2%80%AFAM.png)

On the resulting page, there are two pieces of information that you need.

Copy the **URL** and the **anon public** key to a safe place on your computer, such as a text file stored in your **Computer Studies** folder. You will need this information later on.

![Screenshot 2024-04-15 at 8.07.31 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%208.07.31%E2%80%AFAM.png)

### Fetching table data

We will use `curl` to fetch all the data in the `todos` table.

Select the **API Docs** page:

![Screenshot 2024-04-15 at 8.09.49 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%208.09.49%E2%80%AFAM.png)

Then select the link for the `todos` table:

![Screenshot 2024-04-15 at 8.10.17 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%208.10.17%E2%80%AFAM.png)

Now select the **Bash** option at top right:

![Screenshot 2024-04-15 at 8.11.34 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%208.11.34%E2%80%AFAM.png)

Next, there is an option, also at top-right, to show the API key – click the **hide** button:

![Screenshot 2024-04-15 at 8.12.35 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%208.12.35%E2%80%AFAM.png)

Then, select **(anon) public**:

![Screenshot 2024-04-15 at 8.12.55 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%208.12.55%E2%80%AFAM.png)

Now the documentation page for Supabase automatically generates the `curl` commands that you can use to query your database from the command line.

Note that this is *not* how we will obtain the data for our app – but this is useful to explain how it is that Supabase sends us the information in our database.

Scroll down to the **Read All Rows** option, then copy the command:

![Screenshot 2024-04-15 at 8.16.11 AM.png](/img/user/Media/Screenshot%202024-04-15%20at%208.16.11%E2%80%AFAM.png)

This command uses `curl` to request a web page from the Supabase web server. It sets several *headers* to identify which project to pull data from. The `apikey` is a secret (for your project only) and that lets Supabase know that it is you (and not someone else) requesting data from your database.

So, now, paste that command into your **Terminal** window:

![Screenshot 2024-04-15 at 8.16.46 AM.png|500](/img/user/Media/Screenshot%202024-04-15%20at%208.16.46%E2%80%AFAM.png)

... then press the **Return** key:

![Screenshot 2024-04-15 at 8.17.09 AM.png|500](/img/user/Media/Screenshot%202024-04-15%20at%208.17.09%E2%80%AFAM.png)

You should see output that provides the contents of the `todos` table.

This is how Supabase sends us data (and in turn, how we send data to Supabase).

It is all done by making requests over the World Wide Web.

In part 6 of this tutorial (tomorrow's class) you will learn a little about the format of the data being sent from Supabase, and how to use the actual Supabase library to much more easily obtain data and use it within your to-do list app.

