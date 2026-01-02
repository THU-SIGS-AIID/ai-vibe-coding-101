# Extended Knowledge 4 - What are AI IDEs and Trae

In previous learning stages, we used z.ai to build the simplest web programs and web games. But if we want to build more complex applications - such as more feature-complete websites, desktop programs, or even mobile applications - we must use professional programming software on our own computers to write code.

In the earliest days, you only needed to write a program in a simple text file, then use a specialized language processor to read, package, and execute it. But as code volume grew larger and project structures became more complex, manually managing large numbers of files and editing huge projects became increasingly difficult. Developers urgently needed a tool that could efficiently manage and switch between large numbers of code files, support syntax highlighting for multiple programming languages, and quickly locate and debug issues. Thus, the Integrated Development Environment (IDE) was born.

You can understand an IDE as a program specifically designed to "edit, manage, run, and debug" various application source codes. Before actual packaging and release, programs written in different languages are essentially just code files in specific formats - you can open them with a regular text editor or with an IDE. Early computers were operated almost entirely through terminals (all operations could be completed with just a keyboard, almost no mouse needed), so early IDEs also had very "primitive" appearances - unless you additionally installed plugins to implement simple interactive interfaces.

![](images/image1.png)![](images/image2.png)

Terminal Interface

Image source: https://en.wikipedia.org/wiki/File:Emacs-screenshot.png

A very well-known and mature "built-in IDE" is called `Vim`. On many servers, you can use it directly to edit files (servers usually don't have displays and can only be operated remotely through keyboards).

![](images/image3.png)

Modern IDEs usually have more beautiful and intuitive graphical interfaces, providing more powerful editing, running, and debugging capabilities. A typical IDE usually contains the following core components:

* **Source Code Editor**: A text editor specifically designed for writing and editing code, typically featuring syntax highlighting, automatic code completion, real-time error hints, and other functions.
* **Build and Run Tools (Compiler/Interpreter)**: The IDE has built-in compilers or interpreters that can convert source code written by developers into machine code that computers can execute.
* **Debugger**: A tool for testing and troubleshooting code errors. It supports executing code line by line, viewing variable states, setting breakpoints, etc., helping developers locate and fix problems in their programs.

In addition, modern IDEs often include practical features like version control tools (such as Git) and project management tools. One of the most popular IDEs today is Microsoft's **[Visual Studio Code (VS Code)](https://code.visualstudio.com/)**. It's lightweight and extremely extensible, so it's widely used. Of course, many developers also recommend JetBrains' professional IDEs, such as PyCharm for Python or CLion for C/C++, which provide deeper and more complete support for specific languages. But from the perspective of beginner-friendliness and versatility, we recommend beginners prioritize VS Code as their main development tool.

![](images/image4.png)

# Modern IDE: VS Code

Visual Studio Code (VS Code for short) is a free, open-source, and powerful modern code editor developed by Microsoft. Since its release in 2015, it has rapidly become one of the most popular development tools worldwide, thanks to its excellent performance and flexibility.

One of VS Code's core philosophies is "everything is a plugin." Different programming languages can be used to write different types of programs, and each language has its own unique syntax highlighting rules and navigation capabilities (like "jump to definition," "find references," etc.). Making an IDE natively support all languages is nearly impossible - logically, you would need to prepare a separate IDE for each language.

VS Code cleverly solves this problem through a "plugin mechanism." For example, if you want to write Python, install the Python plugin, which provides Python-specific syntax highlighting, auto-completion, and code navigation features; if you want to write C/C++, you can install the corresponding C/C++ plugin to get support. Without installing any plugins, VS Code is essentially just an "advanced text file manager"; when you install the corresponding plugin for a language, it "transforms" into the ideal development tool for that language.

![](images/image5.png)

Besides writing code, you can even use VS Code as a tool for editing Markdown documents.

![](images/image6.png)

In short, you can browse and download various extensions in VS Code's extension marketplace to provide better editing experiences for different types of files. You can also search for plugins for different languages and debugging tools as needed to try how they can improve your work efficiency.

# Modern AI IDE

The tools introduced above all belong to "traditional modern IDEs." But with the arrival of the AI era, more and more code is being automatically generated by large language models, which naturally gave birth to a new form of development tool - the AI IDE, which is an IDE that can use large language models to automatically write code.

In the latest version of VS Code, a large language model assistant is already built in. You can directly converse with the model for an entire code repository, a specific file, or even a specific function.

You can also, just like when using auto-coding tools on the web before, send requirements in the form of prompts to the built-in coding Agent, letting it automatically help you implement required features, create files, modify code, configure environments, etc.

Typical AI IDEs generally have the following core capabilities:

* Intelligent code generation and completion: In traditional IDEs, we usually type a few characters to complete variable names or function names; in modern AI IDEs, you can write a few lines of pseudocode or simply describe requirements, letting the IDE automatically complete the entire logic, or even directly generate large segments or entire blocks of code based on instructions.
* Code understanding and Q&A: The IDE can understand and answer questions about specific code segments, specific files, or even the entire project directory structure.
* Code refactoring and optimization: The IDE can rewrite or optimize the implementation logic of specified code segments based on your intentions.
* Automatic test generation: The IDE can automatically generate test code for different functions and modules, making it easier for you to conduct targeted testing.
* Agent-style task execution: Intelligent Agents can automatically generate, package, install, run, and modify code, partially replacing the work of junior software engineers in many tasks.

In the latest version of VS Code, you can click the sidebar entry in the upper right corner to open the AI functionality area and experience these capabilities.

![](images/image7.png)

However, VS Code is not the IDE with the strongest AI capabilities. For scenarios requiring extensive AI-assisted coding, we often want to use "smarter, more efficient" tools - good AI IDEs can significantly save time on writing code and fixing bugs. Below we'll introduce several currently popular AI IDEs, focusing on Trae IDE. You can choose any AI IDE based on personal preference.

Since VS Code is open source (anyone can download the source code and compile it themselves), most AI IDEs on the market today are developed based on VS Code. So you don't need to worry about "learning many different IDEs" - once you're familiar with VS Code's basic usage, migrating to these AI IDEs requires almost no relearning.

To briefly summarize the differences between these AI IDEs, they mainly focus on four aspects: price; available model types (some advanced models may be restricted in certain regions); Agent capabilities (intelligence level and execution ability when assisting with coding); and running speed and performance.

## Trae

![](images/image8.png)

Trae is an AI programming assistant launched by ByteDance, supporting over 100 programming languages and capable of integrating with mainstream IDEs. Its features include: generating code with natural language, automatic debugging, converting design drafts into React/Vue components, etc. After the August 2025 update, Trae added smart dependency imports, rename suggestions, task list management, and other features; SOLO mode also began supporting backend code generation and technical architecture document editing.

## Cursor

Cursor is an AI code editor developed by Anysphere, customized based on VS Code, with a focus on optimizing large-scale code repositories and multi-file collaboration scenarios. It supports models like GPT-4o, Claude 3.7, etc.; the Claude Max mode launched in 2025 can handle projects with millions of lines of code. The professional version removes request count limits, making it very suitable for complex enterprise-level projects.

Currently, Cursor can be said to be one of the AI IDEs with the best overall experience among "those with frontend interfaces," with a large user base and high feature iteration frequency. Its biggest disadvantage is the higher price - the professional version costs about $20 per month.

![](images/image9.png)

## Qoder

Qoder is an AI IDE launched by Alibaba that emphasizes "transparent collaboration" and "enhanced context engineering capabilities." It supports breaking down tasks into multiple steps through Action Flow and tracks AI's execution process in real time; it also supports multi-model dynamic routing and task state machine management, making it very suitable for architecture governance in medium-to-large projects and "reverse engineering" analysis of legacy systems.

![](images/image10.png)

## CodeBuddy

CodeBuddy is an AI programming tool launched by Tencent Cloud that emphasizes support for Chinese instructions and enterprise-level compliance capabilities. It provides features like code completion, batch code review, and multi-model switching; its Craft agent can achieve multi-file code generation and API integration. The enterprise version supports private deployment and has passed Level 3 certification, making it suitable for industries with high data security requirements like finance and healthcare.

![](images/image11.png)

## Windsurf (No Longer Recommended)

Windsurf initially received attention for its Agent-based AI programming capabilities. But due to team adjustments in 2024 and model permission issues, its stability declined significantly, and it's currently no longer recommended. Although in the previous year it could still compete with Cursor, it can now basically be considered a "phased out" tool.

![](images/image12.png)

## VS Code + Cline

Cline is an AI programming Agent plugin for VS Code (Visual Studio Code) that can flexibly switch between different large models by configuring different API endpoints. Cline supports multimodal input, MCP tool extensions, and cost monitoring, with all operations requiring user confirmation before execution. It's very suitable for quickly validating ideas or integrating with existing development workflows. Basic features are free, while the enterprise version supports deploying models in private environments.

![](images/image13.png)

![](images/image14.png)

# What is Trae

Trae's full name can be understood as "The Real AI Engineer," an adaptive AI Integrated Development Environment (IDE) developed by ByteDance. It's built on top of the popular VS Code, which means that if you're already accustomed to VS Code, using Trae will feel very familiar and comfortable in terms of both interface layout and basic operations.

Trae's core goal is to be the developer's "intelligent programming partner." Through deep integration of AI capabilities, it can automatically handle a large amount of repetitive work, providing you with a more intuitive and efficient development experience. It's not just a "code completion tool," but hopes to provide help throughout the entire development workflow, from creating projects, writing code, debugging, testing to deployment.

## Installing Trae

Trae is divided into an international version and a Chinese version. The international version requires access to overseas networks but can use the latest overseas models like GPT-5, Claude 4, etc.; the Chinese version mainly supports the latest domestic large models, such as GLM, Qwen, Kimi, etc.

International version download address:

https://www.trae.ai/

![](images/image15.png)

Chinese version download address:

https://www.trae.cn/

![](images/image16.png)

## Trae Interface Introduction

Simply put, Trae and VS Code look almost identical.

![](images/image17.png)

The sidebar on the right is the Copilot interaction window, which can also be understood as the Agent window. If you don't see it temporarily, you can click the sidebar icon in Trae's upper right corner to open it.

![](images/image18.png)

After opening the sidebar, you'll see a `Builder` option - this is Agent mode. Simply put, it's equivalent to a "local version" of z.ai that can help you operate your local environment, install runtime environments, open webpages, etc.

![](images/image19.png)

After clicking "Builder," you'll see "Chat" mode and "Builder with MCP" mode:

* **Chat Mode**: Mainly used for conversing with code in the current folder, or used as a regular chat model. (You can open a folder through the "File" menu in the upper left corner and perform editing operations within that folder. In this case, files created or modified by Builder will only occur within this folder.)
* **Builder with MCP Mode**: Provides more available tools for the Agent (such as connecting language models with other software, querying weather, etc.). You can simply understand it as: MCP allows language models to more conveniently call various external tools.

![](images/image20.png)

In the area below, you'll also see model selection options - click to modify the large model currently in use. In the Chinese version, you can choose to use domestic models like Kimi k2 or GLM; if you're using the international version of Trae, you can also choose overseas models like ChatGPT or Claude. However, since domestic large models are developing very quickly, Kimi, Qwen, GLM, etc. already have practical experience close to Claude 3.5 or 3.7 in many tasks, which is completely sufficient for daily development.

![](images/image21.png)

The above is just a simple introduction to Trae. Next, we can review the operations we did in z.ai before and try to do the same things in Trae.

## Using Trae to Install Python and Frontend Environments

In most cases, our Windows laptops don't come pre-installed with the Node.js environment needed for frontend development, or the Python environment needed for backend/general development. We can try conversing directly with Trae's Agent mode to let it help us install the Python environment or Node.js environment.

![](images/image22.png)

## 📚 Assignment: Write Your First Program with Trae

Next, please try to complete your first program using Trae! Do you remember the previous AI Snake game? Take that prompt you used in z.ai, enter it verbatim into Trae's Agent mode, and see what happens!
