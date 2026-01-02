# Extra Knowledge 9 - CLI AI Coding Tools and Test-Driven Development Principles

In this tutorial, we will introduce AI coding Agents that run directly in the command line. They are different from the Trae and Cursor Agents we've learned about before - CLI AI coding tools can only be used in the terminal. Compared to Agents integrated in AI IDEs, they typically have longer context windows, faster tool invocation speeds, and can support more types of large models. In the latest AI Vibe Coding practice, we often prefer using CLI AI coding tools over IDE built-in coding Agents.

## Starting with CLI

Remember the CLI we introduced earlier? CLI refers to operating software applications through pure text commands in a terminal or command prompt, rather than relying on a graphical user interface (GUI - you can simply understand this as interfaces on computers or phones with buttons that you can click and operate, without needing to enter commands).

> On Windows, common terminals include "Command Prompt (cmd)" and "PowerShell". You can enter "cmd" or "powershell" in your computer's run/search box to launch these command-line programs.

![](images/image1.png)![](images/image2.png)

CLI is naturally suited for text command operations. Among a small group of enthusiasts (programming enthusiasts who pursue excellence), CLI is even more popular than GUI - they want all operations to be completed through the keyboard, feeling that using the mouse actually slows down their coding efficiency.

In industry, CLI is often also the most common interface form, because GUI requires the operating system to additionally render interfaces and manage windows, placing higher demands on computer resources; whereas CLI only needs to pass received commands to the system for execution. Therefore, when connecting to large-scale server clusters, we usually only interact through CLI.

![](images/image3.png)

For many students without CLI experience, you may feel that CLI operations are complex, there are too many commands, and you even worry that "you'll accidentally break your computer." Don't worry. Remember in previous tutorials, we often let Trae help us complete various basic operations? Here we can completely apply this same approach - we can let CLI coding tools help us execute all CLI operations: let it help you enter specified folders, search and process files, run or copy open source projects, etc. The entire process can be completed through conversation with the CLI AI coding tool.

## How It Differs from AI IDEs

We can compare CLI AI coding tools to z.ai and Trae that we learned about earlier. In a sense, CLI AI coding tools can be seen as a special type of z.ai: they similarly only need a simple conversation entry point, and will automatically execute all required operations for you (except sometimes you need to manually open a browser to see the final effect). If comparing to AI IDEs, then CLI AI coding tools can be viewed as the Agent module in the IDE - that is, the conversation area on the side.

![](images/image4.png)![](images/image5.png)

However, because different AI IDEs implement Agents in different ways, with large differences in capabilities, AI coding effects are often unstable. Therefore, CLI AI coding tools are usually developed directly by large tech companies, such as Anthropic behind Claude, and OpenAI behind ChatGPT.

Compared to other AI coding Agents, directly using these major manufacturer products is often the better practice, especially since Claude Code itself is a tool that serves Anthropic's internal R&D team, designed around "meeting engineers' real needs" from the start.

To make a more intuitive comparison, let's briefly look at the differences between Claude Code and a certain AI IDE Agent (using Cursor as an example here):

| Feature                  | Claude Code | Cursor      | Better      |
| ------------------------ | ----------- | ----------- | ----------- |
| Automated task execution | ✅ Very strong | ❌ Limited | Claude Code |
| IDE integration          | ❌ Command line only | ✅ Native VS Code | Cursor |
| Real-time code completion | ❌ None      | ✅ Excellent | Cursor |
| Multi-file operations    | ✅ Very strong | ⚠️ Good    | Claude Code |
| GitHub integrated operations | ✅ Can commit directly | ⚠️ Manual operation required | Claude Code |
| Learning curve           | ⚠️ Medium    | ✅ Easy to start | Cursor |
| Context length           | ✅ Very long | ⚠️ Good    | Claude Code |
| Debugging assistance     | ✅ Automated | ⚠️ Often manual | Claude Code |

Table source: https://northflank.com/blog/claude-code-vs-cursor-comparison

Simply put, CLI AI coding tools can usually:

- Support longer continuous conversations (can even help you "work all day").
- Provide longer context windows (no longer frequently needing you to say "continue").
- Faster response times (can access more custom model APIs).

For coding-related operations, they are usually smarter and more stable than most IDE built-in Agents.

## Common CLI AI Coding Tools

Currently, although there are many open source implementations, in practice we only recommend two main types of CLI AI coding tools as the "preferred combination." You can choose either based on your habits, but it's strongly recommended that you try both, then choose the one that suits you best.

- Codex uses GPT-5 and is stronger in overall capabilities;
- Claude Code works through GLM 4.6 relay API, with overall experience close to Claude 4 but cheaper price.

However, which one is better in actual projects can only be determined by personal testing. Mastering multiple AI coding tools is always beneficial: after becoming proficient, you can flexibly switch between Claude Code, Codex, or Trae in different scenarios. If after multiple attempts you find a certain tool's effect is average, you can directly switch to another tool or model to continue experimenting.

At the same time, because model versions update very quickly, it's recommended to prioritize choosing the solution that performs best in "price-performance (effect/cost)."

### Claude Code

Claude Code is an AI coding tool developed by Anthropic based on Claude large model capabilities. Its main interaction scenario is in the terminal, while also supporting use as a VS Code plugin. Similar to the Agent in AI IDEs, it can deeply understand developers' code repositories and complete end-to-end development tasks through natural language instructions - including code editing, bug fixing, running and fixing tests, managing Git workflows (such as resolving merge conflicts, creating PRs), complex code explanation, executing terminal commands, etc.

![](images/image6.png)

Claude Code's advantages are mainly reflected in: extremely long context window (can handle complete files or even small projects), can proactively clarify vague requirements, automatically plan and assign execution tasks, and deep understanding and explanation capabilities for entire codebase content. Compared to ordinary IDE Agents, it's more suitable for the "immersive vibe coding" development workflow.

In actual use, you can through conversation instructions let it help you create new projects, execute CLI operations (such as organizing folders, batch renaming files, deploying open source projects, etc.), configure development environments (such as installing and debugging Python environments). If you feel a certain piece of code is difficult to understand, or a directory structure is unclear, you can also directly let Claude Code generate structured analysis documents, or provide step-by-step explanations of specific content.

![](images/image7.png)![](images/image8.png)

![](images/image9.png)![](images/image10.png)

If you want to systematically learn Claude Code, you can refer to the course jointly launched by Andrew Ng and Anthropic:
https://www.bilibili.com/video/BV176t2zSEpr

Next, we will learn how to use Claude Code. Because the cost of directly using the official Claude Code is often very high (as shown below), we will instead use APIs compatible with the Claude Code protocol but based on other large models.

![](images/image11.png)

You need to learn the following different solutions (it's best to try them all), then choose the most suitable one as your main practice path.

The first way is to directly use "Anthropic-compatible interface" APIs. With the popularity of Claude Code, more and more large model service providers have begun supporting Anthropic-style calling methods. Common service providers include GLM, Kimi, DeepSeek, and SiliconFlow, etc., all of which provide compatible API interfaces. We will explain specific configurations in detail later.

It should be noted that Claude Code typically consumes a large amount of tokens. If you're worried about API calls generating excessive costs, you can consider purchasing GLM's monthly package (about 20 yuan/month) to control costs. If you want to first feel the actual cost, you can also top up 10 yuan for small-scale testing.

Another way is to use the "Claude Code Route" project. It's an open source tool that not only supports all common API call interfaces, but also allows you to fine-tune the models used for different scenarios, and supports connecting to locally deployed large models. However, because this solution's configuration is relatively complex, it's recommended to start with the first solution.

#### Using Zhipu GLM as Backend (Recommended)

GLM (General Language Model) is a series of large language models independently developed by Zhipu AI. GLM-4.6 is currently the latest version in the GLM series, with its core highlight being excellent performance in code capabilities (on par with Claude Sonnet 4 in public benchmarks and real tasks, and first-tier domestically).

![](images/image12.png)

It also extends the context window to 200K, can handle longer texts and larger volumes of code more comfortably, while strengthening reasoning and tool calling capabilities, achieving a good balance between performance and cost.

![](images/image13.png)

Before connecting GLM, we need to first install Claude Code.

If you find command-line installation steps troublesome, or errors occur midway, you can directly let Trae's Agent help you complete the installation.

```Python
# Install Claude Code
npm install -g @anthropic-ai/claude-code

# Enter your project
cd your-awesome-project

# Start Claude Code
claude

# Press Ctrl+C to exit Claude
```

Next, we need to modify Claude Code's default API request address to support GLM's API service. You can directly copy the content below, let Trae help you create corresponding environment variables; you can also choose to write them permanently into system environment variables (if problems occur, you can also let the Agent help modify them).

First, you need to obtain GLM's API Key and save it in whatever way is most convenient for you.

Domestic version address: https://bigmodel.cn/usercenter/proj-mgmt/apikeys
International version address: https://z.ai/manage-apikey/apikey-list

If you're using **Domestic GLM**, use the following variable configuration:

```Python
# Run the following commands in Cmd
# Note replacing `your_zhipu_api_key` with the API Key you just obtained
setx ANTHROPIC_AUTH_TOKEN your_zhipu_api_key
setx ANTHROPIC_BASE_URL https://open.bigmodel.cn/api/anthropic
```

If you're using **International GLM**, use the following configuration:

```Python
# Run the following commands in Cmd
# Also note to replace `your_zai_api_key`
setx ANTHROPIC_AUTH_TOKEN your_zai_api_key
setx ANTHROPIC_BASE_URL https://api.z.ai/api/anthropic
```

You can directly enter similar prompts in Trae:

⚠️ If you have Trae help you configure "permanent environment variables," then after configuration is complete **you must restart Trae**, otherwise the environment variables in its built-in terminal won't update, which may cause login failure or network connection errors.

```Python
Based on my environment variable settings:
setx ANTHROPIC_AUTH_TOKEN your_zai_api_key
setx ANTHROPIC_BASE_URL https://api.z.ai/api/anthropic

and my key(Replace it with your own key):
681fea485851d29060cc.13gfaendggaFOhb

please help me configure and start Claude Code
```

You will see output similar to the following process:

![](images/image14.png)

> 💡 What are environment variables?
>
> Environment variables are essentially a set of "key-value pair" configuration information stored in the operating system, usually in the form of "variable name = specific value". As long as they're configured in advance in the terminal or system settings, programs can read these variables at any time to get relevant information. Because environment variables can be written directly in the terminal without modifying the code itself, we usually store keys required for accessing large models in environment variables to avoid leakage. Programs only need to read corresponding environment variables to complete large model calls.
>
> In Windows systems, environment variables are also often used to save "call paths" for command-line tools.
>
> We know the terminal itself is also a program. Sometimes we want to start a certain external program in the terminal, such as entering `claude` in the terminal to start Claude Code. The reason you can directly enter `claude` to run is because the terminal reads the system's environment variables, and the PATH variable contains the directory where Claude Code's executable file is located, so the terminal can find and execute it (equivalent to pasting that program's absolute path in the terminal then pressing Enter).
>
> A typical environment variable might look like this: `PATH=C:\Windows\system32;C:\Program Files\Python`. This way we can execute these programs in the system from any path, such as directly entering `python` in the command line to start the Python interpreter.
>
> If you want to view the system's current environment variables, you can enter "environment variables" in Windows search, and in the pop-up "Edit system environment variables" window you can see all variables and their values. Some variables are used to store large model keys, others are used to add program directories for easy invocation from any path.

Now, you can use the latest GLM for Claude Code development. You can try re-running previous projects, or re-challenging tasks Trae didn't complete well, comparing the experience differences.

🎉 Repeatedly "starting over" is not wasting time - every time you redo it, your skills become more solid.

Using exactly the same approach as with GLM, you can also easily connect to other interfaces that support the Anthropic-compatible format.

#### Using Kimi K2 as Backend (Recommended)

https://platform.moonshot.cn/console/account

```Plain
export ANTHROPIC_BASE_URL=https://api.moonshot.ai/anthropic
export ANTHROPIC_AUTH_TOKEN=sk-YOURKEY
```

#### Using DeepSeek as Backend (Recommended)

https://platform.deepseek.com/usage

```Bash
export ANTHROPIC_BASE_URL=https://api.deepseek.com/anthropic
export ANTHROPIC_AUTH_TOKEN=YOU_DEEPSEEK_API_KEY
export API_TIMEOUT_MS=600000
export ANTHROPIC_MODEL=deepseek-chat
export ANTHROPIC_SMALL_FAST_MODEL=deepseek-chat
export CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1
```

#### Other Anthropic-Compatible APIs

Siliconflow:

```Bash
export ANTHROPIC_BASE_URL="https://api.siliconflow.cn/"
export ANTHROPIC_MODEL="moonshotai/Kimi-K2-Instruct-0905"    # Can modify required model yourself
export ANTHROPIC_API_KEY="YOUR_SILICONCLOUD_API_KEY"    # Please replace API Key
```

Alibaba Cloud DashScope (Aliyuncs): https://help.aliyun.com/zh/model-studio/get-api-key

```Python
export ANTHROPIC_BASE_URL="https://dashscope.aliyuncs.com/apps/anthropic"
export ANTHROPIC_API_KEY="YOUR_DASHSCOPE_API_KEY"
```

#### Using Claude Code Route as Backend (Advanced Usage)

Above we explained how to use GLM's official API to replace Claude Code's Anthropic interface. Next, let's look at how the Claude Code Router tool enables Claude Code to adapt to more model APIs.

[Claude Code Router](https://github.com/musistudio/claude-code-router) is an intelligent routing enhancement tool designed specifically for Claude Code. Its core function is to help users distribute AI requests to models on different platforms as needed, with high customizability. It supports connecting to dozens of platforms, including OpenRouter, DeepSeek, Ollama, Gemini, etc., and can also route tasks to specific models by scenario, such as GLM-4.5, Kimi-K2, Qwen3-Coder, etc. For example, you can automatically assign backend tasks to local Ollama to save costs; assign long text/long code tasks to Gemini-2.5-Pro; assign code explanation to DeepSeek.

![](images/image16.png)

This tool also provides convenient UI/CLI configuration management capabilities, and adapts different platforms' API formats through "converters." It supports automated integration such as GitHub Actions and custom extensions, solving the problems of "single model can't cover all scenarios" and "frequently switching platforms is troublesome," helping users use AI tools more flexibly and at lower cost.

![](images/image17.png)

Next, we'll briefly introduce how to install Claude Code Router. It roughly requires the following steps (you can also let Trae help execute them), to prepare the related environment:

```Markdown
npm install -g @anthropic-ai/claude-code
npm install -g @musistudio/claude-code-router
```

After installation is complete, you need to confirm you can use the `ccr` command locally. If you see output similar to the following, installation is successful:

![](images/image18.png)

Next, there are two ways to initialize and configure models:

- Use CCR's built-in UI, open the configuration page it provides in a browser to operate;
- Directly modify CCR's default configuration file (essentially the UI also modifies the configuration file, just provides a more intuitive interface).

If you choose to use CCR UI, you'll see an interface similar to the following:

![](images/image19.png)

At this point, click the "Add Provider" button, and you'll see the following interface. You need to:

1. Enter the model provider's name in Name;
2. Fill in that provider's OpenAI-compatible interface address in API Full URL;
3. Fill in the corresponding platform's API Key in API Key;
4. Fill in the model name in the Models area, click "Add Model" to add;
5. Finally click "Save" to save the configuration.

(There are many advanced options if you scroll down in the interface, but for now you can ignore them.)

![](images/image20.png)

Below are configuration examples for DeepSeek and Kimi:

![](images/image21.png)

![](images/image22.png)

After saving the model configuration, you also need to specify the default model (Default) in the Router area on the right. Click the corresponding dropdown selection, set it to `kimi` (recommended), then click `Save and Restart` in the upper right corner.

![](images/image23.png)

Afterward, just enter `ccr code` in the terminal to start Claude Code's coding workflow through Claude Code Router.

![](images/image24.png)

#### Advanced Usage of Claude Code

Many people when first using Claude Code only treat it as an ordinary conversation tool. But in fact, it has many rich built-in capabilities that can make you more efficient and flexible. Below are some common commands and usage examples:

Reference documentation:

https://docs.claude.com/en/docs/claude-code/cli-reference
https://docs.claude.com/en/docs/claude-code/slash-commands

| Command          | Function                                    | Example                                  |
| ---------------- | ------------------------------------------- | ---------------------------------------- |
| claude           | Start interactive mode                      | `claude`                                 |
| claude "query"   | Execute one-time task and output results    | `claude "explain this project"`          |
| claude -p "query" | Execute one-time question and auto-exit when done | `claude -p "explain this function xxxx"` |
| claude -c        | Continue most recent session                 | `claude -c`                              |
| claude -r        | Resume previous session                     | `claude -r`                              |
| /resume          | Switch back to previous session in current chat | `claude -c`, `/resume`                   |
| claude commit    | Help create Git commit message and commit code | `claude commit`                          |
| /init            | Initialize project description with CLAUDE.md | `/init`                                  |
| /clear           | Clear current session context, prevent information overload | `/clear`                                 |
| /compact         | Compress session history, reduce context token usage | `/compact`                               |
| /cost            | View current consumption                    | `/cost`                                  |
| /model           | Switch model being used (can ignore when using compatible API) | `/model`                                 |
| /memory          | Manage CLAUDE.md memory file                |                                          |
| /help            | Show available command list                 | `/help`                                  |
| exit or Ctrl+C   | Exit Claude Code                            | `exit` or `Ctrl+C`                       |
| /agents          | Advanced feature, will explain later        |                                          |
| /mcp             | Advanced feature, will explain later        |                                          |

**CLAUDE.md**

Reference: https://www.anthropic.com/engineering/claude-code-best-practices

`CLAUDE.md` is a special file that Claude automatically reads and joins into context when starting a conversation. Therefore, it's very suitable for recording:

- Common bash commands
- Core files and tool functions
- Code style conventions
- Testing method descriptions
- Repository collaboration specifications (such as branch naming, whether to use merge or rebase, etc.)
- Development environment configuration descriptions (such as whether to use pyenv, which compiler is recommended, etc.)
- Behaviors or pitfalls in the project that need special attention
- Any information you want Claude to "remember"

`CLAUDE.md` itself has no mandatory format requirements, as long as it's concise and easy for humans to read. For example:

```Plain
# Bash commands
- npm run build: Build the project
- npm run typecheck: Run the typechecker

# Code style
- Use ES modules (import/export) syntax, not CommonJS (require)
- Destructure imports when possible (eg. import { foo } from 'bar')

# Workflow
- Be sure to typecheck when you're done making a series of code changes
- Prefer running single tests, and not the whole test suite, for performance
```

#### Claude Code's Internal Principles

Reference: https://github.com/shareAI-lab/analysis_claude_code

If you're curious why Claude Code is often more useful in many scenarios than Agent coding tools like Trae or Cursor, we can briefly look at its internal working mechanism.

Other CLI AI coding tools' overall implementation is largely similar.

![](images/image25.png)

Claude Code breaks down programming tasks into a continuous "perceive-think-act-verify" loop, calling different tools to complete tasks within it. It mimics human developers' workflow: constantly "write code → run → see results → improve." The system internally continuously executes steps through a main task loop, and in each round, Claude can call different tools - such as reading/writing files, executing commands, searching code, etc. - then based on the real results returned by the tools, decide the next action.

Several key features are worth noting:

- **Stream Processing**: Claude can output results while thinking, rather than having to wait until all code is written before executing.
- **Intelligent Compression**: Long conversations easily lead to excessively long context; Claude reduces the probability of "forgetting" by compressing history into key information, and ensures efficient operation by distinguishing between long-term and short-term memory.
- **Concurrency Control**: Internal parallel design allows multiple tasks to proceed simultaneously without interfering with each other.
- **Sub-agent Management**: In actual work, it's not just equivalent to one "role" handling everything - you can manage multiple sub-agents to collaborate on processing code, with each agent responsible for different tasks, such as specifically responsible for testing, specifically responsible for writing documentation, etc.

### Codex

![](images/image26.png)

![](images/image27.png)

Similar to Claude Code, Codex is an AI collaborative coding tool developed by OpenAI. You can understand it as "OpenAI's version of Claude Code." Its biggest advantage is efficient adaptation to GPT-5.

From actual experience, GPT-5 currently has faster response speeds and lower error rates (higher probability of correct completion in multi-round complex tasks). One of its disadvantages is explanations tend to be "academic" and "technical," sometimes appearing too rigorous and with large amounts of information, which may be slightly difficult for beginners to understand.

You can install Codex through the following command:

```Plain
npm i -g @openai/codex
```

#### Using OpenAI Official API as Backend

If using OpenAI's official Codex entry directly, configuration is very simple: when you've already opened an OpenAI subscription or applied for corresponding API quota, you only need to enter `codex` in the command line to start the program, and complete login following the prompts.

![](images/image28.png)

![](images/image29.png)

#### Using Relayed OpenAI API as Backend

Because the official OPENAI API may have issues such as high prices and strict network requirements, to avoid these restrictions, we can also use other API gateway services to relay calls.

In this way, we only need to purchase corresponding Codex API quota on third-party relay platforms, to get usage experience close to native OpenAI Codex.

Reference: https://open-dev.feishu.cn/wiki/PAqUwWG4IiuwTvkQ2sGcaQuPnXc
Top-up address: https://api.zyai.online/account/topup/recharge

It should be noted that after getting the token quota, we also need to configure the API Key locally.

In the key group settings, pay attention to choose the item specifically for Codex.

![](images/image30.png)

Next, we need to fill the obtained Key into the prompt below, and give the entire prompt to Trae, letting it help you complete the entire configuration process:

```Bash
My API key is: [Paste your obtained sk-xxxxx key here]

Please help me complete the following configuration tasks:

1. Create configuration directory
   - Create a `.codex` folder under my user directory
   - Windows path should be: `C:\Users\[My Username]\.codex`
2. Backup existing configuration (if exists)
   - Check if `.codex\config.toml` exists
   - If it exists, rename it to `config.toml.bak.[current timestamp]` (timestamp format: yyyyMMddHHmmss)
3. Create configuration file
   - Create `config.toml` in the `.codex` directory
   - Write the following complete content:
   ```toml
   preferred_auth_method = "apikey"

   [model_providers.myrelay]
   name = "My Relay Station"
   base_url = "https://api.zyai.online/v1"
   env_key = "MYRELAY_API_KEY"
   wire_api = "responses"
   request_max_retries = 4
   stream_max_retries = 10
   stream_idle_timeout_ms = 300000

   [profiles.myrelay]
   model_provider = "myrelay"
   model = "gpt-5"
   model_reasoning_effort = "medium"

   [tools]
   web_search = true

4. Set system environment variable
Variable name: MYRELAY_API_KEY
Variable value: The key I gave you

5. Confirm completion and report back:

The full path of the configuration file
Whether the environment variable was set successfully
I can use the command `codex --profile myrelay` to run it
```

After configuration is complete, you can start Codex using the relay API through `codex --profile myrelay`. Subsequent usage is similar to Claude Code: just enter your thoughts and requirements in the dialog box at any time.

## More Uses of CLI AI Coding Tools

### Using AI to Write Requirement Documents: Learn to "Specify Requirements"

For large language models, abstract requirements need to be "specified." For example: "I'm hungry" is an abstract requirement, we need to turn it into: "I'm a bit hungry, maybe need to eat a red bean bun, and pair it with a cup of soy milk." - this is a specifiable, specific requirement.

But turning abstract requirements into concrete is actually a very energy-consuming process. If we haven't seen enough cases, it's difficult to quickly associate how to break down abstract problems into detailed modules. At such times, the best approach is to let AI help you complete this "specification" step.

For example, I want to develop a "daily plan" application, the simplest idea might be:

`Please help me write a daily planning app where I can write my plans each day and get reminders.`

AI can indeed break down tasks based on this requirement, then complete them step by step, but errors or understanding deviations can easily occur midway. To reduce risk, we can let AI help us expand the requirements first:

`Based on my needs, please elaborate and provide a more detailed Product Requirement Document for reference. My idea is: Please help me write a daily planner app that supports daily plan-writing and provides reminders.`

At this time, AI might give a complete PRD similar to the following:

```Plain
Product Requirements Document (PRD): "Today's Plan" App
Document Version: 1.0
Creation Date: October 27, 2023
Author: (Your Name/Product Manager)

1. Product Introduction
1.1 Product Name
Today's Plan
1.2 Product Vision
"Today's Plan" is a minimalist and highly efficient daily planning and reminder tool, dedicated to helping users eliminate procrastination and forgetfulness, plan every day clearly, and ensure tasks are carried out through an intelligent reminder system—ultimately enabling users to gain a stronger sense of control and achievement over their time.
1.3 Target Users (User Personas)
We mainly serve three types of users:
Students (Xiao Ming):
Characteristics: Multiple tasks such as courses, assignments, club activities, exam prep, needing organized time arrangement.
Pain Points: Easily forget small tasks or assignment deadlines; feel overwhelmed switching between tasks; want to build regular study and life habits.
Needs: A simple tool to list daily to-dos and provide reminders before class/self-study.
Office Workers (Zhang Wei):
Characteristics: Fast-paced work, many meetings, reports, project milestones, and personal affairs (fitness, picking up children).
Pain Points: Easily forget important meetings or work milestones; get interrupted by urgent tasks and forget the original plan; feel busy but inefficient at end of day.
Needs: Need a tool to quickly record and schedule daily work and send strong reminders at key times (e.g., 15 minutes before meetings).
Freelancers/Self-disciplined Seekers (Li Na):
Characteristics: High freedom of time, but strong self-management required for work output and personal growth.
Pain Points: Easily procrastinate, lack external supervision; start the day without a clear plan, leading to low time utilization.
Needs: Need a tool to help build a daily fixed routine (Morning Routine) and review daily achievements for positive feedback.

2. User Stories
As a user, I want to quickly create today's plan list so I have an overview of all my tasks for the day.
As a user, I want to set specific start and end times for each task so I can create a visual timeline.
As a user, I want to receive push notification reminders before a task starts so I won't miss any important arrangements.
As a user, I want to customize the reminder time (such as 5, 15, or 60 minutes in advance) so reminders better fit my habits.
As a user, I want to easily mark completed tasks so I can feel accomplished and clearly see my progress.
As a user, I want to see a summary of my completed plans at the end of each day for reviewing and self-motivation.
As a user, I want to conveniently edit and delete tasks to handle last-minute changes.
As a user, I want to view plans and achievements from previous days to review my efficiency and habits.

3. Feature Breakdown
Core Features (MVP - Minimum Viable Product)
Module 1: Plan Management
3.1.1 Daily Plan Homepage
Interface: "Today" as the core view, current date shown at the top.
View: Timeline list, clearly showing tasks scheduled from morning to evening. Tasks without a time can be listed in the top or bottom "To-do List" section.
Interactions:
Click the "+" button in the bottom right to quickly create a new task.
Pull down to refresh the page.
Swipe left/right to view yesterday's and tomorrow's plans.
3.1.2 Create/Edit Task
Entry: Click "+" on the homepage or a time slot in the list.
Fields:
Task title (required): Briefly describe the task, e.g., "10 AM Weekly Product Meeting."
Task time (optional):
Set "start time" and "end time."
Provide "all-day" option for unspecified time tasks.
Default time picker should be quick and convenient.
Reminder setting (required, with default value): See Module 2.
Notes (optional): Add further descriptions, links, or location info.
Actions: Save, cancel, delete task.
3.1.3 Task Interaction
Mark as complete: Checkbox before each task; checking adds a strikethrough and gray background, indicating completion. Can unmark if needed.
Edit task: Click the task itself to enter edit page.
Delete task: Swipe left on a task to reveal "Delete" button.
Module 2: Smart Reminder System
3.2.1 Reminder Trigger
Mechanism: Based on task's set "start time" and the user's "reminder lead time," send a push notification from device.
Offline Support: Locally scheduled reminders must trigger even if user is offline.
3.2.2 Reminder Content & Format
Notification title: App name "Today's Plan."
Body: "Reminder: [Task Title] will start at [Start Time]." E.g., "Reminder: Product Meeting will start at 10:00."
Sound: Use system default or offer several simple, effective tones.
3.2.3 Reminder Settings
Global Settings (in Settings page):
User can set a default reminder time, e.g., "15 minutes before task starts." New tasks adopt this by default.
Single Task Settings (in create/edit page):
Users can override global settings for important tasks, choosing specific reminder times like "on time," "5 minutes early," "30 minutes early," or "1 hour early."
Provide "no reminder" option.
Subsequent Features (V1.1, V2.0)
3.3 Daily Review & Statistics
Push a summary notification at a set time every night (e.g., 22:00): "How was your day? Take a look at your achievements!"
Generate a simple daily report card: shows total planned tasks, completed tasks, completion rate, plus an encouraging message.
3.4 History Review
Calendar view to click on any past day and check its plans and completion status. Days with high completion rates marked with a special color.
3.5 Templates
Allow users to save a successful daily plan as a template, e.g., "Efficient Workday," "Relaxing Weekend."
When creating tomorrow's plan, one-click import a template, modify slightly to save time.
3.6 Themes & Personalization
Offer dark mode.
Allow changing several primary color themes.

4. Non-Functional Requirements
4.1 Performance
Response: App launch time under 2 seconds; adding/editing tasks must be smooth and lag-free.
Resource Use: Low battery and memory consumption in background; do not over-consume resources waiting for reminders.
4.2 Usability
Minimal & intuitive: UI must be minimal, primary functions accessible within 3 clicks. No tutorial needed for new users.
Error tolerance: Offer undo (e.g. brief undo after mistakenly deleting a task).
4.3 Reliability
Reliable reminders: Reminder function is the product's lifeline; must guarantee 99.99% timely and accurate delivery.
Data loss-free: User plans must be reliably stored locally. Future versions can support cloud sync to prevent data loss on device change.
4.4 Compatibility
Platform: Support major iOS and Android versions (latest 3-4 releases).
Screen: Layout must fit various phone screen sizes.

5. Roadmap
V1.0 (MVP):
Goal: Validate core value—planning & reminders.
Features: Complete all "Core Features" described above (Plan management, smart reminders).
V1.1 (Quick Optimization):
Goal: Improve retention and achievement.
Features: Add "Daily Review & Statistics," "History Review."
V2.0 (Enhanced Experience):
Goal: Increase efficiency and personalization.
Features: Add "Templates," "Themes & Personalization," and start developing "Cloud Sync."
```

Compared to our original "help me write an app that can record daily plans and remind me," this document is now much more detailed. You can add, delete, or modify content based on your real needs; for certain modules you're unsure about, you can also continue letting AI provide more alternatives, then you choose and merge them into the final version.

Through this method, we can easily turn abstract ideas into specific descriptions. For AI development, "specific" is productivity - the more specific the requirements, the easier to get structurally stable, higher quality projects. You can try using this method to redo a previous small project, comparing the effect differences.

If you feel such "requirement prompts" are too long, a very natural approach is to write them separately into a markdown document as your "requirement document/development document/PRD." Afterwards, every time you let AI write a project, you only need to let it "refer to this document," rather than retyping the long prompt each time. You can also continuously improve this document during iterations, letting future projects directly benefit.

Below are some other common usage scenarios:

### Managing Folders

We can try using CLI AI coding tools to manage various files in the current folder. For example, you have a bunch of messy files that need organizing, you can say to Claude Code or Codex:

`Please help me organize the contents of the current folder. I want to group files with the same content together & I want to group files from the same time period together. Please help me handle this.`

### Developing New Projects

This is almost exactly the same as our previous usage in z.ai and Trae - we can also directly use CLI AI coding tools to develop new projects from scratch. Of course, it's best to prepare a requirement document in advance.

The more detailed the requirement document, the better the final result. You can perform multiple rounds of optimization on the document based on constantly changing ideas; the more complete the document, the more stable and mature the code implementation.

### Deploying Open Source Projects (e.g., Dify)

For students new to computers, deploying an open source project from GitHub is often very difficult. But we can completely leave this to Claude Code, just as we did in the Dify tutorial:

https://github.com/langgenius/dify

If I want to run my own Dify locally, I only need to throw this link to Claude Code, then enter:

`I want to deploy this GitHub project ``https://github.com/langgenius/dify`` . Please help me clone the project and run it.`

Upon receiving your request, Claude Code will automatically complete a series of operations, including pulling code from GitHub, configuring the runtime environment, starting the project, etc. If any step errors or the project startup status is abnormal, you can then perform a small amount of manual processing based on prompts. Besides Dify, you can also use Claude Code to help you deploy most common GitHub open source projects - you only need a dialog box, plus time to drink a cup of coffee ☕️.

![](images/image31.png)

### Explaining Code and Writing Documentation

For some complex projects, or large projects automatically generated by AI, you may feel the code is too long, too much logic, and difficult to understand. At this time you can let CLI AI coding tools help you "read code." You can ask questions like:

- Please help me explain this project: how to run, how to use, how to modify and continue development in the future?
- Please help me explain this project's overall workflow: how does the program run? What operations can users do in the interface?
- Please help me write complete documentation for this project, including development documentation and runtime documentation, etc.
- Please based on all content in my current folder, write a detailed explanation and save it to the specified markdown document.

### More Uses

Of course, CLI AI coding tools can do much more than the above. Don't just treat it as a "code writing tool," but view it as an intelligent Agent with independent action capabilities. You can let it help you:

- Manage and organize local files;
- Write diaries and summaries;
- Analyze and fix system errors;
- Execute various repetitive command-line tasks, etc.

Perhaps in the near future, it will become the most important and most understanding AI partner on your computer.
