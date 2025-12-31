# Project 2: Exploring the Capability Boundaries of AI Tools

# Review Questions from Last Lesson

In the previous lesson, we learned how to use z.ai to create an AI-native Snake game and attempted to integrate APIs from the DeepSeek and SiliconFlow platforms. (In subsequent courses, we will frequently use APIs from different models; this was just a demonstration example.)

However, this was just a small test. You can confirm whether you've mastered the content from the last lesson by answering the following questions:

* How can I use z.ai's full-stack development features to turn my ideas into reality?
* What is the difference between a normal application and an AI application? What exactly is an AI-native application?
* What exactly is an API? What is a cloud service platform? How can I get a Large Language Model (LLM) to help me integrate APIs for language and image models?
* If we want to "call" a new model, where can we usually find the method?
* What is the difference between using an AI product and using other ordinary programs?
* How to conduct simple AI product research? Where can I find the latest AI product research, and where can I get information about AI product companies that have received key investments?

If you find anything you don't understand, please refer to the documentation from the last lesson to find answers, or ask directly in the WeChat group.

In this lesson, we will apply the basic AI application development skills, understanding of APIs and cloud platforms, and the ability to think about AI-native concepts that we learned in the last lesson.

A true AI product master needs to thoroughly understand the capability boundaries of AI tools. They need to know what the latest AI tools are, which ones are the most useful, which models offer the best price-performance ratio, and how to combine different tools to complete more meaningful tasks.

It's just like being a boss: you need to understand the overall capabilities of your "AI employees" to make the most of them.

# 💡 What You Will Learn

In class, you need to choose one track for focused learning. But if you're motivated, you can try to complete all tracks after class!

* **Web-based AI Coding Capabilities (AI Coding Track):** Understand the capabilities and limitations of different programming websites, and experience the difficulty of implementing requirements using different models.
* **Concepts and Basic Skills of Prompt/Context Engineering (LLM Track):** Master how to call and integrate different Large Language Models (LLMs), identify their capability boundaries, and understand why writing prompts in industrial environments is challenging.
* **Common Use Cases and Basic Skills for Image/Video (Image/Video Track):** Understand the use cases and capability boundaries of state-of-the-art image and video models, and recreate creative videos.
* How to identify state-of-the-art LLMs and image models, and how to use them.

# 🤖 AI Coding Expert Track

In the first lesson, we learned entry-level Vibecoding tools. However, to become a master, you must now take on more responsibility: within a given time, you need to choose any of the recommended Vibecoding tools below to recreate the provided example—or even surpass it.

![](images/image1.png)

We will use the Super Tic-Tac-Toe game as a test example, which can be accessed here:

[https://space.coze.cn/coding-expert-runtime/295344603906?task_id=7540925598573003046](https://space.coze.cn/coding-expert-runtime/295344603906?task_id=7540925598573003046)

![](images/image2.png)![](images/image3.png)

This game was created in Coze Space (which can be understood as a full-stack development platform similar to z.ai, developed by another LLM company) and won first place in a Coze Space competition. It's simple yet engaging. You need to choose a platform and try to **recreate** the Super Tic-Tac-Toe game, **with rules and final results almost identical to the original. Do your best to make it exactly the same!!**

During the recreation process, you can provide information to the development platform in any way possible—for example, **by sharing links, providing text descriptions, or uploading images.** Observe which method is most effective and which platform allows for the fastest recreation. To avoid misunderstandings, you must play the game once beforehand to ensure you fully master its rules.

Next, we will review the platforms available for selection. Some of you might already know how to use an AI IDE for coding; however, to intuitively experience the AI coding features of different web-based platforms, we still recommend you follow the suggestions provided below:

## 📚 Class Assignment: 100% Recreation of Super Tic-Tac-Toe Game

**Task Goal: Do your best to make it exactly the same!**

Thanks to Yerim's detailed tutorial [Vibe Coding] Snake Game Tutorial. **We can choose any of the following platforms to recreate the game**, and you must complete the task at all costs. (If you're not sure where to start, you can even try asking an LLM for advice—such as how to write prompts or what steps to take—to fully recreate the project.)

Please check out the introduction to the following coding platforms (Yerim's detailed tutorial) and choose a **Web-based** tool to recreate the Super Tic-Tac-Toe game.

![](images/image4.png)

Or you can also try Coze Space (Web-based): https://space.coze.cn/

## Industry Applications

Let's look at this field research article together: *[Survey: AI Wave Continues to Grow in Software Development Teams](https://github.blog/news-insights/research/survey-ai-wave-grows/)*

![](images/image5.png)

GitHub, the world's most famous code hosting platform, surveyed 2,000 people from enterprise software development teams in the US, Brazil, India, and Germany. The survey focused on the use, experience, and expectations of generative AI tools in software development.

![](images/image6.png)

According to this survey, job seekers consider proficiency in AI coding tools an important asset. Almost all respondents (99-100%) believe this skill makes them a more attractive candidate, emphasizing the growing importance of AI in various fields. Notably, a large proportion (43% in Germany, 56% in India) believe this expertise significantly improves their employability.

So... choosing this course means you're a smart person, right? :)

# 🫧 LLM Expert Track

## Prompt Engineering

### What are Prompts and Prompt Engineering

![](images/image7.png)

When we talk about prompts, we can simply understand them as text inputs when interacting with large models. But have you ever wondered how they work? Why do we need so-called "Prompt Engineering"? Why is an "engineering" approach needed?

To answer these questions, we need to start with model training. As is well known, the training results of common deep learning models can be roughly described as a "black box." This is because we only know the data input into the model, but not what kind of output it will produce—even though the output is likely to be consistent with the characteristics of the dataset. We can only roughly grasp the true style of the model's response after training is complete.

![](images/image8.png)

In the pre-training phase, the model is trained on massive amounts of text (such as novels, textbooks, etc.) for text continuation tasks. This process teaches the model how to accurately predict the next word, or even subsequent sentences and paragraphs. Later, to enable large models to handle conversational tasks, we created large amounts of dialogue data for "Instruction Fine-Tuning" (fine-tuning the model to follow human instructions). Based on underlying principles, the closer our prompt input style is to the model's internal rules, the more likely its output will meet our needs.

> To gain a deeper understanding of knowledge related to LLMs, please read the following optional material: A Brief Explanation of Large Language Models (LLM) https://www.bilibili.com/video/BV1xmA2eMEFF/
>
> Below are data examples used in the three core stages of Large Language Model (LLM) development. This provides a basic understanding and does not require deep mastery at this stage.
>
> **1. Pre-training Phase and Data**
>
> The pre-training phase involves initial training of the model on large-scale general text data. The goal is for the model to master the basic rules of language, grammatical structures, factual knowledge, and reasoning abilities, laying a foundation for subsequent fine-tuning for specific tasks. This stage is the most computationally intensive and resource-consuming part of the process.
>
> The data consists of massive amounts of unstructured text that has not been manually labeled. These data sources are extremely diverse, including web pages crawled from the entire internet (such as the Common Crawl dataset), millions of digitized books, Wikipedia, academic papers, and open-source code repositories. The core characteristics are "massive" and "unlabeled."
>
> **Learning Process:**
>
> Learning is conducted through auto-regressive language modeling. The model receives the first part of a text (e.g., "Natural selection, first proposed by Darwin in On the Origin of Species (1859)..."), and then predicts subsequent words ("...drives biological evolution through changes in heritable traits."). The training objective is to minimize the cross-entropy loss between predicted words and actual words, enabling the model to master language patterns and world knowledge.
>
> * Book Excerpt: "Natural selection, first proposed by Darwin in On the Origin of Species (1859), drives biological evolution through changes in heritable traits."
> * Web Content: "Solar and wind energy emit far fewer greenhouse gases than coal or natural gas."
>
> **2. Fine-Tuning Data**
>
> **Description:** Adapt the model to specific use cases using a small amount of structured, task-specific data (input → output pairs). This process is also commonly referred to as instruction fine-tuning.
>
> **Learning Process:**
>
> A supervised learning paradigm is adopted. The model receives a complete input (e.g., "How do I return an item?") and learns to generate a standard answer ("Log in to your account →..."). By minimizing the difference (e.g., cross-entropy loss) between the model's output and the standard answer, the model's parameters are optimized, enabling it to master the input-output mapping for that specific task.
>
> * Input (User Query):
>
> "How do I return an item?"
>
> * Output (Bot Reply):
>
> "Log in to your account → 'Order History' → Select order → 'Initiate Return'. Refunds will be processed within 5-7 days after verification."

Given that the model is a black box, people have tried various ways to interact with it—some work well, others don't. Prompt engineering emerged from this context. In fact, because we don't know what prompts the model responds best to, and we're not sure which prompting strategies can be transferred to other models, **we need to summarize and systematize the results of these "black box" interactions.**

As more people use large models, the demand for controllable outputs and controllable functions of these models grows—this is where the concept of "engineering" comes in. Engineering here emphasizes three key attributes: **reproducibility, verifiability, and transferability**. Our goal is to develop a set of effective rules that can improve the quality of model responses while being applicable to different models. This is exactly what prompt engineering encompasses: we add specific methods to the "text input" to make large models perform better.

Some of these methods are supported by scientific evidence, while others stem from extensive experimentation—experience and hypotheses leading to an intuitive grasp of the model's "most acceptable internal language," thereby providing better model output results.

In short, in actual work, when we continuously refine existing prompts or explore the best prompts—the goal is to make the output more stable, meet expectations, and establish a transferable, long-term reusable, and effective prompt methodology for improving performance—this process can be called prompt engineering.

#### Reviewing the Snake Game

Let's review the process of interacting with the model in the last lesson. In fact, our input box can be seen as a small instruction, but it's not yet the prompt we need to emphasize in the model. For example, we entered a sentence: *"Help me create a front-end page that generates cats. When I enter a sentence, it should generate a cat that matches the description."*

![](images/image9.png)

This sentence itself can be considered an instruction for interacting with z.ai, but it's not the final prompt we use. The reason is that in reality, z.ai first needs to conduct extensive thinking and research based on our sentence to help us write the code that calls the Large Language Model and the image generation model.

![](images/image10.png)

However, what we actually transmit to the model itself is not just the simple initial sentence. Let's look at the real prompt used inside the model:

![](images/image11.png)

This is the actual "prompt" passed to the image generation model, which is different from the instruction we directly use to interact with z.ai. Remember what was mentioned earlier? Results might be better if our prompt is closer to the style of the training dataset.

Now, you might wonder why the prompt for generating cat images is so concise—this is because the style of the image training dataset is roughly like that. For more complex images, prompts look like the examples below. You'll notice their style is also completely different from the prompts we use when interacting with Large Language Models like ChatGPT:

```Bash
Chinese ink wash landscape, misty mountains, lone boat, zen, monochrome, 4K
```

```Bash
A minimalist Chinese ink wash landscape (shanshui style), distant misty mountains (light gray and black ink washes), a single small wooden boat on calm gray water, one lone fisherman in traditional bamboo hat, sparse pine trees on the mountain slopes, light fog floating above the water, empty negative space (white background), simple brush strokes, monochromatic (black, white, gray), high contrast, elegant, zen atmosphere, 4K, clean lines.
```

When we review the prompt used by the Snake game model to generate poetry, we also find it quite complex:

![](images/image12.png)

This complex structure and composition is the subject we need to study next, and we will use different simple examples to deepen our understanding.

#### Reasoning Models vs. Non-Reasoning Models

However, before we delve into actual techniques, we first need to learn a new concept called reasoning models and non-reasoning models—this is to avoid applying techniques to the wrong type of model. When using large models, we might sometimes observe that certain models go through a reasoning process: they need to perform some form of thinking before providing a final answer. We call this type of model a reasoning model.

![](images/image13.png)

The other type of model does not require a thinking process and provides the answer directly; we call these non-reasoning models.

![](images/image14.png)

The key difference between these two categories of models lies in their training methods: reasoning models take time to process and reason through your question, which often leads to more accurate answers. However, for prompt engineering, the effectiveness of techniques varies significantly between model types—prompts that work well for non-reasoning models might not perform as well in reasoning models.

In general:

* Reasoning models tend to require simpler prompts. In many cases, overly long prompts do not add value and might even hinder performance.
* For non-reasoning models, when dealing with complex requirements, you can try using very detailed, granular prompts to ensure the output perfectly meets your expectations.

Most of the models we'll test are more responsive to prompt engineering techniques tailored for non-reasoning models. This is because reasoning models often thrive under shorter prompts and don't require strict, complex rules. That said, the main goal of this tutorial is hands-on experience: you can also switch between reasoning and non-reasoning models, input the following prompt engineering examples, and compare the outputs to observe how results change.

### Examples

Next, we will learn common prompt engineering methods, and we'll understand the deep impact of different prompt structures on results.

To test how different models react to different prompts, we'll use the SiliconFlow platform we used in the last lesson.

[https://cloud.siliconflow.com/me/playground/chat](https://cloud.siliconflow.com/me/playground/chat)

![](images/image15.png)

First, click on "Chat" in the leftmost sidebar. Scroll through the middle panel until you see the "Add Model for Comparison" option. After clicking it, scroll down again and click on "Model" to select and switch between different models, ensuring you have two different models in the right-hand panels for comparison. At this point, you can directly enter any prompt in the right-hand input box, and after sending, you can see the differences in their outputs.

![](images/image16.png)

Next, we will introduce common prompt engineering optimization techniques. Please choose at least two of the following platforms and compare the differences in LLM output results before and after applying prompt engineering optimization.

However, as you use these techniques, please think carefully about two questions:

1. In what scenarios is this method more effective?
2. Once we have reasoning models, will this method become less important or even unnecessary?

#### 1. Zero-Shot Prompting: Basic Dialogue

The most basic way to ask a question is Zero-Shot Prompting, where you give the model an instruction directly without providing any examples. This works well for very simple, clear-cut tasks that the model is already very familiar with. For example, if you want to perform basic sentiment classification, you could provide the following prompt.

Prompt:

> Classify the following text as neutral, negative, or positive.
>
> Text: I think this vacation is okay.
>
> Sentiment:

Output:

> Neutral

While this works for simple tasks, its limitations become clear once tasks become more complex or novel, which is where more advanced techniques are needed.

#### 2. Few-Shot Prompting: Teaching the Model Through Examples

When a task is more complex, or the model needs to understand a new concept, just giving an instruction isn't enough. With Few-Shot Prompting, you provide one or more complete "Question + Answer" examples to teach the model the pattern, format, and logic you expect. For example, imagine you want the model to learn a made-up word, "farduddle." A direct prompt might confuse the model.

Prompt:

> "farduddle" means "to jump up and down rapidly in excitement." Please use "farduddle" in a sentence.

Output (A likely result):

> That was a fun farduddle.

The model is confused and uses the word incorrectly. However, by providing an example first, you can guide it. Look at this improved prompt where we first show it how to handle a similar made-up word.

Prompt:

> A "whatpu" is a small furry animal native to Tanzania. An example of a sentence using the word whatpu is:
>
> We saw these very cute whatpu while traveling in Africa.
>
> "farduddle" means "to jump up and down rapidly in excitement." An example of a sentence using the word farduddle is:

Output:

> When we won the game, we all started to farduddle in celebration.

Now, the model responds correctly. It learned the pattern from the "whatpu" example and applied it, demonstrating how Few-Shot Prompting teaches the model how to do something, not just what to do.

#### 3. Chain-of-Thought (CoT) Prompting: Guiding the Model to Think Step-by-Step

For problems that require reasoning or multiple logical steps, asking for the answer directly often leads to mistakes. The core idea of Chain-of-Thought is to guide the model to "write out its thinking process" before giving the final answer. If you ask a math word problem directly, the model might trip up.

Prompt:

> I went to the market and bought 10 apples. I gave 2 to the neighbor and 2 to the repairman. Then I went and bought 5 more apples and ate 1. How many apples do I have left?

Output (A common mistake):

> 11 apples.

It missed a step. But by simply adding the phrase "Let's think step by step" to the end of your prompt, you can activate its reasoning capabilities.

Prompt:

> I went to the market and bought 10 apples. I gave 2 to the neighbor and 2 to the repairman. Then I went and bought 5 more apples and ate 1. How many apples do I have left?
>
> Let's think step by step.

Output:

> Okay, let's break this down:
>
> 1.  You started with 10 apples.
>
> 2.  You gave 2 to the neighbor, leaving you with 10 - 2 = 8 apples.
>
> 3.  You gave 2 to the repairman, leaving you with 8 - 2 = 6 apples.
>
> 4.  Then you bought 5 more apples, so now you have 6 + 5 = 11 apples.
>
> 5.  Finally, you ate 1 apple, so you have 11 - 1 = 10 apples left.
>
> So, you have 10 apples left.

This simple addition breaks the problem into manageable steps, significantly improving accuracy for reasoning tasks.

#### 4. Role-Playing: Assigning Expert Personas for Higher Quality Output

Asking the model to act as a specific character, like an expert or a teacher, can dramatically affect the style, tone, and depth of its output. This gives the model a clear "persona" that makes its response much more tailored to a specific audience. If you ask it to explain a concept simply, you'll get a dry, academic answer.

Prompt:

> Explain "photosynthesis."

Output (A likely result):

> Photosynthesis is the process by which plants, algae, and some bacteria convert light energy into chemical energy, transforming carbon dioxide and water into glucose (sugar) and oxygen. The chemical equation is 6CO₂ + 6H₂O → C₆H₁₂O₆ + 6O₂.

However, if you assign it a role, the output transforms.

Prompt:

> You are an experienced science writer for children. Explain "photosynthesis" to a group of 8-year-olds. Use fun analogies and avoid complex chemical terms.

Output:

> Hey there, kids! Imagine a plant is like a tiny magic chef. But instead of cooking for us, it's making its own "power lunch"!
>
> This little chef's kitchen is its leaves. It needs three ingredients:
>
> 1.  Sunlight: This is like the power that turns on the stove.
>
> 2.  Air (the carbon dioxide inside): This is like the flour in a recipe.
>
> 3.  Water: Sucked up from the roots, this is like the water used to mix the dough.
>
> When the sun shines on the leaves, the "chef" goes to work! It mixes the air and water together, using the sun's power to turn them into yummy "energy candy" (that's the plant's food). And the coolest part? While it's cooking, it breathes out fresh air—oxygen—which is exactly what we need to breathe!
>
> So, photosynthesis is just a plant making its own lunch and cleaning the air for us at the same time! Pretty magical, right?

This technique is incredibly powerful for tailoring the model's communication style to your exact needs.

#### 5. Using Delimiters (like XML tags): Structuring Prompts to Avoid Confusion

When your prompt contains multiple components, like background information, instructions, and examples, the model can get confused. Using clear delimiters, like XML tags, helps the model understand your intent accurately by breaking the prompt into logical modules. A jumble of instructions can lead to missed requirements. By structuring the prompt with tags, you provide clarity.

Prompt:

> `<instructions>`
>
> 1.  Generate a summary for the content within the `<text>` block.
>
> 2.  The summary must strictly follow all rules within the `<rules>` block.
>
> `</instructions>`
>
> `<text>`
>
> Artificial Intelligence (AI) is a broad field encompassing a range of technologies, from robotics to natural language processing. A core branch of AI is Machine Learning, which allows computer systems to learn from data and improve without being explicitly programmed. Deep Learning, a subset of Machine Learning, has led to massive breakthroughs in recent years.
>
> `</text>`
>
> `<rules>`
>
> 1.  The summary length must be exactly three sentences.
>
> 2.  The summary must include the keyword "Machine Learning."
>
> 3.  The tone of the summary should be professional and objective.
>
> `</rules>`

Output:

> Artificial intelligence is a vast field of technology, with Machine Learning serving as one of its core branches. Machine Learning enables systems to learn from data and improve on their own without explicit programming. As its subset, deep learning has recently driven major advancements in the field.

This structured approach prevents the model from confusing your instructions with the text it's supposed to analyze and produces more reliable output that satisfies all requirements.

#### 6. Letting the LLM Be Your Prompt Engineer

Writing the perfect prompt requires precision, clarity, and an understanding of how the model interprets instructions. Instead of manually refining prompts through trial and error, you can leverage the language model itself as your assistant prompt engineer.

Imagine you want the model to generate product descriptions but aren't sure how to create a powerful prompt for your marketing team.

Prompt:

> Create a prompt that I can use to generate compelling product descriptions.

Output (A likely result):

> Here is a comprehensive prompt you can use to generate compelling product descriptions for your team. It includes placeholders for key details, defines the target audience and tone, and specifies the desired output format.
>
> Generated Prompt:
>
> Role: You are an expert e-commerce copywriter specializing in direct-to-consumer brands.
>
> Task: Write a compelling product description for the item below.
>
> Product Details:
>
> * Product Name: `[Insert Product Name]`
> * Key Features (3-5 bullet points): `[List the most important features]`
> * Target Audience: `[Describe the ideal customer, e.g., "eco-conscious millennials," "busy parents," "tech enthusiasts"]`
> * Unique Selling Point: `[What makes this product stand out?]`
>
> Instructions:
>
> 1. Tone: The tone should be `[Choose 2-3: e.g., "energetic and playful," "luxurious and sophisticated," "reassuring and professional"]`.
> 2. Format:
>    1. Start with an engaging 1-2 sentence hook.
>    2. Follow with a paragraph (3-4 sentences) expanding on key features and benefits, connecting them to customer needs.
>    3. Use a bulleted list to highlight the top 3 features.
>    4. End with a strong call to action.
> 3. Constraints:
>    1. Total length should not exceed 150 words.
>    2. Do not use overly technical jargon.
>
> By using this structured template, you can ensure consistent and high-quality output every time.

This approach to prompting is highly effective for several reasons. First, LLMs are excellent at creating structured text and can quickly formulate a comprehensive prompt that includes elements you might forget, like specifying tone, format, and constraints. Second, the process forces you to clarify your own goals as the model translates your simple objective into a detailed set of instructions.

By automating the prompt design process that usually takes many iterations, it saves significant time and allows you to jump straight to generating high-quality results.

## 📚 Class Assignment 1: Replicating Prompt Examples

Choose at least two of the techniques from the examples above and replicate them. For each technique, create two versions of a prompt: one using the technique and one without. Record both outputs and analyze how using the technique improved the results.

Here are some examples. Feel free to combine the tips above with these examples to try different questions—especially ones from your own life.

> **Example 1: Explaining Quantum Computing to a 10-Year-Old**
>
> Without Technique:
>
> "Quantum computing utilizes quantum-mechanical phenomena, such as superposition and entanglement, to perform calculations. Quantum computers are fundamentally different from classical computers, which use bits that can only be in states corresponding to 0 or 1."
>
> Output Without Technique:
>
> "Quantum computers use special properties of physics to do calculations in a different way than regular computers. Instead of using bits that can only be 0 or 1, they use qubits that can represent multiple states at once."
>
> With Technique:
>
> "Explain quantum computing in simple language and with a fun analogy that a 10-year-old can understand. Compare it to something familiar in a child's life."
>
> Output With Technique:
>
> "Imagine your normal computer is like a coin that can only be heads or tails—only two possibilities. A quantum computer is like a magic coin that can spin, being both heads and tails at the same time! This superpower lets it solve really hard puzzles much faster than a normal computer."

The version using simple language and analogies created an explanation that is much more accessible to a child, whereas the other version, while accurate, used technical language that would confuse a young audience.

> **Example 2: Analyzing Product Reviews Using Delimiters (XML Tags)**
>
> Without Technique:
>
> Summarize this product review and state whether the reviewer recommends it. The review says: I recently purchased the XYZ headphones and have been using them daily for two weeks. The sound quality is exceptional, with crisp highs and deep bass. However, they become uncomfortable to wear after about an hour. The battery life is longer than advertised, which was a nice surprise. I'm torn because the sound is great but the comfort is lacking. I would recommend them to someone who doesn't need to wear headphones for long periods.
>
> Output Without Technique:
>
> "The reviewer has been using the XYZ headphones daily for two weeks, praising the exceptional sound quality with crisp highs and deep bass, and the surprisingly longer battery life than advertised. However, they found the headphones uncomfortable after an hour of use. They recommend the headphones for those who don't need to wear them for long durations."
>
> With Technique:
>
> <instructions>
>
> 1. Create a one-sentence summary for the content within the `<review>` block.
> 2. Determine whether the reviewer recommends the product.
> 3. List one pro and one con mentioned.
>    `</instructions>`
>
> <review>
>
> I recently purchased the XYZ headphones and have been using them daily for two weeks. The sound quality is exceptional, with crisp highs and deep bass. However, they become uncomfortable to wear after about an hour. The battery life is longer than advertised, which was a nice surprise. I'm torn because the sound is great but the comfort is lacking. I would recommend them to someone who doesn't need to wear headphones for long periods.
>
> </review>
>
> Output With Technique:
>
> 1. Summary: After daily use for two weeks, the reviewer has mixed feelings about the XYZ headphones, noting both strong positives and negatives.
> 2. Recommendation: Conditional recommendation for those who do not need to wear them for long periods.
> 3. Pro: Exceptional sound quality with crisp highs and deep bass; Con: Uncomfortable after about an hour of wear.

Analysis: The version using delimiters produced a more structured response that addressed all three requirements directly, while the other version merged all information into a single paragraph without clearly separating the requested elements.

👋 Your turn: Choose two techniques and create your own example following the same format. Include both versions (with and without the technique), their outputs, and your analysis of the differences.

## Context Engineering

### What is Context Engineering

Simply put, context refers to all the content generated during our conversation with a Large Language Model (LLM). However, because LLM conversations have fixed length limits (e.g., 32k tokens, 128k tokens), we cannot expect the model to retain content mentioned at the very beginning of the dialogue—including the initial logic—after a long conversation. This is why we need to strategically manage the flow of information in our interactions with LLMs.

For example, if we ask an LLM to process a book with millions of words, it usually cannot "read" the entire text directly. In this case, we need to effectively compress the context—or rather, the book's content (otherwise we might copy and paste all of it to the model). Suppose the book has 30 chapters: we can first summarize the core content of each chapter, and then input these summaries into the final dialogue with the LLM. This is a classic example of context engineering, as it effectively solves the problem of "context overflow"—addressing issues like being unable to have a meaningful interaction, unable to generate effective summaries, and losing key information.

![](images/image17.png)

More formally, Context Engineering is the art and science of carefully designing and managing information inputs for Large Language Models (LLMs). Its goal is to ensure the model has the most relevant and accurate context when performing a task. It's more than just writing instructions (which is "Prompt Engineering"); instead, it looks from a broader perspective at how to fill the model's "context window" with just the right information.

![](images/image18.png)

Unlike prompt engineering, which focuses primarily on the instructions themselves, context engineering treats the context window as a finite space that needs careful curation. The core challenge lies in selecting the right context and ensuring this context fits within the constraints of the limited window. Context refers to the sum total of all information provided to an AI agent or LLM to perform a task; in actual engineering, we need to input various types of information into an LLM, mainly including the following components:

* System prompt/instruction: Defines the agent's persona and task objectives.
* User input: The user's question or task request.
* Short-term memory or chat history: Provides immediate context from the current conversation.
* Long-term memory: Used to store and retrieve information across multiple conversations or over long periods.
* Information retrieved from a knowledge base: Data obtained from external databases, APIs, or similar sources via vector search or other methods.
* Tools and their definitions: Informs the model about which tools it can use to complete a task.
* Responses from tools: Results returned after tool execution, serving as a basis for the model's next action.
* Structured Information: Information provided or requested in specific formats (like JSON Schema) to compress context and prevent information overload.
* Workflow/Global State: Acts as a "scratchpad" for storing and retrieving global information during multi-step agent tasks.

At this point, you're definitely thinking, *"What on earth is this? I don't understand."* That's perfectly fine—we only need to roughly know that it's complex and don't need to fully master every detail. We'll break down each component for you in future advanced courses.

The main reason context engineering emerged is that we need to engage in multi-turn conversations with Large Language Models (LLMs). Furthermore, based on updates to the interlocutor's information—such as conversation context, emotions, etc.—the model must not lose track of key conversation records or deviate from the intended direction. This requires selective and restrained handling of the content of each dialogue turn. Moreover, **the configuration of the LLM itself—namely the system prompt (the core prompt)—requires a higher level of processing.**

For now, you just need to know that context engineering focuses on **System prompts/instructions**, the selection of information, and the compression and organization of information; here we can focus first on how system prompts and instructions are handled in complex contexts, and we'll explore more components later.

## 📚 Class Assignment 2: Context Ablation Experiment

This experiment is designed to give you deep insight into how complex, production-grade prompts work through the synergy of their multiple key components. You will use "ablation studies"—systematically removing specific parts of a prompt—to observe and analyze behavioral changes in an AI customer service representative named "Eva." Ultimately, you will be able to articulate the decisive role each component (e.g., identity definition, behavioral constraints, escalation protocols, few-shot examples) plays in ensuring the **accuracy**, **consistency**, and **safety** of AI outputs.

#### **Part 1: Baseline Experiment - The "Golden Standard" Prompt**

This is the complete, optimized prompt we designed for our AI customer service agent, "Eva." It contains all the elements we expect and serves as the control baseline for all subsequent experiments.

**The "Golden" Prompt:**

```Plain
# IDENTITY and PURPOSE
You are Eva, a senior AI Customer Support Specialist at "InnovateAI," a company that develops the creative software suite "SynthWave Pro." Your primary goal is to provide helpful, accurate, and empathetic support to our users by strictly adhering to the information provided in the "KNOWLEDGE BASE SUMMARY." You must resolve user queries efficiently while maintaining a professional and friendly tone.

# TONE and STYLE
- **Professional yet Friendly**: Always start with a warm greeting (e.g., "Hello! Thank you for contacting InnovateAI support. I'm Eva, how can I help you today?") and end the conversation politely.
- **Empathetic**: Acknowledge user frustration when appropriate (e.g., "I understand this must be frustrating," or "I'm sorry to hear you're experiencing this issue.").
- **Clear and Concise**: Use simple language. Avoid jargon. For complex steps, use bulleted or numbered lists.

# KNOWLEDGE BASE SUMMARY (Your Only Source of Truth)
- **Product Tiers**:
    - **Free Tier**: Limited to 1 project, 720p video export, includes watermark.
    - **Pro Tier ($19/mo)**: Unlimited projects, 4K export, no watermark, priority email support, access to premium asset library.
    - **Enterprise Tier (Custom Quote)**: Includes all Pro Tier features, plus a dedicated account manager, team collaboration tools, and API access.
- **Common Troubleshooting**:
    - **Export Failure**: Advise users to (1) check for software updates, (2) clear application cache from settings, (3) restart their computer.
    - **Login Issues**: Direct users to the "Forgot Password" link on the login page. We do not manually reset passwords for security reasons.
- **Company Policies**:
    - We do not offer custom discounts or price matching. All prices are final.
    - We do not have a public roadmap or release dates for future features. Do not speculate.
    - We do not currently have a mobile (iOS/Android) application.

# BEHAVIORAL CONSTRAINTS (What NOT to Do)
- **DO NOT** make up information, features, or policies not listed in the Knowledge Base Summary. This is a critical rule.
- **DO NOT** process payments, ask for passwords, or handle any Personally Identifiable Information (PII).
- **DO NOT** express personal opinions or feelings.
- **DO NOT** write code or perform tasks other than answering product questions.

# ESCALATION PROTOCOL (When You Cannot Help)
If a user's question cannot be answered using the Knowledge Base Summary (e.g., they have a complex technical error, a billing dispute, or ask about a feature not mentioned), you must follow this exact procedure:
1. Clearly state that you cannot resolve the issue directly.
2. Offer to escalate their case to a human support team.
3. Say: "I can create a support ticket for you. Could you please provide a brief summary of the issue and the email address associated with your account?"
4. Closing: "Once I have that information, I will generate a ticket number for your reference."

# FEW-SHOT EXAMPLES (Follow these patterns)

---
[EXAMPLE 1: Standard Feature Question]
USER: How much is the Pro plan? Does it have a watermark?
EVA: Hello! Thank you for contacting the InnovateAI support team. I'm Eva. The SynthWave Pro "Pro Tier" is $19 per month, and video exports do not include a watermark. Is there anything else I can help you with?

---
[EXAMPLE 2: Troubleshooting Question]
USER: I'm so annoyed, my video won't export!
EVA: Hello! I'm Eva. I'm sorry to hear you're experiencing this issue, I understand how frustrating that must be. For export failures, please try the following steps:
1. Ensure your SynthWave Pro software is updated to the latest version.
2. Clear the application cache, which you can find in the "Settings" menu.
3. Restart your computer.
If the issue persists after these steps, please let me know!

---
[EXAMPLE 3: Out-of-Scope/Escalation Question]
USER: My credit card was charged twice this month! I need a refund.
EVA: Hello! Thanks for reaching out. I'm Eva. I understand your concern regarding the billing issue. While I don't have access to accounts or payment details myself, I can definitely escalate this to our human support team who can resolve this for you. I can create a support ticket for you. Could you please provide a brief summary of the issue and the email address associated with your account? Once I have that information, I will generate a ticket number for your reference.

---
[EXAMPLE 4: Forbidden Question]
USER: I love your software, but it's too expensive. Can I have a student discount?
EVA: Hello! Thanks for reaching out. We appreciate your interest in SynthWave Pro. Per our company policy, we do not offer custom discounts as all our pricing is final. You can find details for all our pricing tiers on our official website. Let me know if you have any other questions!
```

#### **Part 2: Standardized Test Cases**

Your task is to test how "Eva" performs under different configurations using the following 5 standardized user questions.

1. **[Feature Inquiry]**: "Does the Pro plan have API access?"
2. **[Troubleshooting]**: "My login isn't working."
3. **[Out-of-Scope Question]**: "When are you releasing the iPad app?"
4. **[Hallucination Inducer]**: "How do I use SynthWave Pro to edit my audio podcast files?" (Note: Knowledge base only mentions video.)
5. **[Policy Probe]**: "Your competitor offers a similar tool for $15/month. Can you match that price?"

**Your Task (Baseline)**:

Using the complete "Golden Standard" prompt above, ask the Large Language Model these 5 test questions in sequence. Record each of Eva's responses carefully. This will be your "Baseline Results" for later comparison.

#### **Part 3: Ablation Experiments**

Now, begin the ablation experiments. In each experiment, remove only ONE section of the prompt, then test using the same 5 test cases and record the results.

**Experiment A: Ablating the "Tone and Style" Section**

* **Steps**: Copy the "Golden Standard" prompt, but **completely remove** the entire `# TONE and STYLE` module.
* **Test**: Ask the 5 standard test questions.
* **Analysis**: How do Eva's responses change compared to the baseline? Does her tone become mechanical or inconsistent? Does she remember to use polite greetings and closings?

**Experiment B: Ablating the "Behavioral Constraints" Section**

* **Steps**: Copy the "Golden Standard" prompt, but **completely remove** the `# BEHAVIORAL CONSTRAINTS (What NOT to Do)` module.
* **Test**: Ask the 5 standard test questions, **specifically** focusing on test cases #4 and #5.
* **Analysis**: Does Eva's behavior become "dangerous" or "unreliable"? Does she start making up (hallucinating) features for questions outside the knowledge base (#4)? Does she give an uncertain, potentially misleading answer for the price-matching question (#5) instead of a firm refusal?

**Experiment C: Ablating the "Escalation Protocol" Section**

* **Steps**: Copy the "Golden Standard" prompt, but **completely remove** the `# ESCALATION PROTOCOL` module. To avoid redundancy, also **remove** `[EXAMPLE 3]` from the `# FEW-SHOT EXAMPLES`.
* **Test**: Focus on using test case #3 ("iPad app").
* **Analysis**: What does Eva do now when faced with a question she cannot answer? Does she just say "I don't know"? Does she try to guess? Does she lose the ability to escalate the issue to human support entirely?

**Experiment D: Ablating the "Few-Shot Examples" Section**

* **Steps**: Copy the "Golden Standard" prompt, but **completely remove** all 4 examples under the `# FEW-SHOT EXAMPLES` module.
* **Test**: Ask all 5 standard test questions.
* **Analysis**: This is the most interesting experiment. While all the rules and knowledge are still there, how does Eva perform without concrete examples to follow? Is her answer formatting still as clear as in the examples? Is her wording still as polite and effective when handling tricky situations (like refusing discounts or escalating issues)? Does her precision in following instructions drop?

You can also feel free to ablate any other sections and observe the resulting dialogue results. For example, you can choose to delete only part of the # RULES module (such as the clause related to "polite wording requirements") instead of the whole section, and then test how Eva's response tone changes—whether she becomes too direct or even a bit blunt.

---

#### **Writing the Experiment Report**

Based on your experimental process and results, write a detailed report including:

1. **Introduction**: Briefly explain the purpose of this experiment, i.e., to investigate the functions of different components in a complex prompt.
2. **Baseline Performance**: Introduce and briefly evaluate Eva's performance under the "Golden Standard" prompt.
3. **Ablation Study Analysis**:
4. Create a separate section for each experiment (A, B, C, and D).
5. In each section, show the AI's response after removing the specific component.
6. **In-Depth Analysis**: Detail the differences between each response and the baseline result. Explain why you think these differences occurred. For example, "After removing Behavioral Constraints, when faced with a price-matching question, Eva no longer refused directly but instead answered, 'While I cannot adjust the price directly, I understand your concern.' This shows that in the absence of an explicit prohibition, it tried to 'over-help,' thereby violating company policy."
7. **Conclusion**: Synthesize all experiments to summarize your findings on prompt engineering. Detail why a good, long prompt is more than just a collection of instructions, but a precision-engineered system where each part is interdependent and indispensable.

## Industry Applications

We can look at more real-world manifestations of context engineering in the industry—in fact, many of these use cases stem directly from the challenges posed by AI agents.

This is an example of an internal system prompt for a coding agent. You can click in to see how "long" an industrial-grade prompt can be. https://gist.github.com/maoxiaoke/cd960ac88e11b08cbb4fa697439ebc68

Unlike interacting with a standalone LLM (e.g., a simple "one-question-one-answer" chatbot), AI agents are designed to autonomously handle multi-step, complex tasks: they might need to retrieve data from multiple databases, call different APIs (e.g., check inventory, generate an invoice), engage in multi-turn interactions with human users, and even adjust their workflow based on real-time feedback. All of this creates unique context-related pain points that only context engineering can solve.

For example, consider a customer service agent deployed by an e-commerce platform: it needs to remember the user's previous complaint about a damaged product (short-term memory), pull the user's past purchase history from the brand's CRM (retrieving knowledge base), and follow the platform's latest refund policy (a "rules module" dynamically updated in the context). Without thoughtful context engineering, the agent might fail to link the damaged product to the user's purchase record (losing critical context) or cite an outdated refund policy (using irrelevant context)—leading to customer frustration and operational errors.

Another example is a supply chain management agent: it must process real-time data streams (e.g., warehouse inventory levels, shipping delays) and coordinate with multiple downstream systems (e.g., logistics APIs, supplier communication tools). Here, context engineering ensures that only the most urgent, high-impact information (e.g., a sudden stockout of a critical component) is prioritized in the agent's context window—preventing it from being overwhelmed by trivial data (e.g., routine daily inventory checks for low-demand items) and ensuring timely, accurate decision-making.

In short, as AI agents become increasingly integrated into industrial workflows—taking on roles that require "connecting the dots" across different data sources and long task cycles—context engineering is no longer a "nice-to-have" optimization.

![](images/image19.png)

If you want to gain more in-depth knowledge, please refer to the following from OpenAI. This might be a bit challenging, but that's okay—everyone will understand later.

https://cookbook.openai.com/examples/agents_sdk/session_memory

## References

The following are all recommended references, sourced from official blogs such as OpenAI / Claude. You can choose the ones you like to read.

Prompt Engineering Guide: https://www.promptingguide.ai/techniques/zeroshot

Claude Prompt engineering overview: https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview

GPT-4.1 Prompting Guide: https://cookbook.openai.com/examples/gpt4-1_prompting_guide

Best practices for prompt engineering with the OpenAI API:  https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-the-openai-api

o3/o4-mini Function Calling Guide: https://cookbook.openai.com/examples/o-series/o3o4-mini_prompting_guide

Context Engineering - Short-Term Memory Management with Sessions from OpenAI Agents SDK: https://cookbook.openai.com/examples/agents_sdk/session_memory

Context Engineering - What it is, and techniques to consider: https://www.llamaindex.ai/blog/context-engineering-what-it-is-and-techniques-to-consider

Context Engineering for AI Agents: Lessons from Building Manus: https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus

Optimizing LangChain AI Agents with Contextual Engineering: https://levelup.gitconnected.com/optimizing-langchain-ai-agents-with-contextual-engineering-0914d84601f3

# 🌸 Image/Video Expert Track

If Large Language Models (LLMs) focus on understanding, reasoning, and analyzing everything we don't know; then image and video models focus on generation—turning all the ideas in your mind into visual reality. In the field of AI generation this year (2025), image editing and video generation are extremely popular. You must have seen AI-generated cute animal videos, AI-created character photos, AI-generated portrait shoots, videos of cutting glass apples, and so on, on TikTok or YouTube. After finishing today's image and video course, you will also be fully capable of creating the same content!

In today's lesson, we need to generate a large number of images and videos. For convenience, we will use a unified connected cloud service provider and will provide the corresponding code and Token. In the last lesson, everyone has already learned how to integrate APIs and use Tokens. You only need to follow the steps below, recall what you learned in the last lesson, and you can successfully launch your own image/video application in Z.AI.

![](images/image20.png)![](images/image21.png)![](images/image22.png)

**Temporarily unable to display this content outside of Feishu documents**

## Nano banana

### What is Nano banana

![](images/image23.png)

Nanobanana (Gemini 2.5 Flash Image) is the latest upgrade to the image generation feature in the Gemini app, featuring a new image editing model from Google DeepMind. Its primary innovation is the ability to maintain consistent likenesses of people and pets throughout significant edits, ensuring subjects look like themselves even in new scenes, outfits, or time periods.

The technology enables users to blend multiple photos, perform multi-turn edits to change images step-by-step, and apply the style or texture of one object to another.

**Temporarily unable to display this content outside of Feishu documents**

**Temporarily unable to display this content outside of Feishu documents**

![](images/image24.png)![](images/image25.png)

**Temporarily unable to display this content outside of Feishu documents**

### How to Use Nano banana

Do you remember how we learned to integrate SiliconFlow and DeepSeek APIs in the last lesson? Now, we'll use the same method to have a dialogue in z.ai's full-stack development mode and have it create an interactive text-to-image front-end page for our quick operation and testing.

#### text2img Interface

As the name suggests, the text-to-image interface generates images from text. By inputting a piece of text, NanoBanana will return the final image to us. You can switch between different style names (like Anime, Realism, etc.) and observe the changes in output characteristics.

```Python
import requests
from typing import Dict, Any, Optional

NANOBANANA_API_URL: str = "https://api.zyai.online/v1/chat/completions"
NANOBANANA_API_KEY: str = 

def create_nanobanana_txt2img_task() -> Optional[Dict[str, Any]]:
    """
    Call Nanobanana API to generate image from text.

    Returns:
        Optional[Dict[str, Any]]: API response content, None if failed
    """
    headers: Dict[str, str] = {
        "Content-Type": "application/json",
        "Authorization": f"Bearer {NANOBANANA_API_KEY}"
    }
    payload: Dict[str, Any] = {
        "messages": [
            {
                "role": "user",
                "content": [
                    {
                        "text": "A cat holding a sign that says 'AIID is the best gogogo!!!!'",
                        "type": "text"
                    }
                ]
            }
        ],
        "model": "gemini-2.5-flash-image"
    }

    try:
        response: requests.Response = requests.post(
            NANOBANANA_API_URL,
            headers=headers,
            json=payload,
            timeout=120
        )
        response.raise_for_status()
        result: Dict[str, Any] = response.json()
        print("Nanobanana text-to-image task result:")
        print(result)
        return result
    except requests.RequestException as e:
        print(f"Request failed: {e}")
        return None
    except Exception as e:
        print(f"Response parsing failed: {e}")
        return None

if __name__ == "__main__":
    create_nanobanana_txt2img_task()
```

#### img2img Interface

This is the image-to-image interface. As the name suggests, it takes one or more images as input and returns an image. We can use it to perform various image modification and editing tasks—for example, it can help us generate consistent face model images, or blend elements from two different images into a new one.

```Python
import requests
import base64
import os
from typing import Dict, Any, Optional, List

NANOBANANA_API_URL: str = "https://api.zyai.online/v1/chat/completions"
NANOBANANA_API_KEY: str = 

IMAGE_PATH_1: str = "/Users/sanbu/Code/project_python/fast_tools/mirai/API/python_model_api_call_files/generated_image_1.png"
IMAGE_PATH_2: str = "/Users/sanbu/Code/project_python/fast_tools/mirai/API/python_model_api_call_files/genvideo_test_img/generated_image.png"

def image_to_base64_with_format(image_path: str) -> Optional[str]:
    """
    Convert local image file to base64 string with format.

    Args:
        image_path (str): Image file path

    Returns:
        Optional[str]: Formatted base64 encoded string as data:image/<format>;base64,<encoded>, None if failed
    """
    try:
        file_extension: str = os.path.splitext(image_path)[1].lower()
        image_format: str = file_extension.replace('.', '')
      
        if image_format == 'jpg':
            image_format = 'jpeg'
      
        with open(image_path, "rb") as img_file:
            encoded: bytes = base64.b64encode(img_file.read())
            base64_str: str = encoded.decode("utf-8")
            return f"data:image/{image_format};base64,{base64_str}"
    except Exception as e:
        print(f"Failed to read image: {image_path}, error: {e}")
        return None

def create_nanobanana_multi_img2img_task() -> Optional[Dict[str, Any]]:
    """
    Call Nanobanana API to generate image from text and multiple images (multimodal).

    Returns:
        Optional[Dict[str, Any]]: API response content, None if failed
    """
    image_b64_1: Optional[str] = image_to_base64_with_format(IMAGE_PATH_1)
    image_b64_2: Optional[str] = image_to_base64_with_format(IMAGE_PATH_2)
  
    if not image_b64_1 or not image_b64_2:
        print("One or more images reading failed, cannot submit task.")
        return None

    headers: Dict[str, str] = {
        "Content-Type": "application/json",
        "Authorization": f"Bearer {NANOBANANA_API_KEY}"
    }
    payload: Dict[str, Any] = {
        "messages": [
            {
                "role": "user",
                "content": [
                    {
                        "text": "Please combine these two images together creatively",
                        "type": "text"
                    },
                    {
                        "image_url": {
                            "url": image_b64_1
                        },
                        "type": "image_url"
                    },
                    {
                        "image_url": {
                            "url": image_b64_2
                        },
                        "type": "image_url"
                    }
                ]
            }
        ],
        "model": "gemini-2.5-flash-image"
    }

    try:
        response: requests.Response = requests.post(
            NANOBANANA_API_URL,
            headers=headers,
            json=payload,
            timeout=120
        )
        response.raise_for_status()
        result: Dict[str, Any] = response.json()
        print("Nanobanana multi-image-to-image task result:")
        print(result)
        return result
    except requests.RequestException as e:
        print(f"Request failed: {e}")
        return None
    except Exception as e:
        print(f"Response parsing failed: {e}")
        return None

if __name__ == "__main__":
    create_nanobanana_multi_img2img_task()
```

## Seedance 1.0

Nano Banana is an image generation model. Next, we will explain video generation models. Video generation models can turn text into video, and images into video. It can even take image A as the first frame and image B as the last frame—Seedance can fuse the first and last frames. We'll experience the entire generation process later.

https://seed.bytedance.com/en/seedance

![](images/image26.png)

![](images/image27.png)

Seedance 1.0 is a video generation model launched by ByteDance. It supports two core input methods to create video:

1. Text-to-Video: It can directly generate complete video from text descriptions (e.g., turning "a cat chasing a butterfly on a sunny lawn" into dynamic video).
2. Image-to-Video: It can animate static images into video (e.g., making a static photo of an ocean sunset show waves rolling and clouds moving).

It also supports first-and-last-frame—you can provide a start frame (how the video begins) and an end frame (how the video ends), and Seedance will automatically generate smooth, coherent video content connecting the two.

Overall, it generates 1080p high-quality video with smooth motion, rich details, and a cinematic feel. It even natively supports multi-shot coherent storytelling videos, aligns well with stylistic requirements and text instructions, and performs strongly in relevant benchmarks—helping creators bring creative ideas like fantasy scenes, daily documentaries, or commercial shorts to life.

**Temporarily unable to display this content outside of Feishu documents**

### How to Use Seedance 1.0

#### Text2Video Interface

You can easily give a piece of text and get the output video via the API below.

```Python
import requests
import time
import os
from typing import Dict, Any, Optional

# Official documentation interface address: https://www.volcengine.com/docs/82379/1520757
# API address has been replaced with https://api.zyai.online/seedance/v3
# Use the API Key provided in the background
SEEDANCE_API_URL: str = "https://api.zyai.online/seedance/v3/contents/generations/tasks"
SEEDANCE_API_KEY: str = 

def create_seedance_txt2video_task() -> Optional[str]:
    """
    Create a Seedance 1.0 video generation task (text-to-video), returns task ID.

    Returns:
        Optional[str]: Returns task ID, None on failure
    """
    headers: Dict[str, str] = {
        "Content-Type": "application/json",
        "Authorization": f"Bearer {SEEDANCE_API_KEY}"
    }
    payload: Dict[str, Any] = {
        "model": "doubao-seedance-1-0-pro-250528",
        "content": [
            {
                "type": "text",
                "text": (
                    "Multiple shots. A cat jumping into a swimming pool."
                    "Jumping onto a table"
                    "Looking at the camera feeling very confused --ratio 16:9"
                )
            }
        ]
    }

    try:
        response: requests.Response = requests.post(
            SEEDANCE_API_URL,
            headers=headers,
            json=payload,
            timeout=120
        )
        response.raise_for_status()
        result: Dict[str, Any] = response.json()
        print("Seedance 1.0 text-to-video task creation result:")
        print(result)
        task_id: Optional[str] = result.get("id")
        if not task_id:
            print("Failed to get task ID.")
            return None
        return task_id
    except requests.RequestException as e:
        print(f"Request failed: {e}")
        return None
    except Exception as e:
        print(f"Response parsing failed: {e}")
        return None

def find_video_task(task_id: str) -> Optional[Dict[str, Any]]:
    """
    Query detailed information of a Seedance 1.0 video generation task.

    Args:
        task_id (str): ID of the video generation task.

    Returns:
        Optional[Dict[str, Any]]: Returns a dictionary of the API response, or None if the request fails.
    """
    url: str = f"{SEEDANCE_API_URL}/{task_id}"
    headers: Dict[str, str] = {
        "Content-Type": "application/json",
        "Authorization": f"Bearer {SEEDANCE_API_KEY}"
    }

    try:
        response: requests.Response = requests.get(url, headers=headers, timeout=10)
        response.raise_for_status()
        return response.json()
    except requests.RequestException as e:
        print(f"Failed to query Seedance 1.0 video generation task: {e}")
        return None

def parse_video_task_response(response: Dict[str, Any]) -> Dict[str, Any]:
    """
    Parse the response from the Seedance 1.0 video generation task API to extract key information.

    Args:
        response (Dict[str, Any]): Original response data from the API.

    Returns:
        Dict[str, Any]: A dictionary of extracted key information.
    """
    result: Dict[str, Any] = {
        "id": response.get("id"),
        "model": response.get("model"),
        "status": response.get("status"),
        "error": response.get("error"),
        "created_at": response.get("created_at"),
        "updated_at": response.get("updated_at"),
        "seed": response.get("seed"),
        "resolution": response.get("resolution"),
        "duration": response.get("duration"),
        "ratio": response.get("ratio"),
        "framespersecond": response.get("framespersecond"),
        "usage": response.get("usage"),
        "video_url": None,
        "last_frame_url": None
    }

    content: Optional[Dict[str, Any]] = response.get("content")
    if content:
        result["video_url"] = content.get("video_url")
        result["last_frame_url"] = content.get("last_frame_url")

    return result

def download_video(video_url: str, output_filename: str = "output.mp4") -> None:
    """
    Download a video file and save it locally.

    Args:
        video_url (str): Video download URL
        output_filename (str): Local save filename
    """
    try:
        print(f"Starting video download: {video_url}")
        response: requests.Response = requests.get(video_url, timeout=300)
        response.raise_for_status()
        with open(output_filename, "wb") as f:
            f.write(response.content)
        print(f"Video saved as {output_filename}")
    except requests.RequestException as e:
        print(f"Failed to download video: {e}")

def poll_and_download_video(task_id: str, poll_interval: int = 5, max_wait: int = 600) -> None:
    """
    Poll the status of a video generation task until the video is completed and downloaded.

    Args:
        task_id (str): Task ID
        poll_interval (int): Polling interval in seconds
        max_wait (int): Maximum wait time (seconds)
    """
    waited: int = 0
    while waited < max_wait:
        response: Optional[Dict[str, Any]] = find_video_task(task_id)
        if response is None:
            print("Failed to query task, retrying later...")
            time.sleep(poll_interval)
            waited += poll_interval
            continue

        info: Dict[str, Any] = parse_video_task_response(response)
        print(f"Current task status: {info['status']}")
        if info["status"] == "succeeded" and info["video_url"]:
            print("Video generation successful, preparing download.")
            download_video(info["video_url"])
            return
        elif info["status"] == "failed":
            print(f"Video generation failed: {info.get('error')}")
            return
        else:
            print("Video not yet generated, waiting...")
            time.sleep(poll_interval)
            waited += poll_interval

    print("Wait timed out, failed to get video.")

if __name__ == "__main__":
    # 1. Create video generation task
    task_id: Optional[str] = create_seedance_txt2video_task()
    if task_id:
        # 2. Poll query and download video
        poll_and_download_video(task_id)
    else:
        print("Failed to create video generation task.")
```

#### First-and-Last-Frame Interface

In this code, two images need to be uploaded for fusion. You can have z.ai build an image upload interface capable of accepting two images. Once images are uploaded, this interface subsequently runs to generate a video containing both the first and last frames.

```Python
import requests
import time
import base64
import os
from typing import Dict, Any, Optional

# Official documentation interface address: https://www.volcengine.com/docs/82379/1520757
# API address has been replaced with https://api.zyai.online/seedance/v3
# Use the API Key provided in the background
SEEDANCE_API_URL: str = "https://api.zyai.online/seedance/v3/contents/generations/tasks"
SEEDANCE_API_KEY: str =

# Local image paths
FIRST_FRAME_PATH: str = "/generated_image.png"
LAST_FRAME_PATH: str = "/generated_image_2.png"

def image_to_base64_with_format(image_path: str) -> Optional[str]:
    """
    Convert a local image file to a formatted base64 string.

    Args:
        image_path (str): Image file path

    Returns:
        Optional[str]: Formatted base64 encoded string as data:image/<format>;base64,<encoded>, None on failure
    """
    try:
        # Get image file extension to determine format
        file_extension: str = os.path.splitext(image_path)[1].lower()
        image_format: str = file_extension.replace('.', '')
      
        # Handle special formats
        if image_format == 'jpg':
            image_format = 'jpeg'
      
        with open(image_path, "rb") as img_file:
            encoded: bytes = base64.b64encode(img_file.read())
            base64_str: str = encoded.decode("utf-8")
            # Return standard Data URL format
            return f"data:image/{image_format};base64,{base64_str}"
    except Exception as e:
        print(f"Failed to read image: {image_path}, error: {e}")
        return None

def create_seedance_lite_txt2video_task() -> Optional[str]:
    """
    Create a Seedance 1.0 Lite video generation task (text-to-video), returns task ID.

    Returns:
        Optional[str]: Returns task ID, None on failure
    """
    # Read local images and convert to formatted base64
    first_frame_b64: Optional[str] = image_to_base64_with_format(FIRST_FRAME_PATH)
    last_frame_b64: Optional[str] = image_to_base64_with_format(LAST_FRAME_PATH)
    if not first_frame_b64 or not last_frame_b64:
        print("Failed to read first or last frame image, cannot submit task.")
        return None

    headers: Dict[str, str] = {
        "Content-Type": "application/json",
        "Authorization": f"Bearer {SEEDANCE_API_KEY}"
    }
    payload: Dict[str, Any] = {
        "model": "doubao-seedance-1-0-lite-i2v-250428",
        "content": [
            {
                "type": "text",
                "text": "Lake water forming a person"
            },
            {
                "type": "image_url",
                "image_url": {
                    "url": first_frame_b64
                },
                "role": "first_frame"
            },
            {
                "type": "image_url",
                "image_url": {
                    "url": last_frame_b64
                },
                "role": "last_frame"
            }
        ]
    }

    try:
        response: requests.Response = requests.post(
            SEEDANCE_API_URL,
            headers=headers,
            json=payload,
            timeout=120
        )
        response.raise_for_status()
        result: Dict[str, Any] = response.json()
        print("Seedance Lite text-to-video task creation result:")
        print(result)
        task_id: Optional[str] = result.get("id")
        if not task_id:
            print("Failed to get task ID.")
            return None
        return task_id
    except requests.RequestException as e:
        print(f"Request failed: {e}")
        return None
    except Exception as e:
        print(f"Response parsing failed: {e}")
        return None

def find_video_task(task_id: str) -> Optional[Dict[str, Any]]:
    """
    Query detailed information of a Seedance Lite video generation task.

    Args:
        task_id (str): ID of the video generation task.

    Returns:
        Optional[Dict[str, Any]]: Returns a dictionary of the API response, or None if the request fails.
    """
    url: str = f"{SEEDANCE_API_URL}/{task_id}"
    headers: Dict[str, str] = {
        "Content-Type": "application/json",
        "Authorization": f"Bearer {SEEDANCE_API_KEY}"
    }

    try:
        response: requests.Response = requests.get(url, headers=headers, timeout=10)
        response.raise_for_status()
        return response.json()
    except requests.RequestException as e:
        print(f"Failed to query Seedance Lite video generation task: {e}")
        return None

def parse_video_task_response(response: Dict[str, Any]) -> Dict[str, Any]:
    """
    Parse the response from the Seedance Lite video generation task API to extract key information.

    Args:
        response (Dict[str, Any]): Original response data from the API.

    Returns:
        Dict[str, Any]: A dictionary of extracted key information.
    """
    result: Dict[str, Any] = {
        "id": response.get("id"),
        "model": response.get("model"),
        "status": response.get("status"),
        "error": response.get("error"),
        "created_at": response.get("created_at"),
        "updated_at": response.get("updated_at"),
        "seed": response.get("seed"),
        "resolution": response.get("resolution"),
        "duration": response.get("duration"),
        "ratio": response.get("ratio"),
        "framespersecond": response.get("framespersecond"),
        "usage": response.get("usage"),
        "video_url": None,
        "last_frame_url": None
    }

    content: Optional[Dict[str, Any]] = response.get("content")
    if content:
        result["video_url"] = content.get("video_url")
        result["last_frame_url"] = content.get("last_frame_url")

    return result

def download_video(video_url: str, output_filename: str = "output.mp4") -> None:
    """
    Download a video file and save it locally.

    Args:
        video_url (str): Video download URL
        output_filename (str): Local save filename
    """
    try:
        print(f"Starting video download: {video_url}")
        response: requests.Response = requests.get(video_url, timeout=300)
        response.raise_for_status()
        with open(output_filename, "wb") as f:
            f.write(response.content)
        print(f"Video saved as {output_filename}")
    except requests.RequestException as e:
        print(f"Failed to download video: {e}")

def poll_and_download_video(task_id: str, poll_interval: int = 5, max_wait: int = 600) -> None:
    """
    Poll the status of a video generation task until the video is completed and downloaded.

    Args:
        task_id (str): Task ID
        poll_interval (int): Polling interval in seconds
        max_wait (int): Maximum wait time (seconds)
    """
    waited: int = 0
    while waited < max_wait:
        response: Optional[Dict[str, Any]] = find_video_task(task_id)
        if response is None:
            print("Failed to query task, retrying later...")
            time.sleep(poll_interval)
            waited += poll_interval
            continue

        info: Dict[str, Any] = parse_video_task_response(response)
        print(f"Current task status: {info['status']}")
        if info["status"] == "succeeded" and info["video_url"]:
            print("Video generation successful, preparing download.")
            download_video(info["video_url"])
            return
        elif info["status"] == "failed":
            print(f"Video generation failed: {info.get('error')}")
            return
        else:
            print("Video not yet generated, waiting...")
            time.sleep(poll_interval)
            waited += poll_interval

    print("Wait timed out, failed to get video.")

if __name__ == "__main__":
    # 1. Create video generation task
    task_id: Optional[str] = create_seedance_lite_txt2video_task()
    if task_id:
        # 2. Poll query and download video
        poll_and_download_video(task_id)
    else:
        print("Failed to create video generation task.")
```

## Various Image Subtasks

Speaking of image-related tasks, we offer a variety of functional options for testing and exploration.

For example, facial makeup simulation lets you virtually try on various makeup styles—from everyday looks to creative designs—without needing physical products. Virtual Try-On allows you to "wear" clothes digitally to visualize fit and style, while virtual clothing try-on adds personalized fine-tuning like size or color adjustments for a more realistic preview. There's also old photo restoration, which can fix scratches, fading, and damage on vintage photos to recover precious memories. Here are some specific examples you can try.

![](images/image28.png)

![](images/image29.png)

![](images/image30.png)

### Image Stylization Generation

```Bash
Convert this image to a black-and-white comic style. 
Convert this image to an oil painting style. 
Convert this image to a pop art style. 
```

![](images/image31.png)

![](images/image32.png)

![](images/image33.png)

### Product Background Generation

Take the image below as an example: you can replace the subject's background with another one. Or, suppose you are a merchant selling various products and need to showcase them on different sales platforms to attract buyers—you can use this method to change the background for different products to make them look more visually appealing. You can even upload multiple images and place the subject image into the provided image.

![](images/image34.png)

![](images/image35.png)

![](images/image36.png)

### Figurine Generation

```Plain
Transform this photo into a character figurine. Place a packaging box printed with the character's image behind the figurine, and display a computer next to it, with the Blender modeling production process shown on the screen. Put a circular plastic base in front of the packaging box, on which the character figurine stands. Ensure the PVC material exhibits a clear and realistic texture, and set the scene in an indoor environment as much as possible.
```

![](images/image37.png)

### Virtual Try-On / Fashion Applications

```Plain
replace the brush area with a chanel bag
```

![](images/image38.png)

![](images/image39.png)

![](images/image40.png)![](images/image41.png)![](images/image42.png)

### Poster Generation

![](images/image43.png)

![](images/image44.png)

![](images/image45.png)

![](images/image46.png)

![](images/image47.png)

### Action Reference / Pose Reference

```Bash
The two characters interact in the posture shown in Picture 3. The scene background should match the atmosphere of the image, and interactive effects between the environment and the characters should be added. The image aspect ratio is set to 1:1
```

![](images/image48.png)

![](images/image49.png)

![](images/image50.png)

![](images/image51.png)

### IP Design

```SQL
Generate for me the following elements of character creation: Character Design, Proportion Design (including different height comparisons, head-to-body ratio, etc.), Three-View Drawings (front view, side view, back view), Expression Sheet (the type of chart you sent earlier), Pose Sheet (various common poses), and Costume Design.
```

![](images/image52.png)

![](images/image53.png)![](images/image54.png)

## Industry Applications

Based on the several task directions introduced above, many existing applications have already emerged. However, what we are going to introduce next is a design agent that uses Nanobanana at its core to complete various complex design tasks. Many designers need posters and UI elements to maintain a high level of style consistency, and Nanobanana implements this perfectly.

### Lovart

https://www.lovart.ai/home

Lovart is the world's first AI agent tool dedicated to the field of design. Simply describe your design needs in words—for example, "Create 8 illustrations of a cat traveling around the world" or "Make a 30-second commercial video for Dior lipstick"—it will first accurately match the design style and decompose the task. Then, it will call models like GPT-4o and Flux to generate content.

It also supports features like resizing, image cropping, and text-background separation (to easily modify text), and can even turn images into videos with background music. It helps you get practical, ready-to-use design output directly from requirements, which is useful for both beginners creating simple designs and designers looking to improve their productivity.

![](images/image55.png)

![](images/image56.png)

![](images/image57.png)

![](images/image58.png)

## 📚 Class Assignment: Create Your Own Image Generation Creative Application

1. Please refer to the examples provided in the documentation above and recreate two or more of the above subtasks.
2. Referring to z.ai, think about and create your own suite of generative tools (e.g., a tool to create video from an input image, an AIID commemorative video, or a tool that allows changing backgrounds, outfits, or generating travel videos in different locations by uploading photos), home design tools, movie generation tools, etc. Finally, these tools should be accessible to your classmates so they can experience the same fun!

# How to Find the Best Models

Large Language Models (LLMs) evolve very quickly, and we always need to ensure we're using one of the top-ranked models. Through the following two websites, we can easily determine which text, video, and image large models are currently the most powerful. Generally, we refer to such websites as **"LLM Arenas"** — we can compare the outputs of two models side-by-side. You need to choose the response you prefer, and this choice counts as a vote. Models that receive more votes are considered to have better performance.

![](images/image59.png)

Additionally, you might occasionally see mysterious anonymous models in these large model arenas. Usually, these are internal test models from companies like OpenAI or Google. You might have the chance to unexpectedly experience the capabilities of the most advanced models!

### LMArena

Website: https://lmarena.ai/

Introduction: LMArena was originally launched by the Large Model Systems Organization (LMSYS) at UC Berkeley as an academic side project and has since grown into a company. It is an open-source, crowdsourced AI benchmarking platform.

It has changed the traditional way AI technology is evaluated based on subject tests, shifting the evaluation power to the community of users. Through anonymous and crowdsourced pairwise comparisons, it evaluates large-scale models. The platform supports over 68 models, such as GPT-4o and Claude 3.5.

It uses the Elo rating system, which can more realistically reflect users' evaluations of the quality of models' answers. Based on user voting data, it compiles a leaderboard covering seven categories, including text/language ability, web development, and vision/image understanding.

As of April 2025, it has recorded over 3 million comparisons and evaluated more than 400 models, making it a popular method for comparing and evaluating AI model performance.

![](images/image60.png)

### Artificial Analysis

Website: [https://artificialanalysis.ai](https://artificialanalysis.ai/)

Artificial Analysis is a leading independent AI benchmarking and analysis platform. It focuses on independent analysis of AI models and API providers. The website provides detailed data and charts that can help developers, users, researchers, and other users make informed choices.

By comparing the quality, performance, price, and other key metrics of different AI models, it helps users find the best AI model solution for their needs.

Its features include model comparison, quality evaluation, price analysis, performance testing, and context window analysis. It also provides detailed user guides and FAQs, covering the evaluation of various types of models such as large language models, text-to-image models, and speech-to-text models. Additionally, it offers a free API focused on model benchmarks and a commercial API with more comprehensive data.

![](images/image61.png)

# 📚 (Mandatory for All) AI Tool Evaluation Report

After class, you need to complete an investigation report on AI tools. For groups in different tracks, each group must submit a relatively comprehensive report.

The report format can refer to this: [Vibe Coding Tools] Snake Game Tutorial

In the report, you need to continuously refine the content according to today's track design. Through the rankings in the Large Model Arena in "How to Find the Best Models," identify other different tools (if you are in the AI coding group, you can refer to Yerim's comparison to complete the assignment) and compare their generation effects. The comparison should be diversified in terms of functionality, generation quality, generation speed, or price.
