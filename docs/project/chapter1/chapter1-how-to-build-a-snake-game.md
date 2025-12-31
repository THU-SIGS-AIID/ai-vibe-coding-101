# Project 1: How to Build a Snake Game

This is a **project-based learning** tutorial. We encourage you to follow the steps one by one and try to reproduce the results. Don't worry about making mistakes or modifying things—**the most important thing is:** 🎉 **Completion is more important than perfection.**

In software engineering, **iteration is normal and valuable**. You don't need to create a complete product all at once—**start small and change as you go.**

In this tutorial, we will learn how to use **vibe coding** techniques to create a modern version of the Snake game. We'll start with the basic mechanics of the Snake game, then modify it so the snake eats characters instead of dots. Finally, the game will generate a poem based on these characters and draw a picture inspired by that poem.

> 💡 What is Vibe Coding? Computer scientist [Andrej Karpathy](https://karpathy.ai/) (one of the co-founders of OpenAI and former head of AI at Tesla) coined the term **vibe coding** in February 2025. This concept refers to a coding method that relies on LLMs, allowing programmers to generate working code by providing natural language descriptions instead of manually writing code.
>
> ![](images/image1.png)
>
> Click here for more details on vibe coding:
>
> [https://www.ibm.com/think/topics/vibe-coding](https://www.ibm.com/think/topics/vibe-coding)

# What You Will Learn

* Build a simple game using prompts.
* If you see an error, tell the AI and let it help you fix it.
* Add text and image generation features to your game to make it more interesting.

# 1. Preparation

## 1.1 Which tools should we use?

We will use a very simple tool to build a minimal game. You don't need to know how to call large language models or image generation models.

This tool is called [z.ai](https://chat.z.ai/), developed by Zhipu AI (one of China's leading LLM companies). It supports various features like AI-driven slide generation, poster design, and full-stack development. In this tutorial, we will focus on its full-stack development module.

![](images/image2.png)

The full-stack development module in [z.ai](https://chat.z.ai/) supports real-time editing and previewing of web pages.

![](images/image3.png)

By clicking on the full-stack development example, you can see the entire process of web page creation.

![](images/image4.png)

By the time your coffee is ready, your results will be out!

![](images/image5.png)

You can scroll up and down to browse this web page, or click the 🧭 button at the top to view the page in full-screen mode.

![](images/image6.png)

If you want to view the source code of this web page, you can click the icon in the upper right corner.

![](images/image7.png)

You will be able to see all the code.

![](images/image8.png)

## 1.2 Do we need front-end development knowledge?

We don't need to master front-end or even back-end development skills at the beginning. We only need to learn how to chat with large language models, how to propose new requirements to the LLM based on current running results, and how to provide accurate error information to the LLM when the code fails to run.

However, we recommend that you learn some basics of front-end and back-end development, as this will help you let the LLM create better programs.

Don't worry, you only need to gradually master this knowledge during the learning process; you don't need to be an expert from the start.

> 💡 More about front-end development
>
> Front-end development usually means using **HTML**, **CSS**, and **JavaScript** to create the user interface of a website or application. However, in this tutorial, we will skip the complexities of front-end coding because the tool we use will automatically generate and run the interface for us.
>
> But it's helpful to understand what's happening behind the scenes. Traditionally, building a web interface involves writing **HTML** for structure, **CSS** for styling, and **JavaScript** for interactivity.
>
> For example, this is a very simple web page, but it combines three different types of code:
>
> ![](images/image9.png)
>
> * A simple HTML button:
>
> ```HTML
> <button>Click Me</button>
> ```
>
> * Basic CSS to make the button blue:
>
> ```CSS
> button {
>   background-color: #3498db;
>   color: white;
>   border: none;
>   padding: 10px 20px;
>   border-radius: 4px;
> }
> ```
>
> * A bit of JavaScript to show an alert when the button is clicked:
>
> ```JavaScript
> document.querySelector('button').onclick = function() {
>   alert('Button was clicked!');
> }
> ```
>
> When you try to click this button, you will see an alert message in your browser:
>
> ![](images/image10.png)
>
> In addition, we can try to understand the deeper meaning of these three types of code:
>
> **What is HTML?**
>
> HTML, which stands for **HyperText Markup Language**, is the skeleton of a web page. Its job is to define the structure and content of a page, such as headings, paragraphs, images, links, and the button itself as seen in the example.
>
> * **HTML decides what is on the page**: It tells the browser, "This is a button," "This is a paragraph of text," or "Display an image here."
> * **It uses "tags" to organize content**: `<button>Click Me</button>` is an HTML tag that defines a button and includes the text "Click Me" inside it.
>
> **What is CSS?**
>
> CSS, or Cascading Style Sheets, is responsible for the "look and feel" of a web page. It's used to design and beautify HTML elements, controlling things like color, font, layout, and spacing.
>
> * **CSS decides how the page looks**: In our example, the CSS code turns a standard HTML button into a button with a blue background, white text, rounded corners, and some padding.
> * **It separates content from presentation**: This is a key concept. You can have an HTML file for content and use a separate CSS file to style it. This makes it much easier to maintain and update the design of an entire website.
>
> **What is JavaScript?**
>
> JavaScript is a programming language that adds interactivity and dynamic behavior to web pages. If HTML is the skeleton and CSS is the skin, then JavaScript is the brain and muscles that make the page "come alive."
>
> * **JavaScript decides how the page behaves**: In the example, the JavaScript code makes an alert box pop up when the button is clicked. It defines the actions that should happen in response to user input.
> * **It can create complex features**: Beyond simple alerts, JavaScript is used to handle form submissions, create animations, load new data without reloading the page, build complex applications like games, and much more.
>
> As projects get bigger and more interactive, managing code with just plain HTML, CSS, and JavaScript can become complex and hard to maintain. This is where modern front-end libraries like **React** come in.
>
> ![](images/image11.png)
>
> **[React](https://react.dev/)** is a popular JavaScript library for building user interfaces. It helps developers organize code into reusable components, making it easier to build and maintain complex applications.
>
> React allows you to write components that manage their own logic and appearance, and then combine them to build larger interfaces.
>
> As we go deeper, we'll explore more about how React works and how it fits into our workflow. For now, just know that while front-end development usually means writing code like this, our tools will handle most of the work automatically—we just need to know how to express our needs clearly to the large language model!

# 2. Building Your First Game

## 2.1 Give Clear Instructions When Talking to the LLM

In the beginning, we can talk to the large model in the simplest way, which will help us quickly get a product prototype. We can directly enter in the chat box:

> **💡 Example Prompt:** Help me make a Snake game
>
> ![](images/image12.png)

> **💡 Example Prompt:** Help me make a Snake game that supports:
>
> 1. I can eat different words, and they will be collected in a box
>    ![](images/image13.png)

> **💡 Example Prompt:** Help me make a Snake game that should support:
>
> 1. I can eat different words, and they will be collected in a box.
> 2. When the snake eats 8 words, the LLM should create a poem based on these words, and we can remix the poem as needed.
> 3. When the poem is completed, the next step will automatically create an image based on this poem.
>
> ![](images/image14.png)

## 2.2 Try to Fix Errors Occurring During the Process

During the development process, we might encounter unsatisfactory issues, such as clicking a button having no response, getting an error when using a feature, a feature not working as expected, or the front-end page not matching the expected design.

In this case, we need to further ask the model questions to help fix these unexpected problems.

![](images/image15.png)

## 2.3 How to Pretend to Be a Vibe Coding Master

Actually, in a real vibe coding process, we usually don't use many complex prompts. We might need a specific and moderately complex prompt for the whole program at the beginning, but for every step after that, you might only need prompts of the following types:

```JSON
"There is a bug in the code, please fix it."
"I don't want partial code, give me the full modified code."
"Your code still has problems."
"Please modify again and give me the full corrected code."
"It was working just now, why isn't it working now?"
"Don't you understand what I mean? Don't change my original code."
"Don't add any debugging features."
"Don't do things I didn't ask you to do."
"Where is the feature I asked you to implement?"
"Can't you understand what I'm saying?"
"I only want one function."
"I told you to refer to my previous code."
"Please don't add unnecessary comments."
"Please don't modify the basic logic of my original code."
"Help me modify the code."
"Modify based on my code..."
"DON'T CHANGE MY VARIABLE NAMES!!!"
"Don't change the original function names!"
"Don't mess with my variables."
"Don't add extra features."
"Don't just generate the framework, generate the full code."
```

This might sound a bit exaggerated, but in reality, these are the prompts we might use in our daily work. Due to the context length limits of large language models, or sometimes because their instruction-following ability is not very strong, models might forget content discussed earlier in the conversation.

Or, due to the style of the training data set, large models tend to answer in the style of their training data. For example, some people speak very seriously, some like to add many modifiers, and some large models like to add many comments or unnecessary modules in the code.

That's why we need to set clear boundaries at the beginning, for example: don't add new modules, don't include too many comments. Each large model has its own style, and we can only find our favorite one through actual use.

> 💡 What is Model Context?
>
> Model context is like the AI's **short-term memory**. It's all the text in the current conversation that the AI remembers. This allows you to ask follow-up questions and have a natural conversation because the AI "remembers" what you were just talking about. Without context, every question you ask would be a brand-new, standalone conversation.
>
> Each model has a different effective context length, usually ranging from **32k to 128k** tokens. If you want a large language model to read a very long article all at once, or if you have many materials and conversations you hope the LLM will refer to, you might find that the LLM often forgets some important content from long texts, or you might notice the topic gradually drifting during the conversation, which is a phenomenon caused by context limits.
>
> Therefore, for models, we also focus on context. However, it is worth noting that the longer the context, the greater the resource consumption and the higher the fees charged. In the industry, there are many methods for compressing context, which we will introduce one by one in subsequent studies.

> 💡 What is Instruction Following Ability?
>
> Instruction following ability refers to the **AI's ability to understand and accurately execute the commands you provide**. It's not just about answering questions, but completing tasks according to your specific requirements, such as "summarize this article into three key points," "write a reply in a formal tone," or "translate this word and use it in a sentence."
>
> A model with strong instruction following ability will do exactly as you instructed without performing any unnecessary extra actions.
>
> For example, when we want the LLM to summarize an article into three key points, we don't want it to give us five; when we want it to extract certain key elements (such as the author, time, and events that occurred) from the article, we don't want it to miss any elements.
>
> Therefore, we hope that the LLM has strong enough instruction following ability, as this brings stability and **reproducibility**, making them an important part of industrial applications.

# 3. **Using APIs: Calling LLMs and Image Generators**

## 3.1 What is an API

First, **you need to know what an API is** `Extra Knowledge 2 - What is API`

We will try to integrate two APIs: one for calling the DeepSeek LLM and another for calling the Seedream (Jimeng) model. Both models are great and have excellent performance.

In the process of using an API, there are only two most important elements:

1. API key
2. Official documentation example

As long as you can find these two, you can let the LLM help you modify and implement all types of API calls.

## 3.2 Integrating DeepSeek API into z.ai

### What is DeepSeek

![](images/image16.png)

> 📚 Information cited from [DeepSeek Wiki](https://en.wikipedia.org/wiki/DeepSeek)
>
> **Hangzhou DeepSeek Artificial Intelligence Basic Technology Research Co., Ltd.**, doing business as **DeepSeek**, is a Chinese artificial intelligence (AI) company that develops large language models (LLMs). Headquartered in Hangzhou, Zhejiang, DeepSeek is owned and funded by the Chinese hedge fund High-Flyer. DeepSeek was founded in July 2023 by Liang Wenfeng, a co-founder of High-Flyer, who also serves as CEO of both companies. The company launched its eponymous chatbot and its DeepSeek-R1 model in January 2025.
>
> Let's look at how DeepSeek performs compared to other top models in the GPQA benchmark rankings. It's worth noting that DeepSeek is an open-source (everyone can download the model from the internet) model, while other common models like Grok, Google Gemini, and ChatGPT are all closed-source. As we can see, DeepSeek has already approached the first-tier models to a large extent.
>
> ![](images/image17.png)
>
> GPQA is short for "Graduate-Level Google-Proof Q&A Benchmark," which is a graduate-level benchmark for scientific Q&A tasks. Here is a detailed introduction.
>
> GPQA contains 448 multiple-choice questions covering subfields of biology, physics, and chemistry, such as quantum mechanics, organic chemistry, molecular biology, and more. These questions were written by 61 experts holding PhDs or pursuing PhDs and have undergone a rigorous validation process.

### How to Get DeepSeek API

We will try to let z.ai directly integrate the DeepSeek API into the project based on the information we have.

First, we need to register an account on the DeepSeek open platform.

https://platform.deepseek.com/sign_up

Then, you will see a web interface like this:

![](images/image18.png)

To use the API, we need to top up tokens first. 10 RMB is enough for a while!

![](images/image19.png)

Click on "API KEYS" and find "create new API key" at the bottom of the screen. You will eventually get an API key like `sk-8573341c39fc44315aadc071c53rh7d2`.

![](images/image20.png)

Once you have the key, you have the permission to call the model.

At this point, you can directly read the [API documentation](https://api-docs.deepseek.com/), which usually provides call examples in curl or Python.

![](images/image21.png)

After finding the example, you can copy everything from the documentation related to the key to z.ai and ask it to try to help you integrate the LLM.

![](images/image22.png)

![](images/image23.png)

Automatic integration can be completed in a very short time. We can ask its operator to confirm if the DeepSeek API is already in use.

![](images/image24.png)

Or, we can ask z.ai to help us locate the parts of the project that call the LLM.

Then we can independently confirm whether DeepSeek is being used. Specifically, we can directly request: `"Tell me the location of all the code in the project that needs to call the LLM, I need to check if it's DeepSeek."`, and z.ai will return the detailed addresses of all API calls.

![](images/image25.png)

Next, we will briefly introduce three of the most advanced image generation models currently available. You can choose one to integrate into z.ai according to your preference.

## 3.3 Integrating SiliconFlow QwenImage API into z.ai

### What is SiliconFlow

> [Silicon Flow](https://cloud.siliconflow.com/me/models) was founded in August 2023 and is a world-leading AI capability provider. It offers core products such as SiliconCloud (a large model cloud platform with self-developed inference acceleration) and BizyAir (a ComfyUI plugin for AI image generation), providing AI infrastructure capabilities for customers, possessing strategic partnerships, and holding top industry certifications.
>
> ![](images/image26.png)

### What is QwenImage

> Qwen-Image is a powerful image generation base model capable of complex text rendering and precise image editing. It is a 20B MMDiT image base model that has made significant progress in complex text rendering and precise image editing. Experiments show that it has strong general capabilities in both image generation and editing, performing particularly well in text rendering, especially in Chinese.
>
> From Chinese to English, QwenImage can generate high-quality text just like GPT-4o or the Seedream model.
>
> ![](images/image27.png)
>
> ![](images/image28.png)
>
> ![](images/image29.png)
>
> ![](images/image30.png)

### How to Get SiliconFlow QwenImage API

https://cloud.siliconflow.com/me/models

Check SiliconFlow's official website. There is a "Playground" section on the left where you can try out different models without making API calls. There is a "Filters" button at the top of the page; click it to filter the list of models on the right.

If you select "Image," you will only see all currently supported text-to-image models. In this case, we will use Qwen/Qwen-Image.

![](images/image31.png)

To call the API, first we need to click "API Keys" in the settings on the left, then click the "Create API Key" button to generate an API key. Remember to save this API key.

![](images/image32.png)

To check the available balance, we need to open "Payments" in the settings on the left. Here, you can see a 1 USD gift credit. However, if you want to use the FLUX text-to-image model, you need to top up your account first.

https://cloud.siliconflow.com/me/account/ak

![](images/image33.png)

After everything is set up, we need to refer to the corresponding image generation API documentation. You can find any section marked "API Reference" on the official documentation page. Click it, then navigate to the image generation API endpoint section and find the relevant request example.

https://docs.siliconflow.com/en/userguide/introduction

![](images/image34.png)

```Bash
curl --request POST \
  --url https://api.siliconflow.com/v1/images/generations \
  --header 'Authorization: Bearer <token>' \
  --header 'Content-Type: application/json' \
  --data '{
  "model": "black-forest-labs/FLUX.1-Kontext-max",
  "prompt": "an island near sea, with seagulls, moon shining over the sea, light house, boats int he background, fish flying over the sea"
}'
```

Remember to fill in the model and API key you intend to use into the corresponding fields. After that, you can use the command in your computer's command line to run a direct request test.

```Bash
curl --request POST \
  --url https://api.siliconflow.com/v1/images/generations \
  --header 'Authorization: Bearer sk-defrgqrgrganpncxxibfyzfocgafga' \
  --header 'Content-Type: application/json' \
  --data '{
  "model": "Qwen/Qwen-Image",
  "prompt": "an island near sea, with seagulls, moon shining over the sea, light house, boats int he background, fish flying over the sea"
}'
```

![](images/image35.png)

You can send the modified code lines below to z.ai and ask it to help you create a front-end test demo. Soon, you'll be able to implement the basic API call for SiliconFlow.

![](images/image36.png)

## 3.4 Integrating Recraft API into z.ai

### What is Recraft

> Recraft is an AI tool for designers, illustrators, and marketers—founded in the US in 2022 and headquartered in London. It helps generate/iterate visuals (images, vector art, 3D graphics) with benefits like high-quality output (any text size/length), precise element positioning, and brand-consistent design. Trusted by over 3 million users (including Ogilvy, Netflix) across 200 countries and having created 350+ million images, the team aims for it to be the must-have designer tool, ensuring creators have control over their AI-assisted workflows.
>
> ![](images/image37.png)
>
> ![](images/image38.png)
>
> ![](images/image39.png)

### How to Get Recraft API

First, we still need to find the important API entry point to get our API key. https://www.recraft.ai/profile/api

Since no free credit is provided here, we need to top up 1,000 points ourselves. This website supports Alipay and WeChat Pay, so it's easy to get 1,000 points (note: don't top up more than necessary).

![](images/image40.png)

After that, we still follow the usual method: go to the official documentation to find the corresponding request example.

https://www.recraft.ai/docs/api-reference/getting-started

https://www.recraft.ai/docs/api-reference/usage

https://www.recraft.ai/docs/api-reference/guides

Here, we can directly copy the entire content and paste it into z.ai.

![](images/image41.png)

Note that in the chat window, entering your API key and documentation content is enough; z.ai will automatically build the front-end for you.

If an error occurs during the process, you can directly paste the error message into the chat window and let z.ai help you solve it automatically.

![](images/image42.png)

## 3.5 Integrating Seedream API into z.ai (For Chinese Users)

### What is Seedream 4.0

https://seed.bytedance.com/en/seedream4_0

![](images/image43.png)

> You might already know Nano Banana (developed by Google), but you'd better not miss Seedream. Seedream 4.0 is a new generation image creation model built by ByteDance. It integrates image generation and image editing capabilities into a unified architecture. This allows it to flexibly handle complex multi-modal tasks such as knowledge-based generation, complex reasoning, and reference consistency. Additionally, its inference speed is much faster than its predecessors, and it can generate stunning high-definition images with resolutions up to 4K.
>
> ![](images/image44.png)
>
> ![](images/image45.png)
>
> ![](images/image46.png)

### How to Get Seedream API - Volcengine (For Chinese Users)

We will demonstrate step-by-step how to integrate the Seedream API into the z.ai example.

https://www.volcengine.com/experience/ark?launch=seedream

After visiting the page, click to log in.

![](images/image47.png)

After logging in, find the top-up option in the upper right corner of the page.

![](images/image48.png)

Real-name authentication is required for top-up.

![](images/image49.png)

After successful authentication, you can top up 1 RMB for testing.

https://console.volcengine.com/finance/fund/recharge

![](images/image50.png)

Return to the initial interface and click API Access.

![](images/image51.png)

First, create an API key, then click the select option.

![](images/image52.png)

This will take you to Step 2. Here, you need to confirm that the service called is Seedream 4.0 and copy the provided call example.

![](images/image53.png)

After preparing the API key and call example, you can directly paste them into z.ai to generate a front-end interactive demo.

Important Note: The default example here is relatively complex. Remember to disable the "Add Watermark" option and the "Streaming Response" option to ensure no watermark is generated and no request failures occur.

![](images/image54.png)

After entering the prompt, you will receive the generated result. Enjoy it!

![](images/image55.png)

# Make It More Interesting

After completing the basic features, we can try adding some new tricks to our program! If you find the process of the snake eating words or characters a bit boring, you can let the snake eat words of different colors and change the snake's color accordingly.

You can also add special effects to the "eating" process, or introduce magic words that trigger special effects—like increasing the snake's speed or size. Another idea is to let the model generate a poem and a picture every time the snake eats a word, rather than waiting until it eats eight words.

If these feel challenging, you can directly ask the language model for help! It can provide creative suggestions to make your game more fun. Give it a try!

```JavaScript
1. "Words Unlock the World" Mechanism
Every time the snake eats a word, the LLM makes a poetic association for that word (e.g., "tree" → "forest", "green shade"), and the image model instantly generates a small artwork for that word. These images are gradually pieced together into a unique, player-created panorama, so the player is "painting and writing poetry" with every play.

2. "Poetry Puzzle" Gameplay
Each word eaten by the snake triggers the LLM to generate a short verse and the image model to generate an illustration. These verses and images are combined like a puzzle, forming an AI-collaborated poem and painting at the end of the round.

3. "Magic Words" & "Story Branches"
Special "magic words" (e.g., "wind", "night", "dream") not only trigger the LLM to generate poetry but also change the mood or theme of the scene—shifting the style of the generated images to night, storm, or a dreamlike atmosphere.
Branching stories: The LLM gives a theme or riddle at the start (e.g., "Memories of Autumn"). The player's word choices directly influence the evolution of the story and poetry, with the image model updating backgrounds and visuals in real-time.

4. "Real-time Interactive Generation"
After each word, the LLM generates a line of dialogue or description, and an NPC in the game can "speak" to the player, or the environment can change accordingly.
The snake's appearance or obstacles in the game can change visually based on the words eaten, thanks to the image model.

5. "Creation & Sharing"
Players can save and share their AI-created poems and images at the end of the session, showing off their unique "AI collaboration."
Leaderboards for "Most Beautiful Poem + Art," "Most Creative Word Combination," etc., to encourage replayability and creativity.

6. "Sentence Snake" Challenge
Reverse Mode: The LLM gives a line of poetry or a riddle, and the player must guide the snake to eat words in order to reconstruct the sentence. Eating the wrong word triggers funny or artistic consequences via the image generation model.

7. "Themed Levels" & "Style Selection"
At the start of the game, players choose a theme (e.g., "Fairytale", "Sci-Fi", "Tang Poetry"), and both the LLM and image models adjust word choices, poetic style, and visuals to match, making every run feel fresh.

8. "Live Co-creation"
When a special word is eaten, the LLM can prompt the player for a phrase or a style choice, and then the AI generates the corresponding verse and illustration, making it a true human-AI co-creation.

9. "AI Easter Eggs & Achievements"
Certain word combinations are recognized by the LLM as special themes or inside jokes (e.g., "moon", "osmanthus", "riverbank"), triggering rare verses and illustrations that reward exploration.

10. "Story of Growth"
As the snake grows, the LLM generates a continuous story-poem and the image model creates a seamless long scroll or panorama, so the player is "writing, painting, and playing" all at once.
```

In addition, we can ask the LLM to help you generate project-level prompts directly. In the previous section, we only wrote the prompt for the Snake game ourselves. Now let's try to let the large model generate a prompt with an overall framework and implementation path (you can generate it directly with z.ai):

> I want the AI to generate a web-based Snake game and need a more complete prompt to make the generated result more impressive and interesting. Please generate the corresponding prompt. The current goal is: generate a Snake game that implements the feature of eating different words to generate poetry and should include an image generation module.

z.ai's reply will look like this:

![](images/image56.png)

We can use this prompt to re-generate the project in full-stack development mode:

![](images/image57.png)

![](images/image58.png)

# More Reference Cases

Beyond Snake (games), we can let our imagination run wild.

Create whatever we want to create, or even try to mess everything up! Then start over!

```YAML
1. AI Art Gallery Platform
   Description: An online gallery showcasing AI-generated artwork where users can upload, share, and comment on AI art.
   Features: User account system, artwork upload and display, rating system, categorized browsing, AI generation tool integration.
   Technical Highlights: React/Vue frontend, Node.js backend, MongoDB database, AI API integration.

2. Retro Game Archive
   Description: A website paying tribute to classic games, featuring game history, gameplay guides, and online playable retro games.
   Features: Game database, timeline display, online emulator, user reviews, game collection feature.
   Technical Highlights: Responsive design, WebGL/Canvas game implementation, RESTful API, user authentication system.

3. Sustainable Living Tracker
   Description: A website helping users track and reduce their carbon footprint through eco-friendly tips and community challenges.
   Features: Personal carbon footprint calculator, goal setting, progress tracking, community challenges, eco-knowledge base.
   Technical Highlights: Data visualization, mobile optimization, social features, push notifications.

4. Virtual Kitchen Assistant
   Description: An AI-based cooking guidance platform providing personalized recipe recommendations and step-by-step cooking instructions.
   Features: Recipe database, ingredient recognition, personalized recommendations, cooking timer, nutritional analysis.
   Technical Highlights: Image recognition API, machine learning recommendation system, voice control, real-time video guidance.

5. Underground Music Discovery Platform
   Description: A music streaming platform focused on independent and emerging artists, offering a unique discovery experience.
   Features: Music streaming, artist profiles, personalized recommendations, playlist creation, community reviews.
   Technical Highlights: Audio stream processing, recommendation algorithms, social features, music visualization.

6. Minimalist Task Management System
   Description: A task management tool with a Zen aesthetic, focusing on simplicity and efficient task organization.
   Features: Task creation and categorization, priority setting, progress tracking, team collaboration, data analysis.
   Technical Highlights: Minimalist UI design, drag-and-drop functionality, real-time synchronization, cross-platform compatibility.

7. Sci-Fi Writing Workshop
   Description: A platform providing creative tools and inspiration for sci-fi writers, including world-building assistance and character development tools.
   Features: Story structure tools, character profiles, world-building templates, writing statistics, community feedback.
   Technical Highlights: Rich text editor, data visualization, collaborative editing, AI-assisted creation.

8. Personal Knowledge Graph
   Description: A tool helping users build a personal knowledge network, visualizing and connecting various ideas and information.
   Features: Node creation and connection, tagging system, search functionality, import/export tools, visual diagrams.
   Technical Highlights: Graph database, data visualization algorithms, Markdown support, cross-device synchronization.

9. Virtual Botanical Garden
   Description: An interactive plant encyclopedia where users can explore the plant world and create virtual gardens.
   Features: Plant database, 3D plant models, growth simulation, gardening guides, community showcases.
   Technical Highlights: 3D rendering, seasonal change simulation, AR integration, plant identification API.

10. Coding Challenge Arena
    Description: An online competition platform for programmers with various difficulty levels of coding challenges.
    Features: Challenge problems, code editor, automatic evaluation, leaderboards, learning paths.
    Technical Highlights: Code sandbox environment, real-time evaluation system, algorithm visualization, social learning features.
```

And... if you like playing games, let's try to create games together!

```SQL
1. 3D Open World RPG
   Description: A fantasy RPG with a vast open world, quests, and character growth.
   Features: Day/night cycle, dynamic weather, skill trees, multiplayer co-op, crafting system.
   Technical Highlights: Three.js or Babylon.js for 3D rendering, server-side game logic, character customization, save system.

2. First-Person Shooter (FPS) Arena
   Description: A fast-paced multiplayer FPS with various game modes and maps.
   Features: Team deathmatch, capture the flag, weapon customization, ranked matches.
   Technical Highlights: WebGL/Three.js for 3D graphics, multiplayer networking code, hit detection, voice chat.

3. AI Chess and Multiplayer
   Description: A full-featured chess platform with AI opponents and online play.
   Features: AI difficulty levels, endgame challenges, tournament mode, replay analysis.
   Technical Highlights: Chess logic library, WebSockets for real-time play, ELO rating system, anti-cheat.

4. Mahjong Online Multiplayer
   Description: A traditional Mahjong game with online multiplayer and scoring.
   Features: Multiple rule sets, private rooms, ranking system, replay function.
   Technical Highlights: Tile matching logic, real-time multiplayer, lobby system, score tracking.

5. Turn-Based Strategy Game
   Description: A tactical strategy game with grid-based combat and unit management.
   Features: Campaign mode, skirmishes, unit upgrades, fog of war, multiplayer battles.
   Technical Highlights: Grid movement system, AI decision-making, turn synchronization, save/load system.

6. Time Trial Racing Game
   Description: A 3D racing game focused on time trials and track records.
   Features: Multiple tracks, car customization, ghost replays, leaderboards.
   Technical Highlights: 3D car physics, track editor, replay system, online leaderboards.

7. Card Battle Game (Deck Building)
   Description: A strategic card game where players build decks and battle opponents.
   Features: Card collection, deck building, ranked matches, seasonal events.
   Technical Highlights: Card game logic, matchmaking system, AI opponents, card animations.

8. Battle Royale (Top-Down 2D)
   Description: A top-down 2D battle royale with a shrinking play area and loot mechanics.
   Features: Solo and squad modes, weapon variety, in-game events, leaderboards.
   Technical Highlights: Real-time multiplayer, zone shrinking logic, loot generation system, matchmaking.

9. Survival Horror Game (First-Person)
   Description: A first-person horror game with resource management and escape mechanics.
   Features: Atmospheric environments, puzzles, enemy AI, multiple endings.
   Technical Highlights: Dynamic lighting, sound design, enemy pathfinding, save system.

10. Music Rhythm Game (3D)
    Description: A 3D rhythm game where players hit notes to the beat of the music.
    Features: Multiple difficulty levels, track editor, custom song support, leaderboards.
    Technical Highlights: Audio analysis, beat synchronization, 3D note tracks, input timing detection.
```

# Summary

That's the complete tutorial! It might take you **4 hours** to complete everything and build your own Snake game. Don't rush—explore, experiment, and enjoy the process.

If you have a different game idea, that's great too. The most important thing is to start building.

Good luck, and welcome to the world of AI-native creativity :)
