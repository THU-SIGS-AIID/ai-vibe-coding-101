# How to Build the Simplest WeChat Mini Program

# 1. What Are WeChat Mini Programs and WeChat Mini Program Development

In this tutorial, we will complete a full closed loop: from an idea in your mind to a real mini program that can be searched for and opened by scanning a code in WeChat.

Before we start hands-on work, we need to establish two basic understandings.

The first is the **essence**: What exactly is a WeChat mini program? How is it different from ordinary apps and web pages? Why do so many products choose the mini program format? Only by understanding the underlying logic of mini programs can you judge whether your idea is suitable for implementation as a mini program.

The second is the **path**: When you say "I want to make a mini program," what does the complete path from zero to launch look like? What are the key nodes on this road—what to consider during the concept phase, how to set up the development environment, how to use AI-assisted development to improve efficiency, what pitfalls exist in simulator debugging, and what problems test accounts and official releases solve respectively. Run through the entire process in your mind first, so you won't get lost during actual implementation.

After clarifying these two questions, we can formally enter the development phase. Next, let's start with the first question: What exactly is a WeChat mini program?

## 1.1 WeChat Mini Programs

A WeChat mini program can be seen as an application hidden within WeChat. It doesn't require you to search for, download, or install from an app store—just search for its name in WeChat, scan a code, or click on a card shared by someone else, and you can use it immediately. When you're done, just close it, and open it again next time you need it. It won't permanently occupy your phone's home screen or storage space.

For ordinary users, mini programs solve many "small tasks": tracking packages, ordering coffee, checking orders, playing a quick game. Fast loading times and unified access within WeChat are its biggest experiential features.

For enterprises and developers, mini programs are a "small application format" that can be searched for and shared. As long as you register on the WeChat Public Platform, configure your information, and pass review, your mini program can be open to all WeChat users. Compared with traditional apps, it's easier to get your first batch of users because people are already accustomed to doing many things within WeChat.

In this tutorial, we won't build a complex business system, but instead choose a classic example—a Snake game. It's small in size, has clear logic, yet contains all the elements a complete mini program needs: multiple pages, simple interactions, state changes, score recording, etc., making it very suitable as your first work.

## 1.2 WeChat Mini Program Development

Understanding "what a mini program is," the next question to answer is: What does developing a mini program actually involve?

You need to have a clear goal (e.g., make a Snake game that can be played anytime), design the interface that users will see, tell the system what should happen under different operations, and ultimately publish this work.

In traditional development workflows, these steps above are often led by programmers and require writing a lot of code. In AI-assisted development scenarios, this can be broken down more finely: you're responsible for clearly explaining what you want to do, and AI helps you complete most of the specific implementation. This means that for beginners, the most important skill is no longer how much syntax you memorize, but whether you can clearly describe requirements and understand the results AI gives you.

## 1.3 Several Methods for WeChat Mini Program Development

When actually making mini programs, the technical routes people adopt aren't entirely the same. To avoid you being overwhelmed by various terms right from the start, we'll only make a rough classification so you know what the common paths look like.

The first method is to directly use the native capabilities provided by WeChat. After creating a project in WeChat Developer Tools, you'll see a fixed set of file types used to describe page structure, styles, and logic. This approach is close to the official documentation and offers strong control, but for people new to frontend development, the learning curve is slightly steeper.

The second method is to use cross-platform frameworks like uni-app. You mainly write web-like code locally (such as .vue files), then the framework converts this code into a format that WeChat mini programs can recognize. The benefit is: the structure is more unified, and if later you want to publish your product to other platforms (like H5, apps), the changes will be relatively minor.

Based on the above two methods, this tutorial will focus on the mini program development SOP using AI-assisted development tools. For example, open the entire project in Trae, then directly tell the built-in AI assistant: "Please add a home page to this file with a title and button"—"Please write a game page for me that can display the snake and score." AI will generate new code snippets for you or help you modify and refactor, based on understanding the existing code.

These three methods aren't mutually exclusive. You can completely use a uni-app project and rely on Trae's AI features to complete most of the coding work. The key isn't which method you choose, but knowing: where you are now, and what tools are available to you.

## 1.4 WeChat Mini Program Development Steps Introduced in This Article (Rough Preview)

This tutorial will follow an **"from environment to finished product"** rhythm, centering specifically around the Snake example, combining Trae's vibecoding approach, and breaking the entire process into a route you can repeatedly reuse. Overall, you'll experience these stages in the following chapters:

1. First build the cognitive foundation: figure out what WeChat mini programs are, what common development methods exist, and who our Snake mini program is for and in what scenarios it will be used.
2. Then complete environment preparation: register a mini program account, install HBuilderX, Trae, and WeChat Developer Tools, and use HBuilderX to create a basic project skeleton that can run in WeChat Developer Tools, so a simplest page appears on the screen first.
3. Next enter formal development: open this project in Trae, dialogue with AI using vibecoding, step by step generate the layout of the home page and game page, and implement core gameplay like snake movement, eating food, and game over.
4. After the functionality works, learn to treat AI as a "debugging and refactoring partner": when you encounter bugs, ask it to help troubleshoot together; when you feel the structure is messy, let it help organize; and gradually add details like start/pause, high score recording, and interface fine-tuning.
5. Finally enter the release phase: build the project into a version WeChat can recognize, do preview and real device testing in WeChat Developer Tools, first go online as a test account and experience version to verify the process, and after completing filing and review, officially release the mini program so others can also search for and play your work in WeChat.

This section only paints the big picture and doesn't expand on specific commands and code. What you need to do now is just roughly remember these 5 steps: **Understand → Set up environment → vibecoding development → Debug and polish → Build and release**. The following chapters will slowly expand on each step, telling you what to prepare, what to say to AI, and what results you should see on screen at each stage.

# 2. Environment Preparation

Before writing a single line of code, let's get the development environment ready first. The goal of this part is to let you focus on dialoguing with AI and implementing requirements in later chapters, instead of struggling with **where to download software and why things won't run**.

You only need to know how to open a browser, download files, and double-click installers to complete all steps in this section.

## 2.1 Three Tools This Tutorial Will Use

For the development of the entire Snake mini program, we'll use three tools simultaneously, each responsible for different links:

1. The first is Trae. You can understand it as an AI-integrated code editor that can open project files like a normal IDE, and also lets you communicate directly with AI using natural language, asking it to help you write, modify, and explain code. In this tutorial, most "write mini programs with AI" operations will be completed in Trae. You can visit https://www.trae.cn in your browser to get the latest version.
2. The second is HBuilderX. It's an editor with particularly good support for Vue and uni-app, and the official team provides many ready-made mini program project templates. We'll use it to "one-click generate" a basic mini program project, equivalent to first laying the foundation, then handing the foundation to Trae and AI to transform. HBuilderX's download address is https://www.dcloud.io/hbuilderx.html.
3. The third is WeChat Developer Tools. This is a tool specially provided by WeChat for developing and previewing mini programs. It's responsible for running your written project on the computer and supports real device debugging on phones. You can download the version suitable for your operating system from https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html.

To summarize briefly: HBuilderX helps you quickly build a mini program project, Trae helps you write code with AI, and WeChat Developer Tools helps you see the mini program actually running.

## 2.2 Register a WeChat Public Platform Account and Get AppID

With tools, you also need a **mini program identity**, a step completed on the WeChat Public Platform. If you've never registered a WeChat mini program before, you can follow this order:

1. Enter https://mp.weixin.qq.com in your browser's address bar to open the WeChat Public Platform webpage, and log in by scanning the QR code with your WeChat.

![](images/image1.png)

2. Select "Mini Program" on the homepage, follow the page prompts to complete the registration process, and fill in your email, phone number, and entity type (individual or enterprise).
   ![](images/image2.png)
3. After successful registration and entering the backend, find the "Development Management" or "Development Settings" page, and you'll see a unique number called AppID. This number will be used later in project configuration, equivalent to your mini program's ID card in WeChat.

![](images/image3.png)

It's recommended that you record your AppID somewhere easy to find. In later chapters when configuring the project, we'll directly fill in this value to associate the local project with the online mini program.

## 2.3 Install WeChat Developer Tools

Next, we need a place to actually run and preview the mini program—this is the significance of WeChat Developer Tools.

1. Visit the download page https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html. On this page, you'll see multiple versions for different operating systems. Usually just choose the stable version that matches your computer system, such as Windows 64-bit or macOS version.
2. After downloading, double-click the installer and click next step by step following the installation wizard. If you're not sure what settings to change, just keep the default options.
3. After installation completes, launch WeChat Developer Tools from your desktop or start menu. On first launch, it will display a QR code on the screen, prompting you to scan with your phone's WeChat to log in. After scanning with your own WeChat and confirming authorization, you can enter the main interface.

![](images/image4.png)![](images/image5.png)

Later when we've prepared the project files in Trae, we'll import the built mini program into WeChat Developer Tools and see the actual running effect there.

## 2.4 Prepare Trae and HBuilderX

Finally, let's install the two tools actually responsible for writing the project: Trae and HBuilderX.

You can **install Trae first**. Open your browser and visit https://www.trae.cn, then download the version suitable for your system according to the page prompts. The installation process is the same as normal software—double-click the installer and complete following the prompts. After installation, you'll get an IDE that can open local folders, view code, and dialogue with AI. All subsequent vibecoding steps will happen here.

![](images/image6.png)

**Then install HBuilderX**. Visit https://www.dcloud.io/hbuilderx.html and select the distribution package for your corresponding operating system to download. HBuilderX's package is very small and starts up very fast. After installation, you can first familiarize yourself with its interface—no need to深入研究功能; in later chapters, we'll use it to create a uni-app mini program template as the starting point for the entire project.

![](images/image7.png)

After completing all steps in this section, you already have a complete development environment: a WeChat mini program account and AppID, a mini program runtime environment that can preview, and an IDE that can write code with AI. In the next part, we'll start from **creating the first mini program project skeleton** and really get these tools running.

## 2.5 Basic File Preparation

1. Click New Project

![](images/image8.png)

2. Select the default template, name the mini program, choose the storage path, and click Create in the bottom right:

![](images/image9.png)

3. Shows creation successful!

![](images/image10.png)

4. Then you can find this folder in the corresponding directory. Open this folder in Trae, and you can see all the foundation files have been built:

![](images/image11.png)

# 3. Mini Program Development

In the first two parts, we've figured out "what a mini program is" and "how to configure the environment and install tools." Starting from this section, we formally enter actual practice: no longer staying at the conceptual level, but letting AI really help you build the Snake mini program from scratch.

In this section, you'll complete a full SOP of the "development phase," which roughly includes several steps:

1. Open the current project in Trae and give AI your first complete instruction, letting it design and implement a runnable Snake version based on the existing skeleton.
2. Let Trae directly modify real project files instead of just giving you "example code," and learn to use the rollback function to restore to the pre-modification state when needed.
3. Return to HBuilderX and WeChat Developer Tools, and try playing this version in the simulator through "Run to Mini Program Simulator," achieving the switch from "code perspective" to "user perspective."
4. Based on trial results, continuously propose modification requirements using natural language, letting AI help you iterate from button control to joystick control, and by the way experience a closed loop of "discover problem → describe problem → AI fixes → verify again."

You can of course choose to figure out every page and every button clearly before development, then hand it to AI. But for complete beginners, mini program interface and interaction design is itself a brand new field (later we'll teach you how to use AI to help with design), so this time, we deliberately adopt another approach: **just start—let AI first generate a runnable version, then while watching the effect, gradually polish and adjust using natural language.**

## 3.1 Clearly State Requirements at Once: Give Trae the First "Master Instruction"

Open Trae and load the previously prepared mini program project. I didn't rush to modify a certain line of code, but instead said this to the built-in AI assistant:

**I "issue orders" to AI, saying I now need to write a Snake mini program based on the current framework. Please design this mini program and write a prompt for me.**

That is, I'm not "bit by bit asking it to write some function," but first throwing out a complete goal, letting AI help me plan, but AI not only helped me make a plan, but also directly landed the first version implementation.

After Trae receives this instruction, it will automatically read the current project structure, determine in which files to add pages and where to supplement logic, then directly make modifications to the files or code in the project, without you needing to hand-code or manually add/delete/edit files/folders.

## 3.2 Let AI Automatically Modify Code, Not "Hand-Craft"

When you click to execute this instruction in Trae, AI will enter a "help you modify the project" process. During this process, you can see several key points:

1. It will explain its approach in the dialogue area, such as which directory to add new pages under and how it plans to organize game logic.

![](images/image12.png)![](images/image13.png)

2. It will directly make additions/deletions/changes to real project files, instead of just giving you a piece of "example code" for you to copy yourself.
3. After modifications complete, Trae will generate a brief summary telling you: which files it changed this time and roughly what it did.

If you're not satisfied with this round of modifications (or feel something is wrong with a step), no need to panic. Trae provides a "rollback" capability in the upper left corner outside the dialogue box where you issued the conversation. You can one-click restore the project to the state before this instruction executed, equivalent to adding a safe undo key to this operation.

![](images/image14.png)

![](images/image15.png)

## 3.3 View Effects in HBuilderX and WeChat Developer Tools

After AI completes the first round of development, the code has landed in the project, but at this point you haven't seen the effect from the player's perspective yet. Next, we need to run it.

The specific approach is: return to HBuilderX, find the "Run" option in the top menu, and select "WeChat Developer Tools" under "Run to Mini Program Simulator." This operation triggers project compilation and hands the result to WeChat Developer Tools to open.

![](images/image16.png)

The output window at the bottom will show the compilation process. If the final status is "ready" and there are no errors, it means the build succeeded, and you can switch to WeChat Developer Tools to view this version of the mini program's interface and functionality.

![](images/image17.png)

In most cases, HBuilderX will automatically open WeChat Developer Tools for you, letting you directly see the new mini program. If it doesn't open automatically, you can handle it this way:

1. First stop the current run in HBuilderX.
2. Manually launch WeChat Developer Tools and keep it open.
3. Return to HBuilderX and click "Run → Run to Mini Program Simulator → WeChat Developer Tools" again.

This way we can see our Vibecoding mini program in WeChat Developer Tools:

![](images/image18.png)

## 3.4 Repeatedly Adjust and Refine the Mini Program Using Natural Language Until Satisfied

In this practice, AI initially generated for me a Snake with button-controlled direction: four direction buttons on the screen, clicking different directions changes the snake's movement direction. Functionally it's completely playable, but I personally prefer joystick control. For your adjustment needs (not limited to functionality, UI design, interface—when you're proficient, you can even use natural language to have AI help you access other large model APIs or databases)—let me emphasize again: you just need to tell the large model in natural language.

This is where vibecoding's advantage lies: you don't need to dig through the code yourself, find where events are bound and the logic for calculating coordinates, but just directly tell AI your ideas. For example, you can describe it this way in Trae's dialogue box:

  Replace buttons with joystick control, and when the user releases the joystick, the snake continues moving in the same direction until the user releases the joystick again.

As long as you clearly describe the requirement, AI will automatically locate the corresponding interface and logic files, and complete control style, interaction binding, and direction handling modifications for you.

![](images/image19.png)

After modifications complete, return to WeChat Developer Tools to view. If you don't immediately see changes, try clicking the "Run" button on the developer tools or refreshing the mini program preview window to let the latest build take effect. If still no update, you can first stop running in HBuilderX, then execute "Run to Mini Program Simulator" again to see the adjusted mini program:

![](images/image20.png)

## 3.5 What to Do When Problems Arise: Continue Communicating in Natural Language

The version AI generates won't necessarily be perfect from the start. Sometimes you'll encounter these situations:

* Runtime errors, mini program cannot open normally;
* Functionality is roughly correct, but details differ from what you imagined;
* The interface works, but you feel it could be more beautiful or smoother.

In these moments, no need to dig into the code and make blind modifications yourself—just directly describe the encountered problems to the AI assistant in Trae using natural language, for example:

  Now joystick control is working, but sometimes the snake suddenly stops moving. Please help me check what's wrong with the current implementation. Or: Now the game is playable, but the interface is a bit crowded. I want more whitespace at the top and bottom when displaying on phone. Please help me adjust the layout.

AI will give modification suggestions based on your current project state and description and directly apply them in the code. If after modification the result is worse or the direction is wrong, you can still use rollback to restore the project to the previous stable version, then try a different phrasing.

Through these rounds of back and forth, you'll gradually polish from the initial "rough version" to a joystick-controlled Snake mini program closer to your preferences. For example, I gave a picture style and let AI adjust the mini program's UI style according to this style:

![](images/image21.png)

## 3.6 Final Product and Summary of This Section

After round after round of **natural language description → AI modification → preview in WeChat Developer Tools → continue dialogue for fine-tuning**, I finally obtained this finished product:

* Complete game page;
* Snake can move smoothly and eat food;
* Supports joystick control;
* Runs smoothly in mini program simulator.

Final development product as follows:

![](images/image22.png)![](images/image23.png)![](images/image24.png)

In this section, you've seen a complete closed loop:

1. Use one clear instruction in Trae to have AI build the first version of the Snake mini program;
2. With the help of HBuilderX and WeChat Developer Tools, check actual effects from the user perspective;
3. Repeatedly propose modification requirements to AI using natural language, letting it complete functionality adjustments and interface optimization for you;
4. When problems appear at any step, ensure safety through rollback and rerunning.

Next, you can follow the same rhythm to try your own ideas: not necessarily Snake, could also be a tool mini program, an activity page, or even a business prototype you really need in your work. Your main task is to think clearly and speak clearly about requirements—leave the rest to AI and these tools to complete together.

# 4. Mini Program Release

In the first three chapters, we've completed the entire process from **setting up environment**—**developing with AI** to **running Snake in the local simulator**.

Starting from this chapter, our concern becomes: **how to really hang this work on WeChat, not just as a small toy, but as a WeChat mini program everyone can use?**

To lower the barrier, we'll first take a **shortest closed loop**: only let it go online in **test account** form, first for yourself and a few classmates to experience; when you feel the functionality and experience are stable enough, then go through the formal launch process.

This chapter first covers 4.1, helping you complete the **test account launch** shortest path; formal launch for all users will be expanded in 4.2.

## 4.1 Shortest SOP — Test Account Launch

The goal of this subsection is only one: to let you really open your own Snake mini program in WeChat in **experience version** form.

The entire process can be understood as four things:

1. Find and confirm your AppID on the WeChat Public Platform.
2. Configure this AppID in the project.
3. Upload the current version using WeChat Developer Tools.
4. Return to the public platform and set this uploaded version as "experience version."

Let's follow this order to go through it once.

### 4.1.1 Confirm AppID on WeChat Public Platform

The first step is to confirm your mini program's AppID on the WeChat Public Platform.

You already did this once in **2. Environment Preparation**—here we're really putting it to use.

1. Open your browser and visit `https://mp.weixin.qq.com`, log in to your mini program backend.
2. Find "Development Management" in the left menu, enter "Development Settings."
3. At the top of the page, you'll see an area called "Developer ID," inside which there's a line "AppID (Mini Program ID)"—this is your mini program's unique number.

This number needs to correspond one-to-one with the configuration in the project, otherwise WeChat will think you uploaded "someone else's mini program" and naturally cannot preview and publish normally.

![](images/image25.png)

### 4.1.2 Fill in AppID in Project

The second step is to write this AppID into your project configuration, associating the locally built mini program with this "account" on the public platform.

If you're using a uni-app template for your project, you can operate this way:

1. Open HBuilderX and load your Snake project.
2. Find `manifest.json` in the left file tree and double-click to open.
3. Scroll down to the "WeChat Mini Program Configuration" section, and you'll see an input box prompting something like "WeChat Mini Program AppID (please get in WeChat Developer Tools)."
4. Paste the AppID you just saw on the public platform as-is, and save the file.
   ![](images/image26.png)

At this point, your local project has claimed this mini program identity. Next, as long as you upload a version through WeChat Developer Tools, it will be recorded under this AppID.

### 4.1.3 Upload a Version in WeChat Developer Tools

Previously we used HBuilderX to run the project into WeChat Developer Tools and saw the effect in the simulator.

Now what needs to be done is: in the developer tools, "package" the current code and upload it to the server.

The general steps are as follows:

1. In the top right of WeChat Developer Tools' top toolbar, you'll see an "Upload" button—click it.
2. In the pop-up window, you need to fill in two key fields:
   1. Version number: e.g., `1.0.0`, only numbers and decimal points allowed.
   2. Project notes: write a brief description, such as "Completed basic functionality development."
3. After checking everything is correct, click the "Upload" button. The output area below will show the compilation process. When all steps turn green and prompt upload complete, it means this version has been successfully submitted to WeChat servers.

![](images/image27.png)

![](images/image28.png)

![](images/image29.png)![](images/image30.png)

### 4.1.4 Set Version as Experience Version in Management Backend

Uploading just delivers the code to WeChat's side—it doesn't yet tell the system "this is an experience version available for trial."

The last step, we return to the public platform's mini program backend to complete this loop.

1. Open `https://mp.weixin.qq.com` again and enter your mini program backend.
2. Find "Version Management" under "Management" in the left and click to enter.
3. In the "Development Versions" section of the page, you should see the version you just uploaded: version number is `1.0.0`, notes are what you wrote, time is just now's upload time.
4. On the right side of this row, there will be a dropdown button or action button where you can select "Set as Experience Version." After clicking, confirm the operation. Note that before this step, please ensure you've already set your main business category in Home-Mini Program Category.

   ![](images/image31.png)

   ![](images/image32.png)

After completion, this version becomes your mini program's "experience version." You can generate an experience version QR code in the backend, and can also add yourself and colleagues as "experience members," letting everyone scan with WeChat to experience this Snake mini program on real devices.

At this point, we've completed the shortest closed loop from local project to test account launch:

You don't need to be open to all WeChat users from the start—just in a safe range, let a real mini program run in the real WeChat environment. This is enough for you to test functionality, collect feedback, and continue iterating.

## 4.2 Mini Program Official Launch

After the experience version works, you can already play this Snake mini program in your own WeChat. What needs to be done next is to advance it from a state only a few experience members can use to a formal WeChat mini program everyone can use.

Break this into several steps: first supplement information, then select category, complete filing, and finally submit for review. Let's follow this order to go through it once.

### 4.2.1 Enter Mini Program Release Process

First return to the WeChat Public Platform backend and log in to your mini program account. Find the entry related to "Version Management / Release" in the left navigation (the interface may vary slightly at different times)—after expanding, you'll see the "Mini Program Release Process" item.

After clicking to enter, a progress bar will display at the top of the interface, with several steps listed below, such as:

1. Mini Program Information
2. Mini Program Category
3. Operational Information / Mini Program Filing
4. WeChat Certification (depending on your entity)

Initially progress will show 0%, and as you complete each step, the system will automatically move the progress forward.

![](images/image33.png)

### 4.2.2 Fill in Mini Program Basic Information

The first step is to complete the mini program's "business card"—this is also the content users will first encounter when seeing you in WeChat.

On the "Mini Program Information" page, you usually need to fill in and confirm the following:

1. Mini Program name This name will appear in search results and at the top of the mini program, has length limits, and needs to comply with WeChat's naming specifications. It's recommended to choose a name that both expresses functionality and is easy to remember, such as "Snake vibecoding version."
2. Function introduction / brief description Use one or two sentences to explain what this mini program does, such as: "A Snake game developed with AI assistance, suitable for playing a round in fragmented time." Note the description should be consistent with actual functionality, avoid using exaggerated promotional language.
3. Icon and display images
   1. Icons generally require square images, support PNG/JPG and other formats, have clear limits on size and pixels (per page description), it's recommended to provide a clean, high-contrast image.
   2. Display images can upload several screenshots of mini program pages, such as home page, game page, settings interface, etc. These will appear in the detail page helping users understand the content.
4. Other necessary information Such as tags, service area, etc., fill in according to page prompts. The principle is only one: all filled content should match the real functionality of this Snake mini program.

![](images/image34.png)

After filling everything out, click save or next step, and the first step in the release process is complete.

### 4.2.3 Select Mini Program Service Category

After completing basic information, the wizard will guide you into the "Mini Program Category" step. Category can be understood as the mini program's "classification" in WeChat, determining which type of application it's grouped under during review, and also affecting subsequent display and operation.

![](images/image35.png)

On this page, you'll see an "Add Category" button. After clicking, you can choose the direction suitable for your mini program from the system-provided category tree, such as:

![](images/image36.png)

1. First select the "Education" major category;
2. Then choose more specific sub-categories like "Educational Tools / Teaching Assistance" below. This time I chose Educational Equipment, treating it as teaching aids for everyone to learn Vibecoding~

In your own project, you just need to choose the item most suitable for actual use.

![](images/image37.png)

![](images/image38.png)

After confirming the category, click save. If the page prompts "Category created successfully" and displays the item you just added in the list, it means this step is complete.

### 4.2.4 Complete Mini Program Filing Information

Next, the release process will require you to complete the "Operational Information / Mini Program Filing" section. This step is to verify the mini program's entity identity, ensuring the launched application has clear responsible persons.

![](images/image39.png)

Under an individual entity example, you'll roughly go through these actions:

1. Select filing type The page will have you choose between different entity types, such as "Individual" "Enterprise" etc. Keep it consistent with the entity when you registered the mini program.
2. Fill in entity information Including name, ID type, ID number and other basic information. This part needs to be consistent with registration information, otherwise it may be rejected during review.
3. Upload proof materials The page will usually require you to upload ID photos or other proof documents. Specific format, clarity, and size requirements will be written in the instructions. After preparing images according to prompts, upload them ensuring content is clearly identifiable.
   ![](images/image40.png)

After submission, the system will enter "Under Review" status, and the page will display a prompt like "Information submitted, please wait patiently." This process may take some time, and you can check filing progress in the backend at any time.

![](images/image41.png)

### 4.2.5 Submit Review and Wait for Official Release

When "Mini Program Information," "Mini Program Category," "Operational Information / Filing" and other steps are all checked complete, you can perform the last action: submit for review.

1. Return to the "Mini Program Release Process" overview page, confirm each item shows as completed, progress bar near 100%.
2. According to page prompts, click "Submit Review" or similar button to submit the current development version to WeChat team for review.
3. In "Version Management," you'll see this submitted version's status become "Under Review." After passing, it will become "Published" or you can choose "Go Online" status.

If filing review doesn't pass, they'll call the developer and prompt which parts didn't pass.

For filing, you'll receive a verification code and verification link from "Ministry of Industry and Information Technology"—click to enter and fill in the verification code and personal information (verification validity is 1 day). When filing passes, you'll receive email and SMS notification from "Ministry of Industry and Information Technology" informing you of the filing number. WeChat certification: individuals pay 30 yuan, companies/enterprises seem to pay 300 yuan, fees aren't refunded regardless of whether certification passes. You'll receive certification notification and a call to confirm information.

Submit for review, upload operation video and pages, fill in information and submit—click "Submit Release" and it's officially released

![](images/image42.png)

# 5. Summary

At this point, you've completed a full **0 to 1** mini program development closed loop: from knowing WeChat mini programs, to installing Trae, HBuilderX, and WeChat Developer Tools; from throwing ideas to AI and having it "move bricks" in code for you, to trial-playing the first version of Snake in the simulator; then to packaging the work as an experience version, completing filing and review, and really having people use it in WeChat—you've personally walked through this entire chain.

More importantly, you didn't achieve this by memorizing syntax, but by clearly expressing requirements and communicating effectively with AI. You've experienced that **one natural language instruction can let AI perfectly meet your development requirements**. This ability won't stop at Snake—it can transfer to any mini program you want to make in the future—tools, activity pages, educational applications, or even real projects in your work.

If I were to give you a **general SOP**, it's actually just five steps: **think of a small requirement → build project skeleton in Trae → use vibecoding with AI to build first version → keep trial-playing and improving in WeChat Developer Tools → upload, filing, review, launch**. Each time you repeat these five steps, you'll have one more mini program that can really be opened and shared by people, and one more piece of confidence in "I can use AI to turn ideas into products."

Next, you can continue polishing this Snake, or close it and start a new empty project from your own ideas. Whatever you do, just remember one thing: you're no longer just someone who "wants to make something," but a vibecoding developer who's been through the full process. The rest is just doing it a few more times and making this ability a habit.

# References:

- https://zhuanlan.zhihu.com/p/1889401120939567074
- https://blog.csdn.net/2401_87407347/article/details/155193007
