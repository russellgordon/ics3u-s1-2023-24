---
{"dg-publish":true,"permalink":"/tutorials/creating-a-new-mac-os-project-with-a-gui/","dgHomeLink":true,"dgShowToc":true}
---

# Creating a New macOS Project with a GUI

Xcode is a large application that serves several purposes for software developers.

Many different types of projects can be created for different Apple platforms.

This short tutorial will show you how to create a project that:

- runs on macOS
- shows a graphical user interface (GUI)
## Create the project

To create a playground, make sure that Xcode is in the foreground on your computer by clicking it's icon in the Dock:

![Pasted image 20231021072302.png|100](/img/user/Media/Pasted%20image%2020231021072302.png)

From the menu bar at top left, choose **File > New > Project...**:

![Screenshot 2023-10-23 at 6.11.30 AM.png|400](/img/user/Media/Screenshot%202023-10-23%20at%206.11.30%E2%80%AFAM.png)

You will see the following window – here, choose the ==**macOS**== tab, then **App**, and then **Next**:

![Screenshot 2023-10-27 at 7.24.05 AM.png|700](/img/user/Media/Screenshot%202023-10-27%20at%207.24.05%E2%80%AFAM.png)

On the following screen, give your project:

1. a descriptive name, based on what idea you are exploring
2. select your team
	- NOTE: Log in with the Apple ID tied to your LCS email address, if necessary.
3. provide an organization identifier
	- NOTE: If your name is Stephanie Laroux, use `ca.stephanielaroux`
4. interface should be **SwiftUI**
5. language should be **Swift**
6. storage should be **None**
7. no checkmark beside **Include Tests**

![Screenshot 2023-10-27 at 7.29.05 AM.png|700](/img/user/Media/Screenshot%202023-10-27%20at%207.29.05%E2%80%AFAM.png)

On the following screen, choose where to save your project – be sure that source control is enabled:

![Screenshot 2023-10-27 at 7.30.26 AM.png|700](/img/user/Media/Screenshot%202023-10-27%20at%207.30.26%E2%80%AFAM.png)
## Begin coding

You will see the following when your project first opens:

![Screenshot 2023-10-27 at 7.33.10 AM.png|700](/img/user/Media/Screenshot%202023-10-27%20at%207.33.10%E2%80%AFAM.png)

As you change code at left, the preview window updates at right.