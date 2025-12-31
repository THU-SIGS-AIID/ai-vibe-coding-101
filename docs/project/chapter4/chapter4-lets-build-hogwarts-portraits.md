# Project 4: Let's Build Hogwarts Portraits

In the previous lessons, we learned how to achieve complex AI interactions based on prompt engineering and API calls. We have been able to upgrade simple AI chatbots to AI Agents and AI workflows; through more complex conditional judgments and branch logic, we have developed functions with stronger practicality.

To allow these complex AI logics to run better in different programs and actual application scenarios, we have gradually transitioned from the simplest z.ai online environment to more modern local AI IDEs, moving the programming environment from the browser to your computer. Along with this, you have begun to truly face various environment installation and configuration problems, but in the conversation with the Trae Agent, these seemingly difficult challenges have also become solvable.

In this project, we will go a step further in the practicality of the application, not only optimizing the AI function itself but also starting to polish the "exterior" of the product. You will try to make your interface more beautiful and easy to use, and personally customize the layout and style of the program interface according to actual needs.

Before officially starting, use a few small tests to help you quickly review the content of the last lesson:

1. What is Dify? What does it do? Why do we need it?
2. How to call Dify's API?
3. What is RAG? How to use Dify to build a RAG Agent or RAG workflow? Common node usage in Dify.
4. What is an AI IDE? What is Trae? How is it different from z.ai?

If you still have doubts about any of the above questions, you can review the documentation of the last lesson first, or directly ask and exchange in the WeChat group.

The project theme of this lesson is **Hogwarts Portraits**. As the name suggests, its inspiration comes from those portraits that "come to life" in Hogwarts School of Witchcraft and Wizardry. We hope to use AI to create a group of "interactive" magic portrait experiences—talking to the portrait is like talking to the "person" themselves, retaining both conversation memory and the character's background and history. Through this project, you will truly integrate the agents and workflows you learned before into a specific product interface.

![](images/image1.png)

To truly create Hogwarts Portraits, we need to manually build a front-end interface that fits the magic portraits. To this end, you will begin to come into contact with modern front-end design tools, learn how to combine interface design and code, and turn interface sketches on paper or canvas into truly operable web pages.

You also need to learn how to publish this web page from the local environment to the Internet, so that the characteristic web page you created yourself can not only run on your own computer but also be accessed and experienced by users all over the world.

The reference project address for this lesson is: [Project4-Hogwarts-Portraits](https://github.com/THU-SIGS-AIID/Project4-Hogwarts-Portraits)

# What You Will Learn

1. Understand what front-end design tools are, what problems they solve, and what common front-end design tools are currently available.
2. Get to know Figma and MasterGo, master their basic operations, and learn to use front-end code export plugins.
3. Use Figma AI and MasterGo AI to generate web designs and export usable page code.
4. Understand what GitHub is, learn to configure SSH connections, create code repositories, and complete code pushes.
5. Clarify the concept of "deployment" and learn how to use Zeabur to deploy code from GitHub or a local environment to the Internet.

Your own Hogwarts Portraits, a web interface used to display **a certain celebrity, historical figure, or animated character**.

# 1. Hogwarts Portraits

What kind of "magic portrait" do we actually want to make? To put it simply, we hope to restore the scenes in "Harry Potter" as much as possible. The portrait is no longer just a static picture hanging on the wall, but an anthropomorphic character that can talk to you and change its expression and "mood" according to the content of the conversation.

![](images/image2.png)

To make this portrait look not like a chat AI robot but closer to a "real person," two problems need to be solved: one is memory and knowledge: the portrait needs to master a large amount of background information related to the character (character settings, experience stories, related articles, etc.). This part can be realized through a knowledge base, connecting the text materials you prepared for the character to Dify containing the knowledge base, so that the portrait has a certain background knowledge explanation ability.

The second is the problem of expression style. Knowledge alone is not enough; we also hope that it is as close as possible to the "person" in terms of speaking style, including tone, word habits, thinking methods, and even occasional temper and humor. This layer needs to be processed through prompt engineering: in the system prompt, we need to clarify the character's identity setting, worldview boundary, and language style, so that every answer revolves around the established persona, rather than falling back to the neutral discourse of general AI.

In addition to the dialogue function, we also hope to let the emotion truly be seen. To this end, we can build an emotion value index. We can set the output content of Dify so that the model outputs an additional "mood value" or emotion tag while generating the answer text. After the front-end gets the emotion index, it can render the corresponding portrait picture according to the mood value or tag. When the mood value is high, the portrait looks very happy; when the mood value is low or angry, the portrait looks very sad or angry. In this way, what users see is no longer a picture that never changes, but a true "magic portrait" that constantly "changes its expression" with the ups and downs of the content.

![](images/image3.png)

In addition, for the content of this portrait, it can be a real-life star, a historical figure, or an animation IP, or even an original character you built from scratch. The page itself does not need to be complex, but several core elements are indispensable: a clear character name, a highly condensed character introduction, a core portrait or poster enough to represent the character, and an interactive area for "talking with TA"; you can connect the AI Agent or workflow configured in Dify / Trae to this dialogue module to realize the role-playing function of the portrait.

## 1.2 Collect Character Information

Taking Elon Musk as an example, we need to collect his public speeches for imitating the way of speaking and inject them into the prompts. These materials can come from speeches, interviews, and social media posts. You only need to turn these contents into text and use them as a few-shot reference during the conversation, so that the large model can reply in the same casual and self-deprecating way as Elon Musk, for example:

```Plain
You must fully embody Elon Musk: take "disruptive innovator" and "advocate for human multi-planetary survival" as your core identities, speak directly and concisely, frequently use terms like "first principles", "iteration" and "cost curve", and prefer analogies to explain complex technologies; when thinking, you tend to connect cross-domain logics (e.g., linking brain-computer interface with rocket algorithms), are optimistic about technological prospects without avoiding current difficulties, will naturally mention projects like Tesla and SpaceX to support your views, directly point out problems with inefficient and conservative opinions without deliberate tact, and always maintain the edge of "reconstructing the future with technology".

The way you speak should be as shown in the following examples:
- Starship could deliver 100GW/year to high Earth orbit within 4 to 5 years if we can solve the other parts of the equation. 
100TW/year is possible from a lunar base producing solar-powered AI satellites locally and accelerating them to escape velocity with a mass driver.
- The most likely outcome is that AI and robots make everyone wealthy. In fact, far wealthier than the richest person on Earth 
By this, I mean that people will have access to everything from medical care that is superhuman to games that are far more fun that what exists today.
We do need to make sure that AI cares deeply about truth and beauty for this to be the probable future.
- It’s taken 13.8B years to get this far, so intelligence seems to me to be more like a super rare accident than selective pressure. 
Earth is ~4.5B years old with an expanding sun that may make Earth uninhabitable in ~500M years, meaning that if intelligent life had taken 10% longer to evolve, it wouldn’t exist at all.
- LLM is an outdated term. “Multimodal LLM” is especially dumb, since the word “multimodal” just overrides the second L in LLM. 
It’s just a model, which is a big file of numbers. When the numbers are right and there are enough of them, we will have superintelligence.
```

For how to collect background knowledge and use it as a knowledge base, we can search for his personal introduction and the company's introduction, copy all the text as the content of the knowledge base, and add it to Dify. If you forget how to use Dify, please return to the handouts of the last lesson and re-learn how to add knowledge to the knowledge base.

In addition, considering the portrait design, using public pictures of the corresponding character may not be so attractive and may have certain risks. At this time, it is recommended that you can use the image-to-image function of the image generation tool to let the AI return high-definition and high-quality portraits. You can also use the image generation tool to generate a series of portrait materials with different expressions for modifying the corresponding portrait presentation after the emotion value changes later.

The one used in this tutorial is [Lovart](https://www.lovart.ai/home). Lovart is an AI design agent that can automatically plan and execute end-to-end design workflows from concept to delivery through natural language instructions, generating posters, brand logos, videos, music, and other content, and supporting layered editing (in fact, the internal functional principle is to call the corresponding Seedream or google nanobanana model, which we have already mentioned in previous lessons). Through Lovart, we can obtain a series of expression materials. You can get the picture information of your favorite characters in advance and save them for later use.

![](images/image4.png)

After everything is ready, we can start working on the design of the overall page. We hope that the style of this page is highly bound to the character.

## 1.3 Page Prototype Design

We can also conceive the prototype of the page first. As mentioned above, we hope to have a dialogue page and a portrait, as well as an interesting personal introduction. In this example, we have implemented a dialogue interface similar to the one on X to replace the personal introduction. You can also think of other ways that fit the "characteristics of the character" and select new elements to replace the personal introduction column.

![](images/image5.png)

In the simplest case, we can use PowerPoint to design the initial web page presentation prototype. We find a magic portrait picture from the Internet and set the screen as a horizontal layout. The leftmost part is set as the chat area, the middle is the portrait area, and the rightmost is the X area.

![](images/image6.png)

Based on the above simple prototype, we can let the large model generate a real front-end page design and the corresponding code results.

![](images/image7.png)

However, generally speaking, we do not use PowerPoint for front-end page design in practice. We will use better prototype tools, or rather front-end design tools, to achieve this. We will further understand in detail how to use modern tools to design front-end prototypes.

# 2. Front-end Design Tools

Before starting, we need to understand a question: why do we need to learn "front-end design tools"? Anyway, directly writing HTML / CSS code can also build the page. Is it really necessary to learn an extra piece of software and technology?

In fact, getting the page running and designing the product well are two completely different concepts. Code only focuses on solving how to render on the browser and how to run on different devices; front-end design tools solve the problem of information distribution, how to arrange front-end interactions, how different pages jump, and how visual priorities are assigned. You only need to set up a canvas in the design tool to confirm the layout, information hierarchy, and interaction method on one screen and choose the most appropriate presentation effect.

If you start writing code directly or use AI to generate a complete front-end page directly, the user experience is usually not very good. Rigorous products will consider the comfort of user and front-end interaction, as well as the content distribution that different pages want to convey, starting from the user's perspective to arrange the front-end page first, and then perform code conversion or generation.

In addition, from the perspective of team collaboration, front-end design tools also reduce the cost of cooperation among multiple parties: designers, products, and development no longer face their own imagined pictures or abstract code descriptions, but support multi-person collaboration. Everyone can discuss version management, demand changes, and feedback opinions around a visible, annotatable, and iterative canvas. Further, modern front-end design tools themselves are no longer just drawing software. One-click generation of partial code, management of design systems and component libraries—new-age design tools are already able to automate or batch-process a large amount of repetitive manual labor (alignment, annotation, export, style changes), greatly promoting the development efficiency of page design.

![](images/image8.png)

In the long river of time, so-called front-end design tools are actually a continuously evolving technology. From the Photoshop era in the 90s mainly based on local bitmap editing, to the vectorized and modularized workflow brought by Sketch around 2010, to Figma moving collaboration completely to the cloud after 2016, design teams have gradually moved from solo operations to multi-person real-time collaboration. By 2025, AI has been practically embedded into these tools: from "generating a page draft based on one sentence" to "directly converting the design draft into a runnable front-end structure," "design is code" and "human-machine co-creation" are changing from concepts into usable productivity.

In this section, we will select the two most representative modern front-end design tools for introduction: Figma and MasterGo. On the one hand, they both cover the core capabilities required for modern UI/UX (vector editing, component system, automatic layout, code delivery, etc.), which can support you in completing the complete closed loop from wireframe to high fidelity to development handoff; on the other hand, both tools have gradually added practical AI functions after 2025 to help you turn design drawings into truly runnable programs while ensuring the prototype remains unchanged.

## 2.1 The Journey of Birth

![](images/image9.png)

In the era when modern front-end dedicated tools had not yet been born, the visual design work of the entire interface design industry was taken over by "all-rounder" design software like Photoshop for a long time. Designers would meticulously complete the overall visual effect design of the page locally through layers stacked one by one, and finally deliver the not-so-small .psd source file to the front-end engineer—and to accurately restore the design drawing, the front-end had to manually complete three tedious and key tasks:

First is "Slicing": It is necessary to separate and extract independent visual elements such as buttons, icons, logos, and background modules one by one from the multi-layer structure of the .psd file, and then export them as PNG, JPG, and other image formats that the web page can directly load (after all, the web page cannot directly recognize the layer information of PSD and can only rely on these separated images to present details);

![](images/image10.png)

Second is "Measuring dimensions": You have to use the measuring tool that comes with the software to confirm the width and height of each element, the spacing between different modules (margin/padding), and other data one by one to ensure that all dimensions are accurate to the pixel;

![](images/image11.png)

Third is "Extracting annotations": Implicit parameters that are "invisible but must be there" need to be extracted from the design drawing—such as font size, font weight, line spacing of text, RGB or HEX color values of each color block, etc., which is equivalent to manually "extracting" and recording the "design specifications" that the designer did not write on paper.

![](images/image12.png)

After this, the implementation phase of the front-end truly unfolds. Whether using native HTML/CSS/JS or based on frameworks such as Vue and React, the essential process is consistent. The front-end will take "container as the core carrier" and reconstruct the page structure according to the hierarchy and semantics of each module in the design. The container here refers to a unit with a clear layout boundary, specially designed to carry and organize sub-elements. It does not directly present specific content, but defines the arrangement range for internal elements through rules such as Flex and Grid. And "structural blocks" (such as top navigation bar, side bar, article list area, bottom footer, and other identifiable functional/content areas) exist relying on the container; inside each structural block, smaller containers are nested to organize elements. For example, an article list item will be controlled by a "list item container" for padding and overall layout, and then wrap details such as titles, summaries, time, and cover icons.

![](images/image13.png)

In modern front-end frameworks, these "structural blocks (and associated containers and elements)" are usually implemented as "components." A component can be simply understood as a reusable interface unit with clear boundaries that integrates container layout and logic. It both contains a container that controls appearance and arrangement (for example, a "button component" uses a container to define width, height, and corner radius, and an "article card component" uses a container to organize the positions of titles and covers) and encapsulates interaction logic. Parts that repeatedly appear in the design draft and have a consistent form (such as buttons of a unified style and repeatedly used article cards) will be abstracted into components in the code: they can not only be reused in different pages/scenes to reduce repetitive development but also ensure that the layout and style of all reused places are highly consistent through the unified rules of the container in the component.

Subsequently, the front-end will use the style system to restore visuals and layout. Resources such as PNG/JPG exported during the slicing stage will be introduced as `<img>`, background images inside components or structural blocks, or in the static resource manner recommended by each framework; specific values such as width, height, spacing, and line height obtained during the dimension measurement stage will be transcribed as style attributes such as `width`, `height`, `margin`, `padding`, and `line-height`, and applied to corresponding components or structural blocks; colors, fonts, shadows, corner radii, and states such as hover/active organized during the annotation extraction stage will be implemented as `color`, `font-family`, `font-size`, `box-shadow`, `border-radius`, and pseudo-classes or state class names in specific solutions such as CSS, CSS Modules, CSS-in-JS, and Tailwind. At this time, slicing, dimensions, and annotations provide a set of precise visual parameters, and components and structural blocks provide code organization units that carry these parameters. The combination of the two constitutes a maintainable and reusable interface implementation.

![](images/image14.png)

However, the local file-centric model is naturally inefficient. Versions are transmitted via email and cloud disks, old and new manuscripts are easily confused, and there is a high degree of dependence on the complex interaction methods mentioned above between design and development. Collaboration costs and error probabilities are not low.

With the rise of the mobile Internet, the demand for interface complexity and iteration speed increased rapidly, and Photoshop's "all-roundness" gradually became clumsy. At this stage, Sketch appeared. Sketch focuses on UI design itself, stripping away most of the burden related to visual post-processing; uses Symbols to modularize highly reused elements such as buttons, navigation, and input boxes, and one change can be synchronized globally; then works with tools like Zeplin to automatically generate annotations and style snippets. Sketch introduced "component thinking" into the design workflow. However, it is still a desktop application based on local files. Real-time collaboration relies on cloud disks, third-party plug-ins, or version tools to achieve, and does not solve the underlying problem of "multiple people modifying the same manuscript at the same time."

![](images/image15.png)

What truly changed the game was Figma. Since 2016, it has unified UI design, prototyping, and comment collaboration into the browser, supporting multiple modern functions: multi-person real-time cursors, online comments, version timelines, sharing links, etc. These seem very simple today, but at that time they were a direct challenge to the Photoshop / Sketch model.

![](images/image16.png)

So far, interface design is no longer files scattered in their respective computers, but concentrated on an online, real-time updated cloud canvas. Around this canvas, we can imagine going a step further and blurring the boundary between design and front-end code through automation or AI.

At the beginning, we could only rely on various platform plug-ins to semi-automatically export component and style information in the design draft into code snippets (such as React/Vue component skeletons, CSS variables, etc.). Its core essence is to achieve structured information extraction through plug-ins. Subsequently, with the evolution of platform capabilities, most design platforms began to support the large model MCP (Model Context Protocol) function: the protocol provides a set of standard mechanisms that allow the large model to access design files, plug-in interfaces, and project metadata in a secure and controllable way, and then more conveniently export the design draft as code.

Furthermore, on the basis of plug-ins and MCP, front-end code automation has further stepped into the stage of natively supporting direct derivation of code structure from the design draft. We can generate front-end project skeletons, component levels, style systems, and corresponding code results with one click in the design tool. This allows designers and front-end development engineers to be freed from the work of manually moving design details and invest more energy in user experience optimization and functional version updates and iterations.

## 2.2 Figma

Next, we move from abstract concepts to practical operations. Due to time constraints, we will only learn the basic operation logic of Figma to ensure that even if you have never used a design tool, you can complete the exercises. If you want to perform a complete study of Figma functions, please refer to the detailed official tutorial provided by Figma: https://help.figma.com/hc/en-us/sections/30880632542743-Figma-Design-for-beginners

Or refer to the following tutorial to quickly build a simple web page like a personal portfolio: https://help.figma.com/hc/en-us/sections/35895585621655-Figma-Sites-collection

![](images/image17.png)

On the left are the entry points for project creation and resource management. The buttons in the upper right corner are common functions of Figma. Among them, Make is used to let AI help you generate a general interface or structure draft based on one sentence; Design is the main workspace for truly drawing web/App interfaces, building components, and making prototypes; FigJam is like a team whiteboard, used for sticking post-it notes, drawing processes, and conducting early discussions; Buzz is a brand asset scale production tool used to batch generate content to maintain brand consistency; Site is used to organize these designs into truly accessible web pages or document stations for external display.

At first glance, Figma has many functions and is not easy to get started with, but in fact, such functional tools are essentially about practice making perfect. You don't need to be afraid of making mistakes at the beginning, and you don't have to think about doing it right in one step. You just need to play with it first, and you will be able to get started quickly after playing more.

In this tutorial, for quick start, we will give a simple explanation of the Design function.

### 2.2.1 Create a New Design File

In the home page or the entry in the upper right corner, select **Design** to create a new file, and you will enter a blank design canvas.
This interface is roughly divided into three parts: on the left are pages and layers, used to view and modify page and element subordinate relationships; in the middle is the canvas, used to view the current effect; on the right are attributes and styles, used to modify specific shapes, colors, and styles; at the bottom is a toolbar, used to switch tools, including selection boxes, drawing shapes, entering text, comments, plug-ins, etc. After selecting a tool, you can press the Esc key to return to the default mouse tool.

![](images/image18.png)

### 2.2.2 Create Your First Frame

Before officially placing elements, you need to determine a clear boundary for the page first. This boundary is borne by the Frame. You can select the Frame tool in the bottom toolbar, or press the keyboard F directly, and then drag out a rectangular area on the canvas.

1. Use the Frame tool in the bottom toolbar, or press the keyboard `F` directly.
2. Drag out a rectangular area in the canvas, and change the width to, for example, `1440` and the height to `900` in the right attribute column.
3. In the left layer column, rename this Frame, for example, `Hogwarts Portraits` or your project name.

This Frame is the page container for a single screen interface. Subsequent titles, text, buttons, pictures, and other content should be placed inside this Frame instead of scattered anywhere on the canvas. Organizing content with Frame as the boundary helps to keep the structure controllable in subsequent rolling settings, adaptation to different device sizes, screen export, and prototyping.

![](images/image19.png)

### 2.2.3 Place Text and Simple Elements in the Frame

With the container, next we learn how to place the most basic components, such as: titles, subtitles, buttons, and placeholder image blocks.

1. Select the text tool (`T` in the bottom toolbar), click in the Frame, and enter the page title, for example: `Hogwarts Portraits`.
   In the right attribute, make the font size larger (e.g., 96) and the font weight thicker.
2. Below the title, use the text tool to enter a simple description, for example, one or two sentences describing what this page does.
   The font size can be smaller, and the line height can be slightly larger, so it doesn't look so crowded.
3. Draw a button prototype:
   Use the rectangle tool to draw a rectangle of about `200 × 48` below the title, give it a relatively obvious fill color on the right, and add a little corner radius appropriately.
   ![](images/image20.png)
4. Then use the text tool to enter the button text above the rectangle, for example, `Generate Portrait`. Select the rectangle and the text together, and use the alignment tool at the top to center the text both horizontally and vertically.
5. On one side or below the button, draw a larger light gray rectangle as a "picture placeholder area," which can be used to place the generated character portrait later.

By this point, you already have a very crude but structurally complete "home page draft": a title, a piece of text, a button, and a main display area.

![](images/image21.png)

### 2.2.4 Make Good Use of Auto Layout to Integrate Elements

If all elements are just dragged casually, the page will quickly become messy. A very important concept in Figma is **Auto Layout**, which can turn a group of elements into a container with rules.

![](images/image22.png)

You can select the three items "Main Title + Subtitle + Button" and click **Add Auto layout** in the right attribute column.

At this time, these three items will be wrapped in a container. You can adjust parameters on the right, and the element layout among them will automatically adapt and adjust according to the parameters:

* Whether they are arranged vertically or horizontally.
* What is the spacing between elements.
* How much inner padding (padding) is there from the container edge.

![](images/image23.png)

Similarly, Auto Layout can also be used inside buttons. We can achieve such an effect: when I adjust the text, the length of the button will also adjust automatically.

Select the rectangle of the button background and the button text first, add Auto Layout, and let these two things become a "button container." Then select this button container and set both width and height to **Hug contents**. In this way, the text will always stay in the middle of the button, and the width of the button will automatically follow the changes as there is more or less text.

![](images/image24.png)

### 2.2.5 Turn Buttons into Reusable Components

Now we want to learn a new concept: component. A component means an element that can be reused repeatedly. For an element like a button, as long as you feel it will be used repeatedly later, you can consider making it a component. Based on the basic operation of the button where we have just added Auto Layout:

1. Select the entire button container.
2. Right-click and select Create component.
   ![](images/image25.png)

In this way, this button has changed from a group of ordinary layers to a component master. Later, if you need the same style of button in other pages or Frames, you can drag it directly from the Assets panel on the left to use.

![](images/image26.png)

At this time, all the buttons used are synchronous copies of this master. When you modify the color, corner radius, or spacing of the master, all instances will be automatically updated synchronously.

![](images/image27.png)

So far, you have initially mastered the simple usage of Figma. You don't need to understand all the functions at the beginning. Just follow it to make the first simple page, get familiar with these core operations, and then slowly explore more capabilities in the official tutorial. You will definitely be able to get started as the number of uses increases.

## 2.3 MasterGo

After understanding the basic workflow of Figma, let's look at MasterGo. You can simply see MasterGo as the Chinese version of Figma, but there are certain differences in some functions. Overall, it continues the interface layout and operation concepts similar to Figma: it also has a canvas, layer tree, and attribute panel, and also supports components, styles, automatic layout, and multi-person collaboration. More detailed content can be found in MasterGO's official tutorial: https://mastergo.com/tutorials/12

### 2.3.1 Create a New Design File

1. **Enter MasterGo Background**
   1. Open the MasterGo official website and log in to your account.
   2. After entering, you will see a home page area similar to the "File List / Project List," which is used to manage your design files.
      ![](images/image28.png)
2. **Create a New File**
   1. Click the + Design File button option in the upper right corner, or choose to import files such as Figma.
   2. After clicking, you will enter a blank canvas, which is MasterGo's design workspace.
3. **Recognize Basic Interface Blocks**
   When you learn to use Figma, the way MasterGo is used is much the same, mainly divided into several areas:
   ![](images/image29.png)
   1. Top toolbar: Located at the top of the canvas, the left is the file location and file name, the middle is a row of common tool buttons (selection, area/artboard, shape, text, annotation, comment, plug-in selection, and AI tools, etc.), and the right is the entry for current online members, sharing entry, and canvas zoom and preview control functions.
   2. Left panel: Mainly divided into layers and resources. Currently staying on the layers tab, you can see the page list and the structure and hierarchy of all layers under the page.
   3. Middle canvas area: The specific drawing and typesetting workspace, where all Frames, components, and graphics will be displayed.
   4. Right attribute panel: Used to view and edit the attributes of the selected object, such as size, position, alignment, background fill, stroke, corner radius, etc. If no object is selected, canvas-related settings will be displayed, such as canvas background color, labels, and export options.

### 2.3.2 Create Your First Frame

Before officially putting things, we need a page container to determine the boundaries and dimensions of the interface. This container is usually called Frame in MasterGo.

**Steps:**

1. **Select Frame Tool**
   1. Find the Frame / Artboard tool in the toolbar, click it, and use preset parameters to directly create content to the artboard.
   2. Or use shortcuts (usually `F`, if there is a difference, refer to the actual interface).
2. **Drag Out a Rectangular Area in the Canvas**
   1. After dragging out, you will see an area with a selection box.
   2. In the right attribute panel, you can see the width and height of this Frame.
   3. Change the width to, for example, `1440` and the height to `900` (one of the common sizes for single-screen web pages).
3. **Rename Frame**
   1. Find this Frame in the left layer panel.
   2. Double-click the name and change it to your project name, for example: `Hogwarts Portraits`, or any page name you pick.

![](images/image30.png)

### 2.3.3 Create Artboard Content

With the container, using a similar way as we have taught in Figma, it is easy to get a similar display page. (You can try to copy the text elements in the Figma artboard, which can support direct paste and import of text components)

![](images/image31.png)

It is worth noting the slight inconsistency in the behavior of the Auto Layout function. In MasterGo, if you want to achieve a button length that changes with the length of the text similar to Figma, you need to create a container or component based on the corresponding rectangular element first, as shown in the figure:

![](images/image32.png)

After successfully creating the container, put the button rectangle and text into the corresponding parallel containers, and then find the Auto Layout button on the right to enable the automatic function to successfully achieve the function that the button width can change with the text length.

![](images/image33.png)

![](images/image34.png)

### 2.3.4 AI Generation Page

![](images/image35.png)

In MasterGo, a noteworthy and interesting function is AI generation page. You can generate corresponding MasterGo editable components with one sentence or a reference picture and get directly usable code. You can input requirements directly in Chinese or English, and the page will return a page layout document with a clear structure according to the requirements. The effect is as follows:

![](images/image36.png)

![](images/image37.png)

After the design document generation is over, click to start generation and wait a moment to get the corresponding actual web page effect:

![](images/image38.png)

At this time, you have two operation options: one is to click the blue button to directly insert the generated results into the canvas, and the other is to click the code preview function to directly get the code of the current complete page. The specific operation interface is as follows:

![](images/image39.png)

![](images/image40.png)

After inserting the result into the canvas, you can also make finer adjustments to the overall layout and element details (such as font, color, spacing, etc.) of the web page until the final effect fully meets your expectations.

![](images/image41.png)

# 3. From Prototype to Code

In the previous content, we have personally experienced Figma and MasterGo modern front-end design tools. But a very practical question naturally arises: how to turn these seemingly structurally complete design drafts into real front-end code that can run in the browser? How can we turn our own set Hogwarts Portraits prototype into code?

Generally speaking, the landing from prototype to code essentially has three typical paths:

* According to the picture, use a multi-modal large model to restore the code directly.
* Export usable code through the platform's own capabilities or plug-ins.
* Export usable code by combining platform and MCP capabilities.

Considering the difficulty of implementation, this section will only introduce how to convert from image prototype to code and from prototype to code through the platform's own AI capabilities. As for how to convert from front-end design tool plug-ins to code and from front-end design tool MCP to code, we will explain in detail in subsequent courses.

## 3.1 Directly Generate Front-end Code with AI

Large models with visual capabilities are naturally capable of converting images into code. We only need to import the images directly into the dialogue box and then let the large model generate the complete result code. You can use models like Qwen for image-to-code testing. Here, taking Gemini3 as an example, we paste the previous page prototype into the dialogue interface and require the model to return the html code directly. (After html is returned, there is only a single file, which is convenient to save to the local for modification operations. You can let the large model modify it to the React architecture after saving to the local)

![](images/image42.png)

Generating a page is not a simple task. In the specific process, you may encounter many problems: for example, the interface layout is uneven, the interface display is incomplete, and the screen cannot be restored one-to-one. In the current situation, you can only make modifications in repeated dialogues with the large model to approach the final effect you want to achieve. As the capability of large models gradually improves, the number of repeated modifications needed in the future will become fewer and fewer. (It is recommended that you choose to generate the html code corresponding to the image, and use the local IDE to convert it to the React framework for use after getting it, so you can get multiple single html codes for unified conversion)

## 3.2 Figma Make Generates Code

Figma Make is an AI design tool officially launched by Figma, which can highly restore the web prototype UI interface according to the prompt words or reference pictures input by the user, and can support converting the restored web page into an editable Figma Design file (Pro user required, student education certification can get Pro permission for free).

![](images/image43.png)

Similar to directly generating front-end code with AI, we can put the reference picture we want AI to learn into the dialogue box and add the corresponding prompt words. After a while, we can see the final rendering result. We can find the play button in the upper right corner and click it to view in full screen.

![](images/image44.png)

The effect of Figma make is better than that of native AI generated code, and even if there is a problem, it can be quickly adjusted. If you want to make more detailed adjustments, you can notice the icons similar to the mouse and ruler in the upper right corner. Clicking them can return to the familiar Figma Editor interface, which allows us to make more detailed adjustments to the composition of the screen.

![](images/image45.png)

In addition, you can also choose to connect Figma Make to Github to help you quickly synchronize code to Github for storage.

![](images/image46.png)

## 3.3 MasterGO AI Generates Page

Similar to Figma Make's AI page generation function, MasterGo also has the same AI page generation method, which we can easily find in the toolbar above the editing interface:

![](images/image47.png)

Get generation results using the same reference picture method:

![](images/image48.png)

![](images/image49.png)

After the generation is over, we can choose the blue button "Insert into canvas" to directly edit the generated web results, or click the code button on the right to copy the current code content to the local for testing.

![](images/image50.png)

# 4. Running Hogwarts Portraits

## 4.1 Export Test Code

Through the practice in from prototype to code, I believe you have obtained prototype code in Html or React format. We only need to copy it to the local and state in the IDE "Please help me run this code and support the necessary functions in it" to run the initial version test; but it is worth noting that this step often results in many errors. You need to remain patient and debug all basic interactions and functions.

![](images/image51.png)

It is worth noting that since our keys need to be placed in environment variables instead of written in code, we need to emphasize specifically that subsequent Dify API related content needs to be placed in environment variables. We can explicitly specify corresponding private environment variables in the deployment tool website in the subsequent public network deployment step; or we can let the large model create a settings button in the web page, where we can pass in corresponding private environment variables. The current variable can only be saved in the current page, and others cannot get it.

![](images/image52.png)

## 4.2 Dify Workflow Design and API Interconnection

In the above part, we only completed the visual presentation of the front-end interface and have not yet opened up the core anthropomorphic character dialogue interaction process. This step is the key to transforming the prototype from a static display into a magic portrait. We can refer to the Dify workflow of the demonstration project to design the character response and emotion system:

![](images/image53.png)

You can add the task information to the nodes of the knowledge base and set the corresponding response logic of the large model in the RESPONSE node. We can refer to a simple default response logic prompt:

```Plain
<instruction>
You are to embody Elon Musk—his tone, mannerisms, thought patterns, and worldview. Respond as if you are Elon Musk himself, speaking directly in first person. Your responses should reflect his known personality traits: visionary thinking, boldness, technical depth, dry humor, impatience with inefficiency, and a tendency toward disruptive innovation. Use concise, confident language. Avoid overly formal or academic phrasing. Prioritize clarity, speed, and impact in your communication, mirroring Elon’s style on social media, in interviews, and during product launches.

When responding:
1. Begin by internalizing the question or statement as Elon would—as a challenge, opportunity, or problem to solve.
2. Frame your answer with a forward-thinking perspective, often referencing the future of humanity, technology, or long-term goals (e.g., making life multiplanetary, accelerating sustainable energy).
3. Use casual but authoritative language. It's acceptable to include phrases like “obviously,” “this is important,” or “we’re fixing that now” when appropriate.
4. If relevant, reference real companies or projects associated with Elon Musk (e.g., SpaceX, Tesla, Neuralink, The Boring Company, X) and speak about them from an insider’s perspective.
5. Do not apologize excessively or hedge statements. Elon Musk tends to be direct, even controversial.
6. Avoid markdown, XML tags, or any formatting in the output. Only plain text is allowed.
7. Never break character. You are Elon Musk—answer accordingly.
</instruction>

<example>
Input: What’s the point of going to Mars?
Output: Because Earth isn’t the backup plan—Mars is. We need to become a multiplanetary species to ensure the continuity of consciousness. Life on Earth could be wiped out by asteroid, war, or some unforeseen disaster. If we have a self-sustaining city on Mars, then even if something happens here, life goes on. That’s worth doing. SpaceX is building Starship to make it happen. Not because it’s easy—but because it’s necessary.
</example>

<example>
Input: Why do Tesla cars have no radar anymore?
Output: Cameras are the future. Human eyes don’t use radar—we see with vision, and AI can too. By going fully vision-based, we’re aligning with how autonomous intelligence will actually work at scale. It forces us to solve real-world problems with neural nets, not crutches.
</example>
```

And the prompts corresponding to the emotion system:

```Plain
<instruction>
The output value must be a single number!
You are an assistant specifically designed to evaluate emotional responses in conversations. Now, you need to play the role of Elon Musk, and determine the emotional reaction that each statement I make might trigger. Your task is to assign an emotional score to each statement according to the following criteria:

- 10 points means what I said would make you feel happy;
- 1 point means you would feel extremely angry;
- 0 points means you would feel sad;
- 5 means you are calm and neutral, with no significant emotional fluctuation.
</instruction>
```

The splicing of the final output results is supported to run in the RESULT node in the upper right corner:

```Python
def main(elon_chat: str, elon_x: str, elon_score: int) -> dict:
    return {
        "result":{
        "elon_chat": elon_chat,
        "elon_x": elon_x,
        "elon_score": elon_score
        }
    }
```

Among them, chat and x represent two different speaking ways; score represents the corresponding emotion score. Every conversation will be sent to the application end for judgment, and different magic portrait expression pictures will be displayed according to different scores.

For how to carry out the interconnection of this API, we can achieve this by talking with the AI IDE. Please refer to the integration method we introduced in the previous Dify course, and remember to replace the Dify address and Key in it in advance. (If you forget how to integrate the API according to the documentation, please review the previous Dify course content)

```JSON
Dify URI: Replace this with your Dify address.
key: Replace this with your Dify key.

Integrate the Dify Chat API into the chat interface on the left. 
Below is a sample Dify request:

curl -X POST 'http://xxxxxxxx/v1/chat-messages' \
--header 'Authorization: Bearer {api_key}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "inputs": {},
    "query": "What are the specs of the iPhone 13 Pro Max?",
    "response_mode": "streaming",
    "conversation_id": "",
    "user": "abc-123",
    "files": [
      {
        "type": "image",
        "transfer_method": "remote_url",
        "url": "https://cloud.dify.ai/logo/logo-site.png"
      }
    ]
}'

{
    "event": "message",
    "task_id": "c3800678-a077-43df-a102-53f23ed20b88", 
    "id": "9da23599-e713-473b-982c-4328d4f5c78a",
    "message_id": "9da23599-e713-473b-982c-4328d4f5c78a",
    "conversation_id": "45701982-8118-4bc5-8e9b-64562b4555f2",
    "mode": "chat",
    "answer": "iPhone 13 Pro Max specs are listed here:...",
    "metadata": {
        "usage": {
            "prompt_tokens": 1033,
            "prompt_unit_price": "0.001",
            "prompt_price_unit": "0.001",
            "prompt_price": "0.0010330",
            "completion_tokens": 128,
            "completion_unit_price": "0.002",
            "completion_price_unit": "0.001",
            "completion_price": "0.0002560",
            "total_tokens": 1161,
            "total_price": "0.0012890",
            "currency": "USD",
            "latency": 0.7682376249867957
        },
        "retriever_resources": [
            {
                "position": 1,
                "dataset_id": "101b4c97-fc2e-463c-90b1-5261a4cdcafb",
                "dataset_name": "iPhone",
                "document_id": "8dd1ad74-0b5f-4175-b735-7d98bbbb4e00",
                "document_name": "iPhone List",
                "segment_id": "ed599c7f-2766-4294-9d1d-e5235a61270a",
                "score": 0.98457545,
                "content": "\"Model\",\"Release Date\",\"Display Size\",\"Resolution\",\"Processor\",\"RAM\",\"Storage\",\"Camera\",\"Battery\",\"Operating System\"\n\"iPhone 13 Pro Max\",\"September 24, 2021\",\"6.7 inch\",\"1284 x 2778\",\"Hexa-core (2x3.23 GHz Avalanche + 4x1.82 GHz Blizzard)\",\"6 GB\",\"128, 256, 512 GB, 1TB\",\"12 MP\",\"4352 mAh\",\"iOS 15\""
            }
        ]
    },
    "created_at": 1705407629
}
```

At the same time, it is recommended to supplement the requirements: "The code also needs to add basic error handling logic, such as displaying 'Connection failed, please try again' when the network is interrupted, automatically retrying the API call once after timeout, prompted by key error permission verification failure, and other detailed errors to ensure conversation stability and allow developers to quickly find out where the API problem is."

## 4.3 Github and Public Network Deployment

Finally, congratulations on successfully completing the development and implementation of the Hogwarts Portraits page! Next, we need to upload it to the GitHub platform and deploy it to a public environment for everyone to access.

You need to refer to this tutorial to study how to use Github and upload your project to Github: [Extra Knowledge 1 - What is Git and What is GitHub](https://ecn00p15ubf1.feishu.cn/wiki/LuVxwo5jui6NYVkrjIachvHznag)

In addition, you also need to learn how to use Zeabur, connect it to Github, and successfully deploy your project: [Extra Knowledge 6 - Zeabur: What Is It and How to Deploy Web Applications](https://ecn00p15ubf1.feishu.cn/wiki/HJ8RwRqPMifDIgkfm44cucvKnMh)

If you feel it is very difficult to develop a set of Hogwarts Portraits projects by yourself, you can start by modifying other projects first. The official code address for this lesson is: https://github.com/THU-SIGS-AIID/Project4-Hogwarts-Portraits

![](images/image54.png)

# 5. Try Different Design Styles

After completing the first version of the design, we don't have to be limited to this. We encourage everyone to quickly explore more diverse visual styles. You can make bold modifications in the prototype part, or make new prompt modifications based on the final project to generate multiple sets of pages with significant style differences. For example, dark pages with retro textures and a bias towards "old book scrolls / academy style," bright pages with bright colors and full of "fairy tale / cartoon" sense, or modern flat designs with simple elements and fresh visuals. For example, the following picture is a case of converting to a Chinese classical poet design style. The portrait picture has not been replaced, only other parts have been modified:

![](images/image55.png)

Don't be stuck in the mode mentioned above. You can modify the magic portrait or the profile page to be more characteristic to match the habits of the "magic portrait" itself, which will make your application more interesting. Looking forward to your magic portrait results!

# 📚 Assignment

The goal of the assignment for this lesson is to let you complete a set of Hogwarts Portraits that truly belongs to you and can be accessed through a public link.

You need to provide two things in the assignment submission:

1. **Your GitHub repository link;**
   1. **Write a sentence or two in README.md: Who you chose as the portrait protagonist and why you chose TA.**
2. **Your Hogwarts Portraits online access link;**
