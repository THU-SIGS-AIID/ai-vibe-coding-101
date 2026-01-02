# AI Capability Handbook: An Overview of Mainstream Models, Product Forms, and Application Scenarios

As generative AI technology is widely implemented in various products and business scenarios, an increasingly real issue is presented to each of us: ** What exactly are the available AI capabilities? ** In specific requirements, ** which capabilities, models, or products should be selected to implement them? **

In the face of such confusion, the most intuitive approach may be to "cram at the last minute":  ** search for the product APIs of cloud service providers on the market or the corresponding models when a requirement arises, or refer to the documentation and demos of commercial solutions on the market for handling ** . When faced with image requirements, think of image generation; when dealing with text tasks, find large models; when it comes to voice interaction, think of ASR and TTS, and then compare among a vast number of APIs and services. However, simply piling up scattered products together is completely different from systematically planning, selecting, and combining AI capabilities in enterprise-level scenarios. Relying solely on ad-hoc information retrieval and experience-based judgment will bring about a series of serious challenges, such as fragmented understanding of capabilities, arbitrary solution design, and difficulty in reusing capabilities.

To address these pain points, the organizing idea centered around the "AI Capability Panorama" emerged. In this handbook, what we aim to do is not to pile up jargon but to help you quickly figure out three things: ** "What AI capabilities can be used for this task? Which type of model or product should be selected? What keywords should be used next to search for APIs, projects, or services to try?" ** Through systematic sorting from modalities (text, image, audio, video, 3D, MultiModal Machine Learning) to architectural layers (model, retrieval, Agent, platform engineering),  ** we can find the corresponding AI capabilities, representative models/products, and common uses in real-world business for each type of typical requirement and scenario ** , helping teams build an AI system with lower trial-and-error costs, higher decision-making efficiency, and stronger reusability.

In this manual, we will systematically introduce the current mainstream AI capabilities landscape, from single-modal to MultiModal Machine Learning, from single-point models to the overall framework of platforms and engineering, and provide practical-oriented reference for capability selection by combining common Product Forms and application scenarios.

> Due to  **the large amount of content** , you can refer to the manual for reference when you encounter scenarios during practice and don't know how to select the appropriate option; it is recommended that you**let the AI refer to this manual based on the specific application direction and provide reference suggestions for model selection and API call suggestions for the solution.**

If you only want to know the corresponding category and don't want to read the specific content, you only need to read the initial paragraph of each major chapter, such as the content of 1.1 and 1.2, but not the content of 1.1.1 or 1.1.2.

**It is recommended that this manual be consulted only for the corresponding sections when needed or only the first-level table of contents be browsed, and if interested, the full text can be browsed.**

**Subsequent updates will include recommended and available model API service addresses in each chapter section.**

# You will learn in this lesson

* AI Capability Landscape: Overall Capability Classification Approach from Text, Image, Audio, Video, 3D to MultiModal Machine Learning, Agent, RAG, Security, and Platform Engineering
* Models and products corresponding to each capability: Understand the representative models and services behind key capabilities such as Embedding, OCR, ASR, TTS, VLM, and RAG
* Mapping method from capabilities to scenarios: Master how to transform the "capability inventory" into specific applications such as product content, search Q&A, intelligent customer service, and automated operations

After completing the study of this manual, you will establish an entry-level systematic understanding of mainstream AI capabilities. You will not only know "what capabilities are available in the market and which products they are commonly paired with", but also understand their positions and interrelationships within the overall architecture. You will know how to quickly identify the required capabilities and make informed selections when faced with specific business requirements, laying a solid foundation for building an AI capabilities system.

## Model parameters involved in the manual

Before delving into the specific capability map, let's first clarify a frequently mentioned yet somewhat abstract concept: What exactly counts as a large model? What counts as a small model?

 **Academically speaking ** , large models generally refer to general models with parameters in the tens of billions, hundreds of billions, or even trillions, while small models are specialized models tailored to specific tasks or scenarios with fewer parameters (tens of millions to billions).

 **From a price perspective** , if the API calls of a model are very inexpensive, such as costing just a few cents or fractions of a cent per call, or only a few cents to fractions of a cent per thousand tokens, and there is no particular emphasis on general large models, then it is usually either a typical small model (e.g., models specifically designed for OCR, ASR, image classification, content moderation) or a lightweight large model with a relatively small number of parameters (compressed or distilled specifically for high concurrency and low cost). If the price per call is significantly higher, such as starting at a few dimes or even 1 yuan per call, then it is most likely a large model.

Additionally, if the product copy explicitly emphasizes the use of large language models (LLMs), general large models, or MultiModal Machine Learning large models, or mentions end-to-end completion of complex tasks from input to output (such as end-to-end dialogue robots, end-to-end retrieval Q&A, end-to-end video generation), it can usually be regarded as a large model.

Conversely, if the promotional focus is on a specific vertical capability, such as bank card recognition, invoice recognition, license plate recognition, Click-Through Rate Prediction, speech transcription, or content moderation, it indicates that the underlying technology of this product is more likely to be a single or a set of small models.

Therefore, in the following narrative of this article, a practical convention can be made:

* Large models more often refer to those general-purpose, conversational, programmable models (including their MultiModal Machine Learning versions, such as GPT-4o, Gemini 1.5 Pro, Claude 3.5 Sonnet, etc.) that can cover most general text, code, and multimodal tasks such as images, audio, and video;
* Small models refer to those models fine-tuned or customized for a specific task, which are usually cheaper, have more stable and controllable performance, but have a narrower scope of application and require you to actively combine and orchestrate them in the system.

Here, it might be appropriate to add a key industry change: many of the model capabilities mentioned in the manual were actually handled by "small models" before 2021. Specialized models were trained for specific scenarios and specific data to meet precise requirements. And ** today, the vast majority of general scenarios and tasks can already be directly addressed by calling large models** .

From the perspective of the ultimate pursuit of**precision a****nd ****c** **ost** , the training and application of small models still have their irreplaceable value; however, **for beginners, we can definitely start by learning to find and call large model APIs** , and then gradually delve into advanced gameplay. You only need to make trade-offs among cost, precision, and latency, and then decide where to use general large models and where to continue to retain or introduce dedicated small models.

> **Recognize from some ****com****mon products** commonly used text and MultiModal Machine Learning general large models:

* OpenAI Series: GPT-4, GPT-4.1, GPT-4o, GPT-5.1, etc.
* Google 系列：Gemini 1.5 Pro、Gemini 1.5 Flash 等
* Anthropic 系列：Claude 3.5 Sonnet、Claude 3.5 Haiku 等
* Domestic models: Tongyi Qianwen Qwen series, Wenxin Yiyan ERNIE Bot series, GLM/Zhipu Qingyan, Baidu's Wenxin Big Model family, Tencent Hunyuan, iFlytek Xinghuo, the large model behind Kimi of Yuezhianmian, etc.

> Large models and services that are more focused on visual and video directions, including:

* Image Generation: DALL·E, Midjourney, Stable Diffusion, SDXL, Flux, etc.
* MultiModal Machine Learning Vision Understanding: GPT-4o, GPT-4.1 with Vision, Gemini 1.5 (Image-Text MultiModal), Claude 3.5 Sonnet Vision, LLaVA, etc.
* Video Generation: Sora, Kling, Runway Gen-2, Pika, Luma, Veo, etc.

> Large models in the field of speech and audio, including:

* Automatic Speech Recognition (ASR): Whisper series (Whisper, Whisper-large-v3, etc.), Deepgram, end-to-end ASR large models from various cloud providers (such as iFlytek, Baidu, Volcano, Alibaba, etc.)
* Speech MultiModal Machine Learning and Speech Dialogue: GPT-4o (End-to-End Speech Dialogue), OpenAI Realtime, Audio Understanding Capabilities of Gemini 1.5, etc.
* TTS / Audio and Music Generation: OpenAI TTS, ElevenLabs, Suno, Udio, MusicGen, etc.

> 3D / Spatial Direction Generation and Understanding Model, including:

* 文生 3D 和图生 3D：DreamFusion、Shap-E、GET3D、Zero-1-to-3、TripoSR 等
* NeRF / Neural Rendering Family: Instant-NGP, NeRF Series, Gaussian Splatting-related models, etc.

# 1. Text Tasks (Text / NLP / LLM)

Among AI capabilities, text tasks are the most fundamental function. Whether what we ultimately want to do is content moderation, search recommendation, knowledge Q&A, writing assistant, or code Copilot, essentially we cannot avoid a question: how can machines truly understand text?

## 1.1 Basic Language Modeling and Representation

Let's start with the most fundamental language modeling and representation at the bottom level. Its role is to enable machines to first become familiar with language in a statistical sense, and on this basis, find a stable vector matrix representation for words, sentences, and documents, so as to facilitate subsequent tasks such as classification, matching, extraction, and generation. Regardless of what text-related tasks we may undertake in the future, we all need to answer the same question to some extent: How can I represent this passage with a sequence of numbers?

We can simply examine the relevant content of this issue from three perspectives: scenario, principle, and model.

* **Scenario**
  * **Retrieval and Search Related**
    * General search engine: Users can simply input a sentence and obtain relevant documents, rather than just performing exact keyword matching.
    * In-app Search / E-commerce Search: Users use colloquial descriptions (such as "white shirts suitable for summer commuting") to find products with corresponding meanings.
    * Document Library / Knowledge Base Search: Directly input a sentence in technical documents, policies and regulations, and enterprise knowledge bases to obtain relevant entries.
  * **Related to recommendation ranking**
    * Information Stream / Content Recommendation: Automatically identify other content with similar themes based on the content the user has recently viewed or clicked, rather than relying solely on manual rules or tags.
    * E-commerce / Product Recommendation: Based on the descriptions of products that users have viewed, purchased, or bookmarked, find products with similar styles or uses to provide customized recommendations.
    * User Interest Modeling: Based on the titles users have viewed, the terms they have searched for, etc., summarize several main interest directions to improve the effectiveness of recommendation and ranking.
  * **Related to Q&A Assistant**
    * FAQ Q&A: When users ask the same question in different ways ("How do I get an invoice?" vs "Where can I get an invoice?"), the system can jump to the same answer.
    * Knowledge Base Q&A / Enterprise Assistant: Users ask questions in natural language, and the system searches internal documents for meaning-based matching to find the most relevant paragraphs to answer.
  * **Related to text understanding and analysis**
    * Comment sentiment analysis: Roughly classify a large number of comments and posts into several categories based on "what is being said / how the sentiment is".
    * Text deduplication / similarity detection: Used to identify rewritten manuscripts and pseudo-original articles.
    * Document Clustering / Grouping: Group many articles and reports into several groups based on similar content to facilitate navigation, recommendation, or sampling inspection.
  * **As a general feature for downstream tasks (downstream tasks refer to using the model's basic capabilities to achieve more specific text processing tasks) **
    * Text Classification: Downstream models such as sentiment classification, intent recognition, and spam content recognition directly reuse the representation of this layer.
    * Information extraction: Entity recognition and relation extraction are fine-tuned based on word/sentence representations, rather than trained from scratch.
    * Text Generation: Provides semantic representation input for generation tasks such as summarization, rewriting, and continuation, enhancing generation quality and controllability.
* **Principle**
  Learn the representations of words, sentences, and documents to serve as a foundation for subsequent more complex tasks.
  * Language Modeling
    * Autoregressive language model: predicts the next token (GPT series, LLaMA, Qwen, etc.)
    * Masked Language Model (Masked LM): Predict masked tokens (BERT, RoBERTa, ERNIE)
  * Word / Sentence / Paragraph Representation
    * Static word vectors: Word2Vec, GloVe, FastText
    * Contextual Representation: BERT embedding, Sentence-BERT, etc.
    * Document-level vectors: used for semantic retrieval and similarity matching
* **Models**
  LLMs such as BERT / RoBERTa / ERNIE, GPT family, LLaMA / Qwen / Yi, etc.; various Embedding models (OpenAI text‑embedding‑3 series, bge, E5, SimCSE, etc.).

### **1.1.1 Language Modeling: Learning Language through "Guessing the Next Word"**

The first step in this layer is to let the model ** familiarize itself with language patterns ** in a large amount of text. This can be simply understood as: giving the model countless "word guessing questions", and after seeing the context of a passage, asking it to fill in the most reasonable word (token). With enough practice questions and a wide enough corpus, the model will gradually learn: what a natural sentence looks like, which words often appear together, and what expressions sound awkward. This process is called "language modeling", which in essence is a unified  ** word guessing training mechanism ** .

There are commonly two ways of setting questions, and for each, a simple example is given in one sentence:

1. **Backward connection (autoregressive) ** : Only provide the preceding content and let the model guess "what will be said next".
2. Input Prefix:`It's raining today, so I`
3. Model Task: Guess the next word, such as " **bring** (umbrella)" " **not** (go out)" " **plan** (to stay at home)" etc., and then continue to follow up.
   This method mainly trains the model's grasp of  **continuation, coherence, and common expressions** .
4. **Cloze Test (Masking) ** : Create a hole in the middle and let the model fill in the blank using the context before and after.
5. Original sentence:`It's raining today, so I brought an umbrella`
6. Training sentence:`It [MASK] today, so I brought an umbrella`
7. Model task: Fill `[MASK] `with reasonable words like "  **rain ** ".
   Here, the model must look at both "today" on the left and "so I brought an umbrella" on the right to decide what to fill in, which is more conducive to learning the  **whole sentence semantics ** .

By repeatedly doing these two types of "word guessing questions" on a vast amount of corpus, the model will gradually accumulate ** language sense and statistical common sense ** about language. Based on this, the next step is to explicitly transform this ability into  ** vector representations of words, sentences, and documents ** , laying the foundation for subsequent tasks such as retrieval, recommendation, and question answering.

### 1.1.2 Word, Sentence, and Document Representation: Mapping Discrete Symbols to Semantic Space

The earliest generation of methods for constructing text vectors is  ** static word vectors ** : assigning a fixed vector to each word, which does not change with context after training, is intuitive and simple, but ** cannot distinguish the meanings of polysemous words in different contexts. ** To address this issue, context-based dynamic representation methods emerged later: the same word generates different vectors in different sentences, completely determined by its context. For example, "apple" in "Apple released a new phone" is closer to the semantic direction of "technology company", while in "Apples are rich in vitamins" it is closer to the concept of "fruit".

This mechanism not only enhances the expressive ability at the word level but also paves the way for the vectorization of sentences and documents. For sentences, sentence vectors can be generated; for documents, the entire document can be input for encoding (if the length allows), or it can be segmented for encoding and then aggregated into a global vector through attention mechanisms, hierarchical pooling, contrastive learning, and other methods. In recent years, specialized embedding models (such as bge, E5, and the text-embedding series) have been continuously optimized around the goal of "bringing semantically similar texts closer in vector space," particularly excelling in tasks such as semantic retrieval and similarity matching.

This process, from context modeling to sentence/document vector generation, has become the core infrastructure behind systems such as search, recommendation, and question answering. Let's return to the various scenarios mentioned earlier:

* Retrieval and search scenarios (general search, e-commerce search, Knowledge Base retrieval) all need to encode both user input and candidate documents into vectors, and then perform similarity matching in the vector space to find the semantically closest results, rather than relying solely on keyword exact matching.
* Recommendation ranking scenarios (information stream recommendation, product recommendation, user interest modeling) need to convert the content corresponding to user historical behavior into vectors, and then find new content with similar vectors to recommend to users, achieving the personalized effect of "recommend B after viewing A".
* The FAQ Assistant scenario (FAQ Q&A, Knowledge Base Q&A) needs to encode both the user's questions and the questions or paragraphs in the Knowledge Base into vectors, and then find the most matching answer through vector similarity.
* Text understanding and analysis scenarios (comment sentiment, deduplication, clustering) require first converting each text into a vector, and then performing clustering, similarity calculation, or classification based on the vector.
* Downstream task scenarios (text classification, information extraction, text generation) directly use the vector representation of this layer as input features and feed them to subsequent classifiers, extractors, or generators, thereby avoiding learning semantics from scratch.

In engineering, a common practice is to encapsulate it into a unified "text vector service": input any piece of text, and output a fixed-dimensional vector for multiple systems such as search, recommendation, and question-answering to share and use. At the product level, the capabilities of this layer are mainly reflected in: semantic recall in search and recommendation (no longer relying solely on keywords, but recalling content that "has different expressions but similar meanings" through vector similarity), as well as unified embedding/vector retrieval services for enterprise Knowledge Bases, FAQs, and case libraries.

## 1.2 Text Classification and Text Matching (Classification & Matching)

In the previous section, we used basic language modeling and representation to find the "coordinates" of each text segment in the semantic space. However, coordinates alone are not enough. The questions that business truly cares about are often: which category does this text belong to? Does it talk about the same thing as another text segment? Are the two sentences logically supportive or contradictory to each other? You can understand it as: using the two capabilities of classification and matching to transform the underlying vector representation into labels and correlation signals that can directly drive business decisions. We still organize this layer from three perspectives: scenario, principle, and model:

* **Scenario**
  * Content Understanding and Review: Assign tags such as topic, sentiment, and risk to comments, posts, and articles for review, recommendation, and statistical analysis.
  * Recommendation and Ranking: Based on the matching degree between "user interest tags" and "content tags", determine which content to display and how high it should be ranked.
  * Search and FAQ: When a user enters a natural language question at will, the system can automatically find the most relevant question-answer pair or document fragment.
  * Similar content identification: Find "similar content" entries in a large amount of text, used for deduplication, combined statistics, and recommending "related content".
  * Logical relationship judgment: Determine whether the relationship between two sentences is mutually supportive, mutually contradictory, or unrelated, used for fact-checking, consistency checking in multi-round conversations, etc.
* **Principle**
  Based on semantic representation, make an overall judgment on the entire text or text pair:
  * Text Classification: Assign labels to individual texts (such as sentiment, topic, risk type, etc.);
  * Text matching: Determine the similarity, relevance between two segments of text, or whether the "question - answer" pair matches;
* **Model **
  Based on a pre-trained encoder, followed by a simple classification/matching structure:
  * Single text classification: BERT / RoBERTa / DeBERTa + fully connected classification layer;
  * Text matching: Sentence-BERT, SimCSE, Bi-Encoder, Cross-Encoder;
  * Complex judgment: Through instruction fine-tuning on LLM, enable the model to directly output labels or logical relationships.

### 1.2.1 Text Classification: From "Understanding Content" to "Qualifying Content"

By leveraging the semantic representation of the previous layer, we can very naturally attach a simple classification head on top of it, allowing the model to learn to answer a question through a small amount of labeled data:  ** "Which category does this text belong to?" ** .

The most classic one is  ** sentiment classification ** . A user's comment may be an endorsement, a complaint, or simply a statement of fact. After the model obtains the vector representation of this sentence, it only needs to connect a softmax classification layer to output the probabilities of "positive / negative / neutral". This type of capability has already been very mature in scenarios such as e-commerce, social platforms, and app markets.

Another major category is  **topic/industry classification** . In news recommendation, we hope to know whether an article is about sports, finance, or entertainment; in an enterprise's internal customer service/ticket system, it is more concerned about whether it is a product consultation, a functional anomaly, or a complaint and suggestion. These labels can not only help content be more accurately routed to the appropriate process but also serve as important features during the recommendation and ranking stage.

Furthermore,**risk/compliance classification**is directly related to platform security. We will set up specialized classification models for categories such as advertising diversion, abuse and attacks, politically sensitive content, and vulgar and pornographic content, and cooperate with manual review to intercept or downgrade high-risk content. It can be said that the first line of defense for most Content-Security-Policies is composed of such classifiers.

As can be seen, up to this level, we have been able to transform "abstract semantic representation" into several business-usable labels. Next, what we are going to discuss is: when relationships are formed between texts, how do we perform  ** matching and inference ** .

### 1.2.2 Text Matching: "Find the most suitable other sentence" for a given sentence

Different from the classification pair "qualitative analysis of a single text", ** text matching ** focuses on "the correlation between two texts". In many products, this is often a crucial step in achieving "intelligence": when a user says something, whether the system can find the most appropriate item in the knowledge base to respond depends entirely on the quality of the matching.

The most fundamental is  ** semantic similarity calculation ** . We will first use the embedding model from the previous layer to encode two sentences into vectors, and then determine their distance in the semantic space through methods such as cosine similarity and dot product. Models like SimCSE and Sentence-BERT specifically use contrastive learning to bring "similar sentence pairs" closer and push "dissimilar sentence pairs" farther apart.

Beyond this,**plagiarism detection**and**copying detection**are simply matching tasks for specific application scenarios. The former is used for content deduplication to prevent the platform from being flooded with repetitive expressions; the latter is used in scenarios such as education and knowledge communities to identify highly similar answers or articles. Technically, they are essentially binary classification or ranking tasks based on text similarity.

A very important downstream application is  ** question-answer matching ** . When a user poses a natural language question, we do not directly use keywords to match FAQs, but instead first perform retrieval through semantic vectors, then re-rank several candidates using a more refined matching model (such as the cross-encoder Cross-Encoder), and select the most likely corresponding entry. This pipeline forms the basis of FAQ robots and document question-answering systems.

At this level, we already have the ability to classify and judge relationships for "whole text segments". However, in many scenarios, the business is not satisfied with this and further hopes to know:  ** What specific entities are mentioned in this text segment and what events have occurred ** . This naturally leads to the topic of the next section -  ** Sequence Labeling and Information Extraction ** .

## 1.3 Sequence Labeling & Information Extraction

After completing the overall classification and matching of text, we often encounter a more detailed requirement: not only to know "what this article is about and whether the risk is high", but also to further know "who it specifically mentions, where, when, and how much the amount is". This section is a crucial step towards "fine-grained structuring" on top of the overall judgment. You can understand it as: on the premise of already knowing "which type of text to look at and what it is roughly about", mining entities, relationships, events, and various fields from within the text, so that unstructured text can be directly consumed by business systems. We also look at this layer from four aspects: objective, principle, model, and product:

* **Scenario**
  * Structuring of industry texts: Extract key fields such as names, institutions, amounts, times, and clauses from documents like contracts, reports, announcements, medical records, policies, etc., for storage and retrieval.
  * Knowledge Graph and Relationship Network: Identify entities and their relationships from news, papers, and Q&A, construct a graph of "who has what relationship with whom", and use it for search, recommendation, and analysis.
  * Invoice and Documentation Processing: Automatically extract fields such as title, tax number, amount, and date from invoices, statements, reimbursement forms, etc., to reduce manual data entry.
  * Public Opinion and Event Analysis: Extract "who did what, when, and where" from massive text for event tracking, risk early warning, and statistical reporting.
  * Structuring of logs and tickets: Extract key information from unstructured text such as customer service conversations, tickets, and system logs to facilitate statistics, monitoring, and automated processing.
* **Principle**
  Perform fine-grained annotation and structuring of text at the token/phrase level:
  * Sequence Labeling: Assign labels to each token (such as person names, place names, organization names, product names, etc.) to achieve Named Entity Recognition, Part-of-Speech tagging, phrase segmentation, etc.;
  * Relationship and Event Extraction: Identify the relationships between "entity-entity" and the event structure of "who did what, when, and where" on top of entities;
  * Business field extraction: Centering around specific business schemas (such as contract fields, documentation fields), convert long documents into standardized key-value pairs or record tables.
* **Model**
  completes information extraction through structures such as sequence labeling or span extraction based on pre-trained representations:
  * Sequence labeling models: BiLSTM-CRF, BERT + CRF / Softmax, etc.;
  * Span-based extraction: directly predict the start and end positions of entity/relationship fragments;
  * Document-level extraction: DocIE-like models that combine layout and formatting;
  * LLM-based extraction: Through Prompt / Few-shot, enable the large model to extract the required fields in the specified format.

### 1.3.1 Sequence Labeling: Assign semantic "labels" to each token and phrase

During the text classification stage, we only care about which category the entire text belongs to; while in the sequence tagging stage, we need to label each token and each phrase in the text. The most typical task is Named Entity Recognition (NER): identifying entities of specific types such as person names, organization names, location names, product names, disease names, etc.

* For example, in the sentence "Zhang San joined a certain technology company in Beijing", label "Zhang San" as a person's name, "Beijing" as a place name, and "a certain technology company" as an organization.

From a modeling perspective, the traditional approach is to use sequence tagging structures such as BiLSTM + CRF, while subsequent methods more often adopt BERT + CRF or BERT + Softmax, leveraging the context representation capabilities of pre-trained encoders to determine the label of each token (e.g., B-ORG, I-ORG, O, etc.). In practice, the NER model is often the first "preprocessing" step for subsequent Knowledge Graph and relation extraction.

In addition to NER, part-of-speech tagging and phrase segmentation also belong to typical sequence tagging tasks. They are more focused on serving low-level language analysis, providing the underlying structure for subsequent more complex syntactic/semantic tasks.

* For example, in "rapidly improve model performance", mark "rapidly" as an adverb, "improve" as a verb, and "performance" as a noun for downstream analysis.

### 1.3.2 Relationship and Event Extraction: Connecting "Points" into "Lines" and "Stories"

After we identify entities in text through sequence tagging, a natural question arises: What exactly are the relationships between these entities, and what kind of events do they jointly constitute?

Relation extraction focuses on "entity pair + relation type". For example, in the sentence "Zhang San joined a technology company as CTO in 2024", we not only need to identify the two entities "Zhang San" and "a technology company", but also extract the "employed at" relation between them.

* Simply put, it is to attach a relationship label such as "employed" to the pair of entities "Zhang San - a technology company".

Beyond relationships, event extraction attempts to reconstruct "who did what, when, and where". Taking a news item as an example, a standard event template may include multiple slots such as event type (acquisition, cooperation, accident), time, location, participants, amount, consequences, etc. The event extraction model needs to automatically fill these slots from lengthy text, thereby constructing an "event table" that can be retrieved, statistically analyzed, and inferred.

* For example, extract from "A company acquires another company for 5 billion yuan": Event Type = Acquisition, Amount = 5 billion yuan, Participants = two companies.

In terms of modeling methods, in addition to traditional sequence tagging-based extraction, we will also adopt Span-based IE (directly predicting the start and end positions of entity/relation spans), as well as Prompt-based IE and LLM-based Few-shot extraction, which have emerged in recent years. The advantage of the latter lies in its ability to quickly adapt to new schemas through natural language prompts, reducing the cost of extensive re-labeling and training.

From an engineering perspective, a mature extraction system often forms a pipeline:

* Upstream NER/Sequence Labeling identifies entities;
* The middle layer models relationship and event structures;
* The downstream writes the results into a database or Knowledge Graph for consumption by search, analysis, and risk control systems.

## 1.4 Text Generation & Editing

In the previous sections, we have successively constructed the understanding link of "representation → classification matching → sequence labeling and extraction": the model can not only map text into semantic space, but also make judgments on the entire text and extract structured information from it. What this section aims to do is to "reverse" this understanding link: on the basis of full understanding, enable the model to actively generate, rewrite, compress, and polish text. You can understand it as performing "reverse encoding" in semantic space, transforming internal representations back into high-quality natural language output, which is the layer closest to user perception in the entire text modality capability chain. We will still break it down from four dimensions: objective, principle, model, and product:

* **Scenario**
  * Daily writing and work: Generate emails, notices, draft proposals, or expand, rewrite, and polish existing texts.
  * Knowledge Management and Summarization: Automatically summarize long documents, reports, and meeting minutes to help quickly grasp key points.
  * Customer Service and Q&A: Automatically generate well-structured and consistent answers based on user questions and retrieved materials.
  * Marketing and Creative Content: Generate advertising copy, social media posts, event introductions, scripts, etc.
  * Multilingual Scenarios: On the basis of maintaining the original meaning, complete translation, localization adaptation, and adaptation to different languages and scenarios.
* **Principle**
  Based on language modeling, text is processed in two ways: "from scratch" and "modification based on existing content":
  * Free Generation: Generate a complete text from scratch based on intent, prompts, or outlines;
  * Controlled Rewriting: Adjust style, length, and structure (such as summarization, expansion, style conversion) while keeping the core information unchanged;
  * Correction and Polishing: Correct typos and grammar issues, optimize the expression order and logical structure.
* **Model**
  is mainly based on generative models with large-scale pre-training + instruction fine-tuning:
  * Instruction-tuned LLMs: GPT series, LLaMA / Qwen / GLM, etc., for general generation and editing;
  * Seq2Seq models: T5, BART, mT5, etc., used for tasks such as summarization, translation, format conversion, etc.;
  * Alignment and Safety: Make the generated content more compliant with instructions and safety requirements through means such as RLHF / RLAIF.

Since this part is basically equivalent to prompt engineering, we will not elaborate further. You can refer to the tutorial on the prompt engineering section on your own.

# 2. Image Modality (Image / Vision)

In AI capabilities, the image modality is responsible for "understanding the world visually." Whether the ultimate goal is security monitoring, autonomous driving, short video special effects, e-commerce intelligent photo retouching, MultiModal Machine Learning question answering, or AI painting, in essence, they all rely on a common path: starting from raw pixels, gradually acquiring the ability to obtain structured understanding of the image and controllable generation.

## 2.1 Low-Level Vision

In the previous section, we introduced the role of the visual modality in the MultiModal Machine Learning system as a whole, as well as its connection with language and speech. However, before truly delving into "high-level semantic tasks" such as Object Detection, Image Understanding, and Visual Question Answering, there is a fundamental capability layer that is often overlooked but crucial - low-level vision. You can understand it as: before "understanding what is in the image", the system needs to first address two issues: "how is the quality of this image itself" and "what stable local structures can be reused by the upper layer", using a layer of general restoration, enhancement, and structure extraction to transform the raw pixels into a cleaner and more stable image representation.

From an engineering perspective, low-level vision not only directly affects the "image quality experience" perceived by users' naked eyes but also determines whether the input distribution of high-level tasks such as detection, recognition, and segmentation is healthy. If this layer is not well implemented, all subsequent models will have to operate under the harsh conditions of "high noise, severe distortion, and extreme lighting"; conversely, if the images are repaired as much as possible and structural information is well extracted at this layer, high-level tasks can perform better on a more user-friendly foundation. Next, we will also examine this layer from three perspectives: scenario, principle, and model:

* **Scenario**
  * Camera and shooting equipment: Automatic noise reduction, HDR, night mode, anti-shake, and multi-frame fusion of mobile phones/cameras enhance details and dynamic range.
  * Content Platform and Short Videos: One-click image/video quality enhancement for uploaded content, removing compression artifacts, improving sharpness and contrast, and enhancing subjective visual experience.
  * Old Photo and Document Restoration: Denoising, coloring, and super-resolution of old photos; automatic straightening and enhancement of skewed or dimly lit receipts, contracts, and book pages for easy OCR.
  * Monitoring and Security: Noise reduction, dehazing, anti-raindrop, and resolution enhancement of low-light monitoring images, laying the foundation for subsequent face/license plate recognition.
  * AR/VR and 3D Reconstruction: Provide stable corner points, edges, and local descriptors for SLAM, panoramic stitching, and 3D reconstruction, ensuring the robustness of tracking and registration.
* **Principle**
  Centering around the two core objectives of "image quality" and "local structure", physical and statistical modeling is performed on pixel-level information:
  * Image Restoration and Enhancement: Assuming that the observed image is obtained after the ideal image has undergone degradation such as noise, blur kernel, compression, and imaging nonlinearity, under this assumption, denoising, deblurring, de-compression artifact removal, low-light enhancement, and super-resolution reconstruction are performed to make the output closer to the imaging of the real scene while conforming to the perception habits of the human eye.
  * Structural Feature Extraction: Without introducing specific semantic labels, features such as edges, corners, local textures, and salient regions are extracted from pixel gradients and texture statistics, providing a "geometric skeleton" for subsequent detection, registration, tracking, and segmentation.
  * Geometry and illumination preprocessing: Estimate distortion and perspective relationships based on camera models and simple geometric cues (lines, vanishing points, symmetry, etc.), and align the original image to a more standard and stable input space through operations such as undistortion, rectification, contrast and illumination normalization.
* **Model **
  Comprehensively uses classical image processing methods and Deep learning models, making a trade-off between efficiency and effectiveness:
  * Traditional Image Processing: Bilateral Filtering, Non-Local Means, Guided Filtering, Retinex, Histogram Equalization, Canny/LoG Edge Detection, Harris/FAST Corner Detection, SIFT/SURF/ORB Descriptors, Hough Transform, Camera Calibration and Geometric Correction, etc.
  * Deep Restoration and Enhancement Models: Denoising, deblurring, super-resolution, deraining/dehazing/decompression artifact models based on CNN or Vision Transformer (such as EDSR, RCAN, SwinIR, ESRGAN, etc.), as well as multi-frame/video enhancement networks, which learn the mapping from degraded images to high-quality images in an end-to-end manner, or use modern image editing models such as Dreamina and Qwen editing models.

### 2.1.1 Image Restoration and Enhancement: From "Visible" to "Clear"

In low-level vision, image restoration and enhancement first confront various forms of degradation: noise, blurring, compression artifacts, low illumination, insufficient dynamic range, etc. In many real-world scenarios, the original images are not "clean": night scenes and indoor low-light conditions can cause the image to be filled with grain and color spots, while candid and surveillance images often appear blurry due to motion or inaccurate focusing, and video compression can introduce blocky artifacts. The goal of restoration and enhancement is to restore clear details and natural visual appearance as much as possible without altering the semantic content of the image, transforming "blurry, dim, and dirty" inputs into "clear, bright, and comfortable" outputs.

Typical tasks include denoising, deblurring, low-light enhancement, and super-resolution, etc. Denoising and deblurring require a trade-off between local texture and overall structure: it is necessary to suppress high-frequency noise and deconvolve the effects of the blur kernel, while not smoothing out real details; low-light enhancement needs to enhance brightness and contrast while avoiding pulling up dark noise together, correcting color cast, and suppressing overexposed areas; super-resolution focuses on supplementing reasonable high-frequency information while magnifying, so that the magnified image neither appears "blurry" and "plastic-like" nor "fabricates" details excessively. Most modern methods use deep networks (CNN or Vision Transformer), learning the mapping from the observed image y to the ideal image x on a large amount of "degraded-clear" paired data, while using a combined objective that includes pixel error, perceptual loss, and adversarial loss to strike a balance between "good metrics" and "good to the human eye".

The manifestation of these capabilities in products is often implicit: the night mode and HDR photography of mobile phone cameras, the one-click image quality enhancement of Short Video Platforms, old photo restoration tools, and the cloud enhancement services of surveillance systems all essentially rely on the restoration and enhancement modules at this level. For business, they not only directly affect users' subjective perception of "image quality" but also indirectly determine the input quality of algorithms such as upper-level detection, recognition, and segmentation. It can be said that the more complex the upper-level visual tasks are, the more they rely on a high-quality and stably distributed "image foundation" at the bottom layer.

### 2.1.2 Structural Features and Preprocessing: Building the "Scaffold" for High-Level Understanding

After the image quality has been restored to a usable level, the second key task of low-level vision is to extract features from pixels that are temporarily unrelated to specific semantics but are crucial for geometric structure and visual perception, and to unify geometry and illumination. This step will not directly tell you "here is a car" or "this is someone's face", but will answer questions such as "where there are clear contours and corners", "which regions have significant texture structure", and "whether the image is distorted or tilted", providing reliable structural input for upper-level models.

In terms of feature extraction, edges and corners are the most fundamental elements. Through operators such as Canny and Sobel, the system can mark the "edges" with the most drastic changes in canary release or color across the entire image, which often correspond to object contours, component boundaries, and texture directions; corner detection (such as Harris and FAST) finds the "corners" where local gradients change significantly in multiple directions, usually appearing at object corners and line intersections. Further, local descriptors like SIFT, SURF, and ORB encode the texture patterns of a small area around these key points, enabling the same physical point to still be matched under different perspectives, scales, and certain lighting changes, which provides fundamental support for image registration, panoramic stitching, SLAM, AR tracking, and 3D reconstruction.

Parallel to feature extraction are various geometric and illumination preprocessing operations. Barrel/pincushion distortion caused by wide-angle lenses, as well as tilt and perspective stretching when photographing documents, are all identified through low-level geometric cues such as line detection and vanishing point estimation, and are "pulled back to normal" through steps such as undistortion, rectification, and perspective correction; global or adaptive histogram equalization, contrast stretching, and illumination normalization enhance local contrast, reduce the effects of uneven illumination and shadows, while ensuring that details are not lost. Color space transformation (RGB→HSV/Lab) and color histogram statistics provide directly usable inputs for tasks such as simple color-based segmentation, salient region detection, and color cast correction.

After end-to-end deep learning became mainstream, some of these structural features and preprocessing steps were "internalized" into the convolution kernels and normalization strategies of the first few layers of the network, and no longer appear in the system architecture diagram as explicit operators. However, functionally, they still play the same role: first, use a relatively general, category-independent low-level processing layer to organize the raw pixels into a more stable representation in terms of geometric shapes, lighting conditions, and local structures, and then pass it on to the upper-level classification, detection, segmentation, and multi-modal machine learning modules to complete the task of "understanding what this is". Without this "scaffold", the upper-level models would have to operate directly on the raw images with high noise, severe distortion, and blurred structures, and the robustness and generalization ability of the overall system would significantly decline.

## 2.2 Image Classification & Recognition

In most image tasks, the issues that business parties truly care about are: ** What category does this image as a whole belong to? Who is the person in the image? Is this pedestrian the same person across different cameras? ** You can understand this layer as: on a unified and clean input space, assigning "category labels" or "identity labels" to the entire image or the entire person/target, and converting visual signals into the most directly usable recognition results.

From a product perspective, image classification and recognition were among the earliest batch of visual capabilities to be widely deployed, and they also serve as the "entry module" for many upper-level applications. E-commerce and content platforms use them to automatically tag images and identify the main categories; security and access control systems use them to confirm "whether it is the same person"; pedestrian re-identification systems sift through multiple camera feeds to find the cross-scenario trajectories of the same target. Next, we will also sort out this layer from the three perspectives of scenario, principle, and model:

* **Scenario**
  * Universal Image Understanding: Automatically assigns theme tags such as "scenery / food / pet / document" to images uploaded by users for retrieval, recommendation, and content moderation.
  * Face Recognition and Access Control: In face access control and attendance systems, personal identities are recognized based on facial images to enable "face recognition entry" and "face recognition clock-in".
  * Pedestrian/person re-identification: Determines whether it is the same pedestrian or person in different camera frames, used for security retrieval and trajectory analysis.
  * Human Attribute Recognition: Without directly confirming identity, it identifies attributes such as gender, age group, whether wearing a hat/backpack/uniform, etc., providing clues for retrieval and behavior analysis.
* **Principle**
  In a unified visual feature space, discriminative modeling is performed on the entire image or the entire person/target:
  * Image Classification: Taking the entire image as input, global features are extracted through a convolutional network or a vision Transformer, and a classification head is connected to the top layer of the features to output single-label or multi-label class probabilities, which are used to answer "What type of image is this?"
  * Identity/Instance Recognition: Transforms the question of "who" into a metric learning problem in the feature space, that is, learns an embedding space where image features of the same identity are close to each other, and features of different identities are far from each other, and then uses nearest neighbor search or clustering to complete recognition and retrieval.
  * Attribute Recognition: On top of the shared pedestrian/human body features, additional multi-task output heads are added to predict attribute labels such as gender, age group, clothing color, and whether carrying items, enabling the same features to serve various downstream retrieval and analysis requirements.
* **The model **
  uses deep convolutional networks and visual Transformers as the backbone, combined with classification heads or metric learning heads to implement different types of recognition tasks:
  * Image Classification Backbones: ResNet, DenseNet, EfficientNet, ConvNeXt, Vision Transformer (ViT), Swin Transformer, etc., are usually pre-trained on large-scale datasets such as ImageNet and then fine-tuned on specific business data.
  * Universal Classification Structure: Backbone + Fully Connected Classification Layer (Softmax / Sigmoid), used for single-label or multi-label image classification tasks, and can address long-tailed distributions through techniques such as class reweighting and focal loss.
  * Identity/Instance Recognition: Above the feature output of the Backbone, loss functions with angular constraints such as ArcFace, CosFace, and SphereFace are used to explicitly increase the inter-class spacing between different identities, enhance separability in the feature space, and complete comparison on large-scale databases through vector retrieval (ANN).
  * Pedestrian/Attribute Recognition Structure: For pedestrian Re-ID and human attribute recognition, the common practice is to use a shared backbone to extract pedestrian features, and then separate the "identity branch" and "attribute branch" at the top layer, which not only optimizes the ability to distinguish identities across cameras but also takes into account multi-attribute prediction.

Corresponding to specific product forms, the capabilities at this level are often provided externally in the form of "Image Content Recognition/Classification API", "Facial Recognition SDK/SaaS", "Pedestrian Re-identification Platform", etc. They often not only directly drive business decisions (such as access control release, content tag writing), but also serve as an upstream source, providing structured tags and stable identity representations for subsequent retrieval, recommendation, behavior analysis, and MultiModal Machine Learning understanding. Next, we will expand from two perspectives: image classification and identity/attribute recognition.

### 2.2.1 Image Classification: Answer "What kind of image is this?"

In the most basic image classification task, the system deals with the entire image, with the goal of assigning one or several semantic category labels to it. The most common is single-label classification. For example, in a dataset like ImageNet, each image is labeled with a primary category such as "dog", "cat", "car", "airplane", etc.; in business scenarios, this type of capability is widely used to add theme labels such as "landscape / food / pet / portrait / document" to images uploaded by users, supporting retrieval, recommendation, and content moderation. Similar to text classification, the model will connect a fully connected + Softmax layer on top of the global visual features extracted by the pre-trained Backbone to output a probability distribution for all candidate categories.

In many practical applications, an image often belongs to multiple categories simultaneously. For example, a "selfie at sunset by the sea" image can be both a "landscape" and a "portrait", and may also be labeled as "travel" or "seaside". In such cases, multi-label classification (Multi-label Classification) is required: the model still starts from the features of the entire image, but the output layer is no longer the mutually exclusive Softmax, but instead predicts the presence/absence probability (Sigmoid) for each label separately, and uses a multi-label loss function for training. To address the large number of "long-tail categories" (categories with very few samples of rare labels) in real-world data, multi-label classification models often incorporate mechanisms such as category reweighting, hard example mining, or label structure modeling to improve the recall of niche categories.

At the human-machine interface level, image classification is typically provided externally in the form of a "Picture Content Recognition API". Upstream services only need to upload an image to obtain a set of category labels and their Confidence Levels, which are used for subsequent policy judgments: for example, advertising delivery systems can restrict certain sensitive categories based on picture content, e-commerce platforms can use image classification to assist in correcting product category errors, and content platforms can use it to enrich recommendation features and review signals. Although technically, this type of capability is relatively mature, it remains the cornerstone for more complex capabilities such as subsequent Object Detection, Instance Segmentation, and Visual Question Answering.

### 2.2.2 Image Recognition and Attribute Recognition: Answer "Who is this / What instance is this?"

Different from "what type of image this is", image recognition is more concerned with "who this person/object in the image is", that is, identity-level and instance-level discrimination. Typical representatives are face recognition and pedestrian re-identification: the former determines "which identity in the database the current face is closest to" in scenarios such as access control, attendance, and payment; the latter searches for the presence of the same pedestrian in surveillance footage from multiple cameras and different time periods, assisting in case backtracking and trajectory analysis. The core of this type of task is no longer simple multi-classification, but rather how to learn an embedding that is "compact within classes and separated between classes" in the feature space, so that images of the same identity captured under different poses, lighting conditions, and cameras can still be clustered together.

In model design, face recognition and pedestrian re-identification typically adopt similar paradigms: first, use backbones such as ResNet, ConvNeXt, ViT, and Swin to extract face/pedestrian-centered features, and then connect them with loss functions specifically designed for metric learning, such as ArcFace and CosFace. Different from ordinary classification losses, these losses directly constrain the inter-class boundaries in the angular space or feature space, explicitly increasing the gap between features of different identities, so that the trained features can be used for large-scale vector retrieval without being limited to the fixed categories seen during training. During online service, the system first precomputes and indexes the features of each identity in the gallery, then performs approximate nearest neighbor search on the face/pedestrian features of online queries, finds several most similar candidates, and makes the final decision by combining business thresholds and MultiModal Machine Learning information.

Corresponding to "direct identity recognition" is  **attribute recognition** , which does not point to a specific individual. In many security and retail scenarios, the system only needs to know attributes such as "male or female", "approximate age range", "whether wearing a hat/mask", "clothing color and style", "whether carrying a backpack/pulling luggage", etc., for quickly screening targets, without the need or suitability to directly output personal identity. Such tasks usually connect multiple parallel attribute heads (a head refers to the position where probability is output, and multiple probability output results can be used to judge categories) on top of shared pedestrian/body features, with each head responsible for predicting one or a set of attribute labels, forming a multi-task learning framework. On the one hand, multi-task training can make features more abundant and generalize better; on the other hand, attributes themselves can also serve as auxiliary conditions for Re-ID or retrieval, enhancing the system's usability in complex scenarios.

In terms of product form, this type of capabilities are usually packaged as "Face Recognition SDK/Cloud Service", "Pedestrian Re-identification Platform", "Human Attribute Recognition API", etc., and integrated into access control gates, attendance machines, security platforms, and video structuring systems. Compared with general image classification, they have higher requirements for data security and privacy protection, and are more sensitive to the trade-off between false recognition rate and recall rate. Therefore, in addition to algorithms, they are also supplemented by mechanisms such as quality inspection (e.g., whether it is a real person, whether it is occluded/photographed), live detection, and MultiModal Machine Learning cross-verification, to form a more complete and responsible identity recognition solution.

## 2.3 Object Detection (Object Detection)

In the previous image classification and recognition, we only assigned an overall label to the "entire image" or "whole person", while ignoring its position and size in the image. However, the more common problems in real-world business are: ** What objects are in this image? Where are they located respectively? ** For example, in a street view image, we hope to simultaneously mark all pedestrians, vehicles, and traffic signs; in an industrial production line, we need to mark all defective areas and part positions in the same frame. Object Detection is designed for these needs: it simultaneously predicts the ** position (bounding box) and category ** of each object in a single image or video frame, and is the fundamental ability for many downstream vision tasks (tracking, segmentation, behavior analysis, multi-object counting, etc.).

From an engineering application perspective, Object Detection is the "first step of structuring" for many vision systems, breaking down an original image into several labeled rectangular boxes, each of which can be further sent to other modules for recognition, tracking, attribute analysis, and even semantic generation. The detection of pedestrians/vehicles in security cameras, the detection of products on unmanned retail shelves, the detection of defects/foreign objects in industrial quality inspection, and the "Object Detection" API provided by cloud providers all essentially rely on this layer of capabilities. Below, we will sort out Object Detection from three perspectives:  ** scenarios ** ,  ** principles ** , and  ** models ** , and expand on the key directions in the subsequent sections.

* **Scenario**
  * Security and Traffic Monitoring: Real-time detection of pedestrians, vehicles, non-motorized vehicles, traffic signs, reverse/illegal occupation targets, etc. in camera footage, providing a basis for subsequent behavior analysis and alerts.
  * Industrial Quality Inspection and Manufacturing: Detect product defects (scratches, damages, foreign objects), component positions, and missing assemblies on the production line, supporting automatic rejection and robot positioning.
  * Retail and Logistics: Product detection and settlement for unmanned retail shelves; Object Detection and positioning of packages, pallets, and stacks in warehouses, assisting inventory counting and robot grasping.
  * Content Understanding and Moderation: Detect people, logos, weapons, sensitive items, etc. in images/videos to provide structured signals for content moderation, advertising compliance, and brand recognition.
* **Principle**
  The core of Object Detection is to build a dense prediction mechanism on images:
  * The input image is extracted into multi-scale feature maps through the Backbone. On these feature maps, for each "location" (or candidate region), predictions are simultaneously made for "whether there is an object", "what category it belongs to", and "the corresponding bbox parameters".
  * According to the architecture, there is the **two-stage detection (Two-stage)** that first generates candidate boxes and then refines them, as well as the integrated **one-stage detection (One-stage)** that directly performs classification + regression on the feature map. The two have different focuses on accuracy and speed.
  * Divided by the design of candidate boxes, there are **anchor-based** methods that rely on predefined anchors, as well as **anchor-free** methods that directly predict the center point/boundary and the **DETR family** based on set matching.
  * To address small targets, dense targets, occlusion, and scale variations in real-world data, detectors typically optimize by combining multi-scale features (FPN), higher resolution inputs, specific loss functions, and post-processing strategies (such as NMS variants and multi-scale testing).
* **Model **
  The detection model is generally composed of ** backbone network + feature pyramid / head structure + loss and post-processing ** three parts:
  * Classic two-stage detectors: Faster R-CNN, Mask R-CNN, etc., first generate candidate boxes through RPN, then perform fine-grained classification and regression on each candidate region, with high accuracy, clear structure, and suitable for scenarios with extremely high accuracy requirements.
  * Single-stage detectors: SSD, RetinaNet, YOLO series (YOLOv5/6/7/8, YOLOX, YOLOv10, etc.), etc., complete detection in a unified network, featuring a compact structure and low latency, and are the mainstay of real-time detection in the industrial sector.
  * Anchor-free / Transformer Detectors: FCOS, CenterNet, ATSS, etc., directly predict bounding boxes centered on pixel points; DETR / Deformable DETR, etc., treat detection as a problem of "generating a set of targets from a set of queries" through Transformer and set matching, simplifying various handcrafted designs.
  * Video Detection and Tracking: Based on the image detector, introduce temporal information and association strategies (such as tracking head, optical flow, trajectory matching) to form a unified framework of Detection + Tracking, which supports long-term, multi-target behavior analysis.

Overall, Object Detection occupies the "central position" in the spectrum of visual capabilities - on the one hand, it receives clean image inputs provided by low-level vision, and on the other hand, it deconstructs images into "object-level" elements for recognition, tracking, segmentation, and MultiModal Machine Learning understanding. Next, we will expand from three directions:  **Single/Double-Stage Detection Architectures** ,  **Anchor-based / Anchor-free / Transformer Detection** , and  **Small Object and Video Detection** .

### 2.3.1 Single-Stage vs. Two-Stage Detection: Structural Trade-Off between Accuracy and Speed

Architecturally, the most classic division of Object Detection is  ** Two‑stage and One‑stage ** . The main difference between the two lies in whether it is to "coarsely select a batch of candidate boxes first and then refine them" or to "predict all boxes and classes at once" on the feature map.

Two-stage detection is represented by Faster R-CNN. It first generates a batch of candidate boxes (first stage) that "highly likely contain the target" on the Backbone feature map through the RPN (Region Proposal Network), then performs RoI alignment and feature extraction on each candidate region, and finally conducts more refined classification and bounding box regression (second stage). The advantage of this design is that a large number of negative samples are filtered out at the RPN stage, allowing the second stage to focus on a small number of candidate regions for high-quality discrimination. Therefore, it often has an advantage in accuracy and is easier to extend to tasks such as instance segmentation (Mask R-CNN) and keypoint detection (Keypoint R-CNN). However, the computational and implementation complexity brought by the multi-stage structure is relatively high, making it more suitable for offline or quasi-real-time scenarios where real-time requirements are not as stringent but accuracy and scalability are emphasized.

Single-stage detection aims to streamline the entire process, simultaneously performing category classification and bounding box regression within a unified network. Representative models include SSD, RetinaNet, and the YOLO series: they directly predict the "foreground/background + category + bbox" of several candidate boxes at each position on the multi-scale feature map, eliminating the explicit proposal stage and being more suitable for end-to-end acceleration and deployment. Early single-stage detectors had a certain gap in accuracy compared to two-stage detectors, but with their simple structure and high speed, they quickly dominated the industrial field; with the introduction of FPN, focal loss, IoU-aware loss, as well as stronger Backbone and Neck, new-generation models such as RetinaNet, YOLOX, YOLOv7/8/10 have achieved an accuracy-speed balance of "approaching or even surpassing two-stage detectors" in many tasks.

At the application level, engineering usually makes trade-offs between these two types of architectures based on requirements: for tasks such as cloud-based batch offline analysis that require high precision and scalability (e.g., simultaneous detection + segmentation + key point detection), two-stage detection remains a stable and reliable choice; while for latency-sensitive scenarios such as edge devices, mobile applications, and real-time camera detection, single-stage detectors like the YOLO series are almost the default first choice, and often combined with techniques such as quantization, pruning, and distillation to further compress the model and improve throughput.

### 2.3.2 Anchor‑based and Anchor‑free: From Manual Setting to End-to-End Learning

Regarding the issue of how to define "candidate boxes", detection methods can be further divided into **Anchor-based and Anchor-free** two major categories. Early mainstream methods (such as Faster R-CNN, SSD, RetinaNet, YOLOv3/v4/v5, etc.) adopted the Anchor-based approach: pre-defining a number of anchor boxes with different scales and aspect ratios at each position of the feature map, and then learning the foreground probability and bbox offset corresponding to each anchor. This approach is simple to implement and effective, but requires manual adjustment of many parameters for the size and ratio of the anchors, and is prone to problems such as a large number of anchors and extreme imbalance between positive and negative samples in scenarios with small targets and dense targets.

Anchor-free methods attempt to break free from the reliance on pre-defined anchors. Represented by FCOS, CenterNet, ATSS, etc., they typically directly predict "whether this is the center of a target (or belongs to the target)" and the corresponding boundary distances at each pixel point on the feature map, thus completely avoiding the complexity of pre-set anchors. The advantages of this approach are: the model structure is more concise, the training sample assignment strategy can be more natural, and it has better generalization and scalability, especially when dealing with real-world scenarios with large scale variations and complex target shapes. Meanwhile, anchor-free detectors have also promoted more unified frameworks based on pixels/points, making it easier to jointly model detection with tasks such as keypoints and segmentation.

Going further, Transformer-based detectors such as DETR/Deformable DETR have rethought the detection problem from another dimension: instead of densely laying anchors on the feature map, they introduce a fixed number of "object queries", and through the self-attention and cross-attention mechanisms of the Transformer, "generate" a set of object predictions from global features, and achieve one-to-one alignment through Hungarian Matching. This set prediction approach completely eliminates traditional components such as NMS and manual sample assignment, and is conceptually very concise, but in early implementations, it had problems such as slow convergence and being unfriendly to small objects; subsequent Deformable DETR has significantly improved both convergence speed and performance by introducing deformable attention and multi-scale mechanisms, and has gradually gained more applications in detection and multi-task scenarios.

In engineering practice, Anchor-based, Anchor-free, and Transformer-based Object Detection are not mutually exclusive choices, but rather resemble an evolutionary chain: from heavily engineered anchor design, to more end-to-end point/center prediction, and then to a unified framework fully based on set prediction and attention. In current industrial implementations, mature Anchor-based models such as the YOLO series remain the mainstay, while Anchor-free and DETR families are more commonly found in systems with high requirements for structural simplicity, multi-task unity, and scalability.

### 2.3.3 Small Object and Video Detection: Towards Robustness in Real-World Scenarios

Object Detection on public datasets often gives the illusion that "the problem has been basically solved," but once it comes to real-world scenarios, two types of thorny problems will immediately arise:**small objects/dense objects** and  **robust detection and tracking in videos** .

In small object detection, objects often occupy only a very small pixel area in the original image, such as pedestrians in the distance, distant vehicles, aerial drones, or tiny defects in high-resolution industrial images. As the backbone down-samples and the resolution of the feature map decreases, these small objects are easily "submerged" in high-level features, leading to missed detections. To address this, detectors typically employ multi-scale feature pyramids (such as FPN/PAFPN), increase the input resolution, add detection heads to shallow feature maps, and even specifically design branches and loss weighting strategies for small objects. Meanwhile, at the data level, it is also necessary to enhance the model's perception and memory capabilities for small-scale objects through methods such as cropping, zooming, and small object resampling.

Dense targets (such as crowded crowds, dense parking lots, and compactly arranged goods/parts) will expose problems such as anchor box overlap, NMS misclassification, and severe occlusion. Improvement strategies include more refined label assignment (such as self-adaptive assignment methods like ATSS), soft NMS or learning-based deduplication strategies, and alleviating inter-box competition through methods such as center point/density map modeling. In industrial quality inspection, many systems also combine detection with pixel-level segmentation to achieve more accurate defect localization for subsequent automatic processing.

When detection expands from single frames to videos, another challenge is  ** temporal continuity and target stability ** . Single-frame detectors make independent predictions on each frame, making it difficult to avoid short-term missed detections, ID jitter, and false alarms. However, alarms, counting, and trajectory analysis in real-world applications often require target trajectories that are consistent across frames. To address this, video object detection typically adds a Tracking module to integrate "detection + object tracking": the classic approach is to use an image detector as the front end and implement multi-object tracking in the back end using Kalman filtering, Hungary matching, appearance feature similarity, etc. (such as SORT, DeepSORT, etc.); a more advanced approach is to directly integrate the tracking head into the detection network, jointly learning detection and cross-frame association to improve robustness in scenarios such as short-term occlusion and fast motion.

In real-world systems, small targets, dense targets, and video detection are often not isolated problems but occur simultaneously: for example, distant pedestrians/vehicles in urban road surveillance, dense crowds in station squares, and high-speed moving parts in production line videos. This also determines that a high-quality Object Detection module, in addition to having outstanding metrics on standard benchmarks, needs to withstand the tests of various complex factors under real conditions such as multi-scale, multi-density, and long-duration videos to truly support upper-level behavior analysis, intelligent alarm, and MultiModal Machine Learning.

## 2.4 Image Segmentation

With Object Detection, we can already know "what objects are in the image and roughly where they are", but many tasks require more refined structured understanding: ** accurate to each pixel, determining which class it belongs to and which instance it belongs to** . For example, in autonomous driving, we need to know which pixels are roads, which are people and vehicles; in image matting tools, hair strands need to be clearly separated from the background; in medical images, the boundaries of tumors and organs need to be precisely delineated. Such tasks are collectively referred to as Image Segmentation, which directly outputs semantic or instance labels at the pixel level, providing more fine-grained spatial structure information compared to detection.

From a product perspective, image segmentation is the core capability of "pixel-level structuring": matting and background replacement tools rely on it to determine which pixels need to be retained; the perception module of autonomous driving relies on it to construct a detailed "drivable area + obstacle" map; medical imaging software relies on it to measure the size, shape, and volume of lesions; remote sensing platforms rely on it to distinguish features such as farmland, water bodies, buildings, and roads. Next, we will sort out image segmentation from three perspectives:  **scenarios** ,  **principles** , and  **models** , and expand on directions such as semantic/instance/panoramic/large model segmentation in subsequent sub-items.

* **Scenario**
  * Content Editing and Image Matting: Portrait Matting, Hair-Level Background Replacement, Object Extraction, and Layered Editing, used for Image Beautification, Short Video Special Effects, and Advertising Creative Production.
  * Autonomous Driving and Robotics: Label each pixel with road surface, lane lines, pedestrians, vehicles, guardrails, buildings, sky, etc., for path planning, collision warning, and environmental modeling.
  * Medical Image Analysis: Accurately segment organs, tumors, and lesion regions in images such as CT, MRI, and ultrasound, supporting auxiliary diagnosis, surgical planning, and efficacy evaluation.
  * Remote Sensing and Geographic Information: Segmenting features such as farmland, water bodies, roads, buildings, and forest land in satellite/aerial images, supporting national land planning, land use monitoring, and disaster assessment.
* **Principle**
  Image segmentation is essentially "dense prediction", which extracts multi-scale features from the input image through an encoder (Backbone), and then gradually restores the feature map to a segmentation map of the same size as the input through a decoder or upsampling module, outputting a semantic or instance label at each pixel position.
  * **Semantic Segmentation** : Assigns a semantic category (such as road, person, car, sky) to each pixel, without distinguishing different individuals of the same category, and is suitable for describing "scene composition".
  * **Instance Segmentation** : Based on semantic information, it further differentiates different instances of the same class, generating independent masks for "each vehicle, each person", and is a combination of detection and segmentation.
  * **Panoptic Segmentation** : It uniformly processes "countable objects (things, such as people and cars)" and "uncountable background (stuff, such as roads and sky)", assigning both semantic labels and instance IDs to each pixel simultaneously.
    Compared with detection, segmentation is more sensitive to spatial details and boundary quality, requiring richer multi-scale contextual information and more refined upsampling/fusion strategies.
* **Model**
  Classic to the latest segmentation models have roughly evolved along the path of "FCN → encoder-decoder → multi-scale context → integrated detection + segmentation → large model segmentation":
  * Semantic segmentation: FCN, U-Net and its variants, DeepLab series (DeepLabv3/v3+), PSPNet, etc., obtain multi-scale context and fine boundaries through methods such as dilated convolution, pyramid pooling, and skip connection.
  * Instance/Panoptic Segmentation: Mask R‑CNN, Panoptic FPN, Mask2Former, etc., combine the detection head with the segmentation head to achieve object-level segmentation and panoptic segmentation.
  * Large Models and General Segmentation: Basic segmentation models such as Segment Anything Model (SAM) have elevated segmentation from "training separately for each task" to "one model adapting to most segmentation scenarios", supporting interactive, prompt-based segmentation.

Overall, image segmentation provides a more detailed spatial structure representation compared to Object Detection, and is an indispensable part when building highly reliable perception systems and advanced editing tools. Next, we will explore from  **Semantic Segmentation and Instance Segmentation** ,  **Panoptic Segmentation and Detection Integration** , and **Generalized Segmentation** ,  **Large Models** , **and Unsupervised Segmentation**in three directions.

### 2.4.1 Semantic Segmentation and Instance Segmentation: From "Pixel Class" to "Pixel Instance"

**Semantic Segmentation **The goal is to assign a semantic category to each pixel in the image, so that the network learns "this area is the road, that area is the car, here is the person, there is the sky and buildings". The classic approach usually adopts an encoder-decoder structure: the encoder (such as ResNet, EfficientNet, Swin Transformer, etc.) extracts gradually downsampled high-level features, and the decoder combines rough high-level semantic features with low-level details through upsampling, skip connection, and multi-scale fusion to restore the original resolution. FCN systematizes this dense prediction form for the first time. U-Net has achieved great success in medical imaging through symmetrical U-shaped structure and a large number of skip connections. The DeepLab series expands the receptive field without reducing resolution through dilated convolution and ASPP. PSPNet obtains global contextual information through pyramid pooling. These models have jointly promoted large-scale applications in fields such as road scenes, remote sensing, and medicine.

**Instance Segmentation ** further distinguishes different individuals of the same class based on pixel semantic labels: not only do we need to know which pixels belong to "cars", but also which car each of these pixels belongs to. The most representative model is Mask R‑CNN, which adds a parallel segmentation branch to the detection framework of Faster R‑CNN: first, the detection head predicts the category and position of each candidate box, and then generates a binary mask within each box, thus obtaining the object-level segmentation result of "box + mask". Compared with pure semantic segmentation, this method can handle object overlap and occlusion well, and is the basis for tasks such as portrait/commodity matting, multi-object counting, and fine-grained editing. Subsequent instance segmentation methods have continuously improved in terms of mask quality, multi-scale, and speed, and new architectures based on anchor-free and Transformer have also emerged, but the idea of "detection + local segmentation" remains very mainstream.

At the product level, semantic segmentation typically appears in "scene-level" applications, such as autonomous driving road segmentation, remote sensing object recognition, medical organ segmentation, etc.; instance segmentation is more commonly used for "object-level" keying, counting, and editing, such as selecting and separating each vehicle, each person, and each item with a single click. Combining the two can provide both detailed and structured spatial information for upper-level tasks.

Semantic segmentation alone will mix objects of the same class together (all "car" pixels belong to the same class); instance segmentation alone often only focuses on countable "things" (such as people, cars, animals) while ignoring large areas of uncountable "background" (such as roads, grasslands, skies). In many scenarios, we need to know both** the instance-level mask of each object** and understand ** the overall scene composition** . This has given rise to ** Panoptic Segmentation** : assigning both a semantic class and an instance ID to each pixel simultaneously, achieving unified modeling of things + stuff.

Early panoptic segmentation systems were typically implemented through the approach of "semantic segmentation model + instance segmentation model + post-processing synthesis": first, a network was used to predict the semantic class of each pixel, then another network was used to output the masks and classes of each instance, and finally, the two were combined into a consistent panoptic segmentation result through a set of rules (such as priority and overlap handling). Panoptic FPN represents a more elegant engineering path: on a shared backbone and feature pyramid network (FPN), a semantic segmentation head and an instance segmentation head are respectively attached, and through joint training and feature sharing, both outputs are obtained simultaneously, and then they are fused through lightweight post-processing. This not only improves efficiency but also enhances the consistency between semantics and instances.

At the model level, with the development of integrated detection/segmentation and the Transformer architecture, unified panoramic segmentation frameworks such as Mask2Former have emerged: they tend to use a set of common "query + mask decoder" structures to simultaneously predict masks for semantic, instance, and even other downstream tasks within the same network, thereby significantly simplifying the system in terms of architecture and facilitating multi-task expansion. For complex tasks such as autonomous driving, robot navigation, and AR scene understanding, panoramic segmentation provides a complete scene description that is closer to the "subjective perception of the human eye", enabling higher-level decision-making and planning to be carried out on more accurate spatial semantics.

In terms of product form, panoptic segmentation is often embedded in autonomous driving, robotic systems, and high-end visual analysis platforms. Users may not directly perceive the concept of "panoptic segmentation," but they will truly benefit from more robust scene understanding and more natural interaction experiences.

### 2.4.2 General Segmentation and Unsupervised Segmentation: From Task Customization to "Segment Anything"

Traditional segmentation models are often trained around specific datasets and tasks, such as "19-class semantic segmentation of road scenes", "segmentation of certain tumors", "segmentation of certain types of goods", etc. Each task needs to be re-labeled and re-trained. In practical business, this method of relying heavily on precision-labeled data is costly and difficult to cover long-tail categories and emerging new scenarios. In recent years, with the development of large-scale pre-trained visual models and prompt-based paradigms, a **universal segmentation large model **represented by the **Segment Anything Model (SAM) **has emerged, attempting to elevate segmentation capabilities from "task customization" to "infrastructure".

Taking SAM as an example, it learns the general features of the entire image through a powerful image encoder (usually a large-scale pre-trained ViT), and then converts user-provided point, box, text prompts, etc. into segmentation results through a lightweight prompt encoder and mask decoder. During the training phase, SAM utilizes massive, multi-source, and multi-task mask annotations, enabling the model to learn a "generalized segmentation ability" rather than rote memorization of labels from a specific dataset; during the usage phase, users only need to provide a very small number of prompts (a single point or a rough box) to obtain high-quality masks on various unseen image types and object categories. This paradigm significantly lowers the threshold for building new segmentation applications and also provides a powerful tool for unsupervised/weakly supervised scenarios.

Related to this is the broader**unsup****er****vised/self-supervised segmentation**direction: without relying on or relying very little on manual masks, it automatically divides images into several meaningful regions through signals such as internal image similarity, temporal consistency, and multi-view constraints. Early work mostly focused on "visual clustering" and region proposal generation, while today it is more often internalized by large models as a form of representation learning, providing good initialization for downstream segmentation tasks. By combining text-image contrastive learning models such as CLIP, more and more methods can perform zero-shot or few-shot segmentation under the condition of "only providing text category names without mask annotations", offering new solutions for cold-start scenarios and long-tail classes.

In actual products, general-purpose large segmentation models often appear in forms such as "interactive image matting tools", "intelligent selection", and "one-click background removal", and are gradually integrated into professional software in fields such as medicine, remote sensing, and industry, serving as accelerators for semi-automatic annotation and auxiliary segmentation. Compared with traditional customized models, they may not achieve the ultimate performance in a specific task, but they have significant advantages in "being able to do a little of everything and quickly deploying in multiple scenarios", and also lay the foundation for the subsequent construction of truly multi-modal basic vision models.

## 2.5 Keypoint Detection & Action Recognition

After classification, detection, and segmentation, we can already know "what is in the image, where it is, and what each pixel belongs to". However, in many real-world tasks, what the business cares about is not only "the existence and location of objects", but  ** posture and motion ** : Is a person walking or running? Is this hand raised or making a certain gesture? Are workers correctly wearing safety equipment and performing standard actions? Are the technical movements of athletes standard? These questions require us to further understand  ** the internal structure and temporal changes of objects ** .

Key point detection and action recognition are two levels of capabilities designed to meet this need:

* **Keypoint Detection** : On an image or video frame, predict several "skeleton points" (such as joints, fingertips, facial features) of the target (usually a human body, hand, face, or specific mechanical structure) to obtain a detailed structured pose representation (pose).
* **Action Recognition** : Analyze the changes of these key points or appearance features over time in the time sequence to determine "what action or behavior this person/these people are performing".

From a product perspective, this capability is widely applied in scenarios such as human-computer interaction (gesture control), sports analysis (technical movement assessment), security (fall detection, abnormal behavior recognition such as fighting/running), industrial safety (violation action detection), virtual human driving (driving 3D skeletons and animations based on human body/face key points), etc. Next, we will sort out this layer of capabilities from three perspectives:  **scenario** ,  **principle** , and  **model** , and expand key point detection and action recognition respectively in subsections.

* **Scenario**
  * Human-Computer Interaction and AR/VR: Through gesture recognition and body posture detection, achieve natural interaction where "a gesture can control" or drive virtual humans in real-time in AR/VR.
  * Sports Training and Movement Analysis: Conduct key point tracking and angle analysis on movements such as running, high jump, shooting, weightlifting, etc., and provide technical movement evaluation and error correction suggestions.
  * Security and Public Safety: Detect abnormal behaviors such as falls, fights, intense running, and climbing over guardrails for timely alerts; identify whether operations are conducted in compliance with regulations at construction sites and industrial zones.
  * Industrial and human-robot collaboration: Detect whether workers operate in accordance with standard postures, the safety distance when collaborating with robots, and whether dangerous actions occur.
  * Facial/Expression Driven and Virtual Human: Capturing expression details through facial key points for expression transfer, digital human driving, virtual avatars in video conferencing, etc.
* **Principle**
  The two types of tasks respectively focus on spatial structure and temporal variation, but in essence, they are both structured prediction in high-dimensional feature space:
  * Key point detection: Locate a set of predefined key points (such as 17/25 human body joints, 21 hand joints, 68/106 facial key points) on an image. The common approach is to predict the heatmap of each key point on the feature map, and then infer the coordinates through the peak position; in the scenario of multiple people, "assembly of joints to people" is also required.
  * Single-frame/short-term action recognition: Based on a single image or a short time window, through human body pose (keypoints) and appearance features, determine the action category (such as walking, running, raising a hand, waving, sitting, etc.) that occurs in the frame/segment.
  * Temporal action recognition: On a longer time scale, analyze feature sequences (such as image features, key point sequences, or optical flow), model the start, duration, and end of actions, and recognize complex behaviors such as "talking on the phone", "doing push-ups", and "two people shoving each other".
  * Structured representation: The key point sequence provides a more compact and stable structured representation than raw pixels, facilitating the handling of viewpoint changes, background interference, and appearance differences in action recognition.
* **Model**
  Common models generally develop along the unified paradigm of "convolution/Transformer feature extraction + keypoint/temporal head":
  * Key point detection: OpenPose series, Hourglass Network, HRNet, based on two major branches: top-down (first detect people and then estimate poses) and bottom-up (first detect joints and then assemble); in recent years, there have also been pose estimators based on Transformer.
  * Video action recognition: Video models based on 2D/3D CNN (such as I3D, SlowFast, etc.), skeleton-based GCN models (such as ST-GCN, etc., which directly model spatio-temporal relationships on the key point graph), and end-to-end solutions based on video Transformer (such as Video Swin, TimeSformer, etc.).
  * Unifying multi-task and large models: Simultaneously output detection, segmentation, keypoint, and action labels on a general-purpose vision backbone, or use MultiModal Machine Learning large models to directly understand "what action this person is performing" through text prompts, connecting structured prediction with semantic understanding.

Next, we will proceed separately from**keypoint detection and pose estimation**and**action recognition and behavior understanding**in two directions.

### 2.5.1 Key Point Detection and Pose Estimation: "Drawing Skeletons" for People and Objects

Key point detection (also commonly referred to as pose estimation) focuses on  **the spatial structure in a single frame or single image ** : finding a set of semantically meaningful key points in a two-dimensional image and connecting them into a skeleton. For example, in human pose estimation, we usually need to detect joints such as the head, shoulders, elbows, wrists, hips, knees, and ankles; in facial pose, it's the corners of the eyes, mouth, nose tip, face contour, etc.; in hand pose, it's the finger roots, finger joints, and fingertips. For non-human objects such as robotic arms and joint structural components, a set of key point systems can also be similarly defined.

In model design, the commonly used paradigm for key point detection is the **"feature extraction + heatmap prediction"** paradigm:

* First, use CNN or visual Transformer (such as ResNet, HRNet, Swin, etc.) to extract multi-scale features from the input image.
* Then, through a decoder head or multi-layer convolution, a heatmap is output for each keypoint type, where each pixel value represents "the probability that this location is the keypoint".
* During the inference phase, the peak position of each heatmap is usually taken as the key point coordinate, and sub-pixel level optimization is performed through methods such as bilinear interpolation and local fitting.

For multi-person scenarios, pose estimation methods can be roughly divided into two categories:

* **Top-down** : First, use a pedestrian detector to find the bounding box of each person in the image, and then perform single-person pose estimation on the image within each box separately. This approach has high accuracy for single-person cases and a simple framework, but it has high computational cost and is sensitive to detection quality in crowded multi-person scenarios. Representative systems include many combinations based on Faster R-CNN/YOLO + Hourglass/HRNet.
* **Bottom-up** : Instead of first distinguishing each individual, it directly predicts all potential key points (and their types) on the entire image, while also predicting the connection relationships or affinity fields between key points (such as PAF in OpenPose). Then, through graph matching/clustering algorithms, the key points are assembled into multiple independent human skeletons. This type of method is more efficient in crowded multi-person scenarios and more robust to the number of people, but the assembly process is complex and sensitive to the quality of connections.

In recent years, Transformer-based pose estimation models have gradually emerged, treating key point detection as a set of "query-response" tasks. Similar to DETR, they can unify object detection and pose estimation in architecture. In engineering applications, key point detection capabilities are usually encapsulated as "human/gesture/facial key point SDK or API". Upstream applications only need to input images or video frames to obtain structured skeleton coordinates for subsequent action recognition, interactive control, or animation driving.

### 2.5.2 Action Recognition and Behavior Understanding: Making the "Skeleton" Move

After obtaining key points or high-level visual features, the next step is to understand ** changes in the temporal dimension ** — that is, action recognition and behavior understanding. Different from key point detection, action recognition is no longer limited to a single frame; it focuses on the evolution patterns of features over a period of time: from "raising a hand" to "waving", from "walking" to "running", and from "standing" to "falling".

In terms of input representation, there are roughly three routes:

* **Based**** on**** the original** **video frames**  **/optical flow** : Directly model the video frame sequence, or additionally introduce optical flow (a field describing local motion velocity) as input, enabling the model to jointly learn from appearance + motion information.
* **Based on skeleton/keypoint sequences** : First, obtain the coordinate sequence of human body keypoints through pose estimation, then model on the "spatiotemporal skeleton graph" to weaken the interference of background and illumination, and focus more on human body structure and motion patterns.
* **MultiModal Machine Learning** : Incorporate multiple modalities such as video features, key point sequences, and even audio and text together to handle complex behavior scenarios (e.g., multi-person interaction, event-level actions).

Correspondingly, the model structure also shows diversified development:

* Early action recognition mainly relied on **2D CNN + temporal n pooling **or  **3D CNN ** (such as I3D, C3D): the former extracts features from each frame and then performs pooling or RNN on the temporal dimension; the latter directly performs three-dimensional convolution in space and time to capture short-term motion patterns.
* For skeleton sequences, the typical method is ** Spatio-Temporal Graph Convolutional Network (ST-GCN)**: It treats human key points as nodes in a graph structure, with connections between joints as edges, and also connects edges in the time dimension. Information is propagated on the spatio-temporal graph through graph convolution to learn action patterns. This type of method is lightweight, robust to background, and suitable for deployment on devices with limited resources.
* In recent years, ** video Transformers ** (such as TimeSformer, Video Swin) have shown outstanding performance in action recognition. They divide videos into spatio-temporal patches, model long-term dependencies through self-attention mechanisms, and can better capture complex actions and multi-object interactions.

On the business side, action recognition is often combined with detection, tracking, and key point detection to form an end-to-end User Behavior Analysis system:

* In security, first detect and track people, then perform action classification on the key point sequence of each trajectory to achieve fall detection, fight/run recognition, etc.;
* In sports and fitness applications, analyze whether the movements are standard and the amplitude is appropriate through key point sequence analysis, and provide corrective suggestions;
* In human-computer interaction scenarios, perform lightweight action classification on real-time pose streams to enable interactions such as waving, heart gestures, and gesture commands;
* In industrial safety, continuous monitoring of workers' operational actions is conducted to identify dangerous postures (such as bending over into a hazardous area, crossing the safety line, etc.).

Looking towards the future, MultiModal Machine Learning is elevating "action recognition" to a higher level of "event and intent understanding": the model can not only label "walking, running, making a phone call", but also answer descriptions closer to everyday language such as "this person seems to be signaling to greet someone" and "these two people are arguing". Key point detection and action recognition, as important structured motion cues, together with appearance features and language cues, jointly support more complex spatio-temporal understanding capabilities.

## 2.6 Open Vocabulary / Open World / Open Domain Detection

（Open‑Vocabulary / Open‑World / Open‑Domain Detection）

Previous detection and segmentation capabilities have basically all assumed a premise: ** the set of categories during training and inference is fixed ** . That is to say, the model has fully seen "all categories to be recognized" during the training phase, and only needs to make choices within this set of closed labels during inference. However, the real world is far more complex than datasets: new products, new brands, new road signs, new species, and new scenarios emerge at any time, and it is impossible to prepare sufficient labeled data for each new category to retrain the detector. This has given rise to  ** open-vocabulary / open-world / open-domain detection ** : allowing the model to still perceive, locate, and recognize ** unseen new categories ** during inference, even when the visual style and shooting domain change, while maintaining robustness.

You can understand this layer as adding "the alignment and generalization capabilities for language space and open world" on top of traditional detection. The model no longer simply says "this is one of the 80 COCO classes", but can understand and retrieve targets in the space of any text description, such as "detect all 'red sneakers' in the image" and "mark all 'suspected small aircraft'", even if these fine-grained categories have never explicitly appeared in the training set. Next, we will sort out this layer from three perspectives:  **scenario** ,  **principle** , and  **model** , and expand on open-vocabulary detection, open-world detection, and open-domain generalization respectively in the subsections.

* **Scenario**
  * Universal Scene Understanding API: The user provides any natural language description (category word or short sentence), and the system returns the detection boxes or segmentation masks of the corresponding targets in images of any style, such as "all safety helmets in the image", "all suspected brand logos", "all objects with wheels".
  * Large-scale commodity / species identification: In e-commerce, there are constantly new long-tail commodities, and in nature, there are a vast number of animal and plant species. Training data can only cover a portion of known classes, but the system needs to locate and roughly identify a vast number of new classes, and support retrieval through text or images.
  * Cross-domain security / autonomous driving perception: Training data mostly comes from daytime urban roads / a few camera perspectives, but actual deployment faces "new domains" such as different cities, rural areas, highways, extreme weather, infrared / fisheye cameras, etc., among which there will also be new types of targets (new car models, new traffic facilities, new types of obstacles) that have never been labeled in the training set.
* **Principle**
  The core of this type of method is to replace the traditional "fixed one-hot category head" with  **the embedding space of vision-language alignment** , and handle "unseen classes" and "new domains" through various mechanisms:
  * Open-Vocabulary Detection: During the training phase, a CLIP-like alignment space is pre-trained using large-scale image-text pairs, enabling direct similarity matching between image regions and text embeddings in the same semantic space; the detection head no longer outputs fixed class logits but instead outputs a regional feature vector, which is compared with any text description vector, thus supporting the ability to "train on only some classes during training and specify any text class during inference".
  * Open-World Detection: Further process "new classes that are completely unlabeled in the training set", requiring the model to detect such targets as "unknown classes", and gradually incorporate these unknown classes into the set of known classes through interactive annotation or continuous learning in subsequent steps, forming an online learning system that can continuously expand its categories.
  * Open-Domain / Cross-Domain Detection (Open‑Domain Detection): In the face of significant changes (domain shift) in image style, imaging devices, environmental conditions, etc., through techniques such as Domain Self-Adaptation and Domain Generalization, the detector can maintain stable detection performance in unseen new domains; common methods include adversarial domain alignment, multi-domain training, style randomization, meta-learning, etc.
  * Open-vocabulary segmentation and detection integration: Extend the above idea to the pixel level, generate segmentation masks for any text description (open-vocabulary segmentation), and achieve "using natural language to describe a region/object to obtain the corresponding mask or bounding box" through Region–Word or Mask–Word alignment loss.
* **Model **
  The current mainstream technical routes for open vocabulary / open world / open domain detection basically revolve around "large-scale vision-language pre-training + detection head adaptation + domain generalization mechanism":
  * CLIP-based Detector: Based on CLIP-style image encoders and text encoders, it applies contrastive learning and Region–Word alignment loss between region-level features (ROI, feature map patches, mask regions) and text embeddings; typical implementations include replacing or extending the classification head in architectures such as Faster R-CNN / RetinaNet / YOLO / DETR to output class scores in the form of "cosine similarity + text embeddings".
  * Caption-driven / Prompt-based Detection: Utilizes large-scale image caption data to automatically generate text descriptions for regions or masks in images, then aligns and trains these automatically generated texts with detection/segmentation regions, thereby reducing the reliance on manual category labels; during inference, it drives detection/segmentation through natural language prompts (e.g., "all people wearing red clothes", "all electric vehicles").
  * Open-World Detection Series of Works: Explicitly introduce "unknown class" modeling, progressive category expansion, and incremental learning mechanisms into traditional detection frameworks. Some methods determine "whether it is an unknown class" through distance and uncertainty estimation in the metric space, while others introduce a translation memory and online retraining to enable the system to accumulate knowledge of new categories over time.
  * Domain Self-Adaptation / Domain Generalization Detection: At the Backbone and detection head levels, modules such as domain discriminators, adversarial losses, multi-domain batch normalization, and style randomization augmentation are added to enable the detector to learn more domain-invariant representations across different domains; some work also introduces multi-source domain training and meta-learning strategies into Transformer detection frameworks (such as Deformable DETR) to enhance cross-domain generalization ability.
  * General / Foundation Detection Model: Elevate the detection problem to the level of "foundation models", pre-train a Detection Foundation Model that is as general as possible in terms of categories and domains, and then adapt it to specific scenarios through lightweight fine-tuning or text prompts; such models typically combine large-scale detection annotations, multi-source image-text pairs, and even video data, aiming to make general understanding of "arbitrary text + arbitrary style image" possible.

In terms of specific product forms, open-vocabulary/open-world/open-domain detection often manifests as a "more natural, less restrictive" visual interface: users do not need to pre-agree on a small set of fixed labels, but can describe the target they want to find in natural language; the system also does not need to retrain detectors from scratch for each business scenario, but can quickly adapt based on a unified general model through prompts or a small number of samples. For large-scale commodity/species recognition, globally deployed security and autonomous driving perception systems, this layer of capability is becoming a key springboard from "closed dataset performance" to "real open-world usability".

### 2.6.1 Open-Vocabulary Detection: From Fixed Category Heads to Text-Driven Category Space

 **The starting point of Open-Vocabulary Detection is to break through the limitations of the "fixed category head" in traditional detection. Previous detectors were connected to a fixed-size classification layer (corresponding to N categories in the training set) at the top layer, and after training, they could only choose from these N categories; while Open-Vocabulary Detection, by introducing text ** ,  ** encoders ** ,  ** and a shared semantic embedding space, enables the region features output by the detection head to be compared for similarity with any text description ** , thereby accepting unseen new categories during inference.

A typical approach is to use a vision-language pre-trained model similar to CLIP:

* Text end: Encode the category name or natural language description (such as "person", "red sports car", "yellow construction helmet") to obtain the text vector.
* Vision End: In detection frameworks (Faster R-CNN, RetinaNet, YOLO, DETR, etc.), extract regional feature vectors for each candidate region or feature point.
* Alignment Training: Through contrastive loss and Region–Word alignment loss, text and region features of the same semantics are brought closer in the embedding space, while vectors of different semantics are kept apart. During training, even if explicit box annotations are provided for only a subset of categories, semantic coverage can be extended using image-text pairs or image captions.

During the inference phase, the system no longer relies on a fixed set of class names used during training, but instead allows users to provide arbitrary category terms or natural language descriptions online. These are converted into embeddings via a text encoder and then matched for similarity with regional features. This enables the detector to support flexible requirements such as "detect all skateboards", "detect all green plants", and "detect all safety-related equipment" without retraining, even if some specific categories have never been fully annotated in the training set. As long as their semantics overlap with the pre-trained text-image space, they can be identified and located to a certain extent.

In engineering practice, open-vocabulary detection needs to strike a balance between effectiveness and efficiency: on the one hand, maintaining semantic alignment with large-scale pre-trained vision-language backbones; on the other hand, meeting the requirements of multi-scale and real-time performance for detection tasks. Mainstream CLIP-based detectors often adopt the approach of "precomputing text embeddings + efficient vector similarity computation" to avoid repeatedly encoding text in online services, while also quantizing or distilling regional features to balance accuracy and inference speed.

### 2.6.2 Open World Detection: From "Unseen Classes" to "Learnable Unknowns"

**Open‑World Detection, based on open vocabulary, further requires the model to explicitly handle "unknown classes". ** During training, only some classes are labeled in the training data, while the remaining objects are either unlabeled or collectively referred to as background. During inference, these "unlabeled real objects" should neither be simply treated as background nor misclassified into known classes, but should be detected as "unknown classes" and have the potential to be subsequently converted into "new known classes".

In modeling, open-world detection usually needs to address three issues:

1. **Unknown Class Awareness** : How to prevent all unlabeled targets from being learned as "background" during the training phase? Common practices include: introducing an explicit "unknown class" slot, enabling the model to output "unknown" in low-confidence regions through negative example mining and uncertainty modeling; or leveraging unlabeled data and self-supervised mechanisms to perform clustering and pseudo-label generation on high-confidence potential target regions.
2. **Misclassification Control ** : The model needs to strike a balance between "preferring to classify as unknown rather than misclassifying into a wrong known class", which involves loss design (such as margin, open-set discrimination), decision thresholds, and post-processing strategies.
3. **Progressive Category Expansion ** : When the business party manually labels a new category for a batch of "unknown" targets, the model should be able to incorporate these new categories into the "known class" set through incremental learning without significantly forgetting the old classes. To this end, many works have introduced translation memory, distillation loss, parameter isolation, or replay mechanisms to achieve stable absorption of new categories.

From a product perspective, open-world detection is particularly suitable for those **scenarios with continuously growing categories and extremely long tails** , such as natural species recognition, commodity recognition for rapid new product launches, and abnormal target detection in complex security scenarios. The system can first use open-world detection to mark "any suspicious non-background targets" and gradually upgrade valuable clustering into formal categories through manual or semi-automatic annotation, thus forming a detection system with "sustainable category growth" rather than being constrained by fixed datasets.

### 2.6.3 Open Domain / Open Distribution Detection: Robustness across Styles, Devices, and Scenarios

Even if the category set remains unchanged, the detector will still encounter severe ** domain shift ** in real-world deployment: the training data may come from daytime high-definition cameras in a few cities, while the deployment environment includes different countries, rural areas, highways, tunnels, nighttime, rain and snow, low-resolution cameras, fisheye lenses, and even infrared imaging; there are also significant differences between e-commerce product photography and user real shots, as well as between advertising images/illustrations/anime styles. **Open-Domain Detection** focuses precisely on maintaining the stability and reliability of detection performance under conditions where the image distribution changes significantly.

Typical technical paths include:

* **Domain Adaptation** : On the premise of having unlabeled data or a small amount of labeled data in the target domain, the model learns domain-insensitive features through methods such as adversarial domain alignment (confusing the source/target domains in the feature space), multi-level domain alignment (image style, features, detection head output), and style transfer (e.g., transferring the image style of the source domain to the target domain).
* **Domain Generalization** : On the premise of only having multiple source domain data and no target domain data, by means of multi-domain training, style randomization, feature perturbation, meta-learning, etc., the model is exposed to diverse distributions as much as possible during the training phase to improve its generalization ability to unknown new domains.
* **Universal / Foundation Detection Model** : By pre-training the detection backbone and head structure on large-scale, multi-source, multi-style data (including natural images, video frames, synthetic data, cross-modal data, etc.), and then performing lightweight fine-tuning on specific business scenarios, it achieves stronger open-domain robustness than "single-domain training".

These open-domain mechanisms often interact with open-vocabulary/open-world capabilities: a general-purpose detection system for the real world must be able to understand users' natural language category descriptions (open vocabulary), make reasonable "unknown" judgments and gradually absorb newly emerging targets (open world), and maintain performance across different countries, devices, weather conditions, and styles (open domain). In engineering implementation, these three aspects are not isolated research directions but together form a key combination of capabilities for moving from "closed benchmarks" to "open-world usability".

## 2.7 Vision–Language Tasks

The previous chapters mainly focused on "single-modal vision": the input is an image, and the output is a detection box, segmentation mask, category label, or quality score. In many real-world applications, visual information does not exist in isolation - an image is often accompanied by a title, descriptive text, dialogue, or search query; users want to know "what is the image about" and "whether the image matches the text". ** Visual - Language Tasks ** precisely address such issues: they take image + text as input or output, and through  ** cross-modal alignment and joint modeling ** , enable the system to "describe an image", "answer questions based on an image", "find images with text / find text with images".

From a product perspective, Visual-Language Models (VLM) are the central capabilities of MultiModal Machine Learning systems: search engines rely on them to implement "text-to-image / image-to-text search"; content platforms use them for intelligent image matching, advertising review, and text-image consistency checking; multimodal assistants use them as a basic capability to implement functions such as "chatting with images" and "asking questions about documents / screenshots". Next, we will sort out this layer from three perspectives:  ** scenarios ** ,  ** principles ** , and  ** models ** , and expand on image description, visual question answering, and text-image retrieval in the subsequent subsections.

* **Scenario**
  * Image Captioning: Automatically generates one or two natural language descriptions for images, used for accessible assisted reading, intelligent photo album descriptions, and enriching search indexes.
  * Visual Question Answering (VQA): Users pose natural language questions about images ("What is this person holding?", "What is the license plate number?"), and the system provides accurate answers, which can be used in education, decision support, and MultiModal Machine Learning assistants.
  * Cross-modal Retrieval: Text-to-Image retrieval (searching for relevant images using text) and Image-to-Text retrieval (searching for relevant text using images), supporting "text-to-image / image-to-text" search, creative image selection, and advertising placement review.
  * Image-Text Consistency and Review: Determine whether the image matches the title/advertising slogan, and check for risks such as "image-text mismatch" and "inductive description", which are used for content moderation and brand safety.
* **Principle**
  The core issue is: how to map images and text into  **the same semantic space** , and perform alignment and reasoning within this space:
  * Cross-modal alignment: Through jointly trained image and text encoders, corresponding "image-text pairs" are brought closer to each other in the representation space, while unrelated pairs are kept far apart (a typical example is CLIP); this provides a foundation for retrieval and matching.
  * Joint Understanding and Generation: Based on the aligned representation, cross-modal attention is introduced to enable the language model to generate text (image description), reason, and answer questions (VQA) while "looking at image features".
  * Prompting and Instructionalization: Use natural language instructions to uniformly describe multiple vision-language tasks ("Write a caption for this image", "Answer questions about this image", "Determine whether this text describes the image"), enabling a single model to complete multiple tasks through different prompts.
* **Model**
  Mainstream vision-language models have roughly evolved into two categories:** Contrastive Learning VLM ** and ** Generative MultiModal Machine Learning **  ** Large Model ** :
  * Contrastive learning models: CLIP, ALIGN, etc., encode images and text into vectors respectively, and through large-scale image-text pairing training, they perform excellently in retrieval and matching tasks, serving as the foundation for "text-to-image / image-to-text" search.
  * Vision-Language Generation Models: BLIP / BLIP-2, Flamingo, Kosmos, LLaVA, etc., connect visual encoders with large language models (LLMs), and support complex tasks such as image captioning, VQA, and multi-round dialogue through cross-modal attention and instruction fine-tuning.
  * General MultiModal Machine Learning large models: such as GPT-4.1 with Vision, Gemini 1.5, etc., further unify vision with more modalities (speech, code, etc.) in a single large model, and complete retrieval, Q&A, reasoning, and generation through a unified interface.

Overall, vision-language tasks mark that "vision is no longer a separate perceptual channel", but rather participates together with language in higher-level knowledge representation and reasoning. Next, we will elaborate from two directions:  **image captioning and visual question answering** , **image-text retrieval and cross-modal alignment** (here combined into two subsections according to content).

### 2.7.1 Image Description and Visual Question Answering: From "Describing Images" to "Reasoning from Images"

The goal of **Image Captioning** is to take an image as input and output a natural language description, such as "A little girl is flying a kite on the grass." Traditional approaches typically adopt the "CNN + RNN" architecture: using a convolutional network to extract features from the entire image, and then using LSTM/GRU to generate the description word by word; with the emergence of Transformer and pre-trained VLM, the mainstream paradigm has gradually shifted to the "image encoder + text decoder" architecture, such as BLIP / BLIP-2, ViT + GPT, etc. In terms of training, models are usually trained autoregressively on a large number of image-text pairs, and sometimes reinforcement learning or contrastive loss is also used to optimize the diversity and correctness of the descriptions. At the product level, image captioning is widely used in accessible reading (generating image descriptions for screen readers for the blind), automatically adding captions to smart photo albums, and providing more text indices for search systems.

 **Visual Question Answering (VQA) further introduces human interaction: the input to the model is no longer "image + blank prompt", but "image + question", with the output being a short answer or natural language explanation. Compared to image captioning, VQA places greater emphasis on controllability and reasoning ability ** : questions can focus on local details ("What color is the man's hat?"), relationships ("Which car is closer to the intersection?"), counting ("How many dogs are there?"), or even require external knowledge ("What cuisine does this dish belong to?"). Early VQA models typically used an image encoder + question encoder + fusion module (such as bilinear pooling, attention) + classification head, outputting an answer from a limited vocabulary; modern MultiModal Machine Learning large models directly use an image encoder + LLM, generating natural language based on "looking at the image", with obvious advantages in open-ended answers and multi-round conversations.

Both can be regarded as different "prompt templates" within the unified VLM framework:

* Captioning：`<图像> + "Describe this image in one sentence."` → 文本；
* VQA: `<Image> + "Q:... A:" ` → Text.

Through Instruction Tuning, the same MultiModal Machine Learning large model can be compatible with various tasks such as description, question answering, explanation, and tagging, which is also the basic engineering concept of modern VLM products (MultiModal assistants, image question answering robots, etc.).

### 2.7.2 Image-Text Retrieval and Cross-Modal Alignment: Text-to-Image Search & Image-to-Text Search

**Cross-modal Retrieval** addresses another high-frequency need: given a piece of text, find matching images (Text-to-Image Retrieval); or given an image, find relevant text descriptions, product information, news reports, etc. (Image-to-Text Retrieval). These capabilities form the core of products such as "text-to-image / image-to-text search", "find products by image", and "match images to news".

The core technology is  ** cross-modal alignment ** : models represented by CLIP use separate encoders (such as ViT and Transformer text encoder) for images and text respectively, and are trained using contrastive learning on large-scale image-text paired data:

* For the same pair (image, text), make their vectors close to each other in the embedding space;
* For mismatched image-text pairs, push their vectors apart.

After training is completed, simply encode all images and text into vectors, and then fast matching can be performed in the shared space through vector retrieval (nearest neighbor search):

* Text-to-Image: Text → Text Vector → Nearest Image Vector;
* Image-to-Text: Image → Image Vector → Nearest Text Vector.

In engineering practice, this type of model typically adopts a two-stage structure:

* In the first stage, a lightweight and fast bi-encoder (Bi-Encoder, such as CLIP) is used for coarse retrieval, quickly screening out a small number of candidates from a billion-level image library;
* In the second stage, a stronger cross-encoder or a MultiModal Machine Learning large model can be optionally used to perform fine ranking and re-ranking on candidates to improve relevance and robustness.

On the product side, image-text retrieval and cross-modal alignment are widely used in: image search, ad retrieval (finding suitable images based on ad copy), compliance review (checking whether ad images and text are consistent), content recommendation (recommending relevant images/videos to users based on their text reading history), etc. With the rise of MultiModal Machine Learning large models, this type of retrieval capability has also gradually been integrated into a larger multi-modal framework, providing a unified interface externally in the form of "natural language instructions + multi-modal memory/vector library".

## 2.8 Optical Character Recognition (OCR)

In many businesses, the most important information is neither reflected in the "objects and scenes in the picture" nor in the natural language description of the image, but directly written on the image  **Text ** : contract terms, invoice amount, road sign name, meter reading, error messages on screenshots, etc. Optical Character Recognition (OCR) is a structured understanding task around "image + document layout": automatically detect and recognize text content from complex visual input, understand the layout and structure of documents, and then support search, statistics, automatic input, and intelligent Q & A.

From a product perspective, Optical Character Recognition (OCR) is the key bridge that "transforms paper/image information into computable text" and serves as the infrastructure for electronic, automated, and intelligent work: contract review, invoice entry, digitalization of government and enterprise archives, PDF to Word conversion in office software, document Q&A assistants, etc., are all built on OCR capabilities. The following will sort out the OCR system from three perspectives:  **scenarios** ,  **principles** , and  **models** , and expand on the core directions in the subsequent sections.

* **Scenario**
  * Scene text recognition: store signs, road signs, billboards, packaging copy, etc. in street scenes, used for navigation, search, retail insights, and compliance audits.
  * Document OCR: Text recognition and structuring of scanned documents, faxes, PDFs, photo versions of contracts/invoices/reports, etc., and restoration into editable text.
  * Specialized scenarios: license plate recognition, dashboard reading (electric meter, water meter, gas meter), text extraction from screenshots, test paper/form recognition, etc.
  * Document Understanding: Extract structures such as headings, paragraphs, tables, and annotations from long documents with complex layouts, laying the foundation for search, summarization, and question answering.
* **Principle**
  The OCR system is typically divided into several key steps:
  * Text Detection: Detect all text regions (text lines or text blocks) in an image, output localization boxes (horizontal or four-point polygons), which serve as the input for subsequent recognition.
  * Text Recognition: Perform sequence recognition on each detected text region, converting pixel sequences into character sequences (such as Chinese, English, numbers, symbols, etc.).
  * Layout Analysis: In document scenarios, identify the roles of each region (title, body text, image, table, header, footer, etc.), and restore the reading order and hierarchical structure.
  * Table Structure Recognition: Perform row and column partitioning, cell boundary parsing, merged cell restoration on the table area, and reconstruct the logical table structure.
  * Document Question Answering (DocVQA): Based on OCR and layout understanding, enable the model to answer questions that require cross-region and multi-step reasoning, such as "What is the payment date of this contract?" and "What is the amount of the invoice?"
* **Model **
  Commonly seen in engineering is the combination of "dedicated OCR module + document understanding model + MultiModal Machine Learning large model":
  * Text Detection and Recognition:
    * Detection: Methods based on segmentation or edge learning, such as EAST, DBNet/DBNet++, etc., are good at handling curved text and complex backgrounds;
    * Recognition: Sequence models such as CRNN, RARE, and SAR (CNN + RNN/Attention + CTC or autoregressive decoding), supporting multilingual and multi-font capabilities.
  * Understanding of Document Layout and Structure:
    * LayoutLM / LayoutLMv2/v3, DocFormer, etc., jointly encode text content (tokens), position information (bounding boxes), and visual features;
    * Models such as Donut, which are "end-to-end document understanding" models, directly go from images to structured outputs (such as JSON / Markdown), weakening the boundaries of traditional OCR.
  * Document Q&A and MultiModal Machine Learning Understanding:
    * On the basis of the layout model, a task head is stacked for DocVQA;
    * Or directly use MultiModal Machine Learning (VLM) to read document images, complete question answering and summarization at the natural language level, while implicitly leveraging OCR capabilities.

Overall, OCR has evolved from the early "simple character recognition" to a comprehensive document understanding system that encompasses ** text + layout + structure + question answering ** , and is a key pillar for enterprise digitization, government archive management, and intelligent work. Next, we will delve into it from  ** text detection and recognition ** ,  ** document layout and table structure analysis ** , ** document question answering and MultiModal Machine Learning DocVQA ** in three directions.

### 2.8.1 Text Detection and Recognition: From Pixels to Usable Text

The first step of OCR is  ** text detection ** : finding all regions containing text in the input image. Street view/scene text faces challenges such as diverse fonts, skewed distortion, complex lighting, and severe background interference; document scenes emphasize robust support for dense text and multi-column layout. Methods such as EAST and DBNet transform the detection problem into "pixel-level segmentation + edge learning", predict text probabilities and geometric parameters on the feature map, and then obtain precise text boxes (which can be horizontal boxes or arbitrary quadrilaterals/polygons) through post-processing, taking into account both accuracy and speed.

**Text recognition**cuts out each detected text region and converts it into a character sequence. The classic approach, represented by CRNN, first extracts features using CNN, then performs sequence modeling through RNN or Transformer, and finally uses CTC or attention decoding to output the character sequence. For variable-length text, curved text, and complex languages (such as Chinese-English mixed ranking and multilingual), recognition models need to simultaneously focus on visual feature modeling and character language modeling. Methods such as RARE and SAR introduce spatial transformer networks (STN) or attention alignment mechanisms to correct geometric distortion and improve adaptability to complex layouts.

In engineering systems, detection and recognition typically serve as two decoupled services to form an OCR pipeline: front-end detection splits the image into several text lines/blocks, while back-end recognition performs character recognition on each block and can overlay a language model for error correction (such as spelling repair, number/amount verification). For specific scenarios such as license plates and meter readings, specially fine-tuned detection/recognition models are also used to leverage scene priors (fixed fonts, limited character sets) in exchange for higher accuracy and lower latency.

### 2.8.2 Document Layout and Table Structure Analysis: Restoring the "Shape of the Document"

Simply recognizing text is not enough, especially in scenarios such as long documents, reports, contracts, and invoices. ** Layout structure ** often determines the meaning and importance of information: the hierarchical relationship between headings and body text, the position of charts and captions, the role of headers and footers, the logical order of text paragraphs inside and outside tables, etc. The goal of `<b>` Document Layout Analysis (DLA) `</b>` is to identify the roles and boundaries of different regions on a two-dimensional page and restore a reasonable reading order and hierarchical structure.

Models such as LayoutLM / LayoutLMv2/v3 and DocFormer jointly encode the content (text embedding), spatial position (bounding box coordinates), and local visual features (from CNN/ViT) of each text token, and model the semantic-spatial relationships between tokens through Transformer. By training on datasets with layout annotations, the models can learn to distinguish various region types such as "title/paragraph/list/table/caption/header/footer" and provide corresponding labels and hierarchies in the output. Such models typically serve as an "intermediate layer" to provide structured document skeletons for contract review systems, report parsing, and archival digitization platforms.

**Table Structure Recognition** is a particularly crucial branch in layout analysis: it not only needs to detect the table area but also further analyze row and column boundaries, cell coordinates, and merged cells, ultimately reconstructing a logical table (usually represented as HTML, Markdown table, or structured JSON with coordinates). Implementation methods include:

* Rule/vision-based: Use methods such as line detection, segmentation networks, and object detection to extract table lines and cell regions, and then perform topological mapping;
* Based on Transformer: Encode text blocks and geometric information in the table area into sequences, and directly predict cell structure and association relationships.

In terms of products, these capabilities support high-value scenarios such as "PDF to Word/Excel conversion", "structured entry of bills/invoices", and "report analysis and indicator extraction", and are key components of government and enterprise work automation.

### 2.8.3 Document Question Answering and DocVQA: From "Reading Documents" to "Asking Documents"

When OCR and layout analysis capabilities are strong enough, the next natural requirement is:  ** Instead of having people manually flip through documents, they can directly "ask the document" ** . This is  ** Document Question Answering (DocVQA) ** : The model answers questions on complex documents such as contracts, reports, invoices, and instructions, for example, "When is the effective date of this contract?" "What is the net profit for Q4 2023 in this page of the report?" "Who is the purchaser's name on the invoice?"

Traditional DocVQA systems are typically constructed in the form of "OCR + layout model + QA head":

* First, use OCR to extract text and coordinates;
* Model the tri-modal relationship of text-layout-vision using LayoutLM / DocFormer, etc.;
* Finally, overlay a task head (classification / extraction / span prediction) on this representation, and locate the answer or relevant segments in the document based on the question.

With the development of MultiModal Machine Learning large models, more and more systems have begun to directly use "document image + question" as input, enabling a VLM or MultiModal LLM to directly generate answers or explanations with references. Under this architecture, OCR, layout, semantic understanding, and reasoning capabilities work together in an end-to-end manner within the model: the model can both see the original layout and visual cues and utilize language world knowledge and reasoning patterns to solve complex problems.

In terms of product form, DocVQA typically appears in the forms of "Contract Review Assistant", "Invoice/Report Q&A", and "Long Document Intelligent Q&A", helping users quickly locate key information from a large number of documents, automatically generate summaries, conduct clause comparisons, etc., significantly reducing the burden of manual review and information retrieval.

## 2.9 Image Generation & Editing

Most of the visual capabilities introduced earlier are "discriminative": input an image, output labels, boxes, masks, or text; while another main line that has developed rapidly in recent years is  **generative vision** : the model no longer just understands images, but  **creates or modifies images** , generating high-quality, multi-style visual content given text/image conditions.**Image generation and editing**are precisely the core capabilities of this direction, supporting a large number of products from AIGC drawing platforms to intelligent photo retouching/special effects tools.

From a business perspective, generative vision has evolved from a "technology demonstration" into a practical productivity tool: designers use it for inspiration sketches and detailed drafts; marketing teams use it to generate posters and advertising creatives in bulk; ordinary users use it to create avatars, illustrations, and wallpapers; video creators use it for keying, background replacement, and special effects. Next, we will organize this layer from three perspectives:  ** scenarios ** ,  ** principles ** , and  ** models ** , and expand on text-to-image generation, image-to-image, and editing capabilities in subsequent sections.

* **Scenario**
  * Text-to-Image: The user inputs a description ("Cyberpunk-style night cityscape"), and the system automatically generates multiple images that match the description, supporting image selection and iterative modification.
  * Style Transfer and Image Translation: Convert real photos into anime/sketch/oil painting/watercolor styles, or perform mapping between different domains (day ↔ night, summer ↔ winter).
  * Conditional Repainting and Expansion: Perform inpainting on a local area of the original image and outpainting to expand the image, used for repairing defects, removing/adding objects, and expanding the composition.
  * Text-driven editing: Modify images using natural language instructions ("Change the sky to sunset", "Make this car a red sports car"), without users needing to master complex image editing software.
* **Principle**
  Generative visual models primarily accomplish generation and editing by learning "image distribution" and "conditional control":
  * Distribution Modeling: GAN, Diffusion models, Flow Matching, etc., learn high-dimensional distributions from a large number of images, enabling the model to gradually "sample" realistic images from random noise.
  * Conditional Generation: Based on pure image distribution modeling, introduce conditions such as text, sketches, segmentation maps, key points, depth maps, etc., to make the generation process constrained by external signals (Text-to-Image, Image-to-Image, ControlNet, etc.).
  * Controllable Editing: In the latent space of an existing image, local features are guided and modified through text or local masks to achieve local redrawing, style changes, composition adjustment, etc.
* **Model**
  Currently, the mainstream image generation and editing models are mainly based on  **diffusion models + conditional control** :
  * The GAN series, such as StyleGAN, excels in high-resolution face and style control; however, it suffers from unstable training and difficulty in covering complex MultiModal Machine Learning distributions.
  * Diffusion models: Stable Diffusion, Imagen, DALL·E series, etc., sample through the process of "forward noise addition + reverse noise removal", combining both quality and diversity, and are the current mainstream direction of Text‑to‑Image.
  * Controllable Generation and Editing: ControlNet, T2I-Adapter, etc., overlay conditional channels (edges, poses, segmentation, etc.) on the base diffusion model to achieve precise control; combine text-guided Inpainting/Outpainting to achieve local editing and image expansion.
  * Flow Matching and Next-Generation Generative Models: By learning continuous flow fields to transform noise distributions into image distributions, exploring new balances in efficiency, controllability, and stability.

At the product level, these technologies are presented to users in the forms of Dreamina, Alibaba Qwen Image Model, FLUX, OpenAI, or Gemini nanobanana, Stable Diffusion ecosystem, Photoshop Generative Fill, Canva AI, and intelligent keying and special effects in Jianying/CapCut, gradually evolving from "toys" into formal links in the content production chain. Next, we will expand from  ** text-to-image generation ** , ** image-to-image translation ** and ** text-driven editing ** in three directions.

### 2.9.1 Text-to-Image: From a Sentence to a Painting

**The core task of Text‑to‑Image is: given a natural language description, generate an image that best matches its semantics and style. Modern Text‑to‑Image models are mainly based on diffusion architecture: **

* First, use a text encoder (such as CLIP Text Encoder or T5/LLM) to encode the input text into a conditional vector;
* Then, in the image latent space, starting from a high-noise state, through multi-step reverse denoising sampling, at each step, text conditions are used to guide the generation direction;
* Finally, a high-resolution image that meets the description is obtained, which can be further magnified or post-processed.

Methods such as Stable Diffusion, Imagen, and the DALL·E series are trained on large-scale image-text pairs, enabling the model to not only master the visual spectrum (shape, texture, composition, light and shadow) but also acquire a certain degree of language-vision alignment ability (understanding complex descriptions such as "style", "material", and "composition"). At the product level, this ability allows "people who can't draw to also create images": users only need to describe their ideas in natural language, and the system can provide multiple visual implementations, supporting iterative exploration and refinement.

Text-to-Image models typically support multi-style and multi-resolution outputs simultaneously: by incorporating style tokens, size conditions, etc. during training or inference, the same model can switch between different styles such as "realistic photo style, flat illustration style, 3D rendering style". Commonly used engineering techniques include:

* Prompt Engineering, used to refine and stabilize the output style;
* Lightweight fine-tuning techniques such as LoRA / DreamBooth can quickly adapt to specific characters, IPs, or brand styles on general models.

### 2.9.2 Image-to-Image: Translation, Style Transfer, and Local Repainting

**Image-to-Image** tasks generate another "constrained" version of an image based on a given input image: while preserving the overall structure or content of the original image, they also achieve a certain transformation or enhancement. Typical forms include:

* Image Translation / Style Transfer: Mapping between different visual domains, such as "photo → anime", "summer → winter", "day → night", "sketch → color image". Early methods were mostly based on GANs (CycleGAN, Pix2Pix, etc.), and now diffusion models can also be used to achieve this under conditional control.
* Conditional Generation: Taking sketches, segmentation maps, depth maps, edge maps, etc. as conditions, guiding the diffusion process through modules such as ControlNet and T2I-Adapter, enabling the generated images to strictly adhere to geometric/layout conditions while freely expressing themselves in terms of texture, lighting, and style.
* Inpainting / Outpainting: Define a certain area on the original image, treat it as the part to be redrawn (inpainting), or extend and generate new content outside the image (outpainting), to achieve operations such as "filling holes" and "extending images".

The key to this type of task is  ** to create new content while preserving constraints ** . Diffusion models excel in this regard: in inpainting, the model only samples the masked area while keeping the unmasked area unchanged, and through semantic understanding and contextual information, it enables the new content to blend naturally with the surrounding area in terms of style and lighting. For style transfer, the model samples textures and colors from the target style distribution while preserving the input structure, achieving "changing the shell without changing the core".

Within the product, the Image-to-Image capability supports a wide range of creative tools: style filters, Caricature, one-click sky replacement, automatic beauty retouching, old photo restoration, local photo editing, etc., which are usually presented to users through a highly visual interface.

### 2.9.3 Text-Driven Image Editing: Natural Language as the "Brush"

In traditional image editing software, users need to master a set of professional concepts such as layers, masks, selections, and filters; while ** text-guided image editing (Text-guided Editing) ** attempts to replace most professional operations with natural language:

* "Change the background to a night city skyline";
* "Let this person wear a black suit";
* "Turn this car into a blue sports car and add motion blur effect."

Technically, text-driven editing is typically built on Text-to-Image diffusion models and implemented in several ways:

* Search or sample in the latent space near the original image to ensure that the edited image maintains high similarity to the original image, with changes occurring only locally in areas affected by the text;
* Use an explicit mask (user-defined area) to limit the editing scope to a specific area (this is the "input text instruction after selecting an area" in many tools);
* Introduce "instruction control" modules (such as ControlNet, learnable control tokens) to enhance the controllability and stability of the model in response to editing requests.

Products such as Dreamina, FLUX, Alibaba Qwen Image Model, Stable Diffusion ecosystem, Canva AI, etc., all offer similar capabilities: users can complete complex editing tasks through simple text and minimal interaction. For professional users, this serves as an "intelligent assistant" to accelerate the creative process; for ordinary users, it significantly lowers the threshold of image editing.

## 2.10 Image Quality Assessment (IQA)

In tasks such as low-level visual enhancement, compression encoding, image generation and editing, we often need to answer a seemingly subjective question: ** "Does this image look good?" ** Manual inspection is clearly not scalable, while traditional metrics like PSNR often do not align with human subjective perception. ** The goal of Image Quality Assessment (IQA) ** is to establish an automated mechanism to score or rank the subjective/objective quality of images, serving as a key link between "low-level algorithm output" and "user real experience".

From a system perspective, IQA serves as the "gatekeeper" and "parameter tuning reference" in many pipelines: e-commerce/content platforms use it to filter out uploaded images that are blurry, noisy, or over-compressed; mobile phone cameras/photo albums use it to select the "best shot" from continuous shots; cloud enhancement and compression services use it for pre-and-post comparison and evaluation to guide Model Iteration. The following will sort out IQA from three dimensions:  **scenarios** ,  **principles** , and  **models** , and expand on evaluation types and metrics/learning paradigms in the subsequent sections.

* **Scenario**
  * Upload Quality Inspection and Review: Conduct quality scoring on user-uploaded images/videos, and filter out content with severe blurring, abnormal exposure, obvious noise, and severe compression artifacts.
  * Smart Photo Selection and Deduplication: In the phone's photo album and camera app, select the version with better clarity, expression, and composition from multiple similar photos, while identifying low-quality or redundant images for cleanup.
  * Enhancement/Compression Algorithm Evaluation: In A/B testing of algorithms such as image enhancement, noise reduction, super-resolution, and encoding/decoding, use IQA metrics to objectively measure "which strategy is better" to assist in parameter search and model selection.
  * Automatic Poster/Thumbnail Selection: Automatically select frames with higher visual quality and appeal from videos or multi-image collections as candidates for covers or posters.
* **Principle**
  The core of IQA is to characterize image quality from two dimensions:** the degree of distortion relative to the reference image ** and  ** the subjective perception of the human eye ** :
  * Full-reference IQA (FR-IQA): On the premise of having a high-quality reference image, the image to be evaluated is compared with the reference image pixel by pixel or in terms of features to measure the degree of distortion, which is used for algorithm development and experimental evaluation.
  * No-reference IQA (NR-IQA / Blind IQA): More common in real-world scenarios, where there is no reference image, and image quality can only be inferred from the statistical or deep features of a single image. The model needs to learn from a large number of images and subjective scores what kind of images the human eye prefers.
  * Pseudo-reference / Downsampling reference: In certain scenarios, a low-resolution version before compression, an "ideal image" predicted by a model, etc., can be used as an approximate reference, taking into account both implementability and evaluation accuracy.
* **Model**
  IQA models are roughly divided into**traditional handcrafted feature metrics**and**Deep learning-based quality prediction**two major categories:
  * Traditional Indicators:
    * FR-IQA: PSNR, SSIM, MS-SSIM, FSIM, etc., focus on structural, contrast, and phase information, and are more sensitive to simple degradations (such as noise addition and blurring).
    * Perceptual metrics: LPIPS, DISTS, etc., measure the perceptual differences between images in the deep feature space and have a higher correlation with human subjective perception.
  * No-reference / Learning-based IQA:
    * Early methods: BRISQUE, NIQE, BLIINDS series, etc., starting from natural scene statistics (NSS) and handcrafted features, train shallow models to predict quality scores.
    * Deep NR-IQA: RankIQA, DBCNN, HyperIQA, MUSIQ, etc., directly extract features from images using CNN/ViT and perform supervised training on MOS (Mean Opinion Score) data to make the output quality scores fit human eye evaluations as closely as possible.
    * Pre-trained Representations: Utilize features from large models such as CLIP and ViT as inputs or backbones for the quality prediction network, and fine-tune on limited MOS data to enhance generalization ability for complex distortion types.

Overall, IQA is not a single metric where "the higher, the better", but rather an evaluation system related to specific business objectives: in certain scenarios (such as surveillance enhancement), preserving details and recognizability is more important than visual naturalness; in content creation platforms, subjective perception and aesthetic standards dominate. Therefore, a common practice in the industry is to build a "task-aware" quality evaluator on the basis of a general IQA model by fine-tuning with a small amount of business data or learning weights.

### 2.10.1 Evaluation Types: Referenced, Non-referenced, and Pseudo-referenced

According to the existence of high-quality reference images, IQA can be divided into three categories: ** full reference (FR-IQA)** ,  ** no reference (NR-IQA), and pseudo-reference** .

In  ** full-reference IQA ** , we assume that there is an ideal high-quality reference image, and the image to be evaluated is its degraded version after compression, transmission, or processing. The model quantifies the degree of distortion by comparing the two at the pixel or feature level. PSNR is the simplest metric (based on mean squared error), while SSIM/MS-SSIM/FSIM etc. further consider luminance, contrast, structure, or phase information, and are closer to human visual perception to some extent. These metrics are very suitable for evaluating methods such as codec, super-resolution, and denoising during the algorithm development stage, but in real-world applications, reference images are often lacking, limiting their application scenarios.

**No-reference IQA (Blind IQA) ** is a more common setting in practical systems: only the image to be evaluated itself is available, without any reference. Early no-reference methods (such as BRISQUE, NIQE, BLIINDS, etc.) were mainly based on natural scene statistics: assuming that high-quality natural images have stable forms in certain statistical distributions, and distortion would cause changes in statistical features, thus enabling the training of models to predict quality scores based on these features. In the era of deep learning, NR-IQA models typically directly utilize CNN/ViT to extract features and regress quality scores or learn ranking relationships on datasets with human subjective scores (MOS), enabling them to cover various distortion types such as noise, blur, compression artifacts, and abnormal exposure.

**Pseudo-reference / downsampled reference IQA ** lies between the two: in the absence of a truly high-quality reference, it uses some available approximate version (such as a low-resolution image before compression, a "clean image" predicted by a model) as a reference to estimate the degree of degradation. This approach is commonly used in online video quality monitoring and codec optimization tasks, and can strike a balance between cost and accuracy.

### 2.10.2 Metrics and Learning Paradigms: From PSNR to Perceptual Quality Prediction

At the specific implementation level, IQA employs multiple metrics and learning paradigms to approximate the subjective perception of the human eye.

 **Traditional Indicators** :

* PSNR is directly based on pixel-level error, being simple and efficient, but it also imposes significant penalties on changes that are insensitive to the human eye (such as slight translation and structure-preserving filtering);
* SSIM, MS-SSIM, FSIM, etc., model image similarity from multiple dimensions such as luminance, contrast, structure, and phase, are more sensitive to structural distortion, and also reflect to some extent the human eye's preference for structural information.

 **Perceptual Metrics** : LPIPS, DISTS, etc., calculate vector differences within the internal feature layers of pre-trained deep networks (VGG, AlexNet, ViT, etc.) and weight them according to the importance of different layers to obtain a "distance in feature space", which has a higher correlation with subjective perceptual similarity. They are particularly suitable as training objectives or evaluation metrics for generative tasks (super resolution, generation, editing) to measure "how similar it looks".

 **In terms of learning-based quality prediction ** , deep NR-IQA models (such as RankIQA, DBCNN, HyperIQA, MUSIQ, etc.) directly score or rank images:

* In the training data, each image is accompanied by a set of subjective scores (MOS), based on which the model trains a quality regression or ranking network under supervision;
* In terms of model structure, CNN/ViT + global pooling + MLP is often used to output a quality score, or to output a set of quality distributions and then take the expectation;
* Some methods also utilize contrastive learning or pairwise ranking to enable the model to focus more on "relative good/bad" relationships rather than absolute scores.

With the popularity of large-scale pre-trained vision models, more and more IQA methods adopt the paradigm of "pre-trained backbone + lightweight head": leveraging rich visual representations such as CLIP and ViT, fine-tuning on a small amount of MOS data, and thus maintaining good generalization across distortion types and scenarios.

In the implementation of projects, the above-mentioned multiple metrics are usually used in combination: for example, the FR-IQA metric is used to evaluate algorithm improvements during the experimental phase; the deep NR-IQA model is used for online real-time quality inspection; and the perceptual metric is used for internal optimization of generation tasks. Through A/B testing, these automatic metrics are aligned with real user data (click-through rate, completion rate, complaint rate, etc.), gradually building a "perceptual quality measurement system" that is highly relevant to business objectives.

# 3. 3D / Spatial Mode (3D / Spatial / XR)

As applications evolve from "flat images/videos" to scenarios such as autonomous driving, robotics, AR/VR/XR, etc., systems are no longer content with merely looking at "2D pixels" but need to understand  ** the three-dimensional structure, scale, and pose relationships of the real world ** . These tasks are collectively referred to as 3D/space modalities: they include both precise modeling of geometry and topology, as well as semantic understanding, localization and navigation, and content generation in 3D space. One end of it is connected to various sensors such as LiDAR, RGB-D, IMU, etc., while the other end is connected to autonomous driving perception modules, robot navigation systems, ARKit/ARCore environmental models, mobile phone 3D scanning and modeling applications, and digital twin platforms, etc.

## 3.1 3D Perception & Reconstruction (3D Perception & Reconstruction)

In 2D vision, we only see the "world captured in photos"; while in scenarios such as autonomous driving, robotics, AR/VR, etc., what is more crucial is:  ** the position, shape, and structure of the real world in 3D space ** . 3D perception and reconstruction aim to start from various sensors (cameras, LiDAR, depth cameras, etc.), recover the three-dimensional geometric information of the environment, and express it in forms such as point clouds, voxels, meshes, implicit fields, etc., providing a foundation for path planning, physical simulation, digital twin, and 3D content generation.

In engineering practice, this layer covers multiple technical directions, from ** point cloud processing ** to ** multi-view geometric reconstruction ** to  ** neural radiance field / neural field rendering ** , corresponding to product forms such as autonomous driving 3D perception modules, ARKit/ARCore environment modeling, mobile phone 3D scanning/modeling applications, and digital twin city/park modeling platforms. The following expands from three perspectives:  ** scenario ** ,  ** principle ** ,  ** model ** , and further subdivides several key sub-directions.

* **Scenario**
  * Autonomous driving and assisted driving: Perceive 3D structures such as vehicles, pedestrians, curbs, lane lines, and traffic facilities from in-vehicle LiDAR point clouds and multi-camera images for path planning and safety decision-making.
  * Indoor/Outdoor Environment Scanning: Utilize mobile phones/tablets (structured light/ToF/stereo vision) or handheld scanners to collect multi-view data, and construct 3D models of rooms, buildings, and neighborhoods in real-time for AR modeling, home decoration design, and digital twin applications.
  * Digital Twin and BIM: Reconstructing actual factories, industrial parks, and cities into high-precision 3D models through multi-perspective imagery and point clouds for operation and maintenance management, simulation, and visualization.
  * Consumer-grade 3D scanning: Mobile 3D scanning apps, one-click "photo to 3D model" tools, provide raw geometry for 3D printing, virtual try-on, and game/film asset production.
* **Principle**
  * Point Cloud Processing: Treat the sparse/dense point sets obtained from LiDAR or multi-view reconstruction as 3D sampling point sets, perform filtering, registration, downsampling, and feature learning on them, and then conduct classification, semantic/instance segmentation, or 3D Object Detection.
  * Multi-View Geometry and 3D Reconstruction: Estimate camera poses and sparse 3D point clouds between multiple images through SfM (Structure-from-Motion), then generate dense point clouds through MVS (Multi-View Stereo), and subsequently perform mesh reconstruction and texture mapping.
  * Neural Radiance Fields / Neural Implicit Fields: Using methods such as NeRF, Instant-NGP, Gaussian Splatting, etc., represent 3D scenes as continuous volumetric density/color fields or sets of Gaussian particles, generate images through volume rendering or rasterization, and learn from multi-view supervision; after training, new view rendering and geometry extraction can be performed.
* **Model**
  * Point cloud networks: PointNet / PointNet++, PointCNN, DGCNN, MinkowskiNet, etc., directly learn features on points or sparse voxels for point cloud classification, segmentation, and 3D detection. In autonomous driving, 3D detection frameworks such as VoxelNet, SECOND, and CenterPoint are commonly used, which convert point clouds into voxel or BEV (bird's-eye view) features before performing detection.
  * Geometric reconstruction toolchain: Traditional SfM/MVS systems such as COLMAP, OpenMVG / OpenMVS can recover camera poses and dense point clouds from multi-view photos, and construct high-quality meshes.
  * Neural Field Reconstruction and Rendering: NeRF / Instant-NGP, Gaussian Splatting, and numerous improved models encode scenes in neural networks or Gaussian clouds, enabling high-fidelity novel view synthesis and 3D scene reconstruction, and gradually evolving into engineered products. In the industry, 3D AI services such as "Hunyuan 3D" and "Tripo" have emerged, which are targeted at developers and content production, encapsulating technologies like NeRF/Gaussian into cloud-based APIs or interactive tools.

Starting from this layer, traditional geometry and Deep learning, implicit representation and explicit mesh are closely intertwined. It is necessary to address the issue of "how to accurately restore the real world" while also taking into account real-time performance and usability, serving higher-level 3D scene understanding, 3D generation, and editing.

### 3.1.1 Point Cloud Processing and 3D Object Detection

For autonomous driving, robotics, and high-precision mapping, LiDAR point cloud is one of the most critical 3D sensing information. A point cloud is a sparse set of points composed of a set of three-dimensional coordinates (sometimes accompanied by reflection intensity, timestamp, etc.), without a regular grid structure, which poses challenges to traditional convolution. The goal of point cloud processing is to extract useful geometric and semantic information from these unstructured points, such as "here is a car", "here is a curb/ground", and "here is a building".

In ** point cloud classification and segmentation ** tasks, we often focus on: which type of structure a point (or point cluster) belongs to, such as cars, pedestrians, ground, curbs, buildings, vegetation, etc., or perform semantic/instance segmentation on the scene. From the perspective of modeling methods, they can be roughly divided into three categories:

1. Direct point cloud networks: PointNet / PointNet++, PointCNN, DGCNN, etc., directly define operations that are "insensitive to point set permutation" on point sets, construct hierarchical features through local neighborhood aggregation, and are suitable for classification and segmentation of small- to medium-scale point clouds.
2. Voxels and Sparse Convolution: Rasterize the point cloud into 3D voxels, then perform convolution using sparse 3D CNNs (such as VoxelNet, MinkowskiNet), taking into account both structural regularity and spatial sparsity, and are widely used in 3D detection for autonomous driving.
3. Projection and Multi-View: Projecting the point cloud onto BEV (Bird's Eye View), front-view depth map, or multi-view perspectives, and then using 2D CNN to extract features, is relatively easy to integrate with mature 2D detection networks.

In  ** 3D Object Detection ** , the goal is no longer simply to label points, but to predict 3D bounding boxes (position, size, orientation) and their categories, which is the core of autonomous driving environment perception. Typical methods such as VoxelNet, SECOND, PointPillars, and CenterPoint usually convert point clouds into voxel or pillar representations and perform detection regression in BEV or 3D space. Methods such as CenterPoint detect the target center and its size/orientation directly on BEV through the "center point detection" paradigm, combining both accuracy and speed. With the evolution of Deep learning and sensor hardware, 3D detection has been able to achieve real-time inference on automotive-grade chips, becoming one of the basic modules of the autonomous driving perception stack.

### 3.1.2 Multi-view Geometry and 3D Reconstruction: From Photos to Mesh

Can we still "understand" 3D without LiDAR? The answer is yes - multi-view geometry and 3D reconstruction rely on "multiple photos + camera motion". By capturing the same scene from different perspectives, we can use geometric constraints to recover camera poses and spatial structures, which is the classic SfM/MVS pipeline.

**SfM (Structure-from-Motion) ** mainly addresses two issues:

1. Estimate the camera extrinsic parameters (position and orientation) of each image from multiple paired or multi-view images;
2. Recover a set of sparse 3D feature points in a unified coordinate system.

Typical tools such as COLMAP and OpenMVG can automatically recover sparse point clouds and camera poses from uncalibrated image sets through feature extraction and matching (e.g., SIFT/ORB) and incremental or global BA (Bundle Adjustment).
Based on this,** MVS (Multi-View Stereo) ** uses photometric consistency across multiple views to generate dense point clouds: estimating the depth for each pixel/line of sight and gradually filling in the geometric details of the scene.

After obtaining the dense point cloud, the next step is  ** mesh reconstruction (Mesh Reconstruction) ** :

* Wrap the scattered point cloud into a continuous surface through Poisson Surface Reconstruction, Marching Cubes, or learning-based methods to form a mesh with topological structure.
* Subsequently, hole filling, smoothing, boundary optimization are usually performed, and texture mapping is carried out to obtain a 3D model that can be directly used for rendering and editing.

In terms of product form, this entire pipeline has been implemented through desktop software, cloud services, and SDKs. For example, a 3D scanning application on a mobile phone will call a process similar to SfM/MVS in the background, automatically outputting a mesh model that can be imported into a game engine after the user takes a "360-degree photo" or "360-degree video"; the digital twin platform, on the scale of cities/parks, runs large-scale reconstruction using aerial photography images + street view data to generate an interactive 3D scene.

### 3.1.3 Neural Radiance Fields and Volume Rendering: NeRF, Gaussian, and Next-Generation 3D Reconstruction

Traditional SfM/MVS/mesh reconstruction can obtain well-structured explicit geometry, but still has limitations in rendering quality, view continuity, and detail performance; while Neural Radiance Fields (NeRF) and its subsequent work have redefined 3D reconstruction and novel view synthesis in the form of **implicit field + volume rendering** .

In NeRF, the entire 3D scene is modeled as a continuous function:

![](https://ecn00p15ubf1.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTY0MjY3NDAyNGQzMGY3NzhjMjZiZmJhNDk3ZTZiOTNfN0hPdFdnMTNLM0xZSzJpbUpJaTQyc3RxSjdodnZNSDZfVG9rZW46T2FEWWJjQk1Yb1RRNmh4Ynp3YmNwYkdObkRlXzE3NjczNTAzNjE6MTc2NzM1Mzk2MV9WNA)

Given a point position x and an observation direction d in three-dimensional space, the network outputs the corresponding volume density σ and color c of the point. By performing volume rendering integration on this mapping function along the camera's line of sight, we can obtain the pixel color under the camera pose; conversely, given a set of multi-view photos and their camera parameters, we can solve for the model parameters θ by minimizing the error between the rendered results and the real images. After Model Training is completed, simply changing the camera pose allows us to synthesize new view images (Novel View Synthesis) that "have never been actually captured".

Traditional NeRF has slow training and rendering speeds. Subsequently, methods such as **Instant‑NGP** have significantly accelerated convergence and inference speeds through techniques like multi-resolution hash grid encoding; **Gaussian Splatting** replaces scene representation with 3D Gaussian particles and achieves high-quality, real-time novel view rendering through an efficient rasterization strategy. Meanwhile, a large amount of work has also extended NeRF/Gaussian in terms of editability, multi-modal, and composability, gradually evolving it from a research prototype to an engineering system.

At the productization level, NeRF/Gaussian technologies have been embedded in various 3D AI products:

* The "Multi-view Video → 3D Scene" tool on mobile/PC platforms often relies on neural fields or Gaussian particles at the underlying level to complete reconstruction and rendering;
* In the game/film asset pipeline, neural fields are used for rapid scene capture and lighting restoration, and then exported as Mesh + textures for use in traditional DCC tools;
* 3D AI services launched by major cloud providers and content platforms, such as Tencent's "Hunyuan 3D", Tripo, etc., typically support "multi-view photos/short videos → editable 3D models/scenes", and internally comprehensively utilize neural radiance fields, SDF/Gaussian representations, and subsequent explicit reconstruction to package high-quality 3D results into developer-friendly APIs or interactive products.

## 3.2 3D Scene Understanding & SLAM

If 3D perception and reconstruction answer the question "what does the world look like", then 3D scene understanding and localization further answer: ** "Where am I in this world? Which places in this world are passable, and which are obstacles?" ** For floor cleaning robots, AGV robots, drones, AR navigation, and indoor location systems, the ability to self-localize, self-map, and autonomously plan paths in a 3D environment is a prerequisite for survival.

This part of the work mainly revolves around ** 3D semantic understanding ** and ** SLAM (Simultaneous Localization and Mapping) **: the former performs semantic segmentation and traversable area recognition in the reconstructed 3D scene, while the latter uses sensors such as vision / IMU / LiDAR for camera / robot pose estimation and map construction. In engineering, this layer is usually embedded in robot chassis, UAV flight control, or mobile AR engines in the form of SDKs or algorithm modules.

* **Scenario**
  * Household and Service Robots: Floor cleaning robots, food delivery/inspection robots build maps, identify room types and obstacles in indoor environments, and achieve automatic planning of cleaning or patrol paths.
  * Warehousing and Logistics: AGV/AMR robots perform autonomous navigation in warehouses, identify shelves, aisles, and restricted areas, and complete handling and inventory tasks.
  * Drones and Outdoor Robots: Build 3D maps in outdoor environments, avoid obstacles such as buildings, trees, and power lines, and perform inspection, mapping, and security tasks.
  * AR Navigation and Indoor Location: Mobile phones/AR glasses obtain camera poses through SLAM and overlay navigation arrows, room information, and POIs on the semantic map to achieve immersive guided tours and navigation.
* **Principle**
  * 3D Semantic Segmentation and Scene Understanding: Perform semantic segmentation on point clouds or voxel representations to distinguish structures such as walls, floors, tables and chairs, shelves, doors and windows, while identifying traversable areas and obstacles, providing semantic layer information for navigation and behavior decision-making.
  * Pose Estimation and SLAM: Estimate the 6D pose of the camera/robot from continuous sensor data through Visual SLAM (monocular/stereo/RGB-D) or LiDAR-SLAM, handle loop closure detection and map optimization, and fuse multi-source information such as IMU, wheel speed, and GNSS when necessary to improve robustness.
  * Map Building and Navigation: Overlay geometric and semantic information on local/global maps to form 2D/3D/topological/semantic maps, and based on this, perform path planning, obstacle avoidance, and task allocation.
* **Model**
  * SLAM systems: The classic feature-based method ORB-SLAM series, the direct method DSO, and the inertial-aided VINS-Mono/VINS-Fusion, achieve accurate pose estimation and dense/semi-dense mapping through front-end feature tracking + back-end optimization. Frameworks such as LIO-SAM are commonly used in LiDAR/visual-LiDAR fusion.
  * 3D Semantic Segmentation Networks: 3D CNNs such as 3D U-Net, MinkowskiNet, and point cloud-based PointNet++ / KPConv / SparseConv series, used for semantic and instance segmentation of point clouds/voxels.
  * Multi-sensor fusion localization: Based on graph optimization or filtering (EKF/UKF) methods, it fuses multi-source information such as vision, IMU, LiDAR, and odometry in a unified state space to improve the localization stability in harsh lighting, textureless, or dynamic environments.

Overall, 3D scene understanding and localization form the foundation for robots to "become mobile": they must not only build a reliable self-localization framework in the complex three-dimensional world but also make the map "meaningful" to support high-level task planning and human-robot interaction.

### 3.2.1 3D Semantic Segmentation and Traversable Area Understanding

In a pure geometric map, all structures are just undifferentiated points/voxels; while in real applications, what we care about is: where the ground is, where the walls are, where there are tables or shelves, and where it is passable. ** 3D semantic segmentation ** is to assign semantic labels to each point or voxel, transforming "pure geometry" into "geometry + semantics".

In indoor/outdoor scenarios, typical targets include:

* Fixed structures: walls, floors, ceilings, stairs, columns, roads, curbs, etc.;
* Furniture and fixtures: tables, chairs, cabinets, shelves, doors, windows, handrails, etc.;
* Passable/Non-passable Areas: Areas where the robot can move, obstacles to be bypassed, restricted areas, etc.

In modeling, 3D semantic segmentation often employs:

* Voxel/Sparse Convolution Scheme: After voxelizing the point cloud, use sparse CNNs such as 3D U-Net and MinkowskiNet to learn voxel-level features, taking into account both local details and global structure.
* Point cloud direct approach: PointNet++, KPConv and other point cloud networks perform feature aggregation on local neighborhoods to achieve point-level semantic prediction.

In applications such as floor cleaning robots and AGV robots, the results of semantic segmentation are further abstracted into  ** semantic maps ** : for example, dividing a room into bedroom/living room/kitchen, and dividing the space inside a warehouse into shelf area/passage/no-go area. Robots not only know "where they can go", but also can customize different strategies based on room types (such as avoiding carpet areas in bedrooms and preferentially covering certain cargo areas in warehouses).

### 3.2.2 Pose Estimation, SLAM, and Multi-Sensor Fusion Localization

**The goal of SLAM (Simultaneous Localization and Mapping) ** is to estimate its own trajectory while moving and simultaneously construct an environmental map in an unknown environment. For indoor environments without high-precision external positioning (such as RTK-GNSS) support, SLAM is the preferred solution for most robots and AR engines.

In visual SLAM, methods represented by ORB‑SLAM, DSO, VINS‑Mono/VINS‑Fusion are typically divided into several key modules:

* Frontend: Extract and track key points/image patches from consecutive images, and estimate the relative pose between adjacent frames.
* Backend: Perform BA or graph optimization in sliding windows or global graphs, handling drift, loop closure detection, and relocalization.
* Mapping: Build a dense or semi-dense map based on pose and depth information, providing a foundation for subsequent navigation or rendering.

Pure vision is prone to failure when there is a lack of texture or drastic changes in lighting, so in practice, ** multi-sensor fusion positioning ** is generally adopted:

* Vision + IMU: Frameworks such as VINS-Mono/VINS-Fusion combine the high-frequency short-term accuracy of IMU with the scale and geometric constraints of vision, significantly improving the stability in short-term and sharp turn scenarios.
* LiDAR + IMU + Vision: Odometry frameworks such as LIO-SAM introduce inertial navigation and optional visual information into LiDAR-SLAM, leveraging the complementary characteristics of the three to achieve robust positioning, and are widely used in autonomous driving and high-precision mapping.

At the product level, these methods are typically encapsulated as part of robot chassis controllers, UAV flight controllers, AR engines (such as Visual‑Inertial SLAM in ARKit/ARCore), or Indoor Location SDKs, shielding upper-level applications from complex state estimation and graph optimization logic, allowing developers to directly obtain "real-time pose + map".

### 3.2.3 Semantic Mapping, Navigation, and Obstacle Avoidance

With stable pose estimation and geometric/semantic maps, the next step is to enable the robot to "move smartly". This part mainly involves  ** semantic map construction, path planning, and obstacle avoidance ** .

* **Semantic Map Construction** : Overlay semantic information (room type, POI, area label) on the geometric map to form a map representation suitable for high-level decision-making. For example:
* In the home scenario, the map is divided into areas such as bedrooms, living rooms, kitchens, bathrooms, etc.;
* In the warehousing scenario, mark the locations of shelves, loading and unloading areas, hazardous areas, etc.;
* In large shopping malls/exhibition halls, POIs such as stores, help desks, and restrooms are marked for AR navigation and guidance.
* **Path Planning and Obstacle Avoidance** : Construct a grid map or topological map on the map, and use planning algorithms such as A*, D* Lite, and RRT to find a feasible path for the robot from the starting point to the target point; at the same time, combine real-time perception (front obstacles, dynamic pedestrians/vehicles) to perform local replanning and obstacle avoidance, ensuring operational safety and efficiency.
* **Navigation Behavior and Task Scheduling** : In AGV robots and drones, task scheduling and multi-vehicle collaboration modules are also layered on top of navigation: assigning tasks, avoiding congestion, and optimizing overall paths and energy consumption.

AR navigation and indoor location systems also essentially rely on similar semantic maps and path planning, except that the "executor" has changed from a robot to a human: the system obtains the pose of the user's device through SLAM, plans a walking path on the semantic map, and then visualizes and overlays the path onto the real-world view in the form of augmented reality.

## 3.3 3D Generation & Editing (3D Generation & Editing)

If 3D perception and SLAM are about "collecting and understanding" geometry from the real world, then 3D generation and editing are from the perspective of content production:  ** how to use AI to automatically produce and transform 3D assets ** . This directly addresses the huge content demands of games, film and television, virtual humans, virtual spaces, e-commerce displays, 3D printing, and other fields.

In the past two or three years, with breakthroughs in technologies such as NeRF/Gaussian, SDF representation, and MultiModal Machine Learning diffusion models, 3D generation has entered a period of rapid development: One-click generation of 3D models or scenes from text, images, and videos has become a reality. Major cloud providers and startup teams have launched methods such as "Hunyuan 3D", Tripo, and DreamFusion/Magic3D series, which have been implemented as online tools, gradually evolving 3D production towards the direction of "accessible to all". 3D generation and editing can be roughly divided into four categories of capabilities: text-to-3D, image/video-to-3D, model optimization and editing, and binding and animation.

* **Scenario**
  * Game / Film Asset Production: Rapidly generate usable 3D models for characters, props, buildings, and scenes, significantly reducing the workload of art production.
  * E-commerce and Product Display: Automatically generate 3D display models based on product copy or photos for 3D product viewing, AR trial placement, and interactive advertising.
  * Digital Humans and Virtual Content: Rapidly generate 3D assets such as virtual humans, virtual fitting models, and virtual LIVE creator scenarios, supporting LIVE, short videos, and interactive applications.
  * 3D Printing and Personalized Modeling: Generate printable models from sketches/photos/text, enabling applications in personalized gifts, prototype design, and educational scenarios.
* **Principle**
  * Text-to-3D: Encodes text descriptions into semantic vectors, then generates 3D representations (NeRF/SDF/Gaussian/Mesh) through a multi-stage optimization or diffusion process, often leveraging powerful 2D text-to-image models as "scorers" or priors.
  * Image/Video to 3D: Using single or multiple images, multi-view videos as supervision, combined with NeRF, SDF, or implicit/explicit hybrid representations, to reconstruct 3D models with geometry and texture.
  * 3D Model Optimization and Editing: Perform retopology, model simplification, detail enhancement, LOD generation, UV unwrapping, and texture generation on existing models, as well as language/image-based deformation and stylization.
  * Binding and Animation: Automatically infer the skeletal structure for 3D characters and complete rigging, support skeletal animation and physical simulation (cloth, soft body, rigid body), and form drivable dynamic assets.
* **Model**
  * 3D Generation Basic Representations: NeRF / Instant‑NGP, SDF (Implicit Surface), Gaussian Splatting, and Mesh‑based Generation Networks, constitute the representation space of 3D data.
  * Text-to-3D methods: Typical approaches such as DreamFusion, Magic3D, and Fantasia3D complete end-to-end generation from text to 3D through "2D text-to-image model + 3D optimization" or "3D diffusion model", laying the technical foundation for subsequent products such as Hunyuan 3D and Tripo.
  * Image/Video to 3D Model: A reconstruction and optimization framework based on NeRF/SDF/Gaussian, which recovers stable 3D geometry and texture from multi-view consistency and single-view priors.
  * Binding and Animation Algorithms: Automatic bone extraction, bone weight prediction, Retargeting and motion generation based on deep learning, providing one-click tools for virtual human/character animation.

At this level, traditional 3D DCCs (such as Maya/Blender/3ds Max) are gradually integrating with AI toolchains: many 3D AI services are embedded in existing production workflows in the form of plugins or cloud interfaces, enabling modelers/artists to rapidly iterate on assets through human-machine collaboration.

### 3.3.1 Text-to-3D and Scene Sketch Model

**Wensheng 3D (Text-to-3D) **The goal is to provide a natural language description, such as "a cartoon-style yellow duck toy with a blue scarf, suitable for children's toy display", and the system automatically generates an editable 3D model (Mesh/NeRF/SDF/Gaussian, etc.). This is a typical application that combines large language models/MultiModal Machine Learning models with 3D representation.

Typical technical paths include:

1. **Optimization based on 2D text-to-image models** (e.g., DreamFusion, Magic3D):
2. Use a powerful Text-to-Image model (such as a diffusion model) as an "evaluator" to assess the degree of match between a given 3D representation and a text description based on the image rendered from a certain perspective.
3. Iteratively adjust the 3D representation (NeRF/SDF/Mesh) through gradient optimization or diffusion processes, ensuring that the images rendered from multiple perspectives all conform to the text semantics.
4. **3D Diffusion Model / Direct Generation** :
5. Use 3D data (point cloud, voxel, implicit field parameters, Gaussian particles, etc.) as the generation target of the diffusion model, and pre-train it on large-scale 3D datasets;
6. Achieve end-to-end Text-to-3D sampling through text condition control.

At the scene level,** the scene rough model **capability allows users to describe spatial layouts using natural language or rough sketches, such as "a living room with floor-to-ceiling windows, an L-shaped sofa on the left, a coffee table in the middle, and bookshelves and a TV cabinet on the right." The system automatically constructs a 3D layout sketch with reasonable geometry and semantics. Subsequently, the model and materials can be refined in DCC tools, or a usable scene prototype can be quickly generated directly through the "scene generation" capabilities in tools such as Hunyuan 3D and Tripo.

Currently, multiple platforms have launched Text-to-3D products targeting designers and developers:

* "Hunyuan 3D" and others integrate text-to-3D, multi-view generation, and reconstruction capabilities into a unified interface, supporting the rapid generation of characters, props, and scenes from text and then exporting them to game engines;
* Tripo products emphasize "MultiModal Machine Learning input + one-click 3D output", support the mixing of simple text and reference images, and guide the generation of 3D assets that meet style and structural requirements.

### 3.3.2 Image/Video Generation of 3D and Model Optimization Editing

Compared with plain text, generating 3D models from images or videos imposes stronger geometric constraints and has better visual consistency. Therefore, a large number of 3D AI products support  **Image-to-3D/Video-to-3D** :

* Single Photo → Coarse 3D: Utilize single-view priors (such as shape priors for faces, human bodies, and common object categories) to infer approximate 3D geometry and generate 3D models that can be used for preview or simple interaction.
* Multiple Photos / Short Videos → High-Quality 3D: By comprehensively using NeRF/SDF/Gaussian reconstruction, multi-view geometry, and post-processing, dozens of photos or a few seconds of video can be converted into high-fidelity 3D models, suitable for game/film assets or high-quality e-commerce displays.

Generating 3D geometry is just the first step, and a large amount of**model optimization and editing**work is still needed in the follow-up:

* Retopology and Simplified Modeling: Convert implicit fields or high-polygon meshes into topologies with regular structures and controllable face counts to facilitate rigging, animation, and real-time rendering.
* LOD Generation: Automatically generates multi-level detail models (Level of Detail), using low-poly models for distant views and high-poly models for close views, balancing image quality and performance.
* UV Unwrapping and Texture Generation: Automatically unwrap UVs for models, generate or optimize normal maps, displacement maps, roughness/metallic maps, and other PBR materials; some models also support automatically generating stylized textures from text or reference images.
* Geometry and Style Editing: Perform local modifications based on language or example images, such as "make this chair leg a bit shorter" or "change this building to Cyberpunk style", which is typically implemented through shape latent space operations or neural field editing at the underlying level.

Products such as Hunyuan 3D and Tripo often integrate the above processes: starting from photos/videos or simple text, the system internally completes reconstruction, retopology, texturing, and export, enabling non-professional users to obtain "Plug and Play" 3D models within minutes, significantly reducing the time from concept to asset.

### 3.3.3 Binding, Animation, and Dynamic 3D Assets

Static models are only half of the content; "animated" 3D assets are more crucial in games, film and television, virtual humans, and interactive applications. This involves**rigging, weight painting, animation, and physical simulation**and other processes, which have traditionally been high-threshold professional tasks but are now gradually being assisted or even semi-automatically completed by AI tools.

* **Automatic Rigging** : Given a character mesh, the system automatically infers the bone hierarchy (spine, limbs, fingers, etc.) and the positions of bones within the model, and predicts the weights of each vertex relative to individual bones. In recent years, deep learning methods have been able to learn this mapping on large-scale character datasets with bone annotations, enabling one-click rigging.
* **Animation and Motion Generation** : Overlay motion data (Mocap or AI-generated) on existing skeletons to complete animations such as walking, running, expressions, gestures, etc.; Deep learning-based motion generation and Retargeting can transfer human body movements in videos or movements of other characters to new characters.
* **Physical simulation** : Conduct physical simulations on cloth, soft bodies, rigid bodies, etc., to make the movements of hair, clothing, flags, and soft objects more natural. Some systems use neural networks to accelerate or approximate physics, making the physical effects in real-time engines more realistic.

In terms of products and ecosystems, these capabilities are often embedded in:

* Game / Film Asset Toolchain: Provides one-click rigging, automatic weight assignment, and a basic motion library for modelers, significantly reducing repetitive labor;
* Virtual Human / Digital Asset Creation Platform: Starting from a portrait photo or scan, through 3D reconstruction + automatic rigging + motion driving, it outputs virtual humans that can be driven in LIVE broadcasts, short videos, and interactive applications;
* 3D AI platforms (such as Hunyuan 3D, Tripo, and similar products): After 3D generation, further add rigging and simple animation functions to enable users to "make the generated characters move immediately" without the need for complex DCC tool operations.

With the maturity of 3D generation and editing technologies, the entire 3D content production process is evolving from "centered around professional DCC tools" to "AI-driven human-machine collaboration": AI is responsible for generation and a large amount of basic work, while humans make decisions more on style definition, quality control, and key design nodes. New-generation 3D AI products such as Hunyuan 3D and Tripo are the concentrated embodiment of this trend, providing faster and more user-friendly 3D infrastructure for upper-level applications in gaming, film and television, AR/VR, digital twin, and virtual human.

# 4. Audio / Speech

In the overall technology stack, "audio" corresponds to the perception and generation of acoustic signals: it includes both the processing of raw waveforms and spectra, as well as converting speech into text, understanding "who is speaking" and "what is being said", and further creating and synthesizing sounds and music. Similar to vision, audio can also be broken down into multiple layers: the underlying ** waveform and spectrum processing ** is responsible for "hearing clearly"; the middle layer ** speech recognition and speaker technology ** is responsible for "understanding who is saying what"; on top of this, there is the more abstract ** audio/music understanding ** and  ** speech and music generation ** . This entire set of capabilities jointly supports products such as real-time meeting subtitles, voice assistants, podcast post-production audio tuning, smart speakers, acoustic security monitoring, music recommendation and generation, etc.

## 4.1 Waveform-level Audio Processing: Starting from "Clear Listening"

At the lowest level of audio technology, what we first care about is not "what was said", "who said it", or "what style the music is", but  ** whether the sound itself is clean and clear ** . This layer mainly operates at the waveform and spectrum levels, processing noisy, distorted, and mixed raw sounds into "clean signals" more suitable for subsequent recognition, analysis, and generation through operations such as resampling, enhancement, noise reduction, and separation. It can be compared to "image enhancement + denoising + foreground/background separation" in vision, mainly performing acoustic-level cleaning rather than directly processing semantics.

From a product perspective, this layer is almost "invisible" behind all audio products: real-time noise reduction in conferencing software, post-production audio tuning for podcasts/short videos, the "voice enhancement mode" in voice recorders and mobile phones, the "beauty voice switch" in LIVE platforms, and front-end preprocessing for ASR/voiceprint models are all direct manifestations of audio processing at the waveform level. The following will still be sorted out from the three perspectives of  ** scenarios ** ,  ** principles ** , and  ** models ** , and the three key directions of preprocessing & feature extraction, enhancement & noise reduction, and sound source separation will be specifically expanded in the subsequent subsections.

* **Scenario**
  * Online Communication and Meetings: Zoom, Tencent Meeting, etc., can suppress keyboard noise, tapping sounds, street noise, and echoes in real-time in noisy offices, open workstations, and home environments, making voices clearer.
  * Content Creation and Post-production Audio Tuning: Automatically eliminate background noise, electrical hum, and room reverb in podcast, short video, and LIVE post-production, repair recording pops and frequency band deficiencies, and enhance the overall listening experience.
  * Recording and Transcription Front-End: Before entering ASR, recording pens, intelligent subtitles, and meeting transcription services enhance the robustness of back-end recognition through processing such as VAD, noise reduction, and loudness normalization.
  * Terminals and IoT: "Far-field sound pickup" and "noise reduction mode" on devices such as smart speakers, in-vehicle infotainment systems, and cameras aim to capture the main speaker or key sound source as much as possible in complex sound fields.
* **Principle**
  Waveform-level processing typically does not directly understand semantics but instead focuses on signal optimization around spectral structure and statistical characteristics:
  * Transform back and forth between the time domain and the frequency domain (e.g., STFT → spectrogram/Mel spectrogram → iSTFT) to suppress or model noise bands, reverberation characteristics, or background sounds.
  * By using VAD and energy/spectral features, distinguish "voice segments" from "silence/noise segments" to reduce the impact of invalid segments on the backend.
  * Use deep learning or classical filtering methods to estimate the mask or gain function of the "clean speech spectrum" and "noise spectrum", and weight the spectrum to achieve the purpose of enhancement and noise reduction.
  * In a multi-source mixed scenario, different speakers, vocals and accompaniment, foreground and background environmental sounds are separated into independent tracks through end-to-end separation networks or sparse representation.
* **Models**
  Models at the waveform/spectrum level can be roughly divided into two categories:**spectral domain models** and  **time domain end-to-end models** :
  * U-Net series on spectrogram/Mel spectrogram: Spectrogram-based U-Net, DCCRN, etc., perform "image-like" convolution and encoding-decoding on the time-frequency plane, and are commonly used solutions for tasks such as speech enhancement and singing voice separation.
  * Waveform end-to-end models: Wave-U-Net, Conv-TasNet, Demucs, etc., directly model on the time-domain waveform, avoiding explicit STFT/ISTFT, and often perform better in subjective listening experience and time-domain fidelity.
  * Classical signal processing methods, such as traditional frequency domain methods like spectral subtraction and Wiener filtering, still widely exist in lightweight devices or scenarios highly sensitive to latency, and are often combined with deep enhancement networks to form "hybrid solutions".

### 4.1.1 Preprocessing and Feature Extraction: "Clearing the Stage and Setting the Platform" for the Backend

Any subsequent models such as ASR, voiceprint recognition, event detection, TTS, etc., require a unified, clean, and structured audio input as much as possible, which is the responsibility of the preprocessing and feature extraction layer. It is responsible for performing the most basic yet extremely crucial "cleaning up" and "format standardization" to set the stage for upstream audio models.

During the preprocessing stage, the collected audio will first undergo  ** sampling rate conversion and channel conversion ** : for example, converting 48kHz stereo to 16kHz mono to meet the input specifications of downstream models and reduce computational costs. Subsequently, operations such as loudness normalization, DC component removal, and simple filtering will be performed to make the audio recorded under different devices and scenarios more consistent in terms of energy scale.

**Voice Activity Detection (VAD)** is another key step in preprocessing. It attempts to automatically partition "speech segments" and "silence/pure noise segments" in the audio stream, often based on frame energy, spectral entropy, zero-crossing rate, or small neural network discrimination. The benefits of VAD are: it can significantly reduce the invalid data fed into the ASR/speaker recognition model, reduce computational load, and avoid interference from silent segments during recognition (e.g., misrecognition as long strings of spaces or strange characters). In real-time communication, VAD can also drive the "voice activity indicator" and automatic mute logic.

At the feature extraction level, the most common approach is to convert the time-domain waveform into **spectrum **or  **Mel spectrum ** . Through the Short-Time Fourier Transform (STFT), audio is decomposed into time-varying frequency distributions; then, by using the Mel filter bank, Mel spectrum or Mel cepstral features (such as log Mel-spectrogram, MFCC) that better match human auditory perception can be obtained. These time-frequency features provide a "two-dimensional representation" for subsequent recognition, separation, and generation, similar to canary release or multi-channel feature maps in vision, facilitating processing by structures such as convolution and attention. With the development of end-to-end modeling, more and more models are directly learning features on waveforms (such as Wav2Vec 2.0), but in engineering practice, the combination of STFT + Mel features remains the most common and reliable front-end.

### 4.1.2 Enhancement and Noise Reduction: Correct "muffled sound" to "dry sound"

In real-world environments, sound almost always propagates in noise and reverberation: air conditioning noise, keyboard typing, road noise, crowd noise, and room echoes all reduce the intelligibility and subjective quality of speech and music to varying degrees. ** The goal of speech enhancement and noise reduction ** is to suppress these background interferences and restore the "blurred" sound to as "clean" as possible while maintaining the naturalness and integrity of speech as much as possible.

In traditional methods, this task is mainly achieved through frequency domain techniques such as spectral subtraction and Wiener filtering: first estimate the noise spectrum, and then "subtract" the noise or adjust the frequency band gain on the spectrum according to certain rules. Although it is simple to implement and has good real-time performance, it is prone to produce obvious "musical noise" and artifacts in scenarios with strong noise, non-stationary noise, and complex reverberation.

Deep learning methods, on the other hand, learn a **mapping** on the spectrum or waveform: given noisy speech, they predict a time-frequency mask or directly predict the clean waveform. Common solutions include using **spectrogram-based U-Net, DCCRN** and other encoder-decoder structures on the Mel/linear spectrum to carefully repair the spectrum of each frame; there are also models such as **Conv-TasNet, Demucs, Wave-U-Net** that directly perform end-to-end waveform enhancement on the time-domain waveform. These methods can significantly improve speech clarity and subjective listening experience in scenarios such as voice calls, online meetings, and audio recording restoration.

In content creation and post production, "audio restoration" often involves more "audio engineer-like" operations such as reducing plosives, cutting sibilance, compensating for missing frequency bands, and equalization (EQ) and dynamic processing (compressors/limiters). More and more tools combine these traditional processes with deep models to provide one-click "audio repair" and "audio beautification" capabilities, serving podcasters, video creators, and live streaming platforms.

### 4.1.3 Sound Source Separation: Split the "Mixed Audio"

If enhancement and noise reduction are about "making the main sound more prominent and the background quieter", then ** source separation ** further attempts to completely split multiple mixed sound sources into independent tracks. For example: multiple speakers speaking simultaneously in a meeting recording; vocals and accompaniment mixed together in music; the main event (such as an alarm or shouting) buried in background noise in an environmental recording. The goal of source separation is to recover the waveform or spectrum of each independent sound source from single or multiple mixed signals.

In the field of speech, ** multi-speaker separation ** is a core application: the model needs to separate multiple overlapping voices into different channels based on voiceprints, time-frequency structure, and speaker characteristics without separate microphone tracks. This type of ability not only improves the performance of multi-speaker ASR but also provides cleaner input for speaker separation and annotation (Diarization). In the music field, **vocals/accompaniment separation (singing voice separation)** can separate clear vocal tracks and pure accompaniment tracks from a mixed song for cover singing, remixing, karaoke, music analysis, etc. Similarly, ** ambient sound/foreground sound separation ** can be used in security and IoT scenarios to extract key event sounds (such as glass breaking, conflict sounds) from complex backgrounds.

At the model level, source separation typically employs stronger modeling capabilities and more complex architectures than ordinary enhancement.** End-to-end networks such as Conv-TasNet, Demucs, and Wave-U-Net ** can directly perform multi-source decomposition in the time domain; in the spectral domain, structures such as multi-branch U-Net, attention, and mask estimation are commonly used to predict dedicated masks or spectra for different sound sources respectively. With the growth of training data and computing resources, modern source separation models have been able to output high-quality separated tracks suitable for actual creation and analysis in fairly complex reverberant and noisy environments, providing a solid foundation for LIVE vocal beautification, multi-speaker meetings, music production, and audio retrieval.

## 4.2 Automatic Speech Recognition & Speaker Identification (ASR & Speaker)

After completing preprocessing, enhancement, and separation at the waveform level, we can finally start asking higher-level questions: ** "What was said in the audio?" "Who was speaking?" "When did who speak?" ** This layer focuses on various "understanding and annotation" tasks centered around speech itself: Automatic Speech Recognition (ASR), Speaker Identification and Verification, Speaker Separation and Annotation (Diarization), and Interaction-Oriented Hotword and Keyword Detection (KWS).

From a product form perspective, this layer is the core of most "voice products": voice input methods, meeting transcription, customer service recording analysis, intelligent customer service quality inspection, smart speakers and in-vehicle voice interaction, telephone robots, financial scenario voiceprint verification, etc., almost all directly rely on these technologies. They transform the "clean sound" from the previous layer into text sequences, speaker labels, or keyword events, and are one of the most important bridges from the audio to the semantic world.

* **Scenario**
  * Automatic Speech Recognition (ASR): Real-time subtitles, speech input method, meeting and classroom recording, customer service call transcription, providing users with an instant "hearing-to-text" channel.
  * Speaker Identification and Verification: "Voiceprint Unlock" and "Voiceprint Verification" in mobile phones, banks, and call centers, as well as retrieving a specific speaker from a vast amount of recordings.
  * Speaker Diarization: Automatically answers "who spoke when" in meetings, interviews, and roundtable discussions, enabling "transcription by speaker".
  * Hotword and Keyword Spotting (KWS): Detection of wake words for smart speakers/car infotainment systems (e.g., "Hey Siri", "OK Google"), as well as capturing key phrases (such as "complaint", "refund", "want upgrade", etc.) in customer service recordings and quality inspections.
* **Principle**
  Most tasks at this layer can be uniformly regarded as performing **temporal alignment and sequence annotation** on the audio sequence:
  * ASR: Given a segment of speech, it learns the mapping from acoustic features to text sequences, often using CTC, RNN-Transducer (RNN-T), or attention-based end-to-end architectures; modern models mostly adopt large-scale pre-training (such as Wav2Vec 2.0, Whisper, etc.) followed by fine-tuning.
  * Speaker Identification: Extract a fixed-dimensional **speaker embedding** (e.g., x-vector, ECAPA-TDNN) from the audio. In this embedding space, the voices of the same person are close to each other, while the voices of different people are far apart. Then, combine a metric or classification model to complete identification and verification.
  * Speaker Diarization: By comprehensively utilizing voiceprint embedding, VAD, segment clustering, or end-to-end network (EEND), it assigns speaker labels to each time segment, thereby piecing together the "multi-speaker timeline on the time axis".
  * KWS: Performs low-latency small model detection on continuous audio streams, conducts local pattern matching and confidence level evaluation on predefined wake words or keywords, and takes into account both low computing power and high recall.
* **Model**
  The model lineage of ASR and speaker technology includes both end-to-end architectures and specialized embedding models and clustering methods:
  * ASR: Wav2Vec 2.0, Conformer, Whisper, RNN-T, Citrinet, etc., mostly adopt convolution + self-attention or pure self-attention architectures, supporting multilingual, large vocabulary, and long context.
  * Speaker embedding: ECAPA-TDNN, x-vector, i-vector, etc., obtain a robust speaker feature space through classification training or metric learning on a large amount of speaker data.
  * Diarization: From the traditional process of VAD + segmentation + clustering to end-to-end methods such as End-to-End Diarization (EEND) that directly output a "time × speaker" matrix.
  * Hotword/Keyword Detection: A lightweight CNN/RNN/Transformer front-end combined with CTC or a gating mechanism, embedded locally on the device, enables always-on listening with ultra-low computing power and low latency.

### 4.2.1 Automatic Speech Recognition (ASR): Transforming "sound" into "text"

 **Automatic Speech Recognition (ASR) is the main pathway for "audio → text": whether it is a speech input method, meeting transcription, intelligent subtitles, or customer service recording analysis, the first step is to accurately convert what the user says into text. Modern ASR systems mostly adopt an end-to-end architecture ** : starting from acoustic features (such as Mel spectrograms or direct waveforms), passing through a series of deep networks (such as Conformer, Citrinet, Transformer-based Encoder), and directly outputting text sequences or corresponding token sequences.

In terms of modeling, the challenges of Automatic Speech Recognition (ASR) mainly include long-term dependencies, multilingualism and dialects, accent variations, overlapping speech, background noise, and domain-specific proper nouns. To address these issues, the current mainstream approach is to use large-scale unlabeled audio for self-supervised pre-training (e.g., Wav2Vec 2.0, HuBERT), or conduct large-scale supervised training on multilingual and multi-task data (e.g., Whisper), and then fine-tune with a relatively small amount of domain-specific data to achieve good robustness across different languages, accents, and scenarios.

At the product level, ASR is typically packaged as capabilities such as "Speech Input Method SDK", "Cloud Speech Recognition API", and "Meeting Transcription Service": the front end can be real-time streaming recognition (RNN-T, Streaming Transformer, etc.), and the back end can enhance the recognition of specific person names, place names, brand names, and business terms through hot word injection, custom vocabulary, and context constraints. These recognition results often serve as the foundation for subsequent NLP, dialogue systems, and data analysis.

### 4.2.2 Speaker Identification and Separation Annotation: Answering "Who" and "When Speaking"

Compared with "what was said",** "who said it" is equally important in many applications: scenarios such as finance, government affairs, customer service, and security need to verify identity or investigate risks through voiceprint recognition;** while meeting and interview scenarios need to know "who said each sentence" to support speaker-specific transcription, speech statistics, and behavior analysis.

In ** Speaker Identification/Verification (Speaker Recognition) ** tasks, the goal of the system is: given a speech segment, determine who the speaker is, or determine whether it belongs to the same person as a registered speaker. Modern systems typically extract a fixed-dimensional speaker embedding vector from speech segments through models such as ECAPA-TDNN and x-vector. During the training phase, a combination of speaker classification and metric learning is used to ensure that the embeddings of the same person are more clustered and the embedding distances between different people are larger; during the inference phase, nearest neighbor or back-end discriminators (such as PLDA, Cosine scoring with margin) are then used for verification and identification. In this way, the system can answer "whether it is the same person" with a certain confidence level in telephone, microphone, and noisy environments.

**Speaker Diarization** further answers "who spoke when". Traditional approaches typically involve three steps: first, use VAD to identify speech segments; second, split long audio into short segments; third, extract speaker embeddings for each segment; and finally, perform clustering and temporal stitching in the embedding space to obtain a multi-speaker timeline. More advanced **End-to-End Diarization (EEND)** methods attempt to directly output a "time × speaker" boolean matrix from audio features, learning complex patterns such as overlapping speech and speaker switching in an end-to-end manner. Diarization is highly valuable in scenarios such as meetings, interview programs, court records, and telephone customer service, often combined with ASR to form "transcripts with speaker labels".

### 4.2.3 Hot Words and Keyword Detection: The "Ears" for Interaction and Monitoring

In a continuous audio stream, not every second is worth being fully recognized and stored. The role of **Keyword Spotting (KWS)** is that of an always-on "goalkeeper":

* In smart speakers, in-vehicle infotainment systems, and mobile phone assistants, the KWS module is responsible for detecting wake words (such as "Hey Siri", "OK Google", "Xiaomi Tongxue"). Once a wake word is detected, it hands over the audio stream to the more expensive ASR and dialogue system for processing.
* In intelligent customer service, quality inspection, and compliance scenarios, KWS marks and alerts key phrases (such as "complaint", "return", "rights protection", "fraud") that appear in recordings or real-time calls, providing trigger points for backend analysis and quality inspection strategies.

In Technology Implementation, KWS usually needs to operate under the constraints of  ** extremely low computing power and low latency ** , especially for wake word detection on local devices: the model is often a small CNN/RNN/Transformer front end, followed by a CTC or gated discriminative head, to detect the acoustic patterns of specific words, and uses sliding windows and confidence level smoothing to avoid false wake-ups. For keyword quality inspection scenarios, stronger ASR + keyword matching/regular expressions + statistical analysis can be adopted, or an end-to-end keyword tagging model can be directly trained. Regardless of the form, KWS essentially adds a layer of "event-level" semantic filtering to the speech stream, and is an important interface connecting the audio world and interaction logic.

## 4.3 Audio Event & Music Understanding

Not all audio is centered around "speech". In reality, there are numerous scenarios related to environmental sounds, event sounds, and music, which are more concerned with:** "What sound event has occurred?" "What is the current acoustic environment?" "What is the style of this song, what instruments are used, and what are the rhythm and key?" ** This set of capabilities is collectively referred to as audio/music understanding, which mainly revolves around sound event detection, environment/scene classification, and music attribute understanding.

From a product perspective, audio understanding technology supports a wide range of applications such as security acoustic monitoring, IoT acoustic sensors, environmental self-adaptation of smart devices, music recommendation and classification, music copyright recognition, music retrieval, and creative assistance. Similar to "image classification + fine-grained classification" in images, this layer structures the originally continuous and complex sound space into discrete event labels, multi-dimensional attribute vectors, and style descriptions.

* **Scenario**
  * Sound Event Detection: Detects alarm sounds, glass breaking, baby crying, impact sounds, etc., for security monitoring, smart buildings, vehicle safety systems, and industrial alarms.
  * Environment/Scene Classification: Identify soundscapes such as "indoor/outdoor", "office/car/street/subway", etc., to provide a basis for noise reduction strategies, self-adaptation gain, and mode switching of smart devices.
  * Music Understanding and Music Information Retrieval (MIR): Genre Classification, Instrument Identification, Rhythm and Tonality Analysis, supporting Music Recommendation, Playlist Generation, Music Retrieval, Copyright Identification, and Creative Assistant.
* **Principle**
  Audio/music understanding is mostly based on **time-frequency features + deep neural networks **for classification or multi-label annotation:
  * Using features such as log Mel-spectrogram, convert audio into "acoustic images", and then utilize structures such as CNN, CRNN, or Transformer for time-frequency Pattern Recognition.
  * For sound event detection, multi-label and multi-temporal output are often adopted to predict the existence of each event on the time axis, and sometimes weak supervision labels and multi-instance learning are also combined.
  * When classifying environments/scenes, more emphasis is placed on long-term statistical features and background patterns, often requiring modeling over a longer window.
  * Music understanding tasks combine music theory knowledge to model rhythm (BPM), beat points, tonality, chords, and structure. Some tasks pre-train music embeddings through self-supervised or contrastive learning and then perform downstream fine-tuning.
* **Model**
  Common audio understanding models are often pre-trained on public datasets (such as AudioSet) and then transferred to specific tasks:
  * CNN/CRNN models such as VGGish, YAMNet, and PANNs, after pre-training on large-scale audio data, can be used for various audio event and soundscape tasks.
  * Transformer-based models such as AST (Audio Spectrogram Transformer) directly use self-attention on spectrograms to obtain stronger global time-frequency modeling capabilities.
  * The MusicTagging / MIR model for music will pre-train a label model or an embedding model on millions of songs, which is used for style/ emotion/ instrument tagging, music retrieval, and recommendation.

### 4.3.1 Sound Events and Environmental Soundscapes: Enabling Devices to "Understand the Environment"

In security, IoT, smart cities, and in-vehicle systems, relying solely on cameras is not sufficient to comprehensively understand the environmental state. ** The goal of sound event detection ** is to enable the system to "understand" key events: when glass breaks, alarms sound, babies cry, collisions occur, screams are heard, fights break out, or acts of vandalism take place, the system can recognize and issue alerts in the audio signal. Different from speech recognition, such events are often short-lived, non-verbal, vary in frequency range and energy pattern, and may highly overlap with background noise.

**Environment/Scene Classification ** focuses more on the continuous acoustic scene: is it a quiet office, a bustling street, inside a car, a high-speed railway station, or a coffee shop? The system can automatically adjust noise reduction intensity, echo cancellation parameters, microphone array beam direction, and even change interaction strategies (e.g., through shorter feedback interactions in a car and increasing output volume on a noisy street). In IoT scenarios, an "acoustic network" composed of multiple sound sensors can be used for long-term monitoring and statistical analysis of environmental conditions.

In Technology Implementation, both types of tasks mostly adopt ** multi-label classification + temporal modeling ** solutions: convert audio to Mel spectrograms, use models such as VGGish, PANNs, AST or similar for feature extraction, and then use temporal pooling or sequence models to output the activation of each label on the time axis. Since many datasets only provide "weak labels" (weak labels), models often need to learn the temporal localization of events under weak supervision through methods such as multi-instance learning and self-attention pooling.

### 4.3.2 Music Understanding and Labeling: From "Playlist Tags" to "Structural Analysis"

In the field of music, the goal of audio understanding is not just "what song is this", but also to answer: **"What is the style of this song? What instruments are used? What is the tempo? What is the tonality and approximate harmonic structure?" ** On the one hand, this information supports music recommendation and playlist compilation; on the other hand, it also provides structured "music metadata" for creators and generative models.

**Genre Classification**categorizes songs into different styles such as pop, rock, classical, hip-hop, electronic, Lo-Fi, etc., based on their overall acoustic characteristics and structure;**Instrument Identification**distinguishes the acoustic fingerprints of different instruments such as drums, bass, guitar, piano, strings, etc., in the time-frequency domain, which can be used for instrument statistics, music retrieval, and mixing analysis.**Rhythm/Tonality Analysis**estimates parameters such as BPM, beat position, time signature, key, etc., providing a basis for tasks such as rhythm matching, automatic harmony, DJ mixing, and game soundtrack synchronization.

In terms of models, music understanding mostly follows general audio models (such as PANNs, AST), but there are also a large number of models and pre-trained embeddings specifically designed for music information retrieval (MIR). A typical approach is to perform ** multi-label music tag learning ** (genre, mood, instrument, era, etc.) on large-scale music datasets to obtain a music embedding space, and then fine-tune or perform zero-shot inference on the above specific tasks. By combining these models, music platforms can more intelligently perform music classification and recommendation, copyright platforms can strengthen music fingerprinting and similarity retrieval, and creative tools can leverage these understanding capabilities to recommend suitable accompaniments to users, expand similar styles, or automatically generate music structures.

## 4.4 Speech and Audio Generation (TTS / VC / Music Generation)

After completing the "cleaning", "recognition", and "understanding" of audio, the next natural question at the next level is: ** "Can we directly enable machines to 'speak', 'sing', or even 'compose music'?" ** This is the world of speech and audio generation: from text-to-speech (TTS), from one voice to another (VC / Voice Cloning), to a broader scope of music and sound effect generation, and then to singing synthesis that can perform lyrics and melodies. Similar to image generation, this level no longer simply tags or extracts structures from existing data, but actively "creates" new sound content.

At the product level, this layer of capabilities has already penetrated into various applications: voice product lines such as OpenAI TTS, ElevenLabs, Volcengine, and Minimax provide high-quality synthetic voices for applications; music generation platforms such as Suno and Udio provide the ability to create complete music from text for creators and even ordinary users; games, videos, virtual LIVE creators, and digital humans rely on these models for voiceovers and singing, greatly lowering the threshold for content creation.

* **Scenario**
  * Text To Speech (TTS): News broadcasts, navigation announcements, intelligent customer service voice responses, reading content in learning apps, accessibility screen reading, etc., require converting any text into natural, clear, and controllable speech.
  * Voice Conversion / Voice Cloning (VC / Voice Cloning): Under the premise of maintaining semantics and prosody, change the speaker's timbre to achieve "voice replacement speech" or "few-shot voiceprint cloning" (under strict compliance conditions).
  * Music and Sound Effect Generation: Generate appropriate background music and sound effects (ambient sounds, UI sound effects, transition sounds) for short videos, games, advertisements, podcasts, etc.
  * Singing Synthesis and Cover Version: Given a melody and lyrics, make a virtual singer perform, or generate a cover version of a certain style/timbre under compliant conditions.
* **Principle**
  Speech and audio generation typically adopt the hierarchical modeling approach of **"high-level representation → low-level waveform"**:
  * In TTS, text is first converted into a phoneme/syllable/character-level sequence, then passed through a sequence-to-acoustic feature (such as Mel spectrogram) model (Tacotron, FastSpeech, VITS, etc.), and finally a neural vocoder (WaveNet, WaveRNN, HiFi-GAN, etc.) is used to generate high-fidelity waveforms from the features.
  * In Voice Conversion, by decoupling "what is said (content)" and "who is speaking (timbre)", the content representation is extracted from the source speech and then combined with the target speaker embedding or vocoder conditions to generate a new speech waveform.
  * Music and sound effect generation can be based on tokenized representations (such as musical notes, MIDI, encoded spectrum/codec tokens), using autoregressive, diffusion, or neural codec generative models to sample new audio from text, reference audio, or structural parameters.
  * Singing voice synthesis introduces more refined prosody, pitch contour, and singing control on the basis of TTS, and usually models pitch, duration, legato, vibrato, etc. explicitly or implicitly.
* **Model**
  The current mainstream technical routes for speech and audio generation include:
  * TTS: Tacotron / Tacotron2, FastSpeech series (non-autoregressive TTS), VITS, etc., are responsible for converting text to mel spectrograms or codec tokens; WaveNet, WaveRNN, HiFi‑GAN, WaveGlow, etc., serve as vocoders or decoders and are responsible for converting features to waveforms. Recent Diffusion‑based TTS and Neural Codec models have further improved in naturalness and diversity.
  * Voice Conversion / Cloning: VC framework based on speaker embedding + content encoder, as well as voice conversion models utilizing neural codecs, support few-shot voice cloning and cross-lingual speaker transfer. These technologies have currently been commercially implemented by multiple platforms, providing convenient voice cloning call services. Common domestic platforms include Volcengine, Minimax, iFlytek Open Platform, Baidu Smart Cloud Qianfan Big Model Platform, Alibaba Cloud Speech And Audio Interaction Platform, etc.; overseas, there are mainstream platforms such as ElevenLabs, Resemble.ai, Play.ht, etc. Among them, Volcengine's voice cloning capabilities support rapid training with a small number of audio samples, adapting to commercial calls in multiple scenarios such as intelligent customer service and audiobooks; Minimax relies on its large model technology advantages to achieve natural adaptation between cloned voice and text content, while also supporting cross-lingual speaker voice transfer; iFlytek Open Platform's voice cloning has significant advantages in the clarity of Chinese pronunciation and emotional expressiveness, widely serving fields such as education and radio and television.
  * Music and Sound Effect Generation: Models such as MusicLM, MusicGen, and Suno/Udio typically generate long-duration audio on discrete codec tokens using autoregressive or diffusion architectures, based on text and/or reference audio conditions.

### 4.4.1 Text To Speech (TTS): Enabling machines to "naturally speak"

**Text To Speech (TTS)** is the most intuitive speech generation task: input a text, output a natural and fluent speech, and in an ideal state, it can be almost indistinguishable from human voice. Modern TTS systems are usually divided into two main stages: text to acoustic features (such as Mel spectrogram), and acoustic features to waveform.

In the first stage, the model needs to handle issues such as word segmentation, phoneme conversion, disambiguation of polyphonic characters, punctuation and pauses, and prosody prediction. Typical models include the attention-based Tacotron series and the length prediction-based FastSpeech series, with the latter significantly accelerating synthesis and improving stability through a non-autoregressive architecture. In recent years, end-to-end models such as VITS have integrated acoustic modeling and vocoders into a unified framework, further simplifying the system.

In the second stage, neural vocoders such as WaveNet, WaveRNN, HiFi‑GAN, WaveGlow, etc., are responsible for converting mel spectrograms or other intermediate representations into high-fidelity waveforms. A well-trained vocoder can not only generate natural and clear speech but also effectively reproduce different timbres, emotions, and styles. Modern TTS systems also support ** multi-speaker modeling ** (through speaker embedding), timbre/speech rate/emotion control (such as "excited", "calm", "broadcasting tone"), and cross-lingual TTS, providing highly customizable voice capabilities for various applications.

### 4.4.2 Voice Conversion and Voiceprint Cloning: Changing "Who's Speaking"

In many creative and auxiliary scenarios, we hope to change the speaker's tone or style without  **changing the content and rhythm ** . This is the task of ** speech conversion (VC) **and **voice cloning (Voice Cloning) **. The former mainly solves the problem of "turning A's words into B's voice"; the latter further emphasizes "learning new tones with fewer samples or even a few sentences of speech".

Technically, VC typically adopts the idea of "content-timbre decoupling": a content encoder extracts speech content and prosodic information (which can be discrete units based on ASR or self-supervised continuous representations), and then a conditional generator combines the target speaker embedding or codec conditions to generate new speech with the target timbre but essentially unchanged semantics and rhythm. If a neural codec is introduced, speech can be directly edited in the codec space to achieve high-fidelity conversion.

**Voice cloning**emphasizes few-shot and generalization capabilities on the basis of VC: the model needs to extract stable speaker representations from just a few samples or even a few seconds of audio, and generate synthetic speech with consistent style and similar timbre accordingly. This capability is highly useful in areas such as virtual character design, personalized assistants, game character customization, and dubbing acceleration, but it also requires strict adherence to legal and ethical norms to ensure that it is used only under the premise of compliant authorization, full informed consent, and secure control, thereby avoiding the risks of abuse or identity impersonation.

### 4.4.3 Music and Sound Effect Generation: From Prompt to Complete Soundscape

Compared to speech generation,** music and sound effect generation ** are more complex in terms of structure and time scale: music often has a longer duration and a richer internal structure (paragraphs, melodies, harmonies, rhythms); sound effects come in a wide variety, from natural environments (rain, wind, waves) to onomatopoeia (UI clicks, beeps, game skill sound effects), each with its own pattern. In recent years, models based on neural codecs, sequence modeling, and diffusion have made "generating complete music/sound effects from text" a reality.

In music generation, models such as MusicLM, MusicGen, Suno, Udio, etc., typically encode audio into a sequence of discrete codec tokens, and then train text-conditioned or MultiModal Machine Learning-conditioned generative models in this discrete space. Users only need to provide a text description (such as "moderate tempo, warm and soothing Lo-Fi background music suitable for studying and concentration", "tense electronic orchestral score suitable for science fiction trailers") or upload a reference music snippet, and the model can generate high-quality music up to dozens of seconds or even minutes in length. For creators, this is both a source of inspiration and a powerful tool for rapid prototyping and background music generation.

In sound effect generation, similar technologies can generate UI sound effects, notification tones, game environment sounds, etc. based on text prompts, helping product and game teams quickly iterate on sound design. Combining with the audio understanding capabilities of the previous layer, it can also achieve style alignment and scene self-adaptation, such as automatically matching sound effect styles according to the screen or game level.

Whether it is voice, music, or sound effect generation, the capabilities at this level are evolving rapidly: from the early machine voices with a strong synthetic flavor to the current high-fidelity content that is indistinguishable from human voices and professional music. Meanwhile, issues surrounding copyright, compliance, traceability, and controllability have become particularly important - how to protect the legitimate rights and interests of creators and users while providing powerful creative tools will be a key issue that this level of technology will continue to face.

# 5. Video (Video)

In the MultiModal Machine Learning system, ** the video modality ** is responsible for understanding and generating "time-varying visual signals". Compared to single-frame images, videos not only contain information about texture, shape, and layout in the spatial dimension but also carry rich  ** temporal dimension clues ** , such as the rise and fall of actions, the motion trajectories of objects, and the rhythm of shot transitions. Whether it is behavior recognition in security monitoring, action analysis in sports training, one-click editing on Short Video Platforms, or intelligent parsing of long videos, they all essentially rely on a comprehensive set of understanding and generation capabilities centered around "frame sequences".

From an engineering perspective, video capabilities can generally be divided into several levels: ** The underlying video enhancement and restoration ** is responsible for ensuring "clear visibility"; ** Video understanding and structural analysis ** is responsible for answering "what happened"; on this basis, ** Video + Language MultiModal Machine Learning tasks ** convert video content into structured descriptions and retrieval interfaces that can be used in text; further, ** Video generation and editing ** in turn starts from text or example videos to generate or recombine video content in a controllable manner; and ** Digital humans / virtual humans ** as a representative type of application, integrate speech, language, motion, and video rendering together to form a new form for interaction and content production.

Next, we will also start from the hierarchical capabilities to sort out the video-related capabilities.

## 5.1 Traditional Video Processing: From "Playable" to "Good-looking and User-friendly"

At the lowest level of video technology, what we first care about is not "who is in the picture" or "what event has occurred", but whether the video itself is stable, clear, and comfortable: whether the picture is shaky, blurry, has many noise points, or has a suitable aspect ratio for playback on the target terminal.**Traditional video processing**operates mainly at the frame sequence and spatio-temporal pixel levels. Through operations such as enhancement, restoration, super-resolution, frame interpolation, and reframing, it transforms the original video, which is noisy, shaky, has insufficient resolution, or an inappropriate aspect ratio, into a "high-quality temporal signal" that is more suitable for viewing and subsequent analysis. It can be analogized to "image restoration and enhancement + geometric correction" in the image modality, except that here additional smoothing and consistency in the time dimension are introduced.

From a product perspective, this layer of capabilities is almost "invisible" behind all video products: one-click image quality enhancement in video editing software, automatic image quality upgrade on Short Video Platforms, intelligent super resolution and frame interpolation in TV boxes and players, old film restoration services, and multi-frame preprocessing for upstream detection/recognition models are all direct manifestations of traditional video processing. The following will still be sorted out from three perspectives:  ** scenarios ** ,  ** principles ** , and  ** models ** , and several key directions such as video enhancement and restoration, super resolution, and frame interpolation will be expanded in the subsequent sections.

* **Scenarios**
  In online video platforms, editing tools, surveillance systems, and terminal devices, traditional video processing mainly occurs in the following typical scenarios:
  * Content Platforms and Editing Tools: When uploading or editing short videos or long videos, users can "pick up their phones and shoot, and use the footage right after shooting" through one-click image quality enhancement, image stabilization, anti-shake, and noise reduction; when importing old video creatives into an editing project, they can be made more visually consistent with new creatives through restoration and frame interpolation.
  * Film and Old Film Restoration: Perform digital restoration on historical film, early television programs, and standard-definition creatives, removing scratches, noise, and jitter, restoring colors and details, and providing higher-quality versions for re-screening, re-publishing, and digital archive preservation.
  * Video surveillance and driving record: Perform noise reduction, dehazing, contrast enhancement, and image stabilization on surveillance footage with low light, rain and fog, or severe compression to improve the robustness of subsequent detection and recognition modules, facilitating evidence collection and traceability.
  * Terminal Playback and Device-side Enhancement: TVs, set-top boxes, and mobile phone players locally integrate super resolution and frame interpolation functions, "upgrading" existing 720p/1080p, 24/30fps content at the playback end to approximate 4K, 60/120fps visual effects.
  * Multi-terminal adaptation and distribution: To simultaneously cover portrait mobile screens, landscape tablet screens, and large-screen TVs, perform portrait and landscape adaptation, intelligent cropping, and multi-aspect ratio reframing on the same video, reducing the costs of manual editing and multi-version maintenance.
* **Principle**
  Traditional video processing usually does not directly understand semantic categories, but instead focuses on modeling and optimization at the spatio-temporal signal level around image quality, stability, and temporal consistency:
  * Spatiotemporal Joint Modeling: On the basis of single-frame image enhancement, introduce information from the temporal dimension, and use optical flow estimation, camera motion modeling, or spatiotemporal convolution to treat the preceding and succeeding frames as additional "observations", performing multi-frame fusion and noise suppression along the time axis.
  * Image stabilization and anti-shake: Model camera shake as a sequence of geometric transformations (translation, rotation, scaling, etc.) over a period of time. By estimating the global or local motion trajectory, smooth it and then reproject it into the output video, thereby achieving anti-shake and stabilization effects.
  * Video Super Resolution and Frame Interpolation: Video super resolution maintains temporal consistency while enhancing spatial resolution through multi-frame alignment and detail reconstruction; frame interpolation synthesizes intermediate frames between two frames through optical flow estimation or spatio-temporal generative networks, presenting motion at a higher frame rate and improving smoothness.
  * Reframing and Automatic Composition: By detecting and tracking the subjects (people, objects) in the video, estimating the subject's trajectory on the timeline, and then combining the aspect ratio of the target resolution, a suitable cropping window is selected for each frame, and the motion of the cropping window is temporally smoothed to ensure a natural viewing experience.
  * Quality-Efficiency Tradeoff: Offline processing in the cloud can pursue optimal image quality and complex models, while in mobile phones, players, and real-time scenarios, it is necessary to control the number of model parameters, computational complexity, and latency, and make fine compromises in algorithm structure and inference framework.
* **Model**
  In terms of specific implementation, traditional video processing comprehensively uses classical video signal processing methods and deep learning models to strike a balance among effectiveness, efficiency, and deployment form:
  * Classical video processing methods, such as optical flow-based image stabilization and frame interpolation, temporal filtering and multi-frame fusion, block matching-based denoising and de-compression artifact removal, etc., are still widely used in scenarios with limited computing power or requirements for interpretability.
  * Deep Video Restoration and Enhancement Models: Multi-frame super resolution and enhancement networks represented by EDVR, BasicVSR / BasicVSR++, Real-ESRGAN Video Edition, etc., significantly outperform traditional methods in denoising, deblurring, detail restoration, and de-compression artifacts removal through alignment and spatio-temporal feature aggregation.
  * Deep frame interpolation models: Frame interpolation networks such as DAIN, RIFE, FILM, etc., generate intermediate frames through explicit or implicit optical flow estimation and intermediate feature fusion, and are more stable in complex motion and occlusion scenarios compared to traditional optical flow + resampling methods.
  * Transformer-based Video Restoration: Utilizing spatio-temporal attention to uniformly process spatial textures and temporal dependencies, it has stronger modeling capabilities under complex camera motion and multi-object scenarios, while controlling the computational cost during inference through mechanisms such as sparse attention and sliding windows.
  * Actual products and systems: Commercial enhancement software such as CapCut's intelligent enhancement, Topaz Video Enhance, etc., the image quality enhancement pipelines of Bilibili and various Short Video Platforms, SaaS services for old film restoration, etc., usually cascade multiple models and strategies, dynamically selecting the optimal processing path based on creative type and terminal conditions.

Overall, this layer mainly lays the physical and perceptual foundation for videos "before semantics": it not only helps users obtain a more comfortable viewing experience but also provides cleaner and more stable inputs for upstream detection, recognition, and generation models. Next, we will delve into sub-directions including  **video enhancement and restoration** ,  **super-resolution and frame interpolation** , etc.

### 5.1.1 Video Enhancement and Restoration: Polishing from "Watchable" to "Beautiful"

Under real shooting conditions, videos are often not "clean": severe jitter caused by handheld devices, high noise and smeariness in low light, blocky artifacts and color bands due to network compression, as well as fading and scratches from recordings on old devices, all make the video quality significantly lower than the ideal state. The goal of video enhancement and restoration is to, without changing the semantic content of the video, maximize the restoration of a stable, clear, and natural visual experience, refining "barely watchable" creatives to a level where they "look pleasing or even good".

In the time domain, the primary issue to be addressed in enhancement and restoration is stability. By performing feature matching or optical flow estimation on consecutive frames, global camera motion and local object motion can be separated, and then the output frames can be re-rendered using the smoothed camera trajectory, thereby suppressing rapid jitter and minor shaking and preventing viewers from experiencing dizziness during viewing. On this basis, frame-level denoising, deblurring, and artifact removal are more focused on spatio-temporal joint modeling: multi-frame joint denoising utilizes redundant information from previous and subsequent frames to perform a process similar to "multi-exposure fusion" in the temporal direction, effectively suppressing high ISO noise and compression noise while preserving detailed textures; for slight motion blur, by estimating the blur kernel or using an end-to-end deep network, a deconvolution-like sharpening process is performed on the frame sequence to make both the static background and moving subjects sharper.

For old films and low-quality creatives, restoration also involves "reconstruction" at the color and structural levels. Film aging can lead to yellowing of the picture, decreased contrast, and prominent local scratches and stains, while early digital videos often have issues such as low resolution, severe compression, and jagged edges. Modern restoration processes often adopt multi-step collaboration: first, use detection and segmentation models to locate local damaged areas such as scratches and stains, then "borrow materials to fill the gaps" from neighboring frames and neighboring spatial pixels through spatio-temporal completion networks; at the same time, perform color restoration and contrast reshaping to make the overall color tone close to the original shooting or the set style reference. For severely compressed videos, dedicated de-artifact networks targeting blocking artifacts and ringing artifacts are also introduced to improve edges and details without over-smoothing.

These enhancements and restoration capabilities are often implemented as "one-click" features in the product: users simply need to check "image stabilization", "image quality enhancement", or "old video restoration", and the system will automatically select the appropriate model and parameter combination in the background to perform multi-stage processing on the video frame sequence. From a business perspective, this layer not only directly determines the audience's subjective evaluation of image quality but also indirectly affects the performance of upstream analysis models: cleaner and more stable video input often means more reliable face/license plate recognition, more accurate behavior detection, and fewer false alarms.

### 5.1.2 Super Resolution and Frame Interpolation: From "Visible" to "Smoother"

Against the backdrop of continuous upgrades to display devices and ever-increasing user demands for details and smoothness, a large amount of existing video content appears "inherently deficient" in terms of resolution and frame rate: 1080p looks less sharp on 4K screens, and 24/30fps is prone to motion blur or laggy sensations in large-screen and fast-moving scenarios. Super resolution and frame interpolation technologies are precisely designed to address these two issues: the former "fills in details" in the spatial dimension, while the latter "fills in the process" in the temporal dimension, jointly elevating videos that are "barely visible" to a viewing experience that is "rich in details and smooth in playback".

Video super resolution has an additional key dimension compared to single-frame image super resolution: time. Simple frame-by-frame upscaling can easily lead to inconsistent details between adjacent frames, resulting in flickering and texture jitter. Therefore, mainstream methods leverage information from multiple preceding and succeeding frames, align details from neighboring frames to the target frame through optical flow estimation or feature-level alignment, and then perform detail reconstruction after alignment. Models such as EDVR, BasicVSR / BasicVSR++, and Real-ESRGAN Video Edition first align and aggregate multiple frames in the feature space, and then use deep networks to infer high-resolution details, avoiding the "blurriness" and "plasticity" caused by simple interpolation. In this process, how to balance between "physical plausibility" and "aesthetic appeal" is the core of loss design and training strategies: it is necessary to improve objective metrics (such as PSNR, SSIM) while ensuring that the subjective visual experience is natural, without excessive sharpening or false details.

Frame interpolation focuses on "frame filling" along the time axis. Traditional methods rely on optical flow estimation, first predicting the motion of each pixel between two consecutive frames, and then interpolating to generate new frames at intermediate positions according to certain rules. However, in areas with fast motion, multi-object occlusion, or complex textures, optical flow is often inaccurate, prone to trailing, ghosting, or local deformation. Deep frame interpolation models such as DAIN, RIFE, FILM, etc., learn the fusion strategies of optical flow, depth, or intermediate features simultaneously through end-to-end networks, directly outputting interpolated frames, with significantly improved stability and visual quality in complex scenarios. For sports events, action game recordings, and slow-motion creation, frame interpolation can smoothly increase the original 24/30fps video to 60/120fps, preserving motion details while reducing lag and afterimages.

In engineering practice, super resolution and frame interpolation are often used in combination: for existing content with low resolution and low frame rate, temporal frame interpolation is first performed, followed by spatial super resolution, or both are integrated and implemented in a unified spatio-temporal network. In terms of deployment forms, cloud-based offline processing is suitable for film and television restoration with extremely high image quality requirements and platform-level "image quality upgrade" services, while real-time inference on the edge side is more commonly seen in TV boxes, player apps, and gaming/action cameras, where model compression and hardware acceleration are needed to ensure low latency. Regardless of the form of presentation, super resolution and frame interpolation have become important infrastructure for the "HD/Ultra HD experience", enabling old content to have a "second spring" on new terminals.

## 5.2 Video Understanding and Structural Analysis (Video Understanding)

If traditional video processing mostly stays at the level of "image quality and stability", then ** video understanding and structural analysis ** begin to answer semantic questions such as "what is happening in the video": who is doing what, where it is happening, how long it lasts, whether there are abnormal behaviors, etc. The goal here is to perform a structured decomposition of the video on the timeline: identify actions and behaviors, detect and track targets, segment the foreground and background, divide scenes and shots, and extract high-level semantic signals for downstream decision-making, retrieval, and alerting.

From a product perspective, this layer of capabilities has penetrated into various intelligent security platforms, sports training analysis systems, intelligent driving recorders, and industrial quality inspection video analysis systems: identifying abnormalities such as fighting, falling, and loitering in surveillance; analyzing action standardization and technical details in sports and fitness scenarios; tracking the trajectories of vehicles and personnel and monitoring the normalcy of production processes in transportation and industrial environments. The following will still sort out this type of capabilities from three perspectives:  ** scenarios ** ,  ** principles ** , and  ** models ** , and focus on several representative directions in the subsequent subsections.

* **Scenario**
  * Security and Public Safety: In urban surveillance, industrial parks, and buildings, identify behaviors such as fighting, falling, gathering, running, climbing over fences, etc., and issue early warnings for abnormal patterns such as loitering and late-night stay.
  * Traffic and Travel: Detect and track the trajectories of pedestrians, vehicles, and bicycles at intersections, tunnels, and on highways, analyze behaviors such as running red lights, driving in the wrong direction, occupying lanes, speeding, etc., to provide a basis for traffic management and accident traceability.
  * Sports and Athletic Training: Analyze the key phases and quality of postures in actions such as basketball shooting, tennis serving, yoga poses, etc., providing technical analysis and error correction suggestions for athletes and general users.
  * Industrial Production and Quality Inspection: Monitor whether the operation steps on the production line are standardized, detect whether there are missing installations, incorrect installations, or abnormal actions during the assembly process, and provide basic data for safe production and yield improvement.
  * Content Structuring and Retrieval: Perform shot segmentation, scene classification, and marking of important segments on long videos to provide structured indexes for subsequent retrieval, recommendation, and editing.
* **Principle**
  The key to video understanding and structural analysis is to jointly model spatial targets and semantics in the temporal dimension:
  * Action Recognition and Behavior Analysis: Based on 2D/3D convolution, temporal pooling, or Transformer, a video clip is globally encoded to identify the action categories occurring within it; advanced methods combine human key point sequences and skeletal topology to analyze action quality and patterns at a finer granularity.
  * Object Detection and Tracking: While performing detection on each frame, introduce a cross-frame association mechanism (appearance features, motion trajectories, etc.) to connect the detection boxes of the same object at different times into a continuous trajectory, thereby obtaining multi-object tracking results.
  * Video Semantic Segmentation and Scene Analysis: Perform semantic or instance segmentation on each frame of the video at the pixel level, and utilize temporal continuity to smooth predictions; simultaneously detect shot transitions and scene boundaries to achieve the structural decomposition of long videos.
  * High-level Event and Anomaly Detection: Based on basic action and trajectory features, time-series modeling and Pattern Recognition methods are used to detect rare events and abnormal patterns, often combined with unsupervised or weakly supervised learning to alleviate the problem of scarce annotation.
* **Model**
  In model selection, video understanding and structural analysis typically adopt a combined architecture of "spatial features + temporal modeling":
  * Classic models based on 3D convolution and Two-Stream, such as I3D, perform end-to-end action recognition on short video clips by convolving simultaneously in the spatial and temporal dimensions.
  * The SlowFast series of models based on multi-path and multi-time scale capture semantics through the slow path and motion details through the fast path, achieving a better balance between computational cost and accuracy.
  * Transformer-based video models, such as TimeSformer, Video Swin Transformer, etc., utilize spatio-temporal attention mechanisms to model long-range videos and are more suitable for capturing complex events and multi-agent interactions.
  * Tube-based detectors and spatio-temporal convolution/Transformer models extend detection boxes into "tubes" over time, performing action detection and spatio-temporal segmentation on spatio-temporal joint features.
  * Multi-object tracking (MOT) methods, such as DeepSORT, combine frame-level detection results with appearance embeddings and motion prediction to stably associate target identities in videos.

Overall, this layer of capabilities further abstracts videos from "high-quality pixel streams" into "behavior and event streams", laying a structural foundation for upstream multimodal understanding, retrieval, and decision-making. Next, we will elaborate on this from three directions: ** Action Recognition and Behavior Analysis ** ,  ** Object Detection and Tracking ** ,  ** Event and Anomaly Detection ** .

### 5.2.1 Action Recognition and Behavior Analysis: From Frame Sequences to "Who is Doing What"

Action Recognition and Behavior Analysis focuses on "what the subject is doing within a time window." In security scenarios, this means identifying behaviors such as "walking, running, falling, fighting" from videos; in sports and fitness, it corresponds to more fine-grained actions such as "whether shooting, serving, and squatting are standard" and "whether yoga poses are in place." Technically, early methods mainly relied on 2D convolution + optical flow or handcrafted features, stacking several frames and then performing overall classification; modern methods more often adopt multi-temporal scale structures such as 3D convolution (I3D, a series of 3D ResNet variants), SlowFast, or models based on spatio-temporal attention such as TimeSformer and Video Swin Transformer to jointly model spatial texture and temporal changes.

In many scenarios requiring high-precision pose analysis, directly classifying RGB segments is not sufficient; instead, it combines human pose estimation and skeleton sequence modeling: first extracting 2D/3D key points from each frame, then feeding the key point sequence into RNN, temporal convolution, or GCN/Transformer networks to analyze the temporal structure and spatial coordination of actions. This approach of "pose prior + temporal modeling" is more robust to changes in background, lighting, and clothing, making it suitable for applications with high requirements for action details, such as yoga, fitness, and industrial operation compliance assessment.

### 5.2.2 Object Detection and Tracking: From "Where is this frame" to "The entire trajectory"

Single-frame Object Detection can tell us "what objects are in this frame and where they are", while many real-world tasks require information such as "where this vehicle/person came from, where they are going, and what they did in between". The Object Detection and Tracking module is precisely designed to string together frame-level detections into continuous trajectories over time: on the one hand, it runs a detector on each frame to provide candidate object bounding boxes; on the other hand, it matches and associates the bounding boxes in adjacent frames based on cues such as appearance features (ReID embeddings), motion prediction (Kalman filtering), and spatial overlap, resulting in Multi-Object Tracking (MOT) results.

In engineering practice, a typical pipeline is: "Robust Pedestrian/Vehicle Detection + Association Algorithm like DeepSORT", deployed on surveillance cameras or dashcams, which outputs the motion trajectory of each ID in real time. In more complex systems, these trajectories are also combined with regional semantics (lane, area division) and business logic rules to further infer high-level behavioral patterns such as reverse driving, long-term loitering, and frequent entry and exit, providing continuous time-series signals for upstream security, traffic flow analysis, and industrial process monitoring.

### 5.2.3 Event and Anomaly Detection: Identify "Something Wrong" from "Normal Mode"

In most business scenarios, what truly needs to be focused on are often "minority anomalies" and "critical events": for example, fighting, falling, and gathering in security, abnormal shutdowns or violations in industrial production, dangerous driving behaviors in traffic, etc. Such events are relatively rare, with high annotation costs and extremely imbalanced samples, posing additional challenges to model construction.

A common approach is to build a temporal anomaly detection module on top of basic action recognition, object tracking, and scene segmentation: either directly learn a small number of labeled anomaly samples through supervised methods; or adopt unsupervised/weakly supervised methods to model the distribution of motion and behavior in the "normal mode", and issue an alarm once new observations deviate significantly from the historical distribution. At the model level, temporal autoencoders, contrastive learning, graph neural networks, or temporal transformers will be combined to uniformly encode spatial relationships and temporal dependencies, thereby capturing more complex group behavior patterns and long-range dependencies.

## 5.3 Video + Language MultiModal Machine Learning Task (Video‑Language)

If video understanding addresses the issue of "fully understanding the video itself", then ** video + language MultiModal Machine Learning tasks ** focus on "how to describe, answer questions, and retrieve video content using natural language" and "how to quickly locate key information on the long video timeline based on text requirements". These tasks require simultaneous processing of visual, speech, and text signals: on one hand, extracting the visual and audio features from the video; on the other hand, leveraging the inference and generation capabilities of language models to compress spatio-temporal content into text summaries, question-answer results, and semantic indices suitable for human consumption and machine retrieval.

From a product perspective, this layer of capabilities has penetrated into scenarios such as automatic subtitle and timeline generation for long videos, "intelligent key point marking / key segment extraction" in short video editing platforms, and Q&A assistants for enterprise training and meeting videos: users no longer need to "watch from start to finish", but can directly search, query, and reorganize video content through natural language. The following will still be presented from  ** scenarios ** ,  ** principles ** , and ** models ** three perspectives.

* **Scenario**
  * Subtitle and Summary Generation: Automatically generate multilingual subtitles for courses, lectures, meetings, and long video content, and on this basis, generate chapter-level summaries, highlight lists, and timelines.
  * Video Q&A and Knowledge Access: Build a "Video Q&A Assistant" for teaching videos, operation demonstrations, and enterprise training content, supporting users to ask questions in natural language, such as "How to do this step" and "Where did this person finally put the phone".
  * Video content retrieval and segment localization: Supports precise retrieval of "text → video segment" in large-scale video libraries, such as "find the part that mentions the price" and "find the segment that explains a certain formula"; Automatically marks and annotates highlights and key information within a single long video.
  * Content Production and Editing Assistance: Combining video content understanding and language generation capabilities, it automatically generates titles, copy, and storyboard scripts to assist creators in quickly editing and recombining creatives.
* **Principle**
  The core of the video-language MultiModal Machine Learning system is to align temporal visual features with text representations in a unified embedding space, and perform retrieval, generation, and reasoning on this basis:
  * MultiModal Machine Learning Feature Extraction and Alignment: Extract spatio-temporal features (CNN/ViT/Video Transformer) from video frames/segments, extract language embeddings (pre-trained LLM or text encoder) from text, and align the two modalities through contrastive learning or multi-modal pre-training.
  * Speech and Text Pipeline: For content containing speech, ASR is typically first used to generate timestamp-aligned transcribed text, which is then jointly modeled with visual features. This allows for direct text-driven retrieval and cross-modal comparison and error correction.
  * Temporal Modeling and Segment Localization: For long videos, it is necessary to learn "segment-level" representations on the timeline, dynamically switch between local segments and global context through attention or temporal RAG, and achieve precise localization of problem-related intervals.
  * Generation and Inference: Connect a large language model to the aligned multi-modal representation for natural language generation (captions, summaries, explanations), or conduct multi-round Q&A and logical reasoning.
* **Model**
  In terms of model form, video-language MultiModal Machine Learning tasks have evolved from "dedicated encoder + simple head" to "unified large multimodal model":
  * Early video-language models, such as VideoBERT, jointly model visual and text tokens during the pre-training phase, obtaining transferable video-language representations through masked prediction and contrastive learning.
  * All‑in‑One Video‑Language Models: Integrate video, text (and speech) into a single MultiModal Machine Learning Transformer, and achieve unified processing of multiple tasks such as description generation, retrieval, and QA through shared or partially shared parameters.
  * Long-video MultiModal Machine Learning models: such as Gemini, Claude, GPT with video capabilities, etc., through long context and hierarchical temporal modeling, comprehensively understand videos lasting tens of minutes or even hours, and support timeline-level summarization and Q&A.
  * Temporal RAG + VLM: Build a "temporal vector index" on videos, first use VLM to encode video segments to establish a database, then retrieve relevant segments during query, and combine with LLM for answer synthesis and interpretable reasoning.

Overall, this layer further elevates video from "machine understanding" to the level of "human-machine dialogue and collaboration": users can ask questions to the video just as they would to a person, while the system behind the scenes completes complex visual, speech, and language alignment and reasoning.

### 5.3.1 Subtitles, Summaries, and Timelines: Compressing Long Videos into Browsable Text

For courses, lectures, conferences, and long-form content videos, the most pressing need is often to "quickly know what was covered and where the key points are" rather than watching the entire content from start to finish. The automatic captioning and summarization system uses a combination of "ASR + text processing + visual aids" to transcribe audio content into timestamp-aligned text, and then generates a structured outline and a concise summary based on this, achieving information compression from "hour-long videos" to "minute-long readings".

At the implementation level, the ASR module is responsible for providing multilingual transcription and timeline alignment stably and with high quality; on the text side, large language models are used to correct errors, segment sentences, and restructure semantics of the original transcription, extracting chapter titles, key information, and question-answer pairs. In some scenarios, visual cues (such as PPT page changes and scene transitions) are also combined to assist in dividing chapter boundaries and key segments, ensuring that the summary structure is more consistent with the rhythm of the actual content.

### 5.3.2 Video Question Answering and Semantic Retrieval: "Manipulating" Videos with Natural Language

Beyond subtitles and summaries, a further requirement is the ability to conduct Q&A and retrieval for specific video content: for example, "Where did this person finally put the phone?", "Which segment talks about the pricing strategy?", "At which minute is this step demonstrated?" Such tasks require semantic localization of questions on the timeline: it is necessary to understand the people, objects, and actions involved in the question itself, as well as to find the corresponding segments in the video's temporal representation.

In practice, we usually first build multi-granularity indexes for videos offline: extract multi-modal representations (image + text/voice) from fixed-length segments, and build vector indexes or graph structures. During online interaction, user questions are encoded into text vectors, which are then matched with the segment representations in the index to find the most relevant time intervals; subsequently, the content of these segments (key frame screenshot descriptions, transcribed text, etc.) is fed into the LLM along with the questions, and the model generates natural language answers or returns the corresponding time points. For large-scale video libraries, "cross-video retrieval" can be supported under the same mechanism, such as cross-collection search for relevant segments in enterprise training knowledge bases or e-commerce product videos.

### 5.3.3 MultiModal Machine Learning Editing Assistance: From Understanding to "Editing for You"

Once the system can stably understand the content and semantic structure of videos, the natural next step is to reverse-utilize these understanding results to assist in creation and editing. Video-language MultiModal Machine Learning models can automatically select semantically appropriate segments from existing creatives based on the script or prompt provided by the creator to generate a rough cut timeline; they can also automatically generate titles, cover copy, chapter labels based on video content, and even provide suggestions for shot rhythm and background music.

In the workflow, this type of capability typically manifests in the form of "intelligent recommendation" and "automatic rough cut": after the creator uploads the creatives, the system automatically completes analysis, storyboarding, and keyframe marking, and provides several candidate versions (such as editing plans with different rhythms and durations); the creator can make fine adjustments on this basis without having to start from scratch and screen frame by frame. For enterprise-level applications, the system can also combine the Knowledge Base and Brand Guidelines to ensure that the generated copy, subtitles, and editing style meet the established business requirements and compliance standards.

## 5.4 Video Generation & Editing (Video Generation & Editing)

After acquiring stable comprehension and structural analysis capabilities, ** video generation and editing ** have entered the stage of "actively creating content": no longer just enhancing image quality or performing structural analysis, but generating new shots or performing structural editing and reorganization of the original video based on text scripts, reference images, or existing videos. This includes text-to-video (Text‑to‑Video) from scratch, as well as style transfer, expansion, and rearrangement based on existing images/videos, as well as object-oriented fine editing and replacement.

In terms of products, this level of capabilities has entered the mainstream of content creation through a series of products such as Dreamina Video, Minimax Video, Sora, Runway Gen-2, Pika, Kling, etc.: Advertisements, concept videos, animations, and storyboard shots can be quickly generated without relying on large-scale filming teams and complex post-production; Creators can drive shots and styles through natural language scripts; Traditional video editing processes have begun to deeply integrate with structured generation tools. The following will still be sorted out from the perspectives of  ** scenarios ** ,  ** principles ** , and  ** models ** .

* **Scenario**
  * From copywriting and scripts to short videos: brand advertisements, mini-theaters, plot segments, and concept animations, automatically or semi-automatically generate playable video drafts based on scripts.
  * Image/Video to Video: Generate dynamic versions for illustrations or character designs, perform style transfer on real-world filmed creatives (reality → anime/illustration), or expand/reorganize existing videos in time and space.
  * Structured Editing and Post-production: On the premise of not changing the semantics of the overall content, achieve fine operations such as face swapping, lip-syncing, object erasure and replacement, and text-driven clip rearrangement.
* **Principle**
  Currently, most mainstream video generation and editing methods take the diffusion model (Diffusion) or its variants as the core, gradually "denoising" to generate videos in the high-dimensional spatio-temporal latent space:
  * Text conditional modeling: Map the script to conditional vectors through text encoders (such as T5/CLIP text tower or dedicated language models), guiding the video decoder to align with the text description in terms of style, content, and motion patterns.
  * Spatiotemporal Consistency and Motion Control: Incorporate spatiotemporal convolution, temporal attention, or 4D representation (such as NeRF/GS) into the diffusion process or posterior optimization to ensure the coherence and physical plausibility of the video along the time axis.
  * Conditional generation of images/videos: Initiate the diffusion process in the feature space of the input image or video, and achieve controlled editing or expansion of "preserving the given part + generating new content" by controlling noise injection, masked regions, and conditional channels.
  * Structured control signals: By combining structural information such as pose skeletons, segmentation masks, depth maps, and camera trajectories, they make the generated videos more controllable in terms of subject motion and perspective changes.
* **Model**
  Representative models and directions include:
  * Diffusion-based Text-to-Video models (Sora, Runway Gen-2, Pika, Kling, etc.), pre-trained on large-scale video-text pairs, possess strong generative capabilities in complex scenarios, multi-shot motion, and diverse styles.
  * Image-to-Video diffusion model: conditioned on a single frame image, predicts the dynamic evolution of subsequent frames to achieve "single image → animation/visual effect"; or performs operations such as continuation, expansion, and perspective rotation on short videos.
  * NeRF / 4D Representation and Keyframe + Interpolation Method: By utilizing 3D scene representation or keyframe + temporal interpolation, it combines generation with geometric and consistency modeling to achieve more stable viewport roaming and complex motion.

These capabilities do not exist in isolation but gradually permeate the editing and post-production pipeline: from copywriting to storyboarding, storyboarding to rough cut, rough cut to stylization and local editing, and more and more stages are driven by "text + structured control".

### 5.4.1 Text-to-Video: From Script to "Watchable" Shot Sequence

Text-to-Video aims to achieve the following: users describe a scene, shot, or story segment in natural language, and the system automatically generates a coherent video. Compared with image generation, Text-to-Video adds the challenge of the time dimension: it not only needs to maintain consistent image quality and style at the single-frame level but also ensure the coherence of the subject's identity, lighting, background, and motion trajectory across frames.

A typical diffusion-based text-to-video model first pre-trains on large-scale video-text paired data: the text encoder extracts semantic conditions, and the video decoder repeatedly denoises a "noisy video" in the latent space, gradually converging to a spatio-temporal signal consistent with the text. During this process, structures such as temporal attention, 3D convolution, or 4D representation are used to explicitly incorporate temporal dependencies into the network to avoid issues such as "inter-frame jumps" and "character resets". Some systems also support control over camera movements (push, pull, pan, tilt) and composition rhythm, making the generated results closer to real shooting language.

### 5.4.2 Image/Video to Video: "Growth" and "Deformation" on Existing Content

Another important route is to generate and edit based on existing images or videos: for example, animating an illustration or concept art, stylizing a live-action video into an anime, or changing the background, adjusting the weather and time while keeping the structure unchanged. Technically, such methods often add a "reference channel" to the diffusion process: encoding the input image or video into features, which participate in denoising as conditions or initial states, while controlling "which regions can be changed and which must remain" through mechanisms such as masks and explicit geometric constraints.

For style transfer scenarios, the model will redraw textures and lighting while preserving the original motion and composition to match the target style; for video extension and recombination, it achieves horizontal/vertical scene expansion, perspective rotation, or plot supplementation by "continuing" new frames at both ends or in the middle of the time. These capabilities are highly suitable for integration with traditional editing workflows: editors first provide key shots and rhythms, and then the model automatically generates transitions and variations between these "anchor points".

### 5.4.3 Structured Video Editing: Fine-grained Control at the Object Level

In many business scenarios, completely regenerating a video is not an inelastic demand; rather, the more crucial aspect is to perform fine-grained and controllable structured editing on existing footage, such as face swapping, lip-syncing, erasing unwanted objects, replacing advertising content, or rearranging shot sequences according to a text script. Structured video editing has developed along this line of thinking: on the basis of video understanding, it introduces object-level segmentation, tracking, and parametric representation, enabling editing operations to be stably bound to specific targets and time periods.

Face swapping and lip-sync are the most typical applications in this direction: the model needs to map the identity of the target person onto the performance of the original video while ensuring the natural and coherent head pose and overall expression, and precisely control the lip movement based on the new speech signal. Object erasure/replacement relies on high-quality segmentation and spatio-temporal completion: first segment and remove the target object in each frame, then fill the holes using neighboring frames and contextual textures to avoid obvious "patching" traces. Text-driven editing aligns the "script structure" with the video timeline, automatically selects and stitches together segments that match the script semantics, achieving a higher level of automated editing.

## 5.5 Digital Human / Virtual Human (Digital Human / Avatar)

**Digital Human / Virtual Human (Digital Human / Avatar)** can be regarded as a "system-level integration" of video generation, speech synthesis, MultiModal Machine Learning understanding, and graphics rendering: it is not just about generating a video, but based on text or speech input, continuously and controllably driving a virtual character to "speak, make expressions, and perform actions", and achieving quasi-real-time or even real-time interaction in an increasing number of scenarios. Compared with general video generation, digital humans emphasize three points: ** long-term consistency of identity and image, fine alignment of speech-expression-action, and real-time and stability of the end-to-end system** .

From a product perspective, digital humans have already widely appeared in **scenarios such as content production platforms, virtual customer service / intelligent front desk / virtual tour guides, education and training and online classrooms, brand virtual IPs / virtual idols, and virtual LIVE creators / digital avatar tools for creators** : enterprises can mass-produce video content with fixed images and styles, government and enterprise services can use virtual front desks to serve users 24/7, and individual creators can continuously produce "on-camera" videos without showing their faces. The following will still be sorted out from three dimensions of **scenarios** , **principles** , and **models** , and three directions of driving and expression, image and video generation, and real-time interaction and system integration will be expanded in the subsequent sections.

* **Scenario**
  * Content production and online dissemination: corporate promotional videos, product feature explanations, course recordings, news broadcasts. Using digital humans to replace real people on camera significantly reduces costs associated with shooting locations, lighting equipment, and human resources.
  * Virtual Customer Service and Tour Guide: In places such as bank branches, government service halls, scenic spots, and museums, digital humans are used to undertake tasks such as greeting guests, answering inquiries, providing business consultation, and route guidance, while ensuring unified image and 7×24-hour service.
  * Brand Virtual IP / Virtual Idol: Continuously operate short videos, LIVE, and e-commerce content around a virtual character, maintaining a consistent persona and visual style across different platforms.
  * Virtual LIVE Creators and Digital Avatars: Provide configurable virtual LIVE creators / digital avatars for creators who are reluctant to appear on camera or need to operate multiple identities, which can be bound to real voices or synthetic voices to achieve "stable on-camera appearance just by speaking / typing".
* **Principle**
  The digital human system is essentially a "voice/text-driven + image modeling + video/rendering output" MultiModal Machine Learning pipeline, which varies slightly between offline and real-time scenarios but has similar core components:
  * Speech and Language Driven: Directly synthesize speech using TTS according to the script, or connect to ASR + LLM to generate response text from user speech/text, and then output speech using TTS; speech features (such as mel spectrogram) serve as driving signals to control the lip-sync and facial expression timeline.
  * Modeling of Appearance and Motion Space: Construct controllable geometric and appearance representations for virtual avatars, such as 2D portraits/illustrations, 3D avatars based on skeletons and Blendshapes, or renderable volume representations based on NeRF/4D Gaussians; and define a set of "driving parameters" (e.g., key points, pose skeletons, Blendshape coefficients) to encode expressions and poses.
  * Speech → Facial Expression / Motion Mapping: Through a dedicated "speech-driven" model, map speech features to the driving parameters of the face and upper body to achieve lip-sync, facial expression details, and head and shoulder movements; real-time digital humans require this mapping to be end-to-end low-latency and stable.
  * Rendering and Composition: Based on the current frame driving parameters, perform image or 3D rendering on the virtual avatar, output continuous video streams or real-time images; can overlay elements such as backgrounds, props, subtitles, etc., and integrate with traditional video editing workflows.
* **Model**
  In specific models, digital human systems often comprehensively use multiple types of specialized models and general MultiModal Machine Learning models:
  * Audio-driven Talking Head Model: A lip-sync model such as Wav2Lip, which generates natural mouth movements while ensuring identity consistency by learning the alignment relationship between speech and pixels/geometry in the oral region.
  * Real-time / lightweight digital human models: such as Ultralight‑Digital‑Human, lightweight Talking Head models, etc., significantly compress parameters and computational load in their structure, enabling near real-time driving and rendering on CPU / mobile devices / WebGPU.
  * NeRF / 4D Representation Model: Such as ER‑NeRF (a digital human NeRF solution in the Explicit / Efficient / Editable direction), etc., which models the character's appearance and expression changes in 3D space to make the perspective, lighting, and movement more natural and coherent, suitable for high-fidelity and multi-camera scenarios.
  * Speech-driven and MultiModal Machine Learning alignment models: Models like MuseTalk, which are "speech → facial expression / talking head" models, align audio features with visual features to achieve realistic speaking expressions and head movements without relying on a large amount of 3D annotation.
  * Speech and Dialogue Models: High-naturalness multi-speaker TTS, end-to-end speech dialogue models (integrated ASR + LLM + TTS), provide digital humans with multi-style, multilingual voice and dialogue capabilities.

Overall, a digital human is both a set of models and a complete system: it integrates language understanding, speech, visual generation, and real-time reasoning to present an interactive virtual character "in front of the screen". Next, we will explore from  **driving and expression** ,  **image and video generation** , and **real-time interaction and system integration**in three directions.

### 5.5.1 Driving and Expression: From Script / Speech to a "Talking and Expressive" Person

In the digital human pipeline, ** driving and expression ** are responsible for answering a core question: given a script or speech, what mouth shapes, expressions, and head and shoulder movements should the virtual avatar present in each frame. This includes both offline batch production scenarios and responses to real-time conversations.

In offline content production, the common pipeline is "text script → TTS → voice-driven": the business side provides the broadcast copy, the TTS module generates the voice of the target timbre (such as the brand virtual spokesperson), and then inputs the voice features into the "voice → motion" model. ** Wav2Lip-like models ** are important representatives of this stage:

* It takes a reference portrait frame and the corresponding speech segment as inputs, predicts the mouth region precisely aligned with the speech through a convolution/attention network, and then fuses it with the original portrait, thereby precisely modifying the mouth shape while keeping the identity and most expressions unchanged.
* During training, the network learns the oral morphology corresponding to different phonemes through supervision of speech-video alignment data, maintains temporal continuity, and avoids mouth shape jumps or delays.

Compared to the early pure lip-syncing schemes, the new generation of speech-driven models (such as methods like MuseTalk) have further extended to  ** full-face expressions and head poses ** :

* This type of model typically maps speech features to a low-dimensional "emotion/expression latent space", and then generates key points, Blendshape coefficients, or directly generates image features through a decoder, driving subtle changes in areas such as the eyebrows, eyes, and cheeks, making the "talking expression" more vivid.
* Some models also encode semantic information of speech content (such as questions, emphasis, exclamations), combine syntactic/pragmatic signals analyzed by LLM, and add actions such as nodding, frowning, and gestures at intonation changes to enhance the naturalness and expressiveness of the presentation.

At higher dimensions,**driving and expression**can also incorporate external control signals: for example, using pose skeletons, gesture trajectories, gaze directions, etc. as additional inputs, enabling digital humans to imitate the style of specific speakers or execute predefined action templates based on "directed actions" (such as "pointing at the screen" or "spreading hands") in the script. Whether it is local lip-sync driving like Wav2Lip or more full-body expression modeling such as MuseTalk / real-time skeleton driving, they jointly achieve a continuous mapping from speech / text to facial and upper body movements, which is a crucial part of making digital humans "look like they are speaking seriously".

### 5.5.2 Image and Video Generation: From "One Model" to "One Mutable Character"

The driving chain addresses "how to move", while ** image and video generation ** determines "who is moving, where they are moving, and in what style they are moving". This includes high-fidelity realistic digital humans, as well as stylized images such as anime, cartoon, and low-polygon Avatars, as well as different technical selections for real-time and offline rendering.

In 2D portrait and illustration scenarios, the typical approach is to train a **Talking Head generation model ** based on a small number of reference images and short videos:

* The model encodes the identity information of a person into an "appearance vector" or style feature, takes driving parameters (such as speech latent vectors, key points, and expression encodings) as conditional inputs, and synthesizes new frames in the image space.
* Unlike pure Wav2Lip, which only modifies lip movements, this type of model can make small swings in posture and overlay emotional changes in expression, thus making the digital human appear less "stiff".

In scenarios where higher realism, more flexible viewpoints, and multi-camera switching are pursued, an increasing number of solutions adopt digital human modeling based on **NeRF/4D representation** (such as methods like ER-NeRF):

* Through multi-viewpoint shooting or video, first reconstruct the 3D volume or Gaussian field of the human head/upper body, and encode the states corresponding to different expressions and mouth shapes into an interpolatable latent space;
* During driving, map the voice/expression parameters to this latent space, perform volumetric rendering or Gaussian rendering in 3D, and then project it onto the screen.
* The advantages of this approach are that the perspective, lighting, and background are more natural, it can support "surround perspective" and "virtual camera" movement, and it is particularly friendly to VR/AR, virtual LIVE studios, and high-end advertising production.

In business scenarios that emphasize cross - platform deployment and real - time performance, lightweight solutions such as ** Ultralight - Digital - Human ** are also adopted:

* Compress the Talking Head or Avatar rendering network to a scale that can also run on mobile devices / WebGPU through structural pruning, operator reconstruction, and model distillation;
* Completes the generation of a frame of image from driving parameters within a few milliseconds, aligns with real-time audio stream or control signals, realizes "low-latency digital human", and is suitable for interactive terminals, self-service machines, and web front-end applications.

At the level of full video production, image and video generation also need to be combined with background, props, and shot language: a common workflow is:

* First, customize a digital human image (2D or 3D) for a brand or individual;
* Preset several virtual scenarios (studio, office, classroom, exhibition hall, etc.);
* When producing content, the system automatically selects appropriate scenes and camera positions based on the script, generates digital human footage, and arranges multi-screen layouts with PPTs, demonstration videos, and product images.
  This enables the digital human to be not just a "talking head" but a "character" that can naturally integrate into various program and content formats.

### 5.5.3 Real-time Digital Human and System Integration: From Offline Video to "Colleague on Screen"

With the maturity of ASR, TTS, LLM, and lightweight video generation models, more and more digital human systems are starting to move from **offline batch production **to  **real-time interaction ** : when users speak or input text at the terminal, the digital human on the screen "understands - thinks - responds - speaks" within a few hundred milliseconds to a few seconds, creating an experience similar to that of a real human customer service / tour guide / host. The key here is not just the model itself, but also how to  **compress the MultiModal Machine Learning link to an acceptable end-to-end latency ** .

In a typical real-time digital human closed-loop:

* **Front-end Input ** : The ASR module converts user speech into text in real time or directly receives user text input.
* **Semantic Understanding and Decision Making** : LLM combines business Knowledge Base and tools (RAG, database query, process orchestration) to generate response text and necessary structured instructions (such as which page of PPT to display, which video clip to play).
* **Voice and Driving ** : TTS converts the response text into speech with the target timbre. The speech stream is generated and consumed by the Wav2Lip / MuseTalk / real-time skeleton driving model simultaneously, outputting the corresponding lip-sync and expression parameters segment by segment.
* **Render Output** : A lightweight rendering network of the Ultralight‑Digital‑Human type or a GPU-based NeRF / Avatar rendering engine that converts driving parameters into video frames in real time and outputs them directly to the screen via WebRTC, RTMP, or local rendering.

To provide a consistent experience across multiple terminals, the system also needs to make a careful trade-off between  ** latency, bandwidth, and computing power ** :

* In the cloud rendering solution, most of the computations (LLM, TTS, driving, and rendering) are completed on the server, while the terminal is only responsible for playing the video stream. This is suitable for Web / App with limited computing power and offline large screens, but it relies on network stability;
* In the "cloud + edge hybrid" solution, ASR and some LLM inference are completed in the cloud, while lightweight driving and rendering are performed locally, which can significantly reduce audio-visual interaction latency and is suitable for mobile devices and self-service terminals;
* On high-performance computing terminals (such as high-performance PCs and dedicated workstations), most of the links can also be offloaded locally to achieve stable interaction in weak network environments.

On the model side,** real-time digital humans ** also impose additional requirements on structural design:

* The speech-driven model needs to have streaming inference capabilities, being able to provide mouth shape and expression predictions after receiving a short segment of speech, rather than waiting until the end of the entire sentence;
* The rendering network needs to minimize its reliance on large convolution kernels and global attention as much as possible, and adopt structures such as local convolution, lightweight self-attention, and resolution pyramid to control the computational load;
* For high-fidelity solutions based on NeRF/4D, it is necessary to control the rendering of each frame within a few milliseconds to a few dozen milliseconds through means such as mesh caching, frustum culling, sparse volume, and GPU optimization.

At the system integration level, real-time digital humans often need to be closely bound with  ** business knowledge, personality settings, and dialogue strategies ** :

* Manage industry knowledge, business processes, and FAQs through the Knowledge Base and RAG to ensure "correct and comprehensive narratives";
* Control the speaking style and expression boundaries through persona configuration and narrative templates to ensure that it "sounds like this person (or this brand)".
* Through multi-round dialogue strategy and conversation state management, the digital human can remember user context, confirm and follow up at appropriate times, presenting an interactive experience "like a real colleague / tour guide / lecturer".

Overall, after incorporating models such as Wav2Lip, MuseTalk, ER‑NeRF, and Ultralight‑Digital‑Human, which are specifically designed for lip synchronization, expression driving, and real‑time rendering, digital humans are accelerating their evolution from "offline video template tools" into  ** virtual entities that can respond in real time, have stable personalities, and possess professional knowledge ** , becoming the most comprehensive and application‑oriented component in the video technology system.

# 6. Time Series & Sequential Decision

In previous visual and structural modeling, we have mostly thought about problems in a "static" space: a single image, a single record, or a single text. In real business scenarios, a significant portion of core metrics evolve over time: sales volume and traffic fluctuate daily, server load and sensor readings change every second, and financial prices and macroeconomic indicators are continuously adjusted under the influence of policies and events. ** Time Series and Temporal Decision-Making ** This layer focuses on predicting the future, identifying anomalies, and characterizing structural mutations along the time axis, and making forward-looking decisions and controls based on these.

From a product perspective, this type of capability runs through key processes such as operations, planning, risk control, and scheduling: the indicator prediction module embedded in traditional BI/reporting systems, demand forecasting and safety stock recommendations in financial and supply chain planning tools, macro correlation analysis and causal relationship mining in quantitative research and analysis software, traffic and capacity forecasting on e-commerce and travel platforms, and indicator anomaly detection and alerting in operational AIOps are all typical implementation forms at this level. Next, we will expand from  **classical statistical methods** ,  **deep learning time series modeling** , **anomaly and change point detection** and **spatiotemporal sequence modeling** in four directions.

## 6.1 Classical Time Series Modeling (Statistical TS Modeling)

In many business scenarios, "time" serves as a natural main thread: sales volume changes daily/weekly, website traffic fluctuates with activities, device load rises and falls with user behavior, and sensor readings reflect subtle changes in system state. ** Classical statistical time series modeling ** addresses three core questions on this time series structure by using relatively interpretable and analyzable statistical models: ** What will the future look like? How are variables related? What is the current state of the system? ** Although deep learning has shown promise in many scenarios, traditional methods such as ARIMA, cointegration analysis, and Kalman filtering still play long-term roles in fields such as finance, supply chain, operations, and risk control, and often serve as the "base line" and interpretive tools for more complex systems.

From an application perspective, classical time series models are widely used in the indicator prediction modules of traditional BI/reporting systems, financial and supply chain planning tools, and various quantitative research software. They can directly provide future prediction intervals for single or multiple time series, and can also be used to analyze the co-variation and long-term equilibrium relationships among macro indicators, and estimate trajectories and hidden states through state space modeling. Next, we will sort out the typical usage of this type of method from three dimensions:  ** scenario ** ,  ** principle ** , and  ** model ** , and then expand on specific directions respectively.

* **Scenario**
  * Indicator Prediction: Conduct short-term or medium-term prediction on time-varying numerical values such as sales volume, website traffic, CPU load, sensor readings, etc., for decision-making in inventory stocking, production capacity planning, operation and maintenance scheduling, etc.
  * Macroeconomic and Financial Analysis: Studies the long-term relationships and short-term dynamics among macro and market indicators such as GDP, inflation rate, interest rate, exchange rate, and asset prices, to assist policy research and quantitative strategy development.
  * Process and Trajectory Estimation: In positioning, navigation, object tracking, and device monitoring, estimate and smooth the time-varying trajectory, velocity, and state, and restore the "true process" as much as possible in a noisy environment.
* **Principle**
  Classical time series methods are generally based on the idea of " **statistical assumptions + parametric structure** ":
  * Assuming that the time series satisfies certain stationarity or weak stationarity conditions, the autocorrelation structure (autocorrelation function ACF, partial autocorrelation function PACF) is used to characterize "how many past orders of history determine the current value".
  * In the multivariate case, the long-term equilibrium relationship and short-term deviation correction among multiple time series are characterized through cointegration and vector autoregressive (VAR) models.
  * For systems with severe noise and states that cannot be directly observed, a latent state and an observation equation are introduced to form a state-space model, and Bayesian inference or recursive filtering (such as Kalman filtering) is used for online estimation and prediction.
* **Model**
  The model family of this type of method is relatively well-defined, with a clear structure, facilitating interpretation and parameter tuning:
  * Univariate and multivariate AR/MA/ARIMA/SARIMA series, used for stationary/seasonal time series modeling, are the "resident members" of BI systems and traditional forecasting modules.
  * VAR/Cointegration Model, used for joint modeling and causality testing of multi-dimensional macro and financial time series, suitable for correlation analysis at the policy and strategy levels.
  * State space models, Kalman filters, Hidden Markov Models (HMM), etc., are used for trajectory estimation, device state estimation, and inference of hidden states, and are fundamental tools in engineering control and signal processing.

Overall, the advantages of classical time series modeling lie in  ** interpretability, diagnosability, and engineering controllability ** : the modeling process, hypothesis testing, and residual analysis all have mature specifications and can easily be integrated into existing BI and planning systems. Next, we will explore three directions: single/multivariate forecasting, cointegration and causality, and state space.

### 6.1.1 Univariate/Multivariate Time Series Forecasting: From ARIMA to VAR

In the most typical business scenarios, what we first encounter are one or several time-ordered indicator curves: for example, the daily sales volume of a certain commodity, the hourly PV of a website, the CPU utilization rate per minute in a data center, and the readings per second from device sensors. The goal is to provide predictions for future short-term or medium-term intervals based on historical trends and give reasonable confidence intervals. ** The AR/MA/ARMA/ARIMA/SARIMA ** series of models are precisely the standard tools designed for this purpose.

For univariate time series, ARIMA models assume that "the current value is linearly determined by the historical values of the past periods and random disturbances", and eliminate trends and seasonality by taking differences and seasonal differences of the series to make it stationary:

* The AR (Autoregressive) component characterizes "the impact of its own lags on the current value";
* The MA (Moving Average) component captures "the impact of historical error terms on the current value";
* The I (Difference) part is responsible for removing trends;
* Adding seasonal terms results in SARIMA, which can explicitly describe periodic structures such as weekly and monthly cycles.

In engineering applications, it is common to first conduct stationarity tests (such as ADF), observe ACF/PACF plots, and then select a reasonable order through information criteria (AIC/BIC) and residual diagnostics. For indicators with obvious seasonality (such as daily e-commerce sales volume, holiday traffic), SARIMA modeling is particularly suitable, and incorporating holiday features or exogenous variables can further improve forecasting performance.

When we want to model multiple related time series simultaneously, we can introduce  ** multivariate time series models ** . The representative method is VAR (Vector Autoregression) and its variants. VAR treats multiple series as a joint vector and uses their own and each other's lagged terms to jointly explain the current value, thereby capturing the mutual influence between different indicators. For example, in macroeconomic analysis, GDP growth rate, inflation rate, interest rate, exchange rate, etc. can be included in the same VAR model to study shock responses and transmission paths; in business operations, VAR can also be used to describe "how the traffic change in one channel affects other channels" and "the dynamic relationship between promotion intensity and sales volume", providing a reference for resource allocation.

In terms of product form, this type of single/multivariate forecasting capability is typically embedded in  ** the forecasting function of traditional BI/reporting systems, financial and supply chain planning tools ** : users select one or several time series, and the system automatically completes modeling and forecasting, providing forecasting intervals, residual analysis, and model diagnostic reports to assist decision-making without the need to delve into all the mathematical details behind the decision.

### 6.1.2 Cointegration and Causality: Long-Term Equilibrium among Macroeconomic Indicators

In the fields of economics and finance, many time series appear to be random walks on the surface, but there exists a certain ** stable long-term equilibrium relationship ** on a longer time scale. Typical examples include exchange rates and interest rate differentials, stock indices and macroeconomic earnings, commodity prices and cost indices, etc. Each individual series may be non-stationary; however, a certain linear combination fluctuates around a stable level in the long term. This phenomenon is known as  ** cointegration ** , which provides important clues for our understanding of the structural relationships among macroeconomic indicators.

In engineering practice, cointegration analysis typically involves several steps:

1. Conduct unit root tests on each time series to confirm that they are integrated of the same order (e.g., all I(1));
2. Conduct cointegration tests (such as the Engle-Granger two-step method, Johansen test, etc.) to determine whether there exists a non-trivial linear combination that makes the combination stationary;
3. If a cointegration relationship is found, an Error Correction Model (ECM) can be constructed to describe "how the system gradually corrects itself and returns to the equilibrium state when there is a short-term deviation from the long-term equilibrium".

Related to cointegration is the  **Granger causality test** . It is not strictly the philosophical "causality" but a statistical definition based on predictive power: if the historical information of variable X can significantly improve the prediction accuracy of variable Y, then it is said that "X Granger causes Y". By comparing the prediction errors with/without the lagged terms of a certain variable in the VAR or regression framework, the directional impact between different macro or market indicators can be evaluated. In quantitative research and macro analysis, this test is often used to identify potential leading indicators, construct factors, or validate strategic hypotheses.

From a product perspective, cointegration and causality analysis are more commonly found in  ** quantitative research and analysis software, macroeconomic analysis platforms, and financial research tools ** . They help researchers extract relatively robust structural relationships from piles of time series and map these relationships to higher-level business concepts (such as "long-term constraints of interest rates on exchange rates" and "spread regression between different assets"), serving as important bases for strategy design and risk management.

### 6.1.3 State Space Model and Hidden State Estimation: Kalman Filtering and HMM

In many real systems, the time series we observe is only  ** the appearance after noise contamination ** , while what we are truly interested in is the "system state" evolving over time behind it: for example, the real position and speed of a vehicle, the health status of equipment, the potential behavior patterns of users, etc. At this time, if we still only perform ARIMA-style modeling on the observed sequence, it will be difficult to fully utilize the understanding of the system structure. **State Space Models** are precisely proposed for this type of "hidden state + noisy observation" problem.

State space models typically consist of two parts:

* State Transition Equation: Describes how the hidden state evolves over time, which can be either linear or nonlinear;
* Observation Equation: Describes how the hidden state generates noisy observations.

Under the linear Gaussian assumption, this framework can implement recursive estimation and prediction of the state through ** Kalman Filter and Smoother ** : each step is divided into two major stages, "prediction" and "update", which combines the state distribution at the previous time step with the current observation to obtain a new state estimate. This is extremely common in navigation and positioning (such as trajectory estimation, object tracking), financial time series (such as volatility estimation), and equipment state estimation (such as health monitoring, remaining useful life prediction).

Adjacent to the continuous state space model is  ** the Hidden Markov Model (HMM) ** . The HMM assumes that the system transitions between several discrete hidden states over time, with different probability distributions for generating observed data under each hidden state. Through the forward-backward algorithm and the Viterbi algorithm, the HMM can estimate the hidden state sequence, calculate the probability of the observation sequence, and make predictions about the next state and observation. The HMM was widely used in speech recognition and text annotation in its early days, and is also commonly used in simple behavior pattern recognition and event sequence modeling. It still has advantages in certain industrial and financial scenarios - its structure is interpretable, training is stable, and it is easy to combine with domain experience.

At the system level, state space modeling, Kalman filtering, and HMM are often used as**underlying modules for trajectory estimation, device state estimation, financial and engineering control systems**and are encapsulated in larger toolchains. They are not necessarily directly exposed to end-users, but have long played the role of "invisible engines" behind products such as navigation, object tracking, industrial control, and risk measurement.

## 6.2 Deep Learning Time Series Modeling (Deep TS Forecasting)

With the continuous increase in data scale and scenario complexity, classical models that simply rely on linear and stationarity assumptions have begun to appear "inadequate" in many applications: characteristics such as a large number of nonlinear patterns, long-span dependencies, complex multivariate interactions, and the superposition of sudden behaviors and cycles have made it necessary for us to have more flexible and higher-capacity model structures.**Deep learning time series modeling**has precisely developed against this backdrop: from RNN/LSTM/GRU, to Temporal CNN/TCN, and then to time-series-specific Transformer, hybrid and hierarchical models, they together constitute the main toolbox for modern time series forecasting and modeling.

From an application perspective, deep temporal models have been widely deployed in** e-commerce traffic & sales forecasting platforms, supply-demand/capacity/scheduling forecasting systems, and cloud resource load forecasting and capacity planning tools** to provide unified and flexible forecasting solutions under complex structures involving multiple categories, multiple stores, multiple cities, and even multiple lines of business. Compared with classical models, they place greater emphasis on "end-to-end representation learning" and "global pattern modeling" and are better at handling long sequences, high-dimensional, and multi-variable scenarios. Next, we will also expand from the three dimensions of  **scenarios** ,  **principles** , and  **models** .

* **Scenario**
  * Large-scale multi-series forecasting: Thousands of sales/traffic series at the dimensions of products, stores, and cities need to be simultaneously modeled under a unified model, and support cold start and long-tail series.
  * Complex Operations and Scheduling: In systems such as power supply, water supply, transportation capacity, and shift scheduling, demand is influenced by multi-dimensional features (weather, holidays, prices, events) and has a multi-level structure (stores/cities/nationwide), requiring simultaneous consideration of both global patterns and local differences.
  * Cloud resources and infrastructure: large-scale server clusters, container platforms, network and storage loads exhibit highly non-linear and multi-peak structures, requiring high-frequency prediction and capacity planning to support SLOs.
* **Principle**
  The core of the deep temporal model lies in  **automatically learning multi-scale patterns and long-term dependencies from historical sequences and covariates** :
  * RNN/LSTM/GRU explicitly pass "memory" in the time dimension through a recurrent structure, making them suitable for capturing sequential dependencies and local temporal structures.
  * Temporal CNN / TCN uses one-dimensional convolution and dilated convolution to expand the receptive field while ensuring causality, enabling parallel training and stable gradient propagation.
  * Temporal Transformer and specially designed variants (Informer, Autoformer, TimesNet, etc.) leverage self-attention mechanisms to model complex dependencies and periodic patterns in long-sequence, multi-variable settings.
  * The hybrid and hierarchical model further introduces the structural assumptions of "global + local" and "multi-level time series", simultaneously learning global patterns and individual features within a unified framework.
* **Model**
  In terms of specific implementation, deep temporal modeling has given rise to a series of representative architectures:
  * Classical deep sequential models: autoregressive probabilistic forecasting models such as RNN/LSTM/GRU and DeepAR based on them.
  * Integrated Decomposition and Forecasting Model: N-BEATS and others enhance interpretability through explicit trend/seasonal decomposition modules.
  * Attention-based Temporal Models: Temporal Fusion Transformer (TFT), etc., combine attention, gating, and variable selection, suitable for business scenarios with multiple variables and rich covariates.
  * Long sequence Transformer models: Informer, Autoformer, TimesNet, PatchTST, etc., are specifically designed around long sequence efficiency and multi-scale modeling.

Next, we will proceed from three directions: deep sequence models, convolution and Transformer, as well as hybrid and hierarchical modeling.

### 6.2.1 Deep RNN/LSTM/GRU: From Single Sequence to DeepAR

In the early days of deep learning entering the time series domain, ** RNN/LSTM/GRU ** was the most natural choice. Similar to text and speech modeling, they "memorize" historical information by passing hidden states between time steps, allowing them to capture more complex nonlinear and long-term dependencies than traditional linear models. For single or a small number of time series, simple LSTM/GRU can achieve good prediction results when there is sufficient data; while in large-scale multi-series scenarios, ** RNN/LSTM/GRU models with shared parameters ** can be used, jointly trained on all series to learn general temporal patterns.

On this basis, autoregressive statistical models similar to **DeepAR** provide a standard framework for deep time series modeling: they input historical observations and covariates into a shared RNN/LSTM/GRU network, output the conditional distribution parameters (such as Gaussian, negative binomial distribution, etc.) of sequence values at each time step, and achieve end-to-end probabilistic prediction through maximum likelihood training. Such a design enables the model to naturally generate prediction intervals, handle irregular scales, and mix multiple sequences, which is conducive to implementation in scenarios such as e-commerce sales volume and demand forecasting.

However, RNN models have typical problems: gradient vanishing on long sequences and the inability to be fully parallelized during the training phase. Although gating mechanisms (LSTM/GRU) alleviate some of these issues, training and inference efficiency still remain factors to be weighed under extremely long time spans and high-frequency data. This has also prompted the industry and academia to explore more parallel-friendly architectures, such as TCN and Transformer.

### 6.2.2 Temporal CNN and Transformer: From Local Convolution to Long Sequence Attention

To address the efficiency and stability issues of RNNs in long sequences, ** Temporal CNN / TCN ** introduces one-dimensional convolution and dilated convolution to model temporal dependencies: by stacking multiple layers of causal convolution and gradually expanding the receptive field layer by layer, it enables the modeling of long-range history without violating temporal causality. Compared to RNNs, TCN can be highly parallelized during training, with shorter gradient propagation paths, and thus excels in training stability and efficiency, making it suitable for industrial time series prediction scenarios involving high-frequency data and requiring a large receptive field.

At a higher level of complexity,**Transformer and time-series-specific architectures**have become the protagonists in long-sequence, multi-variable time-series modeling in recent years. Directly using the standard Transformer encounters the problem of computational complexity growing quadratically with sequence length, so a series of time-series-oriented modification schemes have emerged:

* **Informer ** reduces the computational burden on long sequences through mechanisms such as probabilistic sparse self-attention and optimizes the structure for prediction tasks.
* **Autoformer** integrates trend and seasonal decomposition into the self-attention framework, aiming to enhance interpretability and stability while maintaining long-sequence modeling capabilities.
* **TimesNet** better handles complex, multi-period long sequences by enhancing the perception of cycles and patterns in the time-frequency domain or multi-scale expansion.
* **PatchTST** draws on the "patch" concept of Vision Transformer, treating continuous subsequences as patches to improve the modeling efficiency and generalization ability for long sequences.

This type of model is often particularly suitable for  ** complex time series scenarios with long sequences, multiple variables, and high-dimensional covariates ** , such as large-scale cloud resource load, multi-regional energy demand, multi-channel traffic forecasting, etc. They can simultaneously model multi-dimensional inputs, static features, and time-dependent variables within a unified architecture, and provide certain clues for subsequent interpretation and diagnosis through attention weights.

### 6.2.3 Hybrid and Hierarchical Models: Global + Local, Multi-level Time Series

In actual business, time series are rarely "isolated": they often exhibit distinct ** hierarchical structures and shared patterns ** - such as the sales hierarchy of stores/cities/regions/nationwide, the merchandise hierarchy of SKUs/categories/brands, or the organizational structure of lines of business/products/channels. If we simply model each series separately, it is difficult to leverage this hierarchical structure; while directly mixing all series together would ignore their individual differences. ** Hybrid and hierarchical models ** are precisely designed to address such issues.

A common approach is  ** the global + local model ** : learning the common patterns of all sequences (such as overall trends, holiday effects, and seasonality) through a shared "global model", while introducing local parameters or embedding vectors for each sequence or sub - population to capture individual characteristics. This structure not only avoids the data sparsity problem caused by separately training models for long - tail sequences but also retains the ability to perform fine - grained modeling on popular sequences.

Another category is  **hierarchical time series (hierarchical TS) modeling** : explicitly considering hierarchical constraints during the forecasting process (e.g., the sum of sub-levels needs to be consistent with the forecast of the upper level), and ensuring the numerical and structural consistency of forecasts at all levels through top-down, bottom-up, or joint optimization of intermediate levels. In the deep time series framework, this usually manifests as incorporating hierarchical features into input encoding, designing multi-head outputs for different levels, or using hierarchical loss functions for training.

From a product perspective, this type of hybrid and hierarchical modeling is widely used in ** e-commerce sales forecasting platforms, supply-demand/capacity/scheduling forecasting systems ** and other scenarios: the system needs to simultaneously provide forecasts at different granularities such as "single store, single product", "city level", and "national total", and maintain consistency between upper and lower levels during resource planning and KPI decomposition. The flexible structure of deep models allows such constraints to be embedded into the modeling process in an end-to-end manner, rather than relying entirely on post hoc corrections.

## 6.3 Anomaly & Change Point Detection

In time series scenarios, "predicting the future" is only part of the problem; the other equally crucial part is:  ** detecting anomalies and structural changes in real time ** . Whether it's equipment operation, business metrics, transaction behavior, or operation and maintenance monitoring, anomaly detection and change point detection are core capabilities for ensuring system stability and identifying risk opportunities. Traditionally, methods such as statistical thresholding, EWMA, and CUSUM have been widely used; as data dimensionality and complexity increase, various Machine Learning and Deep learning methods (Isolation Forest, One-Class SVM, AutoEncoder/VAE, Time Series GAN, GNN + Time Series Model) have also begun to play important roles.

From the perspective of product form, this type of capability is often embedded in  ** equipment failure early warning systems, business indicator anomaly alarm platforms (such as sudden drops in conversion rates), security attack and fraud detection systems, and operation and maintenance AIOps alarm engines ** , by monitoring multi-dimensional time series signals in real time, automatically marking suspicious points and structural changes, and combining with rules, knowledge bases, and manual decision-making processes. Next, we will continue to expand from  ** scenarios ** , ** principles ** and ** models ** from three perspectives.

* **Scenario**
  * Equipment and Industrial Systems: Monitor sensor data such as temperature, vibration, current, and pressure to detect faults and degradation trends in advance, reducing downtime and losses.
  * Business and Operational Metrics: Monitor key metrics such as PV/UV, conversion rate, order volume, latency, error rate, etc., quickly detect sudden drops, sudden increases, and abnormal fluctuations, and provide alerts for the operations and technology teams.
  * Security Department: Analyze time series such as login behavior, transaction sequences, and access patterns to identify potential attacks, cheating, and fraud.
* **Principle**
  Anomaly and change point detection essentially involves searching for significant deviations and structural mutations from the "normal pattern":
  * For point anomalies and sequence anomalies, it is possible to determine whether the current observation falls outside the "normal region" through statistical distribution fitting, density estimation, or boundary learning.
  * For change points, we focus on abrupt changes in the statistical properties (mean, variance, correlation structure, distribution, etc.) of time series on the time axis and attempt to locate the time position where the change occurs.
  * In high-dimensional and multi-point networks, it is necessary to incorporate the dependency structure (such as topology and correlation) among multiple time series into the modeling to avoid confusing local anomalies with overall trends.
* **Model**
  From the perspective of method families, it can be roughly divided into statistical methods, one-class/isolation learning methods, reconstruction-based deep models, and graph + time series combination models:
  * Statistical anomaly detection: Threshold, EWMA, CUSUM, etc., are extremely efficient for univariate or simple scenarios and are the foundation of traditional monitoring systems.
  * Machine Learning methods: Isolation Forest, One-Class SVM, etc., are used to characterize the "normal region" in the multi-dimensional feature space and isolate abnormal samples.
  * Deep reconstruction models: AutoEncoder / VAE / Temporal GAN, which learn to reconstruct normal sequences and mark anomalies when the reconstruction error is large.
  * Graph Neural Network + Temporal Model: In scenarios such as sensor networks and microservice metrics, introduce graph structure and temporal model to jointly learn normal patterns, strengthening the identification of topology-related anomalies.

Next, we will focus on three directions: point/sequence anomaly, change point detection, and multi-dimensional and graph structure.

### 6.3.1 Point Anomalies and Sequence Anomalies: From Statistical Thresholds to Reconstructive Models

The most intuitive form of anomaly detection is  ** point anomaly ** : the observed value at a certain time point deviates far from the historical normal range (e.g., CPU usage suddenly spikes to 100%, transaction amount increases abnormally, sensor reading jumps instantaneously). In traditional methods, the most common approach is to fit a statistical distribution or sliding statistics (mean, variance, quantile) to historical normal data, and then set thresholds or control charts (e.g., EWMA, CUSUM) based on this. When the current observation exceeds the acceptable range, an alarm is issued. The advantages are simple implementation, low computational cost, and easy interpretation, so it is still widely used in a large number of operation and maintenance monitoring and industrial systems.

When the dimensionality increases or the patterns become more complex, one can introduce  ** one-class/isolation learning methods such as Isolation Forest, One-Class SVM ** : these methods learn an aggregation region (or boundary) on "normal samples" and consider points outside this region as anomalies. By extracting statistical features (such as window mean, variance, frequency domain features, etc.) from sliding windows of sequences, these methods can also be used to identify local "sequence anomalies" (i.e., behavior deviating from the normal pattern over a period of time), and are suitable for scenarios with multi-dimensional metrics and where it is difficult to precisely define the distribution shape.

Under the deep learning framework,** methods such as AutoEncoder/VAE/temporal GAN based on reconstruction error ** provide more flexible options:

* Train a "compression - reconstruction" model using AutoEncoder or VAE on a large number of normal sequences to enable it to learn to reconstruct normal patterns;
* During online monitoring, input a new time window into the model. If the reconstruction error increases significantly, it is considered that an anomaly exists in this interval;
* Temporal GAN-based methods, on the other hand, learn to generate normal sequences and search for abnormal signals in the discriminator's decision results or generation errors.

These methods can adapt to highly nonlinear patterns and complex covariate structures, and are particularly suitable for constructing a unified anomaly detection engine on  ** multi-dimensional business metrics and complex device sensor data ** .

### 6.3.2 Change Point Detection: Structural Break and Event Effectiveness

Unlike point anomalies and local anomalies, **Change Point Detection** focuses on abrupt structural changes in time series, such as a mean shifting from one level to another, changes in volatility, and adjustments to periodic and correlation structures. Such changes often correspond to certain events or state transitions in the real world, such as configuration changes, implementation of new strategies, policy adjustments, changes in production processes, market regime shifts, etc., and are extremely crucial for business diagnosis and causal analysis.

In traditional statistical methods, change point detection often relies on techniques such as likelihood ratio test, CUSUM, Bayesian Online Change Point Detection (BOCPD), etc.

* By fitting models with different parameters (such as different means/variances) before and after different time points, compare the goodness of fit between the "no change point hypothesis" and the "change point hypothesis";
* In online scenarios, the posterior probability of "whether a change point has occurred up to the current paragraph" is recursively updated at each time point, and an alarm is triggered once it exceeds the set threshold.

Under more complex settings, deep representation learning can be combined with segmentation models to treat change point detection as  **a sequence segmentation problem** : extract features using neural networks, then find segment boundaries in the feature space, or directly train a model to predict the probability that a certain time point belongs to a "change point". This is particularly useful for business metrics that exhibit multiple forms of change (not just mean/variance changes) and are difficult to characterize using simple statistical assumptions.

In the product system, change point detection is usually integrated into  ** business indicator analysis platforms, A/B experiment analysis systems, and configuration and policy change monitoring tools ** : when key indicators exhibit structural changes, the system can automatically mark potential change points and associate them with corresponding change events (such as version releases, parameter adjustments, and policy implementations), providing clues for subsequent root cause analysis.

### 6.3.3 Multidimensional Time Series and Graph Structure: Joint Modeling of GNN + Time Series Model

In modern distributed systems and Internet of Things scenarios, we often face  ** multi-point, multi-dimensional time series with associated topological structures ** : for example, multiple measurement points in sensor networks, various service metrics in microservice architectures, and multiple nodes and edges in power distribution networks/transportation networks. At this time, performing anomaly detection on each time series individually and one by one can easily lead to misjudgment of local fluctuations or overlook the overall pattern - true anomalies are often manifestations of "local - global inconsistency" or "incoordination in the topological structure".

To this end, in recent years, a large number of ** combined methods of graph neural networks (GNN) + time series models ** have emerged:

* First, based on the real topology (physical connections, network topology) or a correlation graph estimated from data, construct a graph structure that represents the relationships between multiple points;
* At each time step, GNN is used to perform message passing on node features (the time-series values of each point and its local context) to learn spatial correlation features;
* Then, input the encoded representation of the graph into a temporal model such as RNN, TCN, or Transformer to capture dynamic patterns in the time dimension;
* Finally, anomaly scoring or change point detection is performed on the joint representation to achieve  **spatiotemporal joint anomaly identification** .

This framework is particularly applicable in scenarios such as  ** sensor network monitoring, anomaly detection of microservice metrics, and spatio-temporal anomaly detection in urban computing ** : it can distinguish between "global changes" (such as an increase in the overall system load) and "local anomalies" (such as abnormal congestion at a certain node), and can also better identify topology-related anomaly patterns (such as link-level issues and regional network failures).

At the engineering level, this type of method typically appears as  ** a high-level capability of the AIOps alarm system for operation and maintenance, the Security Department platform, and the equipment group monitoring system ** , combining basic statistical monitoring, rule systems, and expert knowledge to provide a more intelligent and context-aware anomaly discovery mechanism for complex systems.

## 6.4 Spatio-Temporal Modeling

In many critical business scenarios, simply modeling "time" is not enough:  ** "when" and "where" coexist in parallel ** , and the two are highly coupled. Urban traffic flow is jointly influenced by road network structure and temporal patterns, while meteorology and air quality depend on both temporal evolution and geographical proximity and atmospheric flow fields; logistics, shared bicycles, and ride-hailing dispatching require simultaneous consideration of the spatio-temporal distribution of demand and road/regional structure. ** Spatio-Temporal Modeling ** is precisely a systematic approach to such "time + space" joint modeling problems.

Compared with pure time series models, spatio-temporal models need to explicitly incorporate**spatial dependency structure**into consideration: the traffic flow of adjacent road segments, the air quality of neighboring monitoring stations, and the load and status of connected nodes are usually more correlated than points that are farther apart. For this reason, structures such as graph neural networks (GNN) and convolutional LSTM (ConvLSTM) are widely used for feature learning that combines both spatial and temporal dimensions. At the product level, this type of capability supports **a large number of critical applications such as urban computing platforms (traffic/pedestrian flow prediction), meteorological/environmental prediction systems, logistics route planning, and shared bike/ride-hailing dispatch platforms** .

* **Scenario**
  * Traffic flow and pedestrian flow prediction: Based on the structure of road networks or subway networks, predict vehicle and pedestrian flows at different time periods to assist in traffic signal optimization, congestion management, and dispatching decision-making.
  * Meteorological and environmental monitoring: On geographical grids or monitoring station networks, predict the spatio-temporal distribution of future temperature, rainfall, wind, air quality, etc., to provide support for forecasting and decision-making.
  * Logistics and Mobility Scheduling: Predict order demand, vehicle distribution, and the load status of warehouses/stations in urban areas or road network structures, providing a basis for route planning, vehicle scheduling, and capacity allocation.
* **Principle**
  The core of spatio-temporal sequence modeling is  **to simultaneously learn spatial correlations and temporal dynamics within a unified framework** :
  * In the spatial dimension, the graph structure or convolution structure is used to characterize "who is related to whom", and based on this, message passing and feature aggregation are performed;
  * In the time dimension, RNN, TCN, Transformer, or specialized temporal structures are used to characterize dynamic changes;
  * The two can be cascaded (first perform spatial operations, then temporal operations), or intertwined or operate simultaneously (such as spatio-temporal convolution, spatio-temporal attention).
* **Model**
  Most typical spatio-temporal models adopt the combined form of "GNN + temporal model" or "convolution + LSTM":
  * Graph Neural Networks + Temporal Models: ST-GCN, DCRNN, Graph WaveNet, ST-Transformer, etc., capture spatial dependencies through graph convolution or graph attention, and then capture temporal dynamics using a temporal structure.
  * Convolutional LSTM models: ConvLSTM, Conv-TT-LSTM, etc., embed spatial convolutional gating in temporal recursion to jointly model spatio-temporal local features.

Next, we will proceed from three directions: spatio-temporal tasks and data representation, GNN + temporal models, and convolution LSTM and spatio-temporal convolution.

### 6.5.1 Spatiotemporal Tasks and Data Representation: From Road Networks to Geographic Grids

Before delving into specific models, the primary issue to be addressed in spatio-temporal sequence modeling is  ** how to represent spatial structure ** . Unlike the one-dimensional time axis, spatial structure can take the form of regular grids, irregular graphs, or hybrid forms.

* In traffic scenarios, roads and intersections naturally form a directed or undirected graph: nodes represent road segments or intersections, and edges represent road connections and driving directions; each node has a set of features at each time step, such as traffic flow, average speed, congestion index, etc.
* In meteorological and air quality forecasting, regular geographical grids (such as latitude and longitude grids) can be used, or the adjacency relationships between monitoring stations can be constructed into a graph structure, with edge weights defined based on geographical distance, wind direction, or correlation.
* In logistics and shared mobility scenarios, cities can be divided into grids or regional units, each of which has characteristics such as the number of orders and the number of active vehicles over time, and is connected spatially through adjacency relationships or actual road distances.

This unified representation of ** spatial structure + time series ** enables many different scenarios to be modeled as similar problems: given historical spatio-temporal sequences, predict the state of each node or grid over a number of future time steps. Subsequent model design (whether GNN + time series model or ConvLSTM) is carried out from this unified perspective.

At the product level, the abstraction of this layer is often encapsulated in **the data layer and modeling layer of urban computing platforms, meteorological/environmental prediction systems, and path planning and scheduling platforms** : business parties only need to know "how we predict future traffic/demand on road networks/grids", while the underlying data representation and spatio-temporal fusion are uniformly handled by the modeling framework.

### 6.5.2 Graph Neural Networks + Temporal Models: ST-GCN, DCRNN, Graph WaveNet, etc.

When modeling spatio-temporal sequences on graph structures, the most mainstream approach currently is the combination of  ** graph neural networks (GNN) + temporal models ** . Representative models include  ** ST-GCN, DCRNN, Graph WaveNet, ST-Transformer ** , etc., and their common characteristics are:

* In the spatial dimension, methods such as graph convolution (GCN), graph attention (GAT), or spectral domain convolution are used to perform "neighborhood aggregation" on the node features at each time step, thereby capturing the influence of spatial dependencies and topological structures;
* In the time dimension, sequence modeling of node-level features is performed through RNN (such as GRU/LSTM), TCN, or Transformer to capture temporal trends and periodicity;
* Through alternating stacking or joint design, the model can learn local and global patterns at multiple spatio-temporal scales.

For example, **DCRNN (Diffusion Convolutional RNN) **combines graph convolution with gated recurrent units, uses diffusion convolution to simulate the propagation of information on road networks, and then captures the dynamics of the time dimension through RNN, making it highly suitable for tasks such as traffic flow prediction. **Graph WaveNet **introduces Self-Adaptation graph structure learning and multi-scale modeling on the basis of graph convolution and temporal convolution to improve adaptability to complex road networks and irregular topologies. **ST-Transformer **and other models introduce self-attention mechanisms into spatio-temporal modeling, simultaneously considering the correlations between different time and spatial positions through spatio-temporal attention modules.

In real-world systems, this type of GNN + temporal model is widely deployed in ** urban traffic and pedestrian flow prediction platforms, shared mobility scheduling systems, complex IoT network monitoring ** and other products. They typically serve as one of the core prediction engines, forming a closed loop with rule systems, simulation models, and business strategies, enabling scheduling and planning to consider both the global structure and respond to local changes.

### 6.5.3 Convolutional LSTM and Spatiotemporal Convolution: ConvLSTM, Conv‑TT‑LSTM, etc.

Another important route is spatio-temporal modeling based on **Convolutional LSTM (ConvLSTM)** and its variants. Unlike standard LSTM, which passes one-dimensional vectors between time steps, ConvLSTM uses convolutional operators in its gating structure, allowing both the hidden state and input to remain multi-dimensional tensors (such as feature maps on a spatial grid). In this way, the state update at each time step includes both temporal recurrence and local convolutional aggregation in the spatial dimension, enabling natural modeling of spatio-temporal local patterns.

On this basis,**improved models such as Conv-TT-LSTM**attempt to enhance the model's expressive power and efficiency through mechanisms such as tensor decomposition, parameter sharing, and multi-scale convolution, to adapt to larger-scale and more complex spatio-temporal data. For example, in weather forecasting, ConvLSTM can be stacked in multiple layers to perform spatio-temporal recursion on multi-channel meteorological element maps (temperature, humidity, wind direction, etc.), predicting the spatial distribution of the next few hours or days from several historical frames; in traffic and environmental monitoring, road networks or monitoring points can also be mapped onto regular grids, and models such as ConvLSTM can be used for prediction.

Compared with GNN + time series models, the ConvLSTM series is more commonly used in **scenarios with regular grid structures and obvious local spatial smoothness** , such as meteorological radar echo prediction, air quality grid forecasting, video frame-level prediction, etc. Its advantages lie in relatively straightforward implementation, ease of leveraging existing convolutional network infrastructure for acceleration and deployment, and ease of collaborative use with visual models such as CNN/ViT, such as combining convolutional features and time series recursion in remote sensing image spatio-temporal modeling.

In terms of product form, models in this direction are mostly used in  ** meteorological/environmental prediction systems, remote sensing spatio-temporal analysis platforms, video and image spatio-temporal prediction ** , etc., often exposing their capabilities to upstream in the form of "future spatio-temporal scenario prediction maps" and becoming an important input for business decision-making and visual analysis.

# 7. Agents & Tool Use Layer (Agents & Tool Use)

In the previous layers of capabilities such as vision and language, models mostly still take the form of "passive response" - receiving input and providing output. In many real-world business scenarios, what we need is an  ** intelligent agent (Agent) that can actively plan, call external tools, and string together workflows ** : it can not only understand/ read/ listen, but also "decide what to do next" on its own, such as looking up information, running code, reading and writing files, calling internal systems, and then integrating, explaining, and feeding back the results to the user.

This layer can be understood as the key glue layer that "transforms the foundation model into an actionable system": through  ** structured tool invocation interfaces, workflow orchestration, multi-Agent collaboration, and human-in-the-loop mechanisms ** , it expands the LLM from a powerful "cognitive kernel" into a "digital employee" capable of completing end-to-end tasks.

## 7.1 Tool Calling / Function Calling

In the era of pure text where there was only reading without writing and only talking without doing, LLM was more like a "super conversationalist": it could understand questions, give advice, write code, and list plans, but all the "actual execution" tasks - querying databases, running scripts, generating files, and invoking cloud services - still had to be taken over and completed manually. And ** Tool Calling / Function Calling ** has for the first time enabled the model to "take action" within the safety boundary: automatically generating structured parameters based on natural language to call external capabilities such as search engines, databases, computing engines, and image/audio/video generation services, then organizing and returning the execution results, thus forming a closed loop of "understanding → decision-making → execution".

From a product perspective, tool invocation is the "chassis capability" of most Agent systems: OpenAI Assistants API, LangChain, LlamaIndex, AutoGen, and Agent platforms of various cloud providers are essentially building a layer of runtime on top of LLMs, focusing on  ** how to define tools, how to enable models to correctly select tools, and how to handle errors and retries ** . The following also organizes this layer of capabilities from three perspectives:  ** scenarios ** ,  ** principles ** , and  ** models ** , and expands on the three directions of "tool invocation interface design", "tool selection and strategy", and "typical tool types" in the subsequent sections.

* **Scenario**
  * Intelligent Question Answering and Retrieval Enhancement: The model automatically decides whether to call retrieval tools (vector/keyword search), query the enterprise's internal Knowledge Base, or conduct public network searches based on user questions, and integrates the retrieved documents and FAQs into the final answer.
  * Data and Report Automation: In response to requests such as "Help me check the sales volume during this period and create a chart" and "Calculate the risk indicators for this portfolio for me", the model automatically generates SQL or analysis parameters, invokes the database and computing engine, and returns charts and conclusions.
  * Document and File Operations: Automatically read PDF/Word/Excel/database tables, extract and summarize key information, or generate new files (such as reports, contracts, plans) as instructed, and upload/store them to the specified location via tools.
  * Media Generation and Processing: Invoke image/audio/video/3D generation services based on text instructions, or perform operations such as clipping, compression, transcoding, and watermarking on existing media, forming a content pipeline for one-click "copywriting + design + export".
* **Principle**
  The core of tool invocation is:  **using natural language to drive structured function calls** .
  * First, expose the name, description, and parameter structure (type, required fields, enum values, etc.) of external tools to the LLM in the form of JSON Schema or function signature.
  * When a user makes a request, the LLM not only needs to understand the semantics but also determine "whether a tool needs to be invoked", "which tool(s) are needed", and "how to fill in the parameters of these tools".
  * Once the model decides to call a tool, it generates a set of structured parameters (usually JSON), which are then used by the runtime to actually execute the external API / program. The execution result is returned to the model in a structured form, allowing the model to continue reasoning based on the result or generate the final answer.
  * To ensure safety and robustness, the system needs to handle parameter validation, timeout, error return, retry, and fallback during this process, and perform permission and audit control on calls that may involve security/privacy.
* **Model**
  The models and frameworks that support this capability mainly fall into three categories:
  * LLMs that support Function Calling, such as GPT-4.1 / o series, natively understand "tool signature + JSON Schema" at the decoding level and can actively or passively generate structured call parameters at appropriate times.
  * Tool-Augmented Reasoning Paradigm: For example, ReAct and Toolformer, weave "thinking + tool invocation" into the same reasoning chain, treating tool use as part of an intermediate step rather than simple pre/post-processing.
  * Engineering Framework and Runtime: OpenAI Assistants API, LangChain, LlamaIndex, AutoGen, Agent platforms of various cloud providers, etc., provide infrastructure for tool definition, invocation routing, state management, error handling, and log auditing, enabling developers to focus on "which tools to expose" and "how to abstract business APIs" without having to build the runtime from scratch.

### 7.1.1 Tool Invocation Interface: From Natural Language to Structured Function Invocation

An available tool invocation system first requires a clear, standardized, and LLM-friendly "tool interface layer". It is responsible for wrapping APIs, scripts, and services from the external world into "functions" that the model can understand and safely invoke, enabling the model to "state" the tools it wishes to invoke and their parameters as if writing pseudocode.

* **Tool Definition and Parameter Mode**
  At the interface layer, each tool is typically defined using a structure similar to JSON Schema or function signature, including name, description, parameter fields (properties), type (string / number / boolean / array / object), whether it is required (required), value range or enumeration, etc.
  On the one hand, this information is used to drive type checking in the front-end/SDK; on the other hand, it is directly provided to the LLM to help the model "learn" how to correctly fill in parameters. The clearer the description and the more reasonable the constraints, the more standardized the calls generated by the model and the lower the error rate.
* **LLM Generates Structured Parameters**
  When a user makes a request like "Help me look up the revenue for Q3 2024 and draw a bar chart split by region", the model first needs to infer that this requires at least a "report query tool" (to access data) and possibly also a "chart generation tool" (to draw the chart). For each tool, it must extract and map structured parameters from the original language, such as time range (start_date/end_date), dimension (region), metric (revenue), chart type (bar), output format, etc., and then output them in JSON to the runtime.
  In this process, the model is essentially performing integrated reasoning of "natural language → task planning → parameter extraction/filling", so the natural language prompts, parameter examples, and few-shot samples in the tool description are all crucial.
* **Tool Execution and Result Postback**
  Upon receiving a JSON call output by the model during runtime, parameter validation and security checks will be performed first, followed by the actual invocation of the backend API or program. After execution is completed, the results will be encapsulated into structured objects (such as query result tables, file URLs, media resource IDs, etc.) and returned to the model.
  Subsequently, the model will transform these raw results into user-readable explanations or further process them, such as generating summary reports, performing natural language analysis, embedding chart annotation descriptions, etc. For the model, tool results are only part of the intermediate information, and it still has to be responsible for "understanding the results + explaining the results".

### 7.1.2 Tool Selection and Strategy: Making Decisions in a Multi-Tool World

When there is only one tool in the system, "whether to use the tool" is the only question. However, in real-world Agent applications, there are often dozens or even hundreds of tools: retrieval from different data sources, business APIs from different departments, and generation/analysis capabilities from different technical domains, which leads to a new challenge:  ** how the model makes reasonable choices and orchestrations in a multi-tool environment ** .

* **Tool Selection and Routing**
  First, the model needs to determine "whether the current request requires tool invocation" and "which tool (or tools) to invoke". This is typically achieved by listing descriptions of available tools in the system prompt and providing typical examples, enabling the model to learn to select appropriate tools based on user intent.
  For scenarios with a large number of tools and high similarity in descriptions, many frameworks introduce a "tool router" (such as pre-filtering based on vector retrieval or rules) to first screen out several candidate tools from a large list and then expose them to the LLM for selection, thereby reducing the model's burden and the probability of misselection.
* **Multi-Tool Sequencing and Combination**
  Complex tasks often require multiple tools to work together. For example, "researching major listed companies in a certain industry and generating a report containing financial comparison charts" may involve search engines, financial report databases, calculation engines, chart generation tools, document export tools, etc.
  In this case, the model needs to perform a lightweight task planning: first use which tool to obtain a list, then query detailed information for each item in the list one by one, then merge data, perform calculations and visualization, and finally call the export tool to generate the report. Typical practices include the ReAct/Planner-Executor approach, which allows the model to gradually complete the combined invocation of tools in the cycle of "Plan—Act—Reflect".

### 7.1.3 Typical Tool Types: The Capability Jigsaw from Retrieval to Media Generation

Different types of tools provide the Agent system with "external brains" in different dimensions. From an engineering practice perspective, the following types of tools are almost "standard equipment" for all complex applications.

* **Retrieval Tools: Vector and Keyword Search**
  Retrieval tools are responsible for extending "memory" to the external world:
  * Keyword search is suitable for traditional documents and business databases with good structure and clear fields.
  * Vector search, on the other hand, builds semantic indexes for unstructured text, code, conversation records, and even MultiModal Machine Learning data through embedding, supporting "fuzzy but semantically relevant" retrieval.
    In the RAG scenario, the LLM pulls context relevant to the user's question through retrieval tools, and then conducts reasoning and generation on this basis, significantly improving the timeliness and accuracy of responses.
* **Code Execution and Computing Engine**
  Code execution tools (such as Python/JS sandboxes, Notebook executors) enable LLMs to "write a piece of code and run it immediately", solving complex problems such as computation, data processing, numerical simulation, and visualization.
  The model is responsible for generating code and input parameters, while the execution environment is responsible for security isolation, resource limitation, and result collection. These tools are crucial in scenarios such as Data Analysis, quantitative research, automated reporting, scientific computing, and Agent self-verification (using code to verify answers generated by the model).
* **File and Data Source Access**
  File read and write tools are responsible for bringing external file systems and data sources into the Agent's view: reading PDF/Word/Excel, accessing database tables, invoking internal business APIs, etc. The model uses these tools to obtain real business data, and then performs induction, comparison, and report generation.
  There are also supporting file writing and management tools: they persistently store generated reports, charts, PPTs, code, etc., and return links or IDs for users' subsequent access and integration.
* **Media Generation and Processing Tools**
  Media generation tools add the "creation" and "design" arms to the Agent:
  * Image/Video Generation and Editing: Automatically generate accompanying images, posters, and storyboards based on text, or perform operations such as cropping, adding subtitles, and watermarking on existing media.
  * Audio Generation and Processing: TTS, Dubbing, Music Generation, Audio Enhancement, and Editing.
  * 3D/Engineering Tools: Generate simple 3D scenes, CAD sketches, UI prototypes, etc.
    In content production, marketing design, education and training, games, and multimedia applications, these tools bring "from idea to finished product" closer to an automated assembly line.

Overall, tool invocation and execution expand LLM from a "language model" to a "general-purpose controller with action interfaces": the model understands requirements and the environment through language, performs real operations through tools, and continuously refines strategies through feedback. When combined with appropriate workflow orchestration and multi-Agent collaboration (see 7.2), it forms the infrastructure for a new generation of intelligent applications.

## 7.2 Workflow Orchestration and Multi-Agent Collaboration (Workflow & Orchestration)

With the ability to call tools, LLMs are no longer just "question answerers" but can become "execution units" for specific tasks. However, real-world business operations are often far more complex than single conversations: a complete litigation analysis, a market research project, a round of A/B experiment configuration, or an end-to-end operation and maintenance process usually require multiple steps, multiple tools, and even long-term participation from multiple parties. In such cases, the single LLM + tool model becomes strained and requires further  ** workflow orchestration and multi-agent collaboration ** .

From a system perspective, the responsibilities of this layer are:  ** to abstract a complex, multi-step, multi-party business process into a workflow graph that can be understood and manipulated by LLMs ** , and then schedule one or more Agents on this graph, in conjunction with human intervention, to jointly complete tasks. Typical implementations include the Planner-Executor type Agent architecture, Agents with reflection/self-correction capabilities, and graph-based Workflow Orchestrators; the corresponding Product Forms are various types of automated report generation and operational automation platforms, low-code workflow + LLM integration, complex business process robots, automated operation and maintenance systems, etc.

* **Scenario**
  * Report and Content Pipeline: Automate or semi-automate the multi-step content production process from "Receiving Requirements → Retrieving and Data Pulling → Analysis and Visualization → Report Writing → Review and Revision → Export and Distribution".
  * Business process automation: such as "product analysis → competing product monitoring → activity strategy generation → implementation configuration" in e-commerce operations, and "monitoring and alerting → root cause analysis → mitigation measure execution → review report" in operation and maintenance scenarios, etc.
  * Cross-role collaboration: Enables Agents from different domains (legal, finance, technology, operations) to work together on a complex project, such as M&A due diligence, investment and financing material preparation, and large project bid document compilation.
* **Principle**
  The core of workflow and multi-Agent collaboration is to add an additional layer on top of the LLM  **for structured control and state management** :
  * Break down complex tasks into several sub-tasks with dependencies, represent them using structures such as DAGs, finite-state machines, or directed graphs, and configure trigger conditions, inputs and outputs, and required agents/tools for each node.
  * The Planner-type Agent or the upper-level orchestrator determines when to trigger which node, with which Agent or tool, and dynamically adjusts the subsequent path (conditional branches, loops, error fallback) based on the execution results.
  * Introduce Human-in-the-loop at critical junctures to manually confirm and edit high-risk decisions and critical outputs, and feed human feedback back into the system for updating strategies or fine-tuning models.
* **Model**
  The main technical directions supporting this layer include:
  * Planner-Executor Agent Architecture: A "planning agent" is responsible for task decomposition and path design, and one or more "execution agents" are responsible for the implementation of specific steps.
  * Reflection / Self-correction Agent: Continuously review its own performance during execution, reflect on and correct unreasonable intermediate results, and reduce the silent spread of "confidence errors".
  * Graph-based Workflow Orchestrator: Models the entire task process as a graph structure, introduces mechanisms such as node states, edge conditions, parallel/serial control, etc., to transform LLM calls into one or more nodes in the graph rather than the sole control center.

### 7.2.1 Task Decomposition and Planning: From "One-Sentence Requirement" to Executable Process

What users usually give to agents is a highly compressed natural language requirement, such as "Help me conduct a market research on the new energy vehicle industry and output a PPT", which actually encompasses a large number of steps such as retrieval, screening, analysis, visualization, typesetting, and multiple rounds of revisions. How to automatically construct a clear and executable workflow based on this sentence is the first step in workflow orchestration.

* **From Natural Language to Subtask Graph**
  Planner-type Agents first need to "unfold" the requirements: by combining built-in templates, historical cases, and tool lists, identify key stages (such as Information Gathering, Data Analysis, Structural Design, Content Writing, Review and Export), and further refine them into executable subtasks (such as "Retrieve 5 authoritative industry reports from the past year", "Pull sales data from the past 3 years and segment by vehicle model", "Generate 3 comparison charts", etc.).
  The dependencies and scheduling logic among these subtasks will be explicitly represented as a graph or a finite-state machine: which can be executed in parallel, which must be executed sequentially, at which nodes human confirmation is required, and under what conditions rollback or retry is needed.
* **Conditional branches, loops, and exception paths**
  Real-world processes are often not linear pipelines but instead include **conditional branches** (e.g., "if no reports of sufficient quality are retrieved, change the keyword or switch the data source"), **loops** (e.g., "continuously attempt to rewrite and compress until the report length meets the limit"), and **exception paths** (e.g., "when a data source is unreachable, switch to an alternative source or use an estimation method").
  This requires the workflow orchestration layer to be able to express control flow semantics such as if/else, while/for, try/catch on the graph structure, and allow the Planner Agent or the upper-level orchestrator to make decisions based on real-time results during the execution process, rather than simply planning all steps at the beginning once and for all.
* **Connection with Tool Invocation**
  Task decomposition and planning are closely linked to tool invocation in 7.1: When generating subtasks, the Planner often specifies both "which tools/agents are required for this task" and "the input and output formats of this node" simultaneously, laying the foundation for subsequent automatic parameter filling and tool execution.
  Some systems adopt an explicit two-phase approach of "Plan + Execute": First, the Planner outputs a machine-readable plan (such as a JSON workflow description), and then the Executor strictly invokes tools and agents according to the plan; other systems adopt the ReAct style, weaving "think - tool invocation - observe - think again" into the same conversation to achieve more flexible Self-Adaptation execution.

### 7.2.2 Multi-Agent Collaboration: Enabling the "Virtual Team" to Perform Their Respective Duties

While a single large model is powerful, in complex business scenarios, different domains often require different knowledge structures, style preferences, and security policies. ** The concept of multi-Agent collaboration ** involves breaking down a "large and comprehensive" intelligence into multiple "specialized and refined" roles: some are responsible for planning, some for execution, some for review, and some for domain-specific professional judgment, forming a virtual team composed of Agents + tools + humans.

* **Role Division: Planning, Execution, and Review**
  In a typical multi-Agent process, common roles include:
  * Planning Agent: Responsible for understanding user requirements, designing the overall plan, breaking down sub-tasks, and dynamically adjusting the path based on results during the execution process.
  * Execution Agent: Conduct in-depth optimization around certain tools or sub-domains (such as Retrieval Agent, Data Analysis Agent, Content Writing Agent), and complete specific steps as required by the plan.
  * Review Agent: Checks and revises intermediate and final outputs from perspectives such as structural integrity, logical consistency, style uniformity, and risk control, similar to a "virtual editor/Reviewer".
* **Domain Expert Agent Collaboration**
  For highly specialized domains such as law, finance, technology, and operations, domain expert Agents can be further segmented: for example, "Legal Counsel Agent", "Investment Research Analysis Agent", "Cloud Native Operations Agent", "Advertising Optimization Agent", etc.
  These Agents can participate in project-based collaboration based on domain-specific Knowledge Bases, tools, and even specialized fine-tuned models: for instance, in an investment and financing document, the Technology Agent is responsible for the technical feasibility section, the Finance Agent for the financial model and valuation, the Legal Agent for compliance and risk disclosure, the Operations Agent for market and growth strategies, and the Master Control Agent for summarizing and unifying the style.
* **Collaboration Protocol and Message Routing**
  The key to multi-agent collaboration also lies in "who talks to whom and when". The system requires a message routing and coordination mechanism:
  * Determines which Agent should handle a user request or intermediate result.
  * Maintain shared context and respective private memories.
  * Controls parallel and serial execution, as well as conflict resolution (such as how to arbitrate when different Agents propose conflicting suggestions).
    This type of capability is typically provided by an upper-level orchestrator or a "management Agent", while frameworks such as LangChain and AutoGen provide infrastructure at the engineering level, including dialogue routing, multi-Agent conversations, role setting, etc.

### 7.2.3 Human-in-the-loop: Keeping the risk gateway in hand

Even if workflows and multi-agent collaboration are highly intelligent, human judgment is still indispensable in real business operations, especially in ** high-risk, high-cost, and high-sensitivity ** scenarios, such as legal compliance, financial decision-making, medical advice, large-scale production changes, and public opinion response. ** The design of Human-in-the-loop ** aims to strike a balance between automation and controllability: automate what can be automated, and pause for human confirmation when necessary.

* **Manual Confirmation of Key Steps**
  In the workflow diagram, several "manual approval/confirmation nodes" are usually explicitly marked:
  * For example, when automatically generating a contract, dual confirmation from legal and business leaders is required before issuance;
  * In the automated operation and maintenance system, for operations involving production environment changes, batch restarts, and configuration modifications, a duty engineer must click to confirm;
  * In content generation scenarios, manual review is required for a large amount of publicly released or brand-sensitive content. The Orchestrator will pause automatic execution at these nodes, send intermediate results to the corresponding human roles, and continue the subsequent process after receiving feedback.
* **Feedback-driven strategy update**
  Humans not only "press approve or reject" at a certain moment, but more importantly, the content of the feedback can be absorbed by the system:
  * Compare the manually modified version with the original output, record them as "positive and negative examples", and use them for subsequent prompt optimization or model fine-tuning.
  * Based on statistical analysis, identify which types of tasks/steps are most likely to be repeatedly modified manually, and then optimize the corresponding Agent's prompts, tool combinations, or workflow design.
  * In extreme or exceptional cases, humans can add "blocklist / allowlist / special rules", directly influencing the system's strategy selection in similar situations.
* **Risk Classification and Observability ** Finally, human-in-the-loop also requires a clear set of risk classification and observability mechanisms:
  * Based on dimensions such as task type, impact scope, amount scale, and sensitive information involved, processes are classified into different risk levels, corresponding to different intensities of human intervention (such as read-only review, mandatory approval, multi-level approval).
  * Through logs, audits, visual dashboards, and other means, enable operations/management personnel to track at any time which tasks are running, where they are in the process, where manual intervention has been triggered, and what failures and manual corrections have occurred historically.
    These capabilities not only enhance the system's acceptance within the enterprise but also provide a foundation for subsequent compliance reviews and responsibility allocation.

Overall, Tool Invocation and Execution (7.1) addresses the issue of "single-step actions", while Workflow Orchestration and Multi-Agent Collaboration (7.2) attempt to answer the question of "how to string together multiple steps, enable long-term collaboration among different roles, and ensure controllable operation". The combination of these two, along with Human-in-the-Loop and good engineering practices, forms the foundation of a new generation of intelligent applications for real-world business scenarios.

# 8. Retrieval Augmentation and Knowledge Layer (Retrieval & Knowledge)

In the previous Visual and Understanding layer, the model mainly relies on "knowledge learned from its own parameters" to understand and generate content. However, in real business scenarios, many problems cannot be solved solely by "memory": internal enterprise regulations change daily, laws and industry standards are continuously updated, and the historical records of a particular customer only exist in the internal database. At this time, relying solely on the knowledge "memorized" by the model is far from sufficient; what is more crucial is the ability to perform efficient retrieval and reasoning on  ** external Knowledge Bases, Structured Data, and Knowledge Graphs ** .

This layer can be understood as adding an additional layer of "external brain capable of researching information and using databases" on top of the model's capabilities. When a user poses a question, the system no longer directly generates an answer but first "searches for information" in appropriate data sources: document libraries, databases, search engines, Knowledge Graphs, logs, and business systems... Then, it allows the model to provide answers and make decisions based on the actually retrieved content. This not only significantly improves accuracy and timeliness but also greatly enhances interpretability and compliance (e.g., citing sources, retaining SQL execution records, etc.).

Around this layer, common capabilities can be broadly divided into two directions: one is  ** Retrieval Augmented Generation (RAG) ** , mainly targeting "natural language Q&A + document/knowledge base retrieval"; the other is ** Structured Data & ****Knowledge Graph**** (Structured Data & ** **KG**  **) ** , responsible for more precise and controllable access and reasoning of databases, ByteGraph, and domain knowledge mid-platforms. The following will expand on them separately.

## 8.1 Retrieval Augmented Generation (RAG)

RAG (Retrieval-Augmented Generation) can be regarded as an "LLM that can consult materials". Different from purely relying on the internal parameters of the model, before answering each question, RAG will first conduct a search in an external Knowledge Base to find several document chunks most relevant to the question, and then feed these retrieved contents as "context" to the LLM, enabling it to generate answers based on "having consulted the materials". For scenarios such as enterprise Knowledge Base Q&A, industry report search, legal/medical/financial professional Q&A, and internal document search robots, RAG has become the default paradigm.

In terms of system architecture, a typical RAG can be broken down into three layers:  ** Index Building Layer, Retrieval Layer, and Generation Layer ** . The first two layers are mainly about "finding accurately", while the last layer is responsible for "explaining clearly". The following will expand on these three layers and further refine the core design and practice in the secondary subsections.

* **Scenario**
  * Enterprise internal knowledge Q&A: Employees ask questions about institutional processes, technical documents, and project materials in natural language. After the system retrieves relevant content based on internal documents and Wiki, the LLM generates clear answers with citations.
  * Industry Report and Research Search: Retrieve relevant content on a specific industry issue (e.g., "changes in new energy vehicle subsidy policies") from a large number of PDFs, reports, and papers, and automatically summarize, compare, and list the sources.
  * Q&A in the legal, medical, and financial fields: Conduct retrieval enhancement based on authoritative materials such as regulations, judgment documents, clinical guidelines, product manuals, etc., to reduce the risk of "fabrication".
  * Internal Document / Ticket Search Bot: Helps operations, customer service, and R&D quickly locate answers in the Knowledge Base, tickets, and change records, and summarizes the results in natural language.
* **Principle**
  The core idea of RAG is to "store knowledge externally and delegate reasoning to the model":
  * Break unstructured documents (PDF, web pages, Word, technical documents, etc.) into document chunks suitable for retrieval, map them to a vector space using an Embedding model, and build vector indexes (such as FAISS, Milvus, PGVector, etc.).
  * When a user queries, it simultaneously utilizes semantic vector retrieval and keyword retrieval (Hybrid Search) to find several document blocks most relevant to the question, and performs re-ranking (Re-ranking) based on relevance and coverage.
  * Input the retrieved context, user questions, and necessary system instructions/format constraints into the LLM together. The model will provide answers under the constraints of "visible evidence" and cite the source (source citation) in the output to enhance interpretability and auditability.
* **Model**
  A typical RAG system is often a  **model combination architecture** :
  * Embedding Model: Used to encode queries and document chunks into the same semantic space, it is the key to the effectiveness of vector retrieval (including general Embedding and domain-specific Embedding).
  * Retrieval and Re-ranking Model: Hybrid Search (e.g., BM25 + Vector) is responsible for the first round of retrieval, and the Cross-Encoder Re-ranker or the LLM itself is used to perform more refined re-ranking on the retrieved results.
  * Generative Model: LLM answers given the retrieved context; in more complex RAG / HyDE / ReAct + RAG, LLM also participates in processes such as "pseudo-document generation", "multi-round tool invocation", and "alternating thinking + retrieval" to improve recall, reduce forgetting, and enhance reasoning ability.

### 8.1.1 Index Construction and Knowledge Asset Organization

In any RAG system, index construction is fundamental. Without high-quality indexes, even the most powerful subsequent LLMs are like "skilled housewives unable to cook without rice." The goal of index construction is to transform disorganized document resources into "searchable, maintainable, and scalable knowledge assets."

From a process perspective, typical index construction includes the following key steps:

1. **Document Chunking and Preprocessing**
   Documents are often long PDF, PPT, Word files, or web pages. If vectorization is directly applied to the entire document, it can easily lead to "dilution" (a document containing multiple topics) and is also not conducive to efficient retrieval. Therefore, the following steps are required:
   1. Partition by paragraph, title, page number, and chapter structure to balance "semantic integrity" and "block size".
   2. Handle formatting issues (OCR of text in tables, formulas, and images), denoise (headers, footers, table of contents, copyright information, etc.);
   3. Generate "context labels" (such as the document it belongs to, chapter title, page number) for each block, preparing for subsequent explanation and reference.
2. **Embedding and Vector Indexing**
   Based on chunking, generate semantic vectors for each document chunk:
   1. Select appropriate Embedding models (such as general semantic Embedding, domain fine-tuning models) to ensure good expressive ability for the target language and domain terms;
   2. Build high-dimensional vector indexes using FAISS, Milvus, PGVector, etc., supporting approximate nearest neighbor search under large-scale data;
   3. Handling multiple versions and incremental updates: When a document is updated, it is necessary to support incremental index reconstruction, version recording, and old version cleanup strategies.
3. **Metadata Indexing and Filtering**
   Simple semantic vectors are not sufficient to meet complex filtering requirements, and usually it is necessary to build  **metadata indexes** :
   1. Supplement metadata such as time, author, source, document type, Line of Business, and sensitivity level for each document block;
   2. Supports pre-filtering based on meta-information (such as time range, department, permission level) during retrieval to reduce irrelevant results;
   3. lays the foundation for permission control and auditing, preventing RAG from leaking content that users do not have permission to access in its responses.

### 8.1.2 Retrieval and Re-ranking: From "Recalling Relevant" to "Finding the Most Appropriate Evidence"

After the index construction is completed, when a user initiates a query, it enters the retrieval and re-ranking phase. The key here is not just "finding some relevant documents", but rather finding  ** combinations of evidence that are both relevant and fully covered, and support reasoning ** .

1. **Hybrid Search: Complementary of Vector + Keyword**
   Pure vector search excels at capturing semantic similarity, but for precise terms, codes, table fields, etc., keyword search (such as BM25) is often more robust. Therefore, Hybrid Search is commonly used in engineering practice:
   1. First, perform vector retrieval and keyword retrieval on the query respectively to obtain two sets of candidate document blocks;
   2. Merge the two candidate paths using weighted scoring or a learned fusion strategy;
   3. In some scenarios, the weights of vector and keyword retrieval can be dynamically adjusted based on the query type (FAQ Q&A vs. legal provision location).
2. **Re-ranking: More refined selection of the "evidence set"**
   Initial retrieval results often contain many "marginally relevant" or "redundant" document blocks, requiring re-ranking to improve the quality of the final Top-K:
   1. Using Cross-Encoder to perform bidirectional encoding and relevance scoring on "query-document block" pairs has higher accuracy than the dual-tower Embedding model, but incurs higher costs, making it suitable for use as a second-stage reranker;
   2. When performance permits, introduce LLM for lightweight re-ranking, enabling the model to determine which blocks are truly "useful" based on richer semantic and contextual information;
   3. Simultaneously consider coverage and diversity to avoid all retrieval blocks being concentrated in the same document or paragraph, which could lead to a narrow scope of answers.
3. **Retrieval-Generation Closed-Loop Optimization**
   In more advanced practices, retrieval and generation are no longer one-way processes but form a closed loop:
   1. Analyze the "usage" of retrieval results (which blocks are referenced and which are always ignored) using LLM, and use this to guide the optimization of indexing and chunking strategies in reverse;
   2. Utilize the "follow-up/correction" signals in the conversation logs to annotate and retrain samples with recall failures or false recalls, thereby enhancing the system's robustness against ambiguous queries and long-tail questions.

### 8.1.3 Generation and Reference: Answering Questions "Under Evidence Constraints"

The last link is the generation layer, which directly determines the User Experience. The goal here is not to let the model "do as it pleases", but to have it  ** provide clear, bounded, and referenced answers under the constraints of retrieved evidence ** .

1. **Controlled Generation Based on Retrieved Context**
   In the RAG architecture, the LLM receives not only the user's question but also multiple retrieved document chunks and system instructions. The system typically:
   1. Constrain the model via Prompt to "answer only based on the given document" and "clearly state the absence if the answer cannot be found in the document";
   2. Structured organization of the retrieval context (segmentation, numbering, and source annotation) is carried out to facilitate model understanding and reference;
   3. Control the output format (list, table, point-by-point description, etc.) to adapt to downstream systems or front-end display.
2. **Source Citation and Explainability (Source Citation)**
   To facilitate auditing and traceability, especially in high-risk areas such as law, healthcare, finance, and internal corporate systems, answers often need to include clear citations:
   1. Mark the source of references in the output, such as "[Document A, Chapter 3, Section 2]" "[Article 12 of Regulation X]";
   2. Supports one-click jump to the original text location in the front-end interface, facilitating users to verify and further read;
   3. Save the complete link log of "question - retrieval result - reference block - final answer" in the background to provide data for subsequent risk control and model improvement.
3. **Advanced RAG Variants: HyDE / ReAct + RAG, etc.**
   To further enhance performance in challenging scenarios, more complex RAG variants are also used in practice:
   1. HyDE: First, the LLM generates a "hypothetical answer document" based on the question, and then uses the vector of this document to retrieve real documents, thereby improving the quality of recall;
   2. ReAct + RAG: The LLM, in the manner of "Reasoning + Action", repeatedly invokes retrieval tools during reasoning, gradually refining the problem and supplementing evidence, similar to "thinking while consulting materials";
   3. Multi-round RAG: During the conversation, retain historical retrieval results and responses to form a context-aware long-term knowledge session, rather than simply "single-question single-retrieval".

## 8.2 Structured Data & Knowledge Graph (Structured Data & KG)

If RAG mainly addresses "how to search for information in large-scale unstructured documents", then the layer of Structured Data and Knowledge Graph is more oriented towards "how to elegantly utilize structured knowledge in databases, reporting systems, and ByteGraph".

In enterprise environments, truly critical business data - orders, customers, contracts, inventory, and behavior logs - often exists in the form of relational databases, data warehouses, OLAP engines, or ByteGraph. These systems are already highly mature in terms of query capabilities, computational efficiency, and auditing, but for business personnel, directly writing SQL/DSL still has a relatively high threshold. ** Text - to - SQL/Text - to - DSL ** and ** Knowledge Graph Question Answering and Reasoning ** aim to enable LLMs to be inserted as "natural language interfaces" and "reasoning collaboration partners" without disrupting the stability of these systems.

* **Scenario**
  * BI Intelligent Q&A and Self-service Analysis: Business personnel ask questions in natural language (e.g., "Help me check the trend of the Re-purchase Rate of new customers in East China in the past 3 months"), and the system automatically generates SQL, queries the data warehouse, and then returns results in natural language and visual charts.
  * Operations / Sales Analysis Assistant: Operations staff can explore data through conversations ("Why did the conversion rate of this campaign decline?" "Which channels contributed the most high-value users?"), gradually refining conditions and dimensions in multi-round conversations.
  * Domain Knowledge Mid-Platform: Organizes entities, concepts, rules, and cases into a Knowledge Graph, supporting exploration of upstream and downstream relationships and compliance checks around a specific entity.
  * ByteGraph Question Answering and Reasoning System: In scenarios such as risk control, anti-money laundering, and supply chain analysis, it answers and explains questions related to "relationship chains" and "multi-hop reasoning" through the combination of ByteGraph and LLM.
* **Principle**
  The core of this layer is to transform the LLM from a "person who directly provides answers" into an "assistant who can call databases and ByteGraph":
  * In database question answering, the model needs to understand the user's natural language intent, combine it with the database schema (table structure, field meaning, constraints, etc.), generate the correct SQL / GraphQL / internal DSL, and then interpret and visualize the execution results.
  * In the Knowledge Graph scenario, the system first needs to extract entities and relationships from documents and logs to build a structured graph; then, during question answering, the LLM is responsible for translating natural language questions into graph queries (such as Cypher), and performing multi-hop reasoning and explanation based on the query results.
  * Different from RAG, what is emphasized here is  ** precise access to Structured Data and graph structures ** , which on the one hand ensures semantic correctness and grammatical rigor, and on the other hand controls profiling attacks, sensitive data exposure, and high-cost queries.
* **Model**
  Typical solutions usually adopt a multi-module architecture of "LLM + dedicated components":
  * Text-to-SQL Model: A model pre-trained or fine-tuned on large-scale SQL corpora (such as PICARD, DIN-SQL, etc.), focusing on grammatical correctness and schema alignment, and sometimes accompanied by execution feedback for self-correction.
  * Information Extraction and Knowledge Graph Construction Pipeline: Through modules such as Named Entity Recognition (NER), Relation Extraction, and Event Extraction, it constructs and updates the Knowledge Graph from text and logs; LLMs can participate in difficult case extraction and assist in the judgment of relations with fuzzy boundaries.
  * LLM + ByteGraph Joint Question Answering: LLM is responsible for question parsing, query generation, and result interpretation, while ByteGraph (such as Neo4j) is responsible for efficient execution and multi-hop relationship search, and the two are connected through tool invocation protocols or intermediate DSLs.

### 8.2.1 Database Q&A (Text‑to‑SQL / DSL) Practice

The goal of database Q&A is to enable business personnel to "query data in natural language", while the system automatically completes the generation, execution, and interpretation of query statements in the background. To do this well, the key lies in balancing  ** semantic accuracy, syntactic correctness, and execution security ** .

1. **Natural Language to SQL/DSL Conversion**
   In the most basic link, the system needs to:
   1. Parse user intent: identify the query object (e.g., "new customers in East China"), filter (time, region, channel), aggregation method (total, average, year-on-year/quarter-on-quarter), and display requirements (trend, ranking, Top-N);
   2. Combine with the database schema: understand which tables and fields can express the above concepts, and how to perform joins, groupings, and sorting;
   3. Generate executable SQL / GraphQL / internal DSL, and ensure its structural legality through a syntax validator or a dedicated Text2SQL model (such as PICARD, DIN‑SQL, etc.).
2. **Natural language interpretation and visualization of execution results**
   After query execution, the system also needs to transform the "cold result set" into "understandable insights":
   1. Provide a text explanation for simple results, such as "Over the past 3 months, the overall Re-purchase Rate of new customers in East China has shown an upward trend, increasing from 15% to 21%";
   2. Select appropriate visualization forms (line chart, bar chart, pie chart, distribution chart, etc.) for complex results, and provide a brief analysis;
   3. Supports users to continue asking follow-up questions based on the current results (e.g., "Which channels did this wave of growth mainly come from?"), and automatically constructs new queries based on historical SQL and context.
3. **Security and Control: Prevent "random queries" and "exceeding authority"**
   Due to the high flexibility of SQL generated by LLMs, a layer of security and governance mechanism must be in place:
   1. Based on User Persona and permissions, strictly restrict the queryable libraries, tables, fields, and time ranges;
   2. Equip the SQL generated by the model with static/dynamic review rules to filter out dangerous operations (such as large-scale scans, high-cost joins, cross-tenant queries, etc.);
   3. Completely record "natural language question - generated SQL - execution result - final answer" for auditing and anomaly analysis.

### 8.2.2 Knowledge Graph Construction and Query

Knowledge Graph attempts to organize the knowledge scattered in text, tables, and logs into a structured network of "entity - relationship - attribute - event", thereby better supporting  **relationship exploration, multi-hop reasoning, and complex question answering** . In this direction, LLM and traditional information extraction, ByteGraph form a good complement.

1. **Extract entities and relationships from documents to build a Knowledge Graph**
   Building a Knowledge Graph typically employs a multi-stage pipeline:
   1. Information Extraction: Utilize models such as NER, relation extraction, and event extraction to identify entities (people, organizations, products, place names, concepts, etc.), relationships between them (affiliation, cooperation, dependence, causality), and key events (transactions, risks, changes) from text;
   2. Normalization and Alignment: Normalize different expressions (abbreviations, aliases, spelling variants) of the same entity and align them to a unified ID;
   3. Knowledge Graph Update and Version Management: Supports incremental updates, conflict resolution, and error correction to ensure the Knowledge Graph maintains quality and consistency during long-term evolution. LLM can assist traditional algorithms in disambiguation, relationship type refinement, rule induction, and other processes.
2. **Query and Inference of LLM + ByteGraph (e.g., Neo4j)**
   Once the Knowledge Graph is constructed, ByteGraph is responsible for efficient storage and retrieval, while LLM can play the role of "natural language entry + inference controller":
   1. Problem Analysis and Graph Query Generation: Translate natural language questions into graph query statements (such as Cypher for Neo4j), including determining the starting entity, relationship type, path length, and filter conditions;
   2. Multi-hop reasoning: Based on the paths and local subgraphs obtained through graph queries, LLM then performs interpretation and induction, such as "Customer A is indirectly connected to high-risk entity B through three companies".
   3. Result Visualization and Interpretability: Present graph query results in the form of a visualized network, while LLM provides verbal explanations to help users understand complex relationship structures.
3. **Domain Knowledge Mid-Platform and Unified Services**
   In large-scale enterprise or industry-level applications, the Knowledge Graph often exists as a "Domain Knowledge Mid-Platform":
   1. Provides a unified perspective on entities and relationships for upper-level business systems (risk control, compliance, customer 360 view, supply chain analysis, etc.);
   2. Together with RAG and database Q&A, it forms a unified knowledge service layer, where the unified LLM orchestration logic determines whether the current question should access the document index, relational database, or ByteGraph;
   3. Under security and compliance requirements, further reduce the risk of sensitive information leakage through access control and desensitization strategies at the graph level.

The common goal of this layer is to upgrade "the model can talk" to "the model can talk and is truly connected to the enterprise's real data and knowledge assets". Only after the effective combination of RAG, Text-to-SQL, Knowledge Graph, and traditional data infrastructure can AI systems maintain both intelligence and flexibility while also possessing controllability, interpretability, and long-term evolution capabilities in complex business environments.

# 9. Safety / Alignment / Evaluation

In the previous chapters, we started more from "what the model can do": it can view images, write code, and converse with users. But in a real large model system, merely "having the ability" is far from enough: ** How can we prove that these abilities are stable, reliable, and controllable? How can we ensure that the output complies with values and compliance requirements? How can we continuously monitor, iterate, and regress during long-term operation? ** What this layer focuses on is:  ** ability assessment and benchmark testing, value alignment and training, content security and compliance, as well as robustness and hallucination control ** , which together form the "infrastructure layer" of a sustainable large model.

From a product perspective, these capabilities span the entire lifecycle of the model: during the laboratory phase, the model requires standard benchmarks and professional evaluations; before going live, it must undergo alignment training and security reviews; after going live, it relies on content security gateways, log audits, and A/B testing for continuous monitoring; when facing new scenarios and threats, it must return to the evaluation and alignment phases for retraining and validation. Next, we will expand from ** capability assessment and benchmark testing, value alignment and training, content security and compliance, robustness and hallucination control ** four directions.

## 9.1 Capability Evaluation & Benchmarks

During the research, development, and implementation of large models,**capability assessment and benchmark testing**are a crucial step in transforming "model capabilities" into "observable signals": it must answer both "what is the overall level of this model" and "how does it perform in a specific professional domain or real business scenario". On the one hand, we use standardized benchmark sets and automated evaluation systems to measure the model's performance in**language understanding and generation, reasoning and mathematics, knowledge and factuality**and other general dimensions; on the other hand, we also need to construct specialized evaluations for**medical, legal, financial, educational**and other professional domains, and continuously validate and correct them through**real user conversations, A/B testing, and business metrics (Task Success Rate, CSAT, ticket closure rate, etc.). Overall, this layer will ultimately precipitate into an internal capability assessment platform**and an external " **capability specification** ", providing a unified decision-making basis for model selection across multiple versions, multiple tenants, and multiple scenarios. The following will be elaborated from three perspectives: **scenario** ,  **principle** ,  **model** .

* **Scenario**
  * **General Capability Assessment Scenario** : When a foundational model or major version is updated, it is necessary to systematically evaluate its performance on tasks such as reading comprehension, summarization, translation, and dialogue quality in  **language understanding and generation** , as well as its capabilities in tasks such as arithmetic, multi-step reasoning, and code/logic problems in  **reasoning and mathematics** . At the same time, measure its **knowledge and factuality** level through tasks such as factual Q&A, open-domain QA, and knowledge coverage, which is used to determine whether the "new model has overall improvement".
  * **Professional Domain Assessment Scenario** : For subdomains such as healthcare, law, finance, and education, it is necessary to design professional Q&A and decision-making simulations, such as disease Q&A and triage advice, legal provision understanding and case classification, investment and financing analysis and risk control judgment, teaching Q&A and homework tutoring, and test the consistency and stability of the model in the**multilingual and multicultural environment**to confirm whether it can "speak appropriately" in high-risk environments.
  * **Real-world Scenarios and Business Metric Evaluation Scenarios** : During the product launch and continuous operation phases, through methods such as user conversation log replay and online A/B testing, map the model performance to  **Task Success Rate** ,  **Customer Satisfaction Score (CSAT)** , **ticket closure rate** and other business metrics; at this time, the actual evaluation object is the overall system of "model + strategy + product process", which is used to guide version rollback, strategy optimization, and new feature rollout.
* **Principle**
  The Competency Assessment System can be regarded as a hierarchical "measurement system engineering", and its core principles include:
  * **Standard Benchmark Set: Common Scale and Reproducible Experiments **
    * Language / Reasoning: Use  **MMLU** , **BIG-Bench** and other comprehensive tasks, combined with  **GSM8K** , **MATH** and other mathematical and logical problems, to construct a unified scale for language understanding, knowledge mastery, and multi-step reasoning.
    * Programming: Quantify code generation, program repair, and problem-solving abilities through  ** HumanEval ** ,  ** MBPP ** , ** Codeforces ** question banks, etc.
    * MultiModal Machine Learning: Utilize  **VQA** ,  **MMBench** ,  **ScienceQA** , **MathVista** and other benchmarks to test image-text understanding, visual question answering, and mathematical reasoning in images.
      These benchmarks emphasize  **standardization, reproducibility, and comparability** , facilitating horizontal comparison across models and institutions and external disclosure.
  * **Automated Evaluation: Scalability and Continuous Regression**
    * **LLM-as-a-Judge** : Use a stronger or specially trained model to score/rank responses, evaluate correctness, completeness, style, and security, and achieve large-scale automatic subjective evaluation.
    * **Rule-based metrics ** : such as BLEU / ROUGE / BERTScore for measuring text similarity, Pass@k for measuring the passing rate of coding problems, etc., enabling quick comparison of differences between different versions on a fixed dataset. The key to automatic evaluation lies in  ** stability and consistency ** , and even if it is not perfect, as long as the "bias is consistent", it can reliably reflect the relative changes of the model in continuous integration (CI).
  * **Human Evaluation: Aligning Human Perception with Business Objectives**
    * **Pairwise Comparison and Scoring Annotation** : Annotators perform pairwise selection or multi-dimensional scoring (helpful / honest / harmless, etc.) on the responses of two models A and B, which is an important data source for training RLHF / RLAIF reward models.
    * **Online User Experiment** : Conduct AB testing through application scenarios such as conversation assistants, search/recommendation, etc., to directly observe the impact of different models/strategies on indicators such as customer satisfaction score and conversion rate. Manual evaluation is used for both **calibrating automatic evaluation** and is also an important basis for "explaining model behavior" externally.
* **Model**
  In engineering practice, capability assessment will precipitate into a relatively complete "platform + process + indicator system":
  * **Internal C****ap** **ability Assessment Platform and CI Pipeline** : Unified management of various benchmark sets, evaluation scripts, LLM-as-a-Judge configurations, and manual annotation tools, supporting one-click triggering of Benchmark regression after the submission of new models or new strategies; automatically aggregating indicator changes across different tasks and dimensions, providing a visual Dashboard and regression alerts.
  * **External "Capability Specification" and Model Portrait** : Organize internal evaluation results into an externally consumable "Capability Specification", including representative benchmark scores, recommended application scenarios (such as general conversation, code assistance, multi-modal understanding, etc.), known limitations, and inapplicable scenarios, to help customers form correct expectations and provide a basis for compliance and liability allocation.
  * **Unified Evaluation and Selection Tool for Multi-Tenant/Multi-Vers****ion** ** Models** : Under the same evaluation system, it uniformly compares models of different sizes, different alignment strategies, or different architectures, supports configuring weights according to industry, region, and SLA requirements, automatically generates a comprehensive score of "performance-cost-latency", and helps product and business teams make decisions on model selection and canary release.

### 9.1.1 General and Professional Competence Assessment: From Benchmark to Scenario Validation

General and professional competence assessment is the "first layer of foundation" of the entire assessment system, with the focus on: first measuring the model's **basic capabilities** using a unified scale, and then verifying its **usability and risks** in professional scenarios.

In general ability assessment, tasks are typically divided into three dimensions: language understanding and generation, reasoning and mathematics, and knowledge and factuality. The former examines whether the model can accurately understand context, control style, and output coherent text through tasks such as reading comprehension, summarization, translation, and dialogue quality; the middle assesses the model's capabilities in complex reasoning chains and program structures through arithmetic, multi-step reasoning, and code/logic problems; the latter measures knowledge coverage and factuality levels through factual Q&A and open-domain QA. In professional domain assessment, Subject-Matter Experts need to be invited to participate in data design: for example, in medical Q&A, context such as medical history and test results is set, requiring the model to provide risk warnings and boundaries for medical advice in its answers; in legal tasks, provisions retrieval, case comparison, and legal application analysis are designed; in finance and education, the focus is on compliance disclosure and teaching guidance. This level of assessment often combines standard benchmark sets with self-built datasets, pursuing both comparability and business relevance.

### 9.1.2 Automated Evaluation and LLM-as-a-Judge: Making Evaluation Scalable

When the scale of the task and the number of model versions grow rapidly, it is difficult to support the evaluation needs only by manual work. At this time, it is necessary to achieve **scale and high-frequency regression **through the automatic evaluation system.

One approach is to use traditional rule-based metrics: in tasks such as translation and summarization, BLEU / ROUGE / BERTScore are used to compare with reference answers, and in code tasks, Pass@k is used to test whether at least one of multiple generated samples passes unit tests. These metrics are simple to implement and highly automated, but they are insensitive to answer diversity and style details. Another more representative approach is  **LLM-as-a-Judge** : using a stronger or specially trained model as a "scoring judge" to perform dimensional scoring or pairwise ranking on the outputs of the model under test according to a predefined scoring rubric. This allows us to conduct efficient automatic evaluation even in open-ended question-answering and dialogue tasks where there are no standard answers and responses are diverse. In practical engineering, the scoring criteria and prompts of LLM-as-a-Judge need to be calibrated and iterated through manually annotated data to ensure consistency with human judges.

### 9.1.3 Manual Evaluation and Business Metrics: Closed Loop to Real User Experience

No matter how complete offline metrics are, they can only approximate the real User Experience. To close the loop of capability evaluation to business, it is necessary to introduce two types of methods: manual evaluation and online experiments.

On the manual evaluation side, the commonly used method is Pairwise comparison: annotators are asked to make preference selections or assign scores to two responses A and B based on dimensions such as helpful, honest, and harmless without knowing the identity of the models, thereby obtaining high-quality preference data. On the one hand, this data is used for direct evaluation; on the other hand, it can provide data for training reward models in RLHF/RLAIF. On the business side, through online A/B testing, the impacts of different models, prompts, and strategy configuration versions on key indicators such as task completion rate, Customer Satisfaction Score (CSAT), and ticket closure rate are compared, supplemented by user conversation log replay and manual spot checks, to continuously monitor the real performance of the model after it goes live. The output of this level of evaluation, in turn, guides the key directions and weight adjustments of the capability evaluation platform, forming a closed loop of "offline metrics - manual evaluation - online metrics".

## 9.2 Value Alignment & Training

After having strong foundational capabilities, for large models to become "safe, reliable, and controllable" products, they must also undergo  ** value alignment and training ** . This layer no longer focuses on whether the model "can answer", but rather on ** wh****e****ther**** the answers are useful, honest, and harmless ** and "how to speak in different roles and industries". From an engineering perspective, the alignment process generally includes three steps: First, clearly define ** the alignment target definition (What to Align) ** through documents and specifications, breaking down useful (Helpful), honest (Honest), and harmless (Harmless) into annotatable and trainable standards; Second, build extensive  ** instruction data and safety data ** , covering normal tasks, gray area cases, and inappropriate answers; Finally, through  ** methods such as SFT, RLHF / RLAIF, and refusal / retargeting strategy modeling ** , "write" these preferences and rules into the model behavior, supplemented by upstream dialog management and strategy engines, to achieve end-to-end safety alignment. The following also expands from  ** scenarios ** ,  ** principles ** , ** models ** three perspectives.

* **Scenario**
  * **General C-end assistant ****scen** **ario ** : Chat assistants and information retrieval assistants for the general public need to maintain "  **friendly, helpful, and not crossing the line ** " under broad-spectrum topics: both to answer professionally and focus on tasks, and to express limitations candidly when uncertain, and to refuse or flexibly guide obvious inappropriate needs.
  * **Professional Industry Assistant Scenarios** : In fields such as healthcare, law, finance, and education, in addition to basic security, industry regulations must also be added. For example, healthcare assistants need to repeatedly emphasize "non-diagnostic nature + risk warning + advice to seek medical treatment"; legal assistants should avoid providing advice on evading laws; financial assistants must comply with investment compliance disclosure requirements; and education assistants should consider the protection of minors and age-appropriate content.
  * **B-side configurable alignment layer scenario ** : Enterprises often hope to further embed their own industry requirements, brand tone, and internal policies on top of the general security baseline. Therefore, they need a ** configurable alignment layer ** that allows customers to configure security thresholds, sensitive categories, and narrative styles on their own without having to retrain the underlying large model.
* **Principle**
  Value alignment can be understood as "constraining the behavioral space of models with the values of humans and organizations," and its core principles include:
  * **Alignment Target Definition (What to Align)**
    * **Helpful** : Responses should be of high quality, professional, well-structured, and focused on the task objective, without excessive digression or idle chat.
    * **Honest** : Try not to fabricate information. When knowledge is lacking or understanding is unclear, proactively acknowledge uncertainty, provide an estimated range, or suggest verification channels.
    * **Harmless (Harmless) ** : Comply with laws and platform policies, avoid generating content such as hate, discrimination, self-harm encouragement, and criminal guidance, and respect users' dignity and boundaries.
      These goals will be incorporated into annotation guidelines and strategy documents, becoming the unified standard for subsequent data construction, reward modeling, and evaluation.
  * **Al****ignm****ent Training Data Construction**
    * **In** **struction Data (Instruction)** : Design a wide range of task instructions and ideal responses, covering various scenarios such as Q&A, writing, summarization, code, planning, etc., to teach the model the best behavior under "normal requests".
    * **Safet****y Data** ** (Safety) ** : Construct control samples of "good responses vs. inappropriate responses", with particular emphasis on the gray zone (gray zone), such as popular science information vs. specific operations, emotional support vs. self-harm encouragement, legal debate vs. hate incitement, etc., to provide the model with fine-grained boundary examples.
  * **Alignment Training Method**
    * **SFT (Supervised Fine-Tuning) ** : Supervised fine-tuning on high-quality dialogue/instruction data is the first step in shaping the baseline behavior and tone of the model.
    * **RLHF** ** / RLAIF** : Build preference data by human or model scoring, train a reward model, and then perform policy optimization to make the model tend to generate "preferred" responses (more useful, safer, and more honest) during generation.
    * **Refusal / Retargeting Strategy Modeling** : For high-risk or inappropriate requests, the trained model will not only refuse to answer but also provide reasonable explanations and guide users to safe alternatives (such as providing help resources, encouraging consultation with professionals, etc.).
* **Model**
  In system design, value alignment is usually manifested as a combination of  **bottom-level alignment training + upper-level strategic guardrails** :
  * **SFT**** + ****RLHF** ** / RLAIF Alignment Model** : The SFT phase enables the model to learn the basic patterns of ideal responses; the RLHF / RLAIF phase further "tightens" behavior through preference learning, making it closer to human preferences and safety standards. In the safety dimension, a reward head or classifier can be separately constructed for harmfulness to impose penalties during policy optimization.
  * **Constitutional AI / Policy-based Alignment** : By first writing a set of "Constitution" or Policy documents, and then having the model conduct self-criticism and rewriting based on these rules, a large amount of "self-supervised correction data" is generated, which reduces labor costs while strengthening the model's internalization of the rules.
  * **Dialog Management and Intent Detection Collaboration** : In the product pipeline, move the security/ alignment logic part up to the dialog management layer, and determine whether to hand over the request to the large model, whether additional security filtering or templated responses are needed through intent recognition, slot filling, and task routing. This can form a double insurance of "model alignment + policy guardrails".
  * **Internal Alignment Platform and Role Configuration** : Build an internal alignment platform to provide annotation/scoring tools, strategy version management, and training pipelines; at the same time, support configuring differentiated alignment goals and narrative styles for different roles (customer service, medical advice, educational tutoring, etc.), enabling the same base model to exhibit distinct yet controllable and consistent personalities across different products.

### 9.2.1 Aligning Objectives with Training Data: Transforming Values into Learnable Signals

The first step in value alignment is to translate "abstract values" into signals that the model can learn, which is inseparable from the definition of alignment objectives and the construction of training data.

At the alignment target level, the team typically outputs a detailed set of behavioral guidelines, breaking down Helpful / Honest / Harmless into specific clauses, such as: prohibiting the provision of specific steps for certain high-risk operations, attaching disclaimers and risk warnings to medical / legal advice, and maintaining neutrality and multi-perspective presentation when dealing with controversial topics. Then, during the instruction data phase, diverse tasks and ideal responses are constructed around these metrics, covering scenarios such as chatting, writing, coding, and Q&A, and integrating multilingual and multicultural backgrounds; during the safety data phase, paired "good / bad response" examples are constructed for harmful content, high-risk areas, and gray areas, providing training creatives for subsequent preference learning and safety classifiers. In this way, value targets are "translated" into actual data distributions, becoming signals that Model Training can directly perceive.

### 9.2.2 SFT, RLHF / RLAIF, and Refusal Strategy: Shaping Model Behavior

After having alignment objectives and data, the next step is to incorporate these objectives into model behavior through a multi-stage training process.

During the SFT phase, the model undergoes supervised fine-tuning on high-quality human demonstration data, which is similar to "textbook-style learning": it determines the tone, structure, and standard problem-solving paradigms of the model under the vast majority of normal requests. Subsequently, preference optimization is carried out through  **RLHF** ** / RLAIF** : first, a reward model is trained using preference labels generated by human annotations or larger LLMs, and then a policy optimization algorithm (such as PPO, etc.) is used to adjust the model so that it tends to obtain higher rewards during generation. In this way, the model not only "knows what the correct answer looks like" but also "knows which answer better meets human preferences and safety requirements". On this basis, various **refusal and retargeting strategies** are also specifically modeled: for questions that are clearly illegal, extremely high-risk, or not suitable for AI to answer, the model should learn to give clear refusals and explanations, and provide safe alternative paths (such as helplines, professional consultations, etc.), rather than simply remaining silent or casually evading.

### 9.2.3 Strategy Layer and Alignment Platform: Making Alignment Configurable and Evolvable

Even if the underlying model has undergone sufficient alignment training, in the actual system, it is still necessary to ** have a policy layer and an alignment platform ** to achieve finer-grained controllability and evolvability.

The strategy layer typically includes intent recognition, risk assessment, and routing logic: when user input reaches the system, a lightweight model first determines its intent, domain, and risk level, and then decides whether to directly invoke the large model, whether additional security filtering is required, whether it falls into template responses, or whether to transfer to human channels. For different industries and customers, the strategy layer can load different Policy configurations to customize sensitive categories, refusal styles, and brand tones. Meanwhile, the internal alignment platform manages all alignment-related assets: annotation/scoring tools, reward model versions, strategy change records, online A/B results, etc., enabling the team to quickly iterate and perform canary releases on alignment strategies without frequently retraining the base model, thereby maintaining continuous control over model behavior.

## 9.3 Content Safety & Compliance

As large models are embedded into search, conversation, content creation, social platforms, and even enterprise internal systems, ** content security and compliance ** have transformed from "additional features" into "entry requirements". This layer focuses on: whether the model generates illegal and harmful content when generating text, images, audio, and video; whether the system complies with the laws and regulations of the country/region and industry when processing user data; and whether it can provide a clear and traceable evidence chain when facing audits and regulations. To this end, we need to build a complete technology and governance system covering  ** multi-modal content moderation, regional and industry compliance, and local privacy and data protection ** , and encapsulate it into product forms such as SaaS content security services, enterprise compliance mid-platforms, and industry security gateways. The following also unfolds from  ** scenarios ** ,  ** principles ** , ** models ** three perspectives.

* **Scenario**
  * **MultiModal Machine L****ear****ning Content ****Mod** **eration and Filtering Scenarios** : In conversation products, UGC platforms, communities, and social applications, large models generate or receive a large amount of text, image, audio, and video content, which requires unified**MultiModal Machine Learning moderation**capabilities to identify and intercept high-risk outputs involving personal privacy, criminal guidance, hate incitement, extreme violence, pornography, and inappropriate content for juveniles in real time.
  * **Compliance Constraints and Localization Scenarios** : Laws and regulations in different countries/regions have different requirements for data protection, juvenile protection, content moderation, etc.; different industries (medical, finance, education, advertising, etc.) also have detailed compliance specifications. Therefore, the system must support loading different policy templates according to**region and industry**to meet local regulatory requirements.
  * **User Privacy and Data Protection Scenario** : During Model Training and online service processes, a large amount of user conversations and business data need to be processed. How to achieve data anonymization, desensitization, and minimal collection, while protecting privacy through technical and institutional means during the training and inference phases, is another pillar of the content security and compliance system, especially in highly sensitive industries such as finance and healthcare.
* **Principle**
  The underlying principles of content security and compliance can be divided into three levels: strategy, filtering, and privacy:
  * **Security Policy System (Policy Engine)**
    * Formalize laws, regulations, platform rules, and industry standards  ** into executable policies ** , and use a rules engine combined with model scoring to classify content risks (safe / gray area / high risk).
    * Supports selecting different policy templates based on scenarios and clients, such as configuring different sensitive categories and thresholds for youth products, professional communities, or multinational enterprises.
  * **Multi-level content filtering: pre-event – in-event – post-event**
    * **Pre-event** : Intercept and rewrite user prompts (Prompt Shielding), block obvious illegal or highly sensitive intentions before the request enters the large model, or guide them into a relatively safe expression.
    * **During the process ** : When the model generates output, use the safety classification model and rules to conduct real-time review (Real-time Safety Filter) of the content, and truncate, replace, censor, or trigger a rejection response for high-risk content.
    * **After the fact ** : Conduct sampling audits and human review of dialogue and generation logs, trace and analyze the identified issues, then update strategies and models, and provide traceable records for external supervision.
  * **Privacy Protection Technology and **** ****Data Governance**
    * Before data storage and training, user conversation data is subjected to  **anonymization and desensitization ** , removing or replacing sensitive fields such as names, ID numbers, mobile phone numbers, addresses, etc., and adhering to the **principle of minimal collection **to retain only necessary information.
    * In some scenarios, differential privacy (DP) is used to **limit the impact of a single sample on model parameters, or through **FL (FL) training is left in the local data domain to avoid the original data source going to the cloud.
    * Utilize**RBAC** ** / ** **ABAC** and other access control mechanisms to strictly limit who can access what level of logs and sensitive data, and cooperate with audit logs to ensure that access paths are traceable.
* **Model**
  From the perspective of product and system design, content security and compliance will ultimately evolve into a series of reusable "Security Services and Mid-Platform":
  * **SaaS Content Security Service** : Encapsulates text/image/audio-video auditing capabilities into a unified API for integration with upstream applications; takes content as input and outputs risk types, classifications, and handling suggestions (release, block, manual review), helping developers quickly integrate security modules.
  * **Enterprise Internal Compliance Mid-Platform** : Provides large enterprises with centralized management capabilities for compliance strategy configuration, audit reports, and risk alerts, connects to internal business systems and human audit teams, enables each Line of Business to execute custom rules under a unified strategy, and meets external regulatory reporting requirements.
  * **Specialized Security ****Gateway**** and ****Log** ** Audit System for High-Risk Industries** : In high-risk industries such as finance and healthcare, all large model calls are proxied through a specialized security gateway, which conducts real-time inspection and desensitization of traffic, retains critical logs locally or in compliant regions, provides detailed access auditing and event traceability capabilities, and meets strict regulatory requirements.

### 9.3.1 MultiModal Machine Learning Review and Policy Engine: Transforming Rules into "Executable Code"

An actual content security system must first be able to "understand" content from different channels and modalities, and then implement policies for each request and response.

In MultiModal Machine Learning auditing, the system typically constructs multiple detection models for text, images, videos, etc.: the text-side model identifies sensitive keywords, contextual information, and veiled expressions; the image and video sides detect content such as violence, pornography, juveniles, hate symbols, and illegal items, and combine OCR, ASR, and visual features for joint judgment when necessary. The Policy Engine binds the outputs of these models with regulatory requirements: for example, if a region has stricter restrictions on gambling or political content, it can increase the sensitivity of relevant detection categories in the corresponding policy template or enforce manual review for content that hits these classifications. By transforming abstract rules into rule chains, thresholds, and actions (release/block/manual review/censoring), the Policy Engine makes compliance requirements truly "operational".

### 9.3.2 Multi-level Filtering and Log Auditing: Building an End-to-End Secure Closed Loop

Interception at a single stage can hardly cover all risks, so content security systems generally adopt the design of**pre-event, in-event, and post-event**three-tier defense lines.

During the pre-event stage, the system will quickly detect user input, directly reject or rewrite obvious violations or highly sensitive prompts, and guide users to ask questions in a safe manner; for boundary attempts and ambiguous requests, it can also proactively supplement statements and risk warnings. During the in-event stage, model outputs will pass through a real-time security filtering component: this component will use text classification and rule matching to trim, replace, or trigger a rejection process for potentially high-risk outputs, ensuring that the content ultimately presented to users falls within an acceptable range. During the post-event stage, through a log auditing and random inspection mechanism, the security team or a trusted automated system will regularly replay and check conversations, analyze misjudgments, missed judgments, and new risk patterns, and update strategies, training data, and detection models accordingly. This forms a continuously evolving security closed-loop, rather than a "one-time configuration".

### 9.3.3 Privacy Protection and Industry Security Gateway: Making Data Security "Proven"

In highly sensitive industries, simply "not outputting harmful content" is far from enough; it is also necessary to prove that "the internal use of user data is equally safe, compliant, and traceable."

Privacy protection starts from the data entering the system: during the collection and storage stages, anonymization and desensitization are carried out as much as possible to ensure that even if the log is leaked, it is difficult to directly associate it with specific individuals; during the training stage, differential privacy, sampling policies, or FL are used to reduce the impact of individual user data on the final model and the risk of leakage. For model inference traffic, unified access control is carried out through the  **Security Gateway ** : all requests and responses must go through the content check, permission verification, and audit records of the gateway, and different access policies and data views are applied according to Line of Business and User Persona when necessary. Ultimately, these logs and policy change records will precipitate into a "chain of evidence" that can be viewed by internal audit and external supervision, enabling enterprises to not only comply in fact, but also "prove compliance in form".

# 10. AI for Science（AI4Science）

When deep learning and large models move from "recommended advertising, natural language understanding" to  ** scientific problems themselves ** , the goal is no longer just to predict an indicator or perform a classification, but to truly participate in  ** discovering laws, designing experiments, accelerating simulation and reasoning ** . AI4Science attempts to combine "statistical pattern recognition" with "physical laws / biochemical laws / mathematical structures" to enable models to act as "programmable scientific assistants" in molecular design, protein engineering, material discovery, physical simulation, mathematical reasoning and other processes.

In engineering practice, one end of this layer connects to "traditional scientific infrastructure" such as quantum chemistry software, molecular dynamics (MD), CFD/FEA simulators, automated theorem provers, literature databases, and robotic laboratories, while the other end connects to the real scientific research workflows of pharmaceutical companies, materials enterprises, energy companies, and research institutions. The following will be expanded from three perspectives:  ** scenarios ** ,  ** principles ** ,  ** models ** , and further subdivided in several key directions.

* **Scenario**
  * Molecular and Drug Design: Starting from a vast number of small molecules/fragments, predict properties and ADMET, design candidate drugs targeting specific targets, and narrow down the experimental space through virtual screening and multi-objective optimization.
  * Protein and Biological Structure Modeling: Predict the three-dimensional structures of proteins and complexes, assist in the design of antibodies, enzymes, and protein drugs, and evaluate the impact of mutations on function and stability.
  * Physical Simulation and Engineering Design: Accelerate high-cost simulations such as CFD/FEA/Molecular Dynamics with deep surrogate models, providing rapid evaluation and optimization tools for fields such as aerospace, automotive, and energy.
  * Materials Discovery and Crystal Design: Conduct virtual screening and inverse design in the vast chemical/material space to accelerate the research and development of key materials such as batteries, photovoltaics, catalysts, and alloys.
  * Mathematics and Symbolic Reasoning: Perform automated theorem proving, symbolic computation, and equation solving in formal systems to enhance the rigorous reasoning capabilities of large models in mathematical problems and engineering derivations.
  * Scientific Workflow and Automated Experiment: Connecting literature, databases, and automated experimental platforms to build a "Self-Driving Lab", enabling models to participate in experimental design, execution, and result analysis.
* **Principle**
  * Structured Representation and Graph Modeling: Represent complex objects using structures such as graphs, crystal graphs, and molecular graphs, and model geometric and topological relationships on graph neural networks or E(3)-equivariant networks.
  * Physical/Chemical Inductive Bias: Incorporate physical priors into the model structure and loss function through conservation laws, symmetries (translation/rotation/reflection), PDE constraints (PINN), energy potential functions, etc.
  * Generation and Inverse Design: Utilize generative modeling methods such as VAE, GAN, Diffusion, and RL to support inferring structures from "target properties / constraints" and achieve inverse design of molecules / materials / structures.
  * Surrogate Model and Multiscale Coupling: Approximate expensive quantum chemistry/continuum/structural mechanics simulations using deep surrogate models, and stitch together micro–meso–macro models to achieve multiscale modeling.
  * Tool Enhancement and Agent Workflow: Combine LLM with simulators, symbolic calculators, automated theorem provers, literature retrieval systems, and experimental robots to build an Agent capable of automatically planning and executing scientific tasks.
* **Model**
  * Molecular and Material Characterization Models: E(3)-equivariant networks and graph networks such as SchNet, DimeNet, PhysNet, CGCNN, MEGNet, ALIGNN, etc., and molecular language models such as ChemBERTa, MolBERT, MoleculeSTM, etc.
  * Structural Biology Models: AlphaFold / AlphaFold2 / AlphaFold3, RoseTTAFold, OpenFold, ProteinMPNN, ESM-IF, ESM Series Protein Language Models and Structure Generation Models.
  * Physical Simulation and Operator Learning: PINN, DeepONet, Fourier Neural Operator (FNO) and the Neural Operator family, DeepMD, NequIP, and other potential energy surface and operator learning models.
  * Mathematics and Symbolic Reasoning Models: Specialized mathematics/proof models such as Minerva, Gödel, GPT‑f, Lean‑Dojo, etc., as well as tool-enhanced systems of LLM + SymPy/Mathematica/Lean/Coq.
  * Scientific Agent and Workflow System: An "AI Scientific Assistant" and self-driven experimental platform encapsulated for fields such as pharmaceuticals, materials, physics, and chemistry, integrating retrieval, code generation, simulation invocation, and experimental control interfaces.

Starting from this level, traditional scientific computing is deeply intertwined with deep learning and large models: it is necessary to respect the strict constraints of physics, chemistry, biology, and mathematics, while also leveraging the strong fitting capabilities of data-driven methods to improve efficiency. The ultimate goal is to make AI a "collaborator" in scientific research, rather than just a predictive black box.

---

## 10.1 Molecular Modeling & Drug Discovery

In traditional drug development, it often takes more than 10 years and billions of dollars from target discovery to clinical trials, with a significant portion of time and funds spent on the early stages of molecular design, property prediction, and virtual screening. AI-driven molecular modeling and drug design aim to use ** data-driven + generative modeling ** to accelerate this process: starting from structural or textual descriptions, predicting molecular properties and ADMET, designing candidate compounds for specific targets, and significantly reducing the burden of wet experiments through multi-objective optimization and virtual screening.

One end of this direction is connected to data sources such as quantum chemistry software (DFT, ab initio), biological activity experiments, and HTS (High-Throughput Screening), while the other end is connected to the Small Molecule Design platform within pharmaceutical companies, property prediction SaaS, and material/chemical design tools. The following will be elaborated from three dimensions:  **scenario** ,  **principle** , and  **model** .

* **Scenario**
  * Early virtual screening and Hit discovery: Facing virtual molecular libraries ranging from millions to billions in scale, AI is used to quickly predict activity/ADMET, rank candidate molecules, and screen out a small number of high-value Hits for experimental validation.
  * Molecular Properties and ADMET Evaluation: During the Lead Optimization stage, continuously predict indicators such as solubility, toxicity, metabolic stability, and oral bioavailability to provide references for pharmacokinetic and safety evaluations.
  * Target-directed molecular generation: Given protein target information (pocket features, known ligands) or target property constraints, automatically generate structurally diverse, highly active, and synthesizable candidate small molecules.
  * Molecular Design of Materials and Chemicals: For non-drug scenarios, such as molecules in coatings, solvents, electrolytes, surfactants, etc., design formulated molecules that meet specific physical properties (viscosity, polarity, interfacial energy, etc.).
* **Principle**
  * Molecular Characterization and Property Prediction:
    * **Structural Representations ** : Commonly include SMILES sequences, molecular graphs (atoms as nodes, bonds as edges), 3D coordinates, and quantum features; models need to extract generalizable semantic and geometric information from these representations.
    * **Property Prediction ** : Through GNN (GCN, GAT, MPNN) or 3D-equivariant networks (SchNet, DimeNet, PhysNet, etc.), learn quantum properties such as energy, dipole moment, orbital energy levels, as well as ADMET properties such as solubility, LogP, toxicity, and metabolic stability from molecular graphs or 3D structures.
    * **Representation Learning and Pretraining ** : Perform masked prediction, contrastive learning, or autoregressive pretraining based on large-scale molecular libraries (such as ZINC, ChEMBL, PubChem) to obtain transferable general molecular representations, providing features for downstream QSAR/ADMET.
  * Structure Generation and Molecular Optimization:
    * **Generative Modeling** : Utilize generative models such as VAE, GAN, Flow, and Diffusion to sample new molecules in the SMILES or molecular graph space, ensuring the chemical structure's legality (valence state, ring structure, etc.) and diversity.
    * **Conditional Generation ** : Introduce conditional vectors (target activity, physicochemical properties, structural fragments, target pocket description, etc.) to generate candidate molecules under given constraints, achieving property-guided or fragment-completion design.
    * **Multi-objective Optimization and RL** : Perform "editing" operations (adding atoms, modifying bonds, replacing fragments) in the molecular space through reinforcement learning (such as MolDQN, etc.), thereby making trade-offs among multiple objectives such as activity, toxicity, synthetic feasibility, and patent avoidance.
  * Protein - Small Molecule Interaction Modeling:
    * **Binding Sites and Scoring Functions** : Model the spatial relationship between protein pockets and ligands through 3D convolution/graph network/interaction graph, and predict binding sites and binding affinity.
    * **Docking and Binding Pose Prediction ** : Combining conformational search in Docking with deep models, using deep scoring functions or Diffusion-style generation to predict stable conformations, improving docking accuracy and reducing computational costs.
* **Model**
  * Molecular Representation Model:
    * **GNN and 3D Networks ** : 3D equivariant models such as DimeNet / DimeNet++, SchNet, PhysNet, etc., which consider angles / distances, and general graph neural networks such as GCN / GAT / MPNN, etc., are suitable for property prediction and QSAR.
    * **SMILES-based Transformer** : Treating molecules as "chemical language sentences", using Transformer for autoregressive or masked language modeling to provide sequence representations for generation and property prediction.
  * Generate and Optimize Model:
    * Graph generation models: GraphVAE, Junction Tree VAE, GraphAF, etc., generate molecules in the graph/fragment space, emphasizing structural validity and interpretability (fragment-level construction).
    * Diffusion Model: Diffusion for Molecules generates new molecules or conformations by adding/removing noise in the graph or 3D structure space, and can be combined with conditional vectors to achieve customized generation.
    * Reinforcement Learning Optimization: RL-based methods such as MolDQN treat molecular optimization as a sequential decision-making problem in the "molecular editing" state space, encoding multi-objective metrics with a reward function.
  * Molecular Large Model and MultiModal Machine Learning Direction:
    * **Molecular Language Models ** : ChemBERTa, MolBERT, etc., are pre-trained on large-scale SMILES corpora and support zero-shot or few-shot transfer to downstream tasks.
    * **MultiModal Machine Learning Molecular Model** : MoleculeSTM and others integrate structure (graph/3D), text description (synthesis route, literature abstract), and molecular properties to achieve cross-modal retrieval and joint prediction.
  * Product and Application Forms:
    * The early drug screening platform for pharmaceutical companies and the internal Small Molecule Design platform provide integrated capabilities such as virtual screening, molecular generation, and ADMET prediction.
    * Property Prediction SaaS for R&D Personnel: Quickly query molecular properties, ADMET, molecular similarity, etc. via Web or API.
    * Molecular-level design tools for materials and chemical design, used for the customized development of molecular systems such as coatings, solvents, and electrolytes.

Starting from this sub-direction, the drug design process is moving from "expert + high-throughput experiment" to a closed loop of "expert + model + automated experiment", where AI not only provides scores but also gradually participates in the entire process from "idea generation" to "candidate generation" and then to "screening and optimization".

### 10.1.1 Molecular Characterization and Properties / ADMET Prediction

In drug and material R&D, a fundamental ability is:  ** given a molecule, to quickly and accurately predict its properties and behavior ** , including quantum chemical properties (energy, orbitals, dipole moment), physical and chemical properties (solubility, LogP), and ADMET indicators related to pharmacokinetics/toxicity. The essence of this problem is how to learn from different forms of molecular representation  ** a representation that conforms to chemical laws and has generalization ability ** .

* At ** molecular characterization ** level, common representations include:
  * **Strings such as SMILES / SELFIES** : Treating molecules as sequences, they are naturally suitable for language modeling using RNN / Transformer.
  * **Molecular Graph Representation ** : Atoms are nodes, bonds are edges, and nodes and edges carry features such as type, valence, and aromaticity; suitable for modeling neighborhoods and topologies using GNN, MPNN, etc.
  * **3D Geometric Representation** : Information such as 3D coordinates, bond angles, and dihedral angles obtained based on quantum chemistry or force field optimization provides a foundation for E(3)-equivariant networks to capture spatial structures.
* At the ** property and ADMET prediction ** level, the target tasks include:
  * Prediction of small molecule quantum properties: energy, dipole moment, HOMO/LUMO energy levels, etc., to replace expensive DFT/ab initio calculations.
  * QSAR / Activity Prediction: Provides the activity (IC50, Ki), selectivity, etc., of compounds against specific targets, used for screening potential candidates.
  * ADMET-related indicators, such as solubility, permeability, toxicity, metabolic stability, CYP inhibition, etc., are crucial for drug developability assessment.

The typical model path is as follows: Extract high-dimensional representations from molecular structures using DimeNet, SchNet, PhysNet, GNN, etc., and then simultaneously predict multiple properties through multi-task learning; pre-train on large-scale public or enterprise internal data to improve the modeling ability in small-data scenarios. Externally, services are provided in the form of ADMET prediction SaaS or internal platform APIs, providing project teams with rapid "virtual experiment" capabilities.

### 10.1.2 Structure Generation and Molecular Optimization: From SMILES/Graph to Candidate Drugs

After establishing reliable molecular characterization and property prediction models, the next step is to  ** actively generate "better" molecules ** : instead of merely evaluating given compounds, directly design new candidate molecules based on target and property constraints. This direction is commonly referred to as  ** molecular generation and molecular optimization ** .

In  ** structure generation ** , research and engineering practice mainly revolve around three types of paths:

1. **SMILES-based Sequence Generation**
   Treat molecules as strings, and use VAE, GAN, or autoregressive Transformer to sample new structures in the SMILES space; ensure chemical validity through grammar constraints (such as SELFIES) or post-processing.
2. **Graph/Fragment-based Generation**
   Models such as GraphVAE, Junction Tree VAE, and GraphAF directly construct structures at the molecular graph or primitive fragment (Fragment/Motif) level, which is closer to the thinking of chemical synthesis and conducive to controlling ring, group, and backbone structures.
3. **Based on diffusion and 3D generation**
   Methods such as Diffusion for Molecules perform diffusion and denoising in graph or 3D coordinate space, which can simultaneously consider spatial conformations and are suitable for generating ligands or material units sensitive to 3D shapes.

In  ** molecular optimization ** , the key is to introduce  ** objectives and constraints ** :

* **Conditional Generation** : Input the target activity, physicochemical properties, or fragment anchoring as a conditional vector into the model, causing it to be biased towards satisfying these conditions during generation.
* **Reinforcement Learning and Multi-Objective Optimization ** : Using the property prediction model as the "environment", RL is used to make sequential decisions in the molecular space (such as MolDQN), setting rewards and penalties on multi-dimensional indicators such as activity, toxicity, synthetic feasibility, and patent risk to achieve multi-objective trade-offs.
* **Synthesis Feasibility and Chemical Priors ** : Incorporate synthetic pathway prediction models and synthetic complexity metrics (such as SA score) into the generation and optimization process to avoid generating structures that are difficult to synthesize or unstable.

In productization, this type of model is often encapsulated into the "AI Drug Design Platform" within pharmaceutical companies: given a target, known lead structures, and optimization directions, the platform automatically proposes several batches of candidate molecules, and the project team then gradually screens and iterates based on experimental, patent, and commercial considerations to achieve closed-loop optimization of "model - experiment - model".

## 10.2 Protein & Structural Biology Modeling (Protein & Structural Biology)

In life sciences, ** structure determines function ** is an almost dogmatic principle: how proteins fold into three-dimensional structures and assemble into complexes with other molecules directly determines their functional performance in cells. Traditional structure determination relies on experimental methods such as X-ray crystallography, NMR, and cryo-electron microscopy, which have long cycles, high costs, and significant blind spots of "difficult to crystallize and difficult to resolve". Deep learning models represented by AlphaFold have greatly advanced the ability to "go directly from sequence to structure", making it possible to obtain high-quality structures on a whole-genome scale.

One end of this direction connects to sequence and structure databases such as UniProt/PDB, omics experiments, and structural omics projects, while the other end connects to structural design and analysis platforms in industries such as biopharmaceuticals, synthetic biology, and enzyme engineering. Similarly, the following will be expanded from three perspectives:  **scenarios** ,  **principles** , and  **models** , and key sub-directions will be further broken down.

* **Scenario**
  * Target Structure Annotation and Screening: Predict the structures of a large number of proteins at the genomic level to assist in target discovery, functional annotation, and pathway analysis; evaluate potential pathogenic mechanisms in combination with variant information.
  * Antibody/Protein Drug Design: Conducts fine-grained modeling and design of key regions such as antibody variable regions (CDRs) and receptor binding domains to optimize affinity, specificity, and immunogenicity.
  * Enzyme and Biocatalyst Design: Based on the three-dimensional structure of the enzyme and the environment of the active site, design mutation and variant libraries to improve catalytic efficiency, substrate scope, and stability.
  * Complex and Interaction Studies: Predict the structures of protein–protein, protein–nucleic acid, and protein–small molecule complexes, analyze the interaction patterns at the interfaces, and provide a foundation for drug design and signaling pathway modeling.
  * Analysis of Mutation Effects and Drug Resistance: Evaluate the impact of natural variations or artificial mutations on structural stability, function, and ligand binding, and analyze the structural basis of drug-resistant mutations.
* **Principle**
  * Protein Structure Prediction:
    * **Sequence → Structure** : Starting from the amino acid sequence (single sequence or containing multiple sequence alignment MSA), model the geometric constraints (distance, angle, contact map) between pairs of residues, and then generate the full-atom 3D structure through the geometric reconstruction module.
    * **Co-evolution Signal** : By leveraging the co-evolutionary mutation patterns (co-evolution) among homologous sequences, potential residue contact relationships are inferred, providing strong priors for folding constraints.
    * **Structure Refinement and Uncertainty Estimation** : Perform local refinement (relax, repack) on the predicted structure, and output confidence level scores (such as pLDDT, PAE) to guide the selection of "reliable regions" in subsequent applications.
  * Modeling of Complexes and Molecular Assembly:
    * **Multi-chain Joint Modeling** : Taking multiple protein chains or protein + nucleic acid sequences as input, introducing chain identification and interface constraints, and directly outputting the complete complex structure.
    * **Interface Prediction and Assembly** : Based on the known monomer structure, predict the most likely interface configuration and assembly method through graph models or diffusion models.
  * Protein Design and Mutation Effect Prediction:
    * **Inverse Folding ** : Given a three-dimensional backbone structure or topological constraints, generate an amino acid sequence that can stably fold into this structure, achieving de novo protein design.
    * **Modeling of Mutation Effects ** : Combining protein language models and structural models to predict the impact of specific mutations on stability (ΔΔG), activity, or binding affinity, and to assist in directed evolution and variant screening.
* **Model**
  * Structure Prediction:
    * AlphaFold / AlphaFold2 / AlphaFold3: Centered around attention mechanisms and geometric modules, it predicts high-precision protein structures from MSA, template structures, and sequence features, and outputs uncertainty estimates.
    * RoseTTAFold, OpenFold: Adopt multi-track (sequence / pair / structure) representation and multi-scale attention mechanism, providing a fundamental implementation for open source and industrialization.
  * Complex and Interface Modeling:
    * AlphaFold-Multimer: Directly models the structure of protein-protein complexes in multi-chain scenarios, taking into account both monomer folding and interface interactions.
    * RFdiffusion: Based on diffusion models, it generates or optimizes protein backbones and complex interfaces in 3D space, enabling the design of complex assemblies and symmetric bodies.
    * Methods such as DiffDock: In protein-small molecule systems, use diffusion or deep scoring functions to predict Binding Pose and binding modes.
  * Design and Mutation Model:
    * ProteinMPNN: Generate compatible sequences given a structure for stable backbone and interface design.
    * ESM-IF, ESMFold / ESM-2 Series: Language models pre-trained on large-scale protein sequences, capable of inferring structure, function, and mutation effects from sequences.
  * Products and Applications:
    * Protein structure prediction services and databases (such as AlphaFold DB) on the Public Cloud provide large-scale structural annotation and download interfaces for scientific research.
    * Biopharmaceutical Company Internal Structure Design Platform: Integrates modules such as protein structure prediction, antibody design, enzyme engineering, and protein-ligand docking.
    * Biotech SaaS: Provides tools for binding site prediction, interface thermodynamics evaluation, affinity and immunogenicity assessment, serving the development of antibody drugs and biologics.

Starting from this sub-direction, AI is not only "interpreting" naturally occurring protein structures, but also "creating" entirely new protein and complex architectures, propelling structural biology from the "passive measurement era" into the "active design era".

### 10.2.1 Protein Structure Prediction and Complex Assembly

Protein structure prediction is one of the most representative breakthroughs in the combination of structural biology and AI. Its core question is:** Can we predict a 3D structure close to experimental resolution starting from the sequence, without relying on or with minimal reliance on experimental data?** In real-world applications, the monomeric structure is often just the starting point, and more critically, how proteins assemble into complexes with other molecules.

In  ** monomer structure prediction ** , the typical process includes:

1. **Seque** **nce**  **/MSA Encoding** : Mining co-evolutionary signals through sequence feature extraction and multiple sequence alignment.
2. **Geometric Constraint Inference** : Predict the distance distribution, contact probability, and relative orientation between residue pairs to form a geometric field of "pseudo-measurements".
3. **Structure Construction and Iterative Refinement ** : Construct 3D structures using structural modules (such as rotation-translation invariant blocks, internal coordinate updates) under geometric constraints, and perform multiple iterative refinements to reduce geometric violations.
4. **Uncertainty and Quality Assessment** : Output indicators such as per-residue Confidence Level (pLDDT) and residue pair error estimation (PAE), providing references for subsequent modeling and screening.

In  ** complex and assembly prediction ** , the problem is further extended to "how multiple chains are organized and interact in space":

* For  **protein–protein complexes** , specialized multi-chain modeling strategies (such as AlphaFold‑Multimer) are typically used to directly output the assembly structure based on multi-chain input.
* For  ** protein-nucleic acid / protein-small molecule systems ** , one approach is to first predict the respective structures and then predict the assembly mode through docking and interface scoring functions; the other is to directly generate complex conformations in 3D space using diffusion models or joint modeling.
* In the context of multi-subunit and large assemblies, it is also necessary to combine information such as symmetry constraints and low-resolution EM density maps to perform hierarchical and multi-scale assembly.

In product practice, structure prediction and assembly are often encapsulated as cloud services or local toolchains, providing basic structural information for protein function annotation, interaction network modeling, and drug target validation.

### 10.2.2 Protein Design and Mutation Effect Prediction: From Structure to Functional Regulation

After mastering the mapping of "sequence → structure", the next step is the inverse problem: ** How to design appropriate protein sequences and mutation schemes given structural or functional requirements? ** This is the core of protein design and prediction of mutation effects.

In  ** protein design ** , key tasks include:

* **Inverse Folding ** : Given a target backbone or overall topology, generate an amino acid sequence that can stably fold into this structure. This process can be achieved through structure-conditioned generative models such as ProteinMPNN and ESM-IF.
* **Function-oriented design** : On the premise of maintaining the stability of the overall structure, targeted design is carried out for active sites, binding pockets, and interface regions to optimize affinity, specificity, and catalytic efficiency.
* **Manufacturability and Immunogenicity Constraints** : During the sequence design process, constraints such as expression feasibility, post-translational modifications, and immunogenicity risks are introduced to ensure the feasibility of candidate sequences in biopharmaceutical development.

In  ** mutation effect prediction ** , the focus is on:

* **Stability change (ΔΔG)** : Given a wild-type structure and mutation sites, predict the impact of single or multiple mutations on folding stability, used for directed evolution and drug resistance mutation analysis.
* **Changes in Activity and Affinity ** : Combining structural analysis with protein language models to evaluate the impact of mutations on enzymatic activity, ligand affinity, and signal pathway regulation.
* **Design of large-scale variant libraries** : Before in vivo/in vitro screening experiments, use models to pre-screen the vast mutation space, retain high-potential variants, and reduce experimental costs.

At the engineering and product levels, protein design and mutation effect prediction are often integrated into the "structural design and optimization module" within biopharmaceutical/synthetic biology companies: starting from the candidate backbone structure, automatically proposing multi-round mutation and variant library design schemes, and forming a data-driven closed loop with high-throughput screening experiments.

## 10.3 Physics Simulation & Surrogate Modeling

In the fields of aerospace, automotive, civil engineering, energy, chemical engineering, etc.,  ** high-precision simulation is a core part of design and verification ** . However, CFD (Computational Fluid Dynamics), FEA (Finite Element Analysis), Molecular Dynamics (MD), and various PDE solvers often incur high computational costs and struggle to support large-scale parameter scanning, real-time control, or online optimization. AI-driven physical simulation and surrogate modeling attempt to approximate numerical solvers or operators themselves using deep networks, achieving an order-of-magnitude acceleration while ensuring physical consistency and interpretability.

One end of this direction is connected to traditional simulation software (ANSYS, Fluent, COMSOL, self-developed solver), experimental measurement, and sensor data, while the other end is connected to engineering design platforms, autonomous driving and aerospace aerodynamic design, and chemical process simulation and optimization systems. The following will be expanded from three perspectives:  **scenario** ,  **principle** , and  **model** .

* **Scenario**
  * Engineering simulation acceleration: Under given geometry and operating conditions, use deep surrogate models to quickly predict pressure fields, velocity fields, temperature fields, stress/strain distributions, etc., providing support for multiple rounds of design iteration and optimization.
  * Complex Process Simulation and Process Optimization: In process industries such as chemical engineering and energy, rapid evaluation and real-time control are achieved through ML approximation of mechanism models or black-box process models.
  * Molecular/material scale simulation: Replace high-cost ab initio potential and force calculations with ML potential energy surfaces (Neural Network Potential) to accelerate molecular dynamics and material phase behavior simulations.
  * Multiscale and interdisciplinary coupling: By using deep surrogate models to stitch together micro–meso–macro models, an end-to-end multiscale simulation and optimization link is constructed.
* **Principle**
  * Surrogate Models / Proxy Models (Surrogate Models):
    * Learn the mapping of "input parameters → output field / metrics" from numerical simulations or experimental data as an approximation of the high-fidelity solver.
    * In high-dimensional parameter space, by combining active learning with Bayesian optimization, the most informative sample points are automatically selected for high-fidelity simulation or experiment, continuously improving the quality of the surrogate model.
  * Physics-Informed Neural Network (PINN):
    * Write PDEs, initial/boundary conditions, and physical conservation laws into the loss function, and use automatic differentiation techniques to solve the physical field in the continuous space.
    * Supports forward problems (solving for the state field) and inverse problems (inferring source terms, material parameters, etc. from sparse observations), and is particularly suitable for complex geometries and boundaries that are difficult to handle using traditional numerical methods.
  * Operator Learning and Neural Operator:
    * Instead of merely fitting the "solution under specific conditions", it learns the mapping from function to function (operator), such as "boundary conditions / source terms → the entire solution field".
    * Representative methods such as Fourier Neural Operator (FNO), DeepONet, etc., enhance the generalization ability to different grid densities and geometric shapes through frequency domain transformation or specific network architectures.
  * Multiscale Modeling:
    * The training of effective parameters or constitutive relationships at the meso/macro level on micro-simulation data is carried out by the deep surrogate model, which assumes the role of the "scale bridging layer".
    * For problems such as complex materials, fluid-structure interaction, and multiphase flow, use deep models to transfer information between different scales and physical modules.
* **Model**
  * Universal Physical Neural Network:
    * PINN Series: Solved by minimizing PDE residuals at sampling points in the spatio-temporal domain, applicable to equations such as Navier‑Stokes, Maxwell, and elasticity.
    * DeepONet, FNO, Neural Operator Family: Directly learn the "operator-level" approximation of PDE solvers, enabling fast inference under multiple operating conditions and geometries.
  * Molecular/Material Scale Potential Energy Model:
    * DeepMD, SchNet, NequIP, SpookyNet, etc.: Construct high-precision ML potential energy surfaces, significantly accelerating force and energy calculations while maintaining accuracy close to ab initio.
    * Coupled with traditional MD engines, it enables high-precision molecular dynamics for large systems and long time scales.
  * CFD / Structural Mechanics Surrogate Model:
    * Encoder-Decoder networks such as U-Net / UNet++: Predict flow fields or temperature fields from geometric / boundary conditions on regular grids.
    * Graph Neural Networks on Mesh: Perform message passing and updating on nodes/elements on unstructured meshes, suitable for complex geometry and multi-physics coupling scenarios.
    * Neural Operator for CFD: Generalizing Flow Field Prediction under Different Reynolds Numbers, Inflow Conditions, and Geometric Parameters.
  * Products and Applications:
    * AI Acceleration Module in Industrial Simulation Software: Provides fast prediction and sensitivity analysis functions outside the traditional solver.
    * Chemical / Energy Process Simulation and Optimization Platform: Combines mechanism models + surrogate models + optimization algorithms into an integrated process optimization tool.
    * Autonomous driving / Aerospace aerodynamic design: Conduct large-scale design variable scanning and automatic shape optimization in aerodynamic shape design.

### 10.3.1 Surrogate Models and Physics-Informed Neural Networks (PINN)

**Surrogate Models** and **Physics-I****nfor****med** **Neural Networks** **(PINN)** are two complementary paths for AI-enabled physical simulation: the former approximates the simulation mapping from data, while the latter constructs learning objectives from physics.

In ** the alternative model ** scenario, the typical process is:

1. Collect a batch of sample data (input parameters, boundary conditions, geometry → output physical quantities) through high-fidelity numerical simulation or experimental acquisition.
2. Train deep networks (such as MLP, convolutional networks, GNN, Neural Operator) to approximate this mapping function.
3. In design optimization, parameter scanning, or real-time control, surrogate models are used to replace expensive solvers for rapid evaluation.

In ** PINN ** scenarios, the model no longer relies primarily on a large number of supervised labels, but constructs the loss function by minimizing the PDE residual and boundary condition violations:

* At spatial/temporal sampling points, a neural network outputs physical quantities (such as velocity, pressure, displacement field, etc.), and automatic differentiation is used to obtain gradients and derivatives.
* Substitute these derivatives into the PDE to form the residual, which, together with the errors of the boundary conditions and initial conditions, constitutes the total loss.
* By optimizing to make the PDE residual and boundary error as close to 0 as possible, an approximate solution that satisfies the physical equation is obtained.

The two can be used in combination: when there is partial high-fidelity data, data error + physical residual are used together to jointly constrain the training, improving accuracy and generalization ability. In engineering applications, PINN is particularly suitable for handling inverse problems and Data drive modeling, such as inferring material parameters, source terms, or defect locations from sensor observations.

### 10.3.2 Neural Operator and Multiscale Physical Modeling

**Neural Operator** elevates physical modeling from the "point-to-point / parameter-to-solution" mapping to the "function-to-function" level: it learns the unified operator approximation of "given a class of PDEs and boundary conditions, solve their solution fields", rather than specific solutions under a single operating condition. This provides new possibilities for generalization across multiple operating conditions, multiple geometries, and cross-grid resolutions.

In  ** operator learning ** , the typical approach is:

* Taking functions (such as source terms, boundary conditions, material parameter fields, etc.) as inputs, the network (such as FNO, DeepONet) outputs the entire solution field function.
* By training samples on different grids, different parameters, and different geometries, the model learns the "common patterns" of PDE solvers.
* During deployment, simply providing a new input function (such as new boundary conditions or geometry) enables rapid inference to obtain an approximate solution field.

In ** multi-scale modeling ** scenarios:

* Train Neural Operator on a large amount of data generated at the microscale (e.g., molecular dynamics, crystal plasticity) to learn the mapping between microstructure and macroscopic response.
* In the macroscopic continuum model, this mapping is used as a constitutive relation or an effective parameter calculation module to achieve micro - macro coupling.
* For complex systems such as fluid-structure interaction, multiphase flow, and reactive flow, different physical fields can be modeled separately and coupled through shared interface variables (such as fluxes, interfacial forces, etc.).

In engineering practice, Neural Operator has gradually evolved from a research prototype to application, becoming an important technological direction for "accelerated solver + multi-scale bridging" in scenarios such as CFD, geophysics, and climate modeling.

## 10.4 Materials Discovery & Crystal Design (Materials Science & Crystal Design)

In materials science, a core contradiction is that  ** the design space is almost infinite, while the costs of experiments and high-precision calculations are extremely high ** . How to efficiently find candidate materials that meet specific performance requirements in the vast space of chemical and structural combinations is a key issue in fields such as new energy, electronics, structural materials, and functional materials. AI-driven materials discovery and crystal design, through graph neural networks, generative models, and high-throughput virtual screening, are gradually shifting "trial-and-error" R&D towards "Data drive + inverse design".

One end of this direction connects material databases such as Materials Project, OQMD, AFLOW, and DFT/MD calculation results, while the other end connects material R&D platforms for application scenarios such as batteries, photovoltaics, catalysis, semiconductors, and alloys. The following will be elaborated from three perspectives:  **scenarios** ,  **principles** ,  **models** .

* **Scenario**
  * Performance-oriented material screening: Given a crystal structure or chemical formula, predict the band structure, band gap, carrier mobility, thermal/electrical/magnetic properties, etc., providing a basis for material screening and combinatorial optimization.
  * New energy materials R&D: Focusing on systems such as battery electrolytes, electrode materials, solid-state ionic conductors, photovoltaic absorber layers, and catalysts, predict ionic conductivity, stability, electrochemical window, and activity, etc.
  * High-throughput virtual screening (HTVS): In the constructed large-scale candidate library, potential materials are screened out through rapid evaluation by ML models, and then verified and calibrated with a small amount of DFT/experimental data.
  * Reverse design of crystal structure and composition: Starting from the target properties, reverse search for crystal structure/composition combinations that meet performance and process constraints.
* **Principle**
  * Material and Crystal Representation:
    * Represent the periodic crystal structure as a Crystal Graph: nodes are atoms, edges are the nearest neighbor relationships between atoms, combined with lattice parameters and space group information.
    * For amorphous or complex multi-phase materials, their microstructures can be represented by local environment descriptors (such as SOAP), Voronoi features, or multi-scale graph structures.
  * Property prediction:
    * Perform convolution/message passing on crystal graphs using GNN models such as CGCNN, MEGNet, and ALIGNN to predict energy, band gap, elastic modulus, thermal conductivity, etc.
    * Utilize literature and chemical formula-based embeddings such as Mat2Vec to achieve transfer learning and zero-shot estimation in low-data scenarios.
  * High-throughput virtual screening:
    * Construct a candidate library (through combinatorial enumeration, structure generation, empirical rules, etc.) → Use ML models to quickly predict properties → Screen out a small number of top candidates for DFT or experimental calibration → Update the model and screening strategy to form a closed loop of active learning.
  * Generation and inverse design:
    * Sampling new structures in the crystal structure space using generative models such as diffusion models, VAE, or GNN allows for the imposition of constraints such as composition, space group, density, etc.
    * Combining surrogate models with Bayesian optimization, search for suitable structure/component combinations starting from the target properties to achieve inverse design.
* **Model**
  * Characterization and Prediction:
    * CGCNN (Crystal Graph Convolutional Neural Network): Performs convolution on crystal graphs for predicting properties of inorganic materials such as energy and band gap.
    * MEGNet, ALIGNN: Integrating graph structure with edge/angle information, they exhibit stronger generalization and accuracy across multiple material families.
    * Mat2Vec + Lightweight ML: By vectorizing chemical formulas and element information, quickly train small models for specific property prediction.
  * Generation and inverse design:
    * Diffusion for Crystals: Perform diffusion/denoising in the high-dimensional space composed of lattice parameters and atomic positions to generate crystal structures that satisfy certain constraints.
    * GNN - based Generative Models: Achieve structure search from random initialization to the vicinity of target properties by gradually adding/modifying atoms and bonds or manipulating lattices.
    * Surrogate + Bayesian Optimization: Use an ML model as an approximate black box for "structure → property", perform Bayesian optimization on it, and search for the optimal structure or composition.
  * Data Platform and Toolchain:
    * Materials Project, OQMD, AFLOW: Provide a large amount of structural and DFT calculation data, which are the basis for training and evaluating materials ML models.
    * Enterprise internal material database and model: Combining the company's experimental data and process information, a domain-specific material AI design platform is constructed.
  * Products and Applications:
    * New Energy Materials R&D Acceleration Platform: Provides integrated property prediction, HTVS, and inverse design capabilities for teams in battery, electrocatalysis, photovoltaics, etc.
    * Virtual screening software and SaaS: Provide digital screening tools for alloys, semiconductors, functional ceramics, etc., reducing early-stage trial-and-error costs.
    * AI design tools within the materials company: Connect with the Laboratory Information Management System (LIMS) and production line data to form a closed loop from "model → experiment → production".

### 10.4.1 Material Property Prediction and High-Throughput Virtual Screening (HTVS)

In the material R&D process, ** fast and reliable ****pro****perty prediction ** is a fundamental capability: given a candidate structure or composition, can we roughly determine whether it is worth in-depth exploration without performing expensive DFT/experiments? The property prediction model based on GNN and material databases makes high-throughput virtual screening possible.

At the ** property prediction ** level:

* Use crystal graphs to represent periodic structures, and learn the interactions between atoms and their neighborhoods through models such as CGCNN, MEGNet, and ALIGNN.
* Conduct single-task or multi-task training for different tasks (energy, band gap, elastic constants, thermal conductivity, electrical conductivity, magnetism, etc.), achieving prediction performance close to DFT accuracy on datasets such as Materials Project.
* In industrial scenarios, retraining or domain Self-Adaptation is often combined with internal experimental data to improve the adaptability to specific material families and process conditions.

In ** High Throughput Virtual Screening (HTVS) ** scenarios, the typical process is:

1. Build a large-scale candidate library (combination enumeration, structure generation, or expansion from existing databases).
2. Use ML models to quickly predict the target properties and auxiliary properties (such as stability, safety, cost-related indicators, etc.) of each candidate.
3. Screen and rank according to the target nature and multiple constraints, and select Top-K candidates for high-fidelity DFT calculations or experimental verification.
4. Feed the verification results back into the model, update the parameters and uncertainty estimates, and form an active learning closed loop of "screening - verification - re-screening".

This workflow has entered the practical stage in multiple fields such as battery materials, photovoltaic absorber layers, catalysts, and structural materials, becoming the "pre-screening engine" for material R&D teams.

### 10.4.2 Crystal Generation and Inverse Design: From Target Properties to Candidate Structures

After having reliable property prediction and HTVS capabilities, the further goal is  ** to directly propose new crystal structure and composition candidates from the target properties and constraints ** , i.e., the inverse design and generation of materials.

In  ** crystal generation ** , the key issues include:

* How to generate physically reasonable lattice and atomic arrangements under periodic constraints?
* How to explicitly or implicitly impose constraints such as composition, symmetry, and density during the generation process?
* How to ensure that the generated structure remains stable after simple relaxation?

To this end, research and engineering practice often adopt:

* **Diffusion for Crystals** : Add/remove noise in the joint space of lattice parameters + atomic positions to achieve progressive generation from random initial states to structural samples, and incorporate target properties and composition constraints into the noise process or conditional vector.
* **GNN** ** - based Generative Models** : Gradually add atoms and connection relationships to the graph structure, or edit existing structures to generate candidate structures that satisfy the constraints.

In  ** inverse design ** , it is usually combined with surrogate models and optimization methods:

* Treat the property prediction model as a black-box function of "structure → property".
* Explore the structural space through Bayesian optimization, evolutionary algorithms, or RL to gradually approach the target value of the predicted properties while satisfying constraints such as stability, safety, and cost.
* Perform DFT/experimental validation on the candidate structures obtained from the search, and use the results to update the surrogate model and search strategy.

In engineering applications, the inverse design module is often integrated into the materials AI platform, providing R&D personnel with an interactive interface of "setting target properties → the system automatically proposing candidate structures", which significantly improves the efficiency of new material exploration.

## 10.5 Mathematics & Symbolic Reasoning

Mathematics is a highly formalized and precisely verifiable language, which endows it with both the attributes of "extremely difficult" and "potentially highly rewarding" in the AI era. On the one hand, complex theorem proving and high-order reasoning place extremely high demands on model capabilities; on the other hand, the results of mathematical reasoning and symbolic computation can be rigorously verified, making it naturally suitable for collaboration with procedural tools. The goal of AI in the direction of mathematical and symbolic reasoning is to construct models that can**perform reliable reasoning and computation**within formal systems and integrate them into education, scientific research, and engineering applications.

One end of this direction connects to interactive theorem provers such as Lean, Coq, and Isabelle, computer algebra systems (CAS) such as SymPy, Mathematica, and Maple, as well as large mathematical question banks and literature corpora; the other end connects to mathematical education products, auxiliary research tools, and the needs for formula derivation and Risk Analysis in fields such as engineering and finance. The following will be elaborated from three perspectives:  **scenarios** ,  **principles** ,  **models** .

* **Scenario**
  * Automated Theorem Proving and Proof Assistance: Automatically provide theorem proofs in formal systems, or generate readable proof drafts for further review and refinement by humans.
  * Expression Manipulation and Symbolic Computation: Automatically simplify expressions, perform differentiation, integration, series expansion, transformation, and equation solving, providing symbolic tools for engineering modeling and financial Risk Analysis.
  * Mathematical Problem Understanding and Solution Step Generation: Extract structured representations from problems in natural language or images, provide rigorous and verifiable solution steps, and serve educational and training scenarios.
  * Enhanced Mathematical Reasoning Ability: Through specialized fine-tuning and tool enhancement in mathematics, improve the multi-step reasoning and rigor of large models in fields such as arithmetic, algebra, geometry, and combinatorics.
* **Principle**
  * Formal Systems and Search:
    * Within systems such as Lean, Coq, and Isabelle, mathematical objects and theorems are formalized as terms and types, and the proof process corresponds to constructing proof trees under the constraints of rules.
    * Proof search can be regarded as "finding a path that satisfies constraints in a vast state space" and is suitable for methods such as reinforcement learning, MCTS (Monte Carlo Tree Search), and policy network/value network.
  * Neural - Symbolic Synergy:
    * LLM is responsible for extracting problem structure and solution ideas from natural language or unstructured input, and translating them into symbolic expressions (such as SymPy code, Lean proof scripts).
    * Computer algebra systems and theorem provers are responsible for performing rigorous symbolic computations and formal verification, as well as validating and correcting the outputs of LLMs.
  * Improvement of Mathematical Reasoning Ability:
    * Improve the model's understanding of mathematical language and mastery of reasoning styles by conducting targeted pre-training or fine-tuning on large-scale mathematical texts and question banks (e.g., Minerva, Gödel).
    * By adopting the Tool-Augmented LLM framework, using symbolic solvers, numerical computation libraries, plotting tools, and provers as external tools, the model is enabled to learn to "call tools" rather than "memorize results" in complex reasoning.
* **Model**
  * Automated Theorem Proving:
    * AlphaZero-style prover: Treats the proof process as a game process, uses policy networks and value networks to guide the search, and gradually constructs formal proofs.
    * GPT-f, Lean-Dojo, etc.: Trained on large-scale formal theorem and proof corpora, used for automatically generating proofs in systems such as Lean.
  * Mathematical Large Models and Tool Enhancement:
    * Minerva, Gödel, etc.: Large models fine-tuned on corpora such as math textbooks, papers, and question banks perform better on proof problems, competition problems, and high-order reasoning tasks.
    * LLM + SymPy / Mathematica / Lean / Coq: LLM performs problem analysis and strategy planning, and invokes symbolic computation and proof tools for precise operations and verification.
  * Products and Applications:
    * The "Math Assistant / Problem Solving Helper" in educational products provides personalized explanations and multiple solution paths.
    * Auxiliary research tools: assist researchers in formulating conjectures, generating proof drafts, searching for relevant theorems and lemmas, and accelerating theoretical exploration.
    * Formula derivation and risk model analysis in engineering/finance: formalize complex models, conduct symbolic sensitivity analysis and compliance review.

### 10.5.1 Automated Theorem Proving and Formal Reasoning

**Automat****ed ****theorem proving (AT****P) an****d interactive theorem proving (ITP)** are important directions at the intersection of mathematics and computer science. The core task of AI's involvement in this field is to automatically construct or assist in constructing proofs within formal systems, reducing the human burden on low-level details and enabling humans to focus more on high-level thinking.

In  ** formal system ** :

* The theorem is encoded as the goal type to be constructed, and the proof corresponds to constructing a term whose type is this goal type.
* The proof process consists of a series of tactics or inference steps, each advancing under strict logical rules.

AI can play multiple roles in it:

1. **Tactical Selection and Parameter Recommendation ** : In the current proof state, predict the tactics and their parameters to be used in the next step, reducing manual trial and backtracking.
2. **Lemma and Theorem Retrieval ** : Retrieve the most relevant lemmas/theorems from a large library to narrow down the search space.
3. **End-to-end proof generation** : Given a theorem and its context, directly generate a complete or partial proof script, which is then verified for correctness by a prover.

Works such as AlphaZero-style provers, GPT-f, and Lean-Dojo have achieved the automatic proof of a significant proportion of theorems in systems like Lean/Coq by training policy and value networks or language models on large-scale formal corpora. In the product direction, this type of capability is expected to evolve into a "formal verification assistant" for software/hardware verification, cryptographic protocol analysis, and high-reliability system design.

### 10.5.2 Symbolic Computation and Mathematical Problem Solving: LLM + CAS

Compared to theorem proving,** symbolic computation and mathematical problem solving ** are closer to engineering and educational scenarios. Its goal is:  ** starting from natural language problems, automatically constructing symbolic expressions, performing calculations, and providing interpretable problem-solving steps ** .

In this direction, a typical neural-symbolic collaboration process is:

1. **Problem U****nde** **rstanding and Abstraction ** : LLM parses questions from natural language or images into structured mathematical expressions (equations, constraints, objective functions, etc.).
2. **Symbolic Expressi****on ****Genera** **tion** : Translate abstract results into CAS code (e.g., SymPy expressions, Mathematica commands).
3. **Invoke  **CAS ** Execution ** : Use CAS for precise algebraic operations, differentiation, integration, solving systems of equations, limits, etc.
4. **Result Inte****rpr****etat****ion** ** and Step Generation** : Based on the calculation results of CAS, LLM generates problem-solving steps and explanations that conform to human habits.

This model has several key advantages:

* Ensure the correctness of calculations through CAS, avoiding "misaligned operations" and cumulative errors of LLMs in long arithmetic expressions.
* By providing Natural-language Understanding and expression through LLM, it lowers the usage threshold of CAS, enabling non-professional users to also utilize powerful symbolic tools.
* In educational scenarios, it can control the level of detail and style of problem-solving, generating explanations suitable for different learning stages.

In engineering/financial scenarios, this capability can be extended to the formulation and analysis of complex models: automatically extracting model structures from documents and code, constructing symbolic representations, and performing sensitivity analysis, boundary case analysis, and risk identification.

## 10.6 Scientific Workflow & Lab Automation

Most of the previous sub-directions have focused on "single-point capabilities": predicting a property, generating a structure, or proving a theorem. However, in real scientific research and industrial R&D, what is more crucial is how to **connect these capabilities into a complete ****workflow**and integrate it with literature, databases, simulation platforms, and automated experimental equipment. The direction of scientific workflow and automated experimentation aims to build an integrated system of **Agent + Tools + Robots **for scientific scenarios, enabling AI to evolve from "being able to calculate" to "being able to conduct experiments and research".

One end of this direction connects to paper and patent databases (such as PubMed, arXiv), scientific data warehouses, domain Knowledge Graphs, and simulation platforms, while the other end connects to automated laboratories (Robotic Lab), high-throughput screening equipment, and scientific research Process management systems. The following will be elaborated from three perspectives:  **scenarios** ,  **principles** ,  **models** .

* **Scenario**
  * Scientific Literature Mining and Knowledge Base Construction: Automatically extract information such as compounds, proteins, materials, reaction conditions, experimental results, etc. from a vast amount of papers to construct a structured Knowledge Base and Knowledge Graph.
  * Experimental Design and Self-Driving Lab: Under the guidance of the experimental plan proposed by AI, the robotic experimental platform automatically performs formulation, reaction, measurement, and Data Acquisition to achieve "closed-loop" optimization.
  * Scientific Data Management and Reproducibility Assurance: Automatically organize simulation and experimental data, metadata, and code scripts, generate standardized experimental records and reports, and improve traceability and reproducibility.
  * Domain "AI Experiment Assistant": Provides one-stop support for literature retrieval, protocol design, experiment planning, and result analysis for pharmaceutical companies, materials companies, and research institutions.
* **Principle**
  * Literature Mining and Domain LLM:
    * Utilize domain pre-trained models such as SciBERT, BioBERT, and PubMedBERT for Named Entity Recognition, Relation Extraction, Reaction Parsing, and Experimental Condition Extraction.
    * On this basis, train domain-specific LLMs such as Bio-LM, Chem-LM, and Materials-LM to enhance the understanding and reasoning abilities regarding professional terms, experimental statements, and implicit assumptions.
  * Experimental Design and Self‑Driving Lab:
    * Treat the experimental space (formulation, temperature, time, addition order, etc.) as optimization variables, and let LLM + RL or Bayesian optimization strategies propose the next set of experimental conditions.
    * The experimental robots and instruments execute according to the plan, collect data and post it back in real time, with the model updating parameters and estimating uncertainty to form a closed loop of active learning.
  * Workflow Orchestration and Agent:
    * Under the Agent & Tool Use framework, tools for literature retrieval, code generation, simulation invocation, Data Analysis, visualization, and report generation are unified and incorporated.
    * The Agent automatically plans task decomposition, the order of tool invocation, and result integration based on the task objective (e.g., "find a highly conductive electrolyte formulation").
* **Model**
  * Literature and Knowledge Mining Model:
    * SciBERT, BioBERT, PubMedBERT, etc.: Models pre-trained on scientific and biomedical literature, used for entity/relationship extraction, classification, and question answering.
    * Galactica, Domain-Specialized LLM: Trained primarily on scientific corpora, it supports functions such as review generation, code drafting, and experimental design suggestions.
  * Experimental Planning and Control Model:
    * LLM + RL / Bayesian Optimization: Combine domain prior, model uncertainty, and experimental cost to efficiently explore and exploit the experimental space.
    * Agent integrated with the Robotic Lab control interface: Converts natural language experiment descriptions into structured experiment steps and instrument control commands.
  * Science Agent and Workflow System:
    * Based on the capabilities of Chapter 7 Agent & Tool Use, build a "multi-tool Agent" for scientific scenarios: capable of retrieving literature, generating code, invoking simulations, processing data, plotting charts, and writing a first draft of reports.
  * Products and Applications:
    * "AI Experiment Assistant" and automated experimental platform within pharmaceutical companies/material companies: used to accelerate formulation development, process optimization, and candidate screening.
    * Domain Science Search Engine and Knowledge Graph (Bio / Chem / Materials / Physics Knowledge Graph): Supports semantic retrieval, interactive exploration, and knowledge reasoning.
    * Scientific Research Process Management Platform: Integrates experimental planning, data recording, version control, visualization, and automatic report generation to improve the efficiency of research teams and the reproducibility of results.

### 10.6.1 Scientific Literature Mining and Domain Knowledge Base Construction

The vast majority of scientific knowledge first appears in the form of papers and reports. To enable AI to truly participate in scientific research, it must be able to "read papers and extract structured knowledge from them".  ** Scientific literature mining and knowledge base construction ** , precisely starting from unstructured text, aims to build a knowledge infrastructure that is queryable and inferable.

In this direction, the core tasks include:

* **Entity Recognition and Standardization** : Identify entities such as compounds, proteins, materials, reactants, products, experimental equipment, and conditions in the literature, and align them with standard databases (e.g., ChEMBL, Uniprot, Materials Project).
* **Relationship and Event Extraction** : Extract relationships and events such as "who interacts with whom and how" and "what results are produced under what conditions" from text, for example, reaction equations, formula-performance correspondence relationships, etc.
* **Knowledge Graph**  **Construction** : Organizes entities and relationships into a graph structure, supporting complex queries (such as "all reported methods for improving a certain performance under certain conditions") and path reasoning.

To achieve the above objectives, the following are commonly adopted:

* Pre-trained models such as SciBERT, BioBERT, and PubMedBERT perform NER (Named Entity Recognition), RE (Relation Extraction), and document-level event extraction.
* On this basis, domain-specific LLMs (Bio-LM, Chem-LM, Materials-LM) are constructed to perform more complex question answering, review generation, and knowledge completion.

The well-constructed domain Knowledge Base and Knowledge Graph can not only provide more intelligent retrieval and recommendation services for R&D personnel, but also offer data and prior support for subsequent experimental design and material/drug inverse design.

### 10.6.2 Self-Driving Lab and Scientific Workflow Agent: From "Reading Papers" to "Doing Experiments"

After acquiring the capabilities of literature mining, modeling, and optimization, the next step is to combine these capabilities with ** the automated experimental platform ** to build a truly meaningful ** Self-Driving Lab ** and scientific workflow Agent.

In the Self‑Driving Lab, the typical closed-loop of work is:

1. **Goal Setting** : The researcher presents the macro goal (e.g., "improve the conductivity of a certain material under specific conditions") and the constraints (cost, safety, process limitations, etc.).
2. **Literature and Knowledge Retrieval ** : Agent calls literature retrieval and Knowledge Graph to understand existing work and empirical rules, forming initial hypotheses and experimental design space.
3. **Experimental P****lan****nin****g ** **and Optimization Strategy** : Based on LLM + RL / Bayesian optimization strategy, propose the first batch of experimental conditions (formulation, temperature, time, environment, etc.).
4. **Robot Execution and Data Acquisition** : The Robotic Lab conducts experiments, collects results in real-time, and performs postback.
5. **Model Update and Next Round of Design** : The surrogate model updates its parameters and uncertainty estimates based on new data, and then proposes more informative or promising experimental conditions for the next round.

In the broader ** scientific work****flow** ** Agent ** , this closed loop will extend to simulation, Data Analysis, report generation, and other aspects:

* The Agent can automatically generate simulation code or call existing simulation tools to pre-evaluate certain experimental conditions;
* During the Data Analysis phase, automatically complete data cleaning, visualization, and statistical testing;
* When summarizing the project phase, generate structured experimental records and draft reports, accompanied by charts and references.

In terms of product form, this type of system often takes the form of a platform: providing a unified interface and API to connect to literature databases, simulation engines, and experimental equipment, enabling scientists and engineers to set goals using natural language and visual interfaces at a high level, while the remaining steps are automatically orchestrated and executed by Agents + toolchains.

Starting from this sub-direction, the role of AI in science has truly shifted from an "offline analysis tool" to an "online research collaborator": not only capable of reading papers, writing code, and calculating models, but also able to work with robots to complete real experiments and discoveries one by one.

# 11. Platform and Engineering Capabilities (MLOps / Infra)

For large models to move from the laboratory to enterprise production, it is by no means sufficient that "the model itself is good enough"; instead, it must rely on a complete set of stable, scalable, and maintainable  ** platform and engineering system ** . This system needs to cover all aspects of the model, including  ** training and fine-tuning, deployment and inference optimization, data and model operation and maintenance, monitoring and cost management, security and compliance, as well as mid-platform and application support capabilities ** , etc., stringing together the originally scattered technical points into a sustainable closed loop.

From a business perspective, platform and engineering capabilities often determine whether an organization can use large models "at scale, securely, and cost-effectively": for the same underlying model, without a good MLOps system, it is likely to remain at the demo and pilot stages; once a complete platform is in place, enterprises can quickly replicate and evolve high-quality applications across multiple BUs, multiple countries/regions, and multiple industry scenarios. **Below, we will elaborate on six directions respectively:** Model Training and Fine-Tuning Platform, Deployment and Inference Optimization, Data and Model Operation and Maintenance, Monitoring and Cost Reliability, Security and Compliance Infrastructure, and Upper-Level Application and Mid-Platform Capabilities

## 11.1 Model Training & Fine-tuning (Training & Fine-tuning)

At the foundational model level, most organizations do not train trillion-parameter models from scratch, but instead build on open-source or commercial base models to  ** continue pre-training + fine-tuning ** . The core issue at this level is: how to efficiently utilize computing power and data to "adapt" general large models to specific industries, enterprises, and tasks, while ensuring the engineering manageability of multiple models and versions.

From an engineering perspective, this layer typically consists of three components:  ** pre-training and continued pre-training ** , ** fine-tuning paradigms and toolchains ** and ** large-scale **** distributed **  ** training infrastructure ** .

* **Scenario**
  * Research and Development of General Large Model Base: Cloud providers / large enterprises independently develop general language / MultiModal Machine Learning base models for external APIs and internal multi-business sharing.
  * Industry-specific large models and proprietary models: Build industry base models or "enterprise-owned large models" around specific domains such as finance, healthcare, law, manufacturing, energy, and gaming.
  * Enterprise-level model customization: Customize exclusive fine-tuned models or LoRA weights for large single clients (banks, insurance companies, government agencies, manufacturing groups, etc.) based on their internal data.
  * Multi-Tenant Model Market: SaaS/Cloud Computing Platform provides fine-tuning and hosting capabilities of "one model per customer" for numerous small and medium-sized customers, with each tenant having a set of weights or adaptation layers.
  * One-click Fine-tuning Platform: A full-service product open to non-algorithm teams, featuring a process of "upload data → select base model → automatic fine-tuning → one-click deployment".
* **Principle**
  * Pre-training and Continued Pre-training:
    * Large-scale pre-training on massive amounts of general text, code, and MultiModal Machine Learning data enables the model to acquire  **general language understanding, world knowledge, and basic reasoning abilities** .
    * For specific industries, continue pre-training on top of the general model through  ** Domain-adaptive Pretraining (DAPT) ** , introducing industry-specific terms, writing styles, and knowledge distributions.
    * Multilingual / MultiModal Machine Learning pre-training enables the model to have**cross-lingual transfer**and**image-text / speech / Structured Data fusion**capabilities through shared semantic space and joint training.
  * Fine-tuning Paradigm:
    * **Full Parameter Fine-Tuning** : When the target task differs significantly from the pre-trained distribution and there is sufficient computing power and data, directly update all parameters to achieve the highest performance ceiling.
    * **Parameter-Efficie** **nt Fine**  **-** **Tuni** **ng (PEFT) ** : By means of Adapter, LoRA / QLoRA, Prefix / P-Tuning, etc., only a very small number of "incremental parameters" are trained, making it suitable for scenarios involving multiple tasks, multiple clients, and frequent updates.
    * **In****struction**  **Fine-tuning and Task Fine-tuning** : Teach the model to understand natural language task descriptions through the approach of "instruction + example"; it can be either for a single vertical task or support multiple tasks on a unified model.
    * **RLHF** ** / RLAIF** : Train a reward model through human or AI feedback, and further align model behavior (politeness, safety, refusal strategy, values) using reinforcement learning.
  * Distributed Training and Engineering System:
    * Using strategies such as **Data Parallelism, Model Parallelism, Pipeline ** **Parallelism ** **, **  ** Tensor Parallelism ** , etc., the ultra-large model and large-scale data are split across multiple nodes and multiple cards in the cluster for collaborative training.
    * Reduce **** GPU memory usage and improve training throughput through technologies such as ZeRO / FSDP , and achieve large-scale cluster training with efficient scheduling (Kubernetes + Slurm / Ray).
    * Rely on standardized data pipelines (dataset loading, cleaning, deduplication, sharding, caching) and fine-tuning frameworks (Transformers Trainer, DeepSpeed, Lightning, etc.) to reduce reinventing the wheel.
* **Model**
  * Pre-training and Continued Pre-training Toolchain:
    * Training Frameworks: PyTorch, TensorFlow, JAX.
    * Large-scale training acceleration: DeepSpeed, Megatron-LM, Colossal-AI, Fairscale.
    * Distributed training strategies: Data Parallelism (DP), Model Parallelism (MP), Pipeline Parallelism (PP), Tensor Parallelism; ZeRO / FSDP, Megatron (TP+PP), DeepSpeed ZeRO.
    * Cluster Scheduling and Management: Kubernetes + Slurm / Ray / Horovod / TorchElastic.
    * Data Pipeline: Hugging Face Datasets, WebDataset, Petastorm, tf.data, Arrow; Object Storage (S3 / OSS / GCS) + Local Cache; Data Cleaning and Deduplication Tools.
  * Fine-tuning and PEFT Tools:
    * 微调框架：Hugging Face Transformers + Trainer / Accelerate、PyTorch Lightning、DeepSpeed、Colossal‑AI。
    * PEFT Toolkit: PEFT (LoRA / QLoRA / Prefix Tuning / Prompt Tuning, etc.), LLaMA‑Adapter, and various LoRA toolchains.
    * Instruction and Data Construction: Self-Instruct, Alpaca / Dolly-style pipeline, various data augmentation and dialogue rewriting tools.
  * RLHF / RLAIF Toolchain:
    * TRL（Transformers Reinforcement Learning）、trlx、DeepSpeed‑RLHF、自研 RLHF pipeline。
    * Reward Model Training, Ranking / Scoring Model, Rejection Strategy, and Alignment Strategy Template

In terms of product form, this layer often manifests as:  ** Model Base R&D Platform, Enterprise-level "Training + Customization" Service, One-click Fine-tuning Platform, and Model Market (Model Hub / Model Store) ** , supporting the production path from "general model" to "one model per enterprise".

### 11.1.1 Pre-training and Continued Pre-training: From General Capabilities to Industry Foundation

Pre-training is the "source project" of the capabilities of modern large models: through self-supervised learning on massive amounts of unlabeled text, code, and MultiModal Machine Learning data, the model gradually acquires language modeling, world knowledge, basic reasoning, and representation learning capabilities. On this basis, continued pre-training (especially  **Domain-adaptive Pretraining, DAPT** ) then undertakes the task of "pulling the model towards a specific vertical domain".

During ** the general pre-training ** phase, the core concerns include:

1. **Corpus Scale and Diversity** : Mix web page text, books, code, conversations, multilingual content, and multimodal data such as image-text equivalence to cover as wide a range of knowledge and forms of expression as possible.
2. **Training Objectiv****es ** **and Multi-Task Mixing** : In addition to classic autoregressive language modeling, objectives such as fill-in-the-blank, next sentence prediction, contrastive learning, and image-text alignment are sometimes added to enhance the model's semantic alignment and multi-modal understanding.
3. **Multilingual and Alignment** : Through shared vocabulary or subword encoding, as well as cross-lingual parallel corpora or alignment tasks, the model can model different languages in a unified vector space, achieving  **cross-lingual transfer and translation** .

During ** the Domain Adaptive Pre-training (DAPT) ** phase, the focus shifts to:

1. **Industry corpus construction** : Construct proprietary corpora from sources such as medical records and guidelines, legal judgments and regulations, financial research reports and transaction data, manufacturing/energy/game design documents, etc.
2. **Style and Terminology Adaptation** : Through continued pre-training on a large amount of in-domain corpus, the model naturally acquires industry terminology, fixed expressions, professional writing styles, and implicit knowledge (such as clinical expression habits and legal wording).
3. **Enterprise-level proprietary knowledge injection** : For large enterprises or institutions, in addition to general + industry corpora, internal enterprise documents, Knowledge Base, ticket records, etc. can be further added to train an "enterprise-specific large model" as a unified intelligent foundation.

In engineering practice, pre-training and continued pre-training will cooperate with large-scale distributed frameworks (such as Megatron-LM, DeepSpeed ZeRO, etc.) and efficient data pipelines (WebDataset / HF Datasets + object storage) to form  ** a stable and reusable training pipeline ** . For cloud providers or large enterprises, this pipeline is often encapsulated into an internal platform to support periodic incremental pre-training and parallel iteration of multi-industry base models.

### 11.1.2 Fine-tuning Paradigm and RLHF: From "Being Able to Speak" to "Understanding Business and Respecting Boundaries"

After having a powerful pre-trained foundation, the key to making the model "useful for business" and "behaviorally controllable" lies in the fine-tuning and alignment stages. This includes both traditional supervised fine-tuning (SFT), as well as instruction fine-tuning, multi-task fine-tuning, and reinforcement learning based on feedback (RLHF / RLAIF).

At the**fine-tuning paradigm**level, it can be roughly divided into:

1. **Full Fine-tuning**
   In scenarios where the task distribution differs significantly from pre-training, or there are rigid requirements for ultimate performance and sufficient computing power is available (such as specific programming language models, specific language/industry dialogue models), directly updating all parameters can achieve the maximum performance ceiling. However, it has high costs and complex version management, so it is generally only used on a few core models.
2. **Parameter-Effici****ent Fin** **e** **-Tun****ing (PEFT) **
   trains only the inserted "small incremental parameters" or low-rank weight increments through methods such as Adapter, LoRA/QLoRA, Prefix/P-Tuning, while keeping the weights of the original large model frozen. This brings three engineering advantages:
   1. Multiple tasks / multiple clients can share the same base model, only switching different Adapter / LoRA weights.
   2. Significantly reduces the requirements for video memory and computing power, supporting fine-tuning to be completed in small and medium-sized GPU clusters or single-machine environments.
   3. Frequent updates, easy rollback, facilitating rapid trial-and-error and A/B testing.
3. **In****struction Tuning and Task Tuning**
   1. **In****struction Tunin** **g** : Through samples of "natural language instruction + input + expected output", the model learns to understand human instruction forms such as "Help me..." and "Please explain...", thereby breaking free from task-specific templates.
   2. **Single-task fine-tuning** : For example, fine-tuning is performed only for vertical tasks such as customer service Q&A, code completion, legal consultation, etc., to maximize the performance of that task.
   3. **Multi-task fine-tuning** : Simultaneously handle multiple tasks (such as question answering, summarization, translation, code generation, recommendation reason generation, etc.) on a unified model to improve model generality and resource utilization.

At the**behavi****or a****lignment and security**level,**RLHF / RLAIF**plays a key role:

1. **Reward Model Training ** : Collect human or AI preferences (ranking/scoring) for multiple candidate answers of the model, and train a reward model that can evaluate the "goodness or badness of answers".
2. **Rein****for****cem** **ent learning (such as PPO) optimizes the base model ** : Guided by the reward model, adjust the model parameters through reinforcement learning to make it more in line with human preferences and platform values, for example:
3. More polite, neutral, and professional;
4. Reject or safely rewrite requests related to danger, violations, or privacy;
5. When there is uncertainty, indicate it rather than fabricating facts.
6. **RLAIF and Self-Supervised Alignment** : In some scenarios, using a strong base model as a feedback provider, or combining rules with automated evaluation, to perform semi-automatic alignment during the fine-tuning process, reducing the cost of manual annotation.

In terms of toolchains, frameworks such as Hugging Face Transformers + PEFT, TRL / trlx, and DeepSpeed‑RLHF have basically formed a ** standard industrial workfl****ow ** from SFT → RM training → RLHF. In terms of product definition, this layer typically materializes into:  ** model customization / training service, one-click fine-tuning platform, multi-tenant model marketplace, and industry / enterprise-specific large model engineering platform ** .

## 11.2 Model Deployment and Inference (Serving & Optimization)

After training a large model, how to provide inference services in a ** h****igh****ly ****av****ai****lable, ** **low****la****tency ** **, scalable, and cost-effective ** manner is the second pillar of the AI engineering system. The deployment and inference layer connects to computing clusters such as GPU / NPU on one end and API gateways, enterprise applications, and Open Platform on the other end. Its core responsibilities include:  ** deployment architecture design, model routing strategy, inference Performance optimization, and hardware utilization ** .

Overall, this layer needs to address three issues: ** What architecture to use for external services** ,  ** How to make inference faster and cheaper** ,  ** How to maintain high availability and governance in a multi-model, multi-region, and multi-tenant environment** .

* **Scenario**
  * Enterprise Internal AI Mid-Platform / Model Service Bus: Uniformly provides large model APIs for each Line of Business, shielding the differences in underlying models and hardware.
  * Open Cloud API: Provide standardized inference interfaces to external developers and ecosystem partners, supporting multi-model selection and version management.
  * High QPS online services: scenarios with extremely high requirements for latency and stability, such as customer service assistants, search, recommendation, work assistants, etc.
  * Low-cost offline generation: Batch processing tasks such as advertising/game copywriting, Knowledge Base generation, and code batch refactoring, which prioritize throughput and cost and have low real-time requirements.
  * Cross-regional, multi-cluster deployment: Provides nearby access for global or multi-regional users while supporting multi-cloud or Hybrid Cloud configurations.
* **Principle**
  * Deployment Architecture and Model Routing:
    * **Single Model Service** : In early or simple scenarios, a single main model is used to provide unified external services. The architecture is simple, but it is difficult to balance latency and cost.
    * **Multi-model Service and Routing** : Configure models of different sizes or with different specializations based on dimensions such as different tasks, latency requirements, cost constraints, user levels, etc., and perform request routing through rules or Meta-model (including A/B testing, multi-armed bandit/Bandit strategies, etc.).
    * **Multi-Tenant Isolation and **SLA ****** Ma** **nagement** : In multi-customer scenarios, isolation in performance and security between different tenants is ensured through resource quotas, QPS limits, access authentication, and SLA classification.
    * **Elastic Scaling and High Availability** : Leveraging infrastructure such as Kubernetes/Service Mesh to achieve automatic scaling, multi-replica deployment, canary release, Blue-Green Deployment, and cross-region disaster recovery.
  * Inference Performance Optimization:
    * **Model Compression and Acceleration** : Reduce model computational load and memory footprint through techniques such as quantization (INT8 / INT4 / NF4 / GPTQ / AWQ), pruning / sparsification, knowledge distillation, etc.
    * **System-lev****el** ** optimization** : Utilize KV Cache to cache attention key-value pairs, accelerating long conversations and continuous inference; balance throughput and latency through batching, parallel token generation, and streaming output; reduce memory access and kernel launch overhead through operator fusion and graph optimization.
    * **Heterogeneo****us ****hardw****are**** utili****zati** **on ** : Build adapted Runtime and scheduling strategies for different hardware such as GPU, CPU, NPU, FPGA, ASIC, etc., and improve overall efficiency through high-speed interconnection such as NVLink / RDMA in scenarios of single-machine multi-card and multi-machine multi-card.
  * Engineering and Operations and Maintenance:
    * Using dedicated inference frameworks such as vLLM, TGI, and Triton significantly reduces self-developed costs.
    * Perform cross-platform deployment and operator-level optimization through compilers and runtimes such as ONNX Runtime, TensorRT, TVM, and OpenVINO.
    * Build a unified **online inference ****clu****s****te****r and traffic scheduling layer **using Kubernetes, Ray, Service Mesh, and API Gateway.
* **Model**
  * Serving Framework and Inference Service:
    * vLLM、TGI（Text Generation Inference）、Triton Inference Server。
    * Ray Serve、KServe、TorchServe、SageMaker Endpoint、Vertex AI Endpoint 等。
  * Cluster and Scheduling:
    * Kubernetes（K8s）、Kubeflow、Ray、Slurm。
    * Service Mesh: Istio / Linkerd (supports traffic governance such as canary release, rate limiting, circuit breaking, fallback, etc.).
  * API Gateway and Authentication:
    * Kong、NGINX / APISIX / Envoy。
    * IAM / Keycloak / Auth0、云厂商 API Gateway、OAuth2 / OIDC 等。
  * Model Compression and Performance Library:
    * 量化：NVIDIA TensorRT‑LLM / TensorRT、Intel Neural Compressor、OpenVINO（PTQ / QAT）、BitsAndBytes、GPTQ、AWQ、AutoGPTQ。
    * 剪枝 / 稀疏：PyTorch Sparse、TensorFlow Model Optimization Toolkit、SparseML、Neural Magic。
    * Distillation: Reference solutions such as DistilBERT / TinyBERT, or a distillation pipeline based on Hugging Face Trainer + custom distillation loss.
  * Inference Engine / Runtime and Graph Optimization:
    * ONNX Runtime、TensorRT、OpenVINO Runtime、TVM、MNN、NCNN。
    * Specialized inference engines for large models: Sglang, vLLM, FasterTransformer, TGI, LMDeploy, DeepSpeed‑Inference.
    * 编译与图优化：TVM、XLA（JAX/TF）、TensorRT Graph Optimizer、TorchDynamo / TorchInductor、MLIR、Glow、ONNX Graph Optimizer、Intel NNCF 等。
  * Hardware and Heterogeneous Support:
    * GPU：CUDA / cuDNN / cuBLAS、ROCm（AMD）。
    * CPU: oneDNN (MKL‑DNN), OpenBLAS, Eigen.
    * NPU / Specialized Accelerator Card: SDKs such as Ascend CANN, Habana Gaudi, Graphcore IPU, etc.

On the product side, this layer often appears in the form of **Enterprise AI Mid-Platform / Model Service Bus, External Cloud ** **API** **, Unified Inference ** **Gateway **  **, High QPS Online Inference Cluster, Low-cost Batch Processing Platform, and Computing Power Utilization Optimization Solution ** , serving as the runtime "operating system" that supports the large-scale implementation of large model capabilities.

### 11.2.1 Deployment Architecture and Model Routing: From Single Model to Multi-Model ByteMesh

During the early experimental phase, many teams choose to use a "comprehensive" model as the**single entry point**to provide services: all requests are processed by the same model. This model architecture is simple and has low maintenance costs, making it suitable for POC and low-traffic scenarios. However, as business expands and cost pressures rise, the shortcomings of the single-model architecture will quickly become apparent:

1. Different tasks have different requirements for latency, cost, and quality. Using a single large model to handle all requests will result in ** computational resource **  ** waste ** .
2. Providing differentiated capabilities tailored to different industries and customer needs, such as industry-specific models and customer-exclusive fine-tuning weights, is difficult to manage uniformly under the "single model" approach.
3. Scenarios such as canary release, A/B testing, and cross-regional disaster recovery require the ability to flexibly schedule between multiple model versions.

Therefore, a mature large model service system often evolves into**Multi-Model Service and Intelligent Routing**architecture:

1. **Multi-Model Pool and Model Catalog** : Simultaneously maintain models of various sizes (small / base / large / ultra), various specializations (general / code / MultiModal Machine Learning / industry-specific), and various versions (v1 / v1.1 / customer customization, etc.), and perform unified registration and management on them at the service layer.
2. **Routing Policy ** :
3. **Rule-based Routing ** : Explicit selection is made based on request parameters (task type, user level, latency/cost preference, etc.) and business rules (e.g., a specific model is mandatory for a certain industry in a certain region).
4. **Model S****elec****tor (** **Meta**  **‑model)** : Uses a lightweight model to automatically select the optimal model (e.g., fast small model vs. slow large model) based on input content, historical performance, and real-time metrics.
5. **A/B / Bandit Routing** : Conduct online experiments between old and new models or different configurations, and automatically converge to a better solution based on metrics such as CTR, Customer Satisfaction Score, and Task Success Rate.
6. **Multi-tenant Isolation and Quota Management** :
7. Overlay quota control, QPS limits, access authentication, and SLA classification at the tenant dimension on top of model routing to ensure resource and data isolation between different customers.
8. Through ** Logical Separation + Physical Separation (Exclusive Cluster or Dedicated Node) ** n to address high-compliance scenarios such as finance, healthcare, and government affairs.
9. **Elastic Scaling and High Availability ** :
10. Based on Kubernetes HPA/VPA and Cluster Autoscaler, it implements automatic scaling according to traffic.
11. Ensure service stability through multi-replica deployment, load balance, canary release, Blue-Green Deployment, and multi-region disaster recovery.

Technically, a combination of **Kubernetes + Service Mesh (Istio / Linkerd) + ****API** ** Ga****teway** **(Kong / APISIX / ** ** Envoy ** **) + Model Serving Framework (vLLM / TGI / Triton / Ray Serve / KServe) ** is often adopted to form a ** service mesh-based inference platform ** that supports both multi-model, multi-tenant, and traffic governance and canary release.

### 11.2.2 Inference Performance Optimization and Hardware Acceleration: Minimize the cost per inference

In large model large-scale commercial scenarios, inference cost is often one of the largest ongoing expenditures. How to compress ** cost per request / per token and end-to-end latency ** to an acceptable range while ensuring the user experience is the core technical challenge at the deployment layer.

On the  **model side** , common measures include:

1. **Quantization**
   significantly reduces GPU memory usage and bandwidth overhead by compressing weights and activations from FP16 / BF16 to low-bit formats such as INT8 / INT4 / NF4.
   1. Post-Training Quantization (PTQ): Such as GPTQ, AWQ, BitsAndBytes, etc., which perform offline quantization on existing models.
   2. Quantization Aware Training (QAT): Considers quantization error during the training/fine-tuning phase to improve post-quantization accuracy.
2. **Pr****uning ** **and Spa****rsity ( **  **Pruning ** ** & Sparsity) **
   Sparse the model by removing unimportant weights or channels through structured/unstructured pruning, and improve inference speed by combining hardware-friendly sparse operators (such as NVIDIA sparse matrix acceleration).
3. **Distillation**
   Uses a large model as a teacher to distill knowledge onto a smaller student model or task-specific model, significantly reducing the parameter scale while maintaining comparable task performance, making it suitable for online services highly sensitive to latency or edge deployment.

On the  **System and Runtime side** , key optimization points include:

1. **KV** ** Cache and Long Context Optimization**:
   In autoregressive generation, cache the attention key-value pairs of historical tokens to avoid redundant computation, thereby improving the efficiency of long conversations and multi-round requests; combine block computation and dynamic pruning strategies to control GPU memory overhead.
2. **Bat****c****h ****Processing and Parallel**  ** Generation ** :
   By dynamically batching multiple requests, performing grouped scheduling, and parallel token generation, overall throughput is increased without significantly increasing P95 latency; combined with streaming output to improve the front-end interactive experience.
3. **Operator and Graph Optimization** : Use compilers and Runtimes (such as TensorRT, TVM, ONNX Runtime, TorchInductor) for operator fusion, memory layout optimization, and static graph compilation to reduce kernel launch and memory access overhead.
4. **Heterogeneous Hardware Sched****uli** **ng ** :
   Based on the computational characteristics and latency requirements of different tasks, make reasonable allocations among heterogeneous resources such as GPU, CPU, NPU, and FPGA:
5. Extremely latency-sensitive and high-concurrency conversation/search requests are preferentially scheduled to GPU/NPU.
6. Tasks such as batch generation, offline evaluation, and log replay can be scheduled to CPU or low-cost GPU/NPU.

In terms of tools and frameworks, TensorRT-LLM, SgLang, vLLM, FasterTransformer, LMDeploy, DeepSpeed-Inference, etc. have formed a relatively mature **large mo****de****l ** **inference acceler****ati** **on ecosystem ** . On the business side, these optimizations are ultimately reflected in: ** high ** **QPS ** **, ** **low-latency **  **online inference cluster, low-cost batch generation platform, ** ** computing power *** utilization optimization scheme and MaaS/  **API ** billing and cost accounting system ** .

## 11.3 Data and Model Operation and Maintenance (Data / Model Ops)

Once a large model enters the production environment, it is no longer a static asset of "one-time delivery", but a dynamic system that needs to be continuously iterated in **five dimensions: data, model, configuration, version, and experiment** . The Data / Model Operation and Maintenance layer (Data / Model Ops) is an engineering paradigm built around this reality: from data flywheel, model lifecycle management to online experiments and automated release, it provides a foundation for the**sustainable improvement and controllable evolution**of model capabilities.

This layer connects the Data lake / data warehouse, logging and collection systems at one end, and the training platform, evaluation system, and online service gateway at the other end, serving as the central hub for closing the loop of "data - model - business feedback".

* **Scenario**
  * Enterprise-level Data Mid-platform + Integrated Model Training Platform: Connects the whole-link from data acquisition, cleaning, annotation, management to training/fine-tuning, supporting continuous iteration of multiple models.
  * The "continuous effectiveness improvement mechanism" for C/B-end AI applications: relies on a data flywheel driven by user feedback and usage data.
  * Data management and annotation workbench shared by the annotation team and the algorithm team: supports task assignment, quality inspection, and version rollback.
  * Group-level ModelOps Platform: Unified recording and management of all model versions, evaluation results, and release status.
  * Online business experiment and canary release system: Supports A/B testing, small-traffic trial runs of multiple models, and automatic optimal scaling.
  * Model Hosting Service: Provides partners/customers with model management capabilities of "upload once, deploy across multiple environments, and manage multiple versions".
* **Principle**
  * Data Management and Data Flywheel:
    * **Data Acquisition and Governance** : Collect samples from business logs, user conversations, public data, and partner data, and perform deduplication, noise reduction, desensitization, format standardization, and quality assessment on them.
    * **Annotation and F****ee** **dback Closed Loop** : Build high-quality annotated data through the combination of expert annotation and crowdsourcing, and in conjunction with the quality inspection mechanism; feed back user feedback such as likes/dislikes, corrections, and manual reviews back into the training sample pool.
    * **Data Flywheel** : After the model is launched, continuously collect real usage data → select high-value samples (such as model errors, low confidence, high-yield tasks) from it → retrain or fine-tune → improve model performance → start a new round of usage, forming a positive feedback loop.
  * Model Lifecycle and Release:
    * **Model Version Management** : Maintain clear version numbers (major and minor versions), training data versions, configuration parameters, evaluation results, security reports, and change logs for each model.
    * **CI/CD** **and Automated Pipeline**: After training is completed, evaluation and security checks are automatically triggered. Through regression testing and threshold gating, canary release and full release are only allowed if key metrics do not degrade excessively.
    * **Experiment and Traf****fic A** **llocation** : Use online experimental methods such as A/B testing and multi-armed bandits to compare multi-version models, and automatically select the best one based on real-time business metrics (e.g., task success rate, ticket resolution rate, Customer Satisfaction Score).
* **Model**
  * Data lake and data warehouse:
    * Delta Lake, Apache Hudi, Iceberg, Hive, BigQuery, Snowflake, etc., are used for unified storage and management of large-scale structured/unstructured data.
  * Streaming Data Processing:
    * Kafka, Pulsar, Flink, Spark Streaming, etc., are used for real-time log, user conversation, and event stream ingestion.
  * Feature and Sample Management:
    * Feature Stores such as Feast, self-developed sample repository, and ML Metadata Store are used to record sample, feature, and training metadata.
  * Annotation and Quality Inspection Platform:
    * Label Studio, Scale-like platforms, and self-developed annotation systems support multi-task annotation, quality inspection, and personnel management.
  * MLOps / ModelOps Platform:
    * MLflow, Kubeflow, SageMaker, Vertex AI, Azure ML, Weights & Biases, etc., are used to manage training experiments, parameters, metrics, and model artifacts.
  * Model Registration and Version Management:
    * MLflow Model Registry、SageMaker Model Registry、W&B Artifacts 等。
  * CI/CD Tools:
    * GitHub Actions, GitLab CI, Jenkins, Argo CD, Flux, etc., are used to build the Code Pipeline for model continuous delivery.

### 11.3.1 Data Flywheel and Training Closed Loop: Making the Model "Smarter with Use"

In traditional software development, version upgrades are often driven by development plans; while in the era of large models, ** data and feedback ** have become the main drivers of iteration. The goal of the data flywheel is to turn "model usage → data precipitation → retraining → model upgrade" into an automatically rolling closed loop, enabling the model to ** become more and more useful ** in actual business.

Core steps include:

1. **Online Data Acquisition and Screening**
   In applications such as dialogue robots, Copilot, search Q&A, and code assistants, each user interaction is a potential high-value training sample. Through the logging system and event tracking, requests, model responses, and user behavior (clicks, acceptance or not) are structured and collected, and privacy desensitization and field cropping are performed at the collection end to ensure that no additional compliance risks are introduced.
2. **High-value Sample Mining**
   Filter out a small subset of samples that are most valuable for training from massive logs, for example:
   1. Answers that are clearly incorrect or downvoted by users are used for "error-correction" retraining.
   2. High-difficulty long questions and complex workflow task samples, used to enhance the model's capabilities in "long-chain reasoning / multi-step tool invocation".
   3. Typical business cases and high-value tickets are used to build industry/enterprise-specific capabilities.
3. **Annotation and Quality Control**
   Manually or semi-automatically annotate candidate samples (including expected answers, ranking of pros and cons, safety labels, etc.), and ensure the annotation quality through multiple rounds of quality inspection, review, and spot checks to provide reliable data for subsequent SFT or RLHF.
4. **Continuous Retraining**** an****d Evaluation Laun****ched**
   Periodically add new samples to the training set, perform retraining operations such as SFT / DAPT / RLHF, and simultaneously evaluate "offline metrics + online effectiveness" through standard evaluation sets and online A/B experiments to ensure that the new version is generally superior to the old version and avoid the data flywheel "turning in the wrong direction".

In its mature form, most operations of the data flywheel will be automatically encapsulated into  ** the Data / Model Ops Platform ** : from data acquisition, sample screening, annotation task distribution, to model retraining triggering, evaluation result collection, and go-live decision-making, minimizing manual operations and making model iteration a stable and controllable engineering process.

### 11.3.2 Model Lifecycle and ModelOps: From Experimental Models to Production Assets

With the exponential growth of the number and versions of models, if there is a lack of rigorous lifecycle management, problems such as "models scattered everywhere, version chaos, and difficulty in rollback" are likely to occur. The goal of ModelOps is to treat models as**first-class citizen engineering assets**for management, with full traceability, comparability, and rollback capabilities.

Key points include:

1. **Versioni****ng an****d **** Metadata Management**
   Assign a clear version number to each model (e.g., `industry-legal-base-v1.2.3`) and record:
   1. Training data version and time range;
   2. Training configuration (hyperparameters, training script version, code commit used);
   3. Evaluation Metrics (General Benchmark + Business-Specific Benchmark);
   4. Security Assessment and Alignment Strategy (e.g., Sensitive Topic Response Strategy Version);
   5. Online / Offline / Rollback History.
2. **End-to-End ****Autom****ated Pipeline (**  **CI/CD** ** for Models)**
   Encapsulate the process of "Model Training Completion → Automatic Evaluation → Security and Bias Check → Canary Release → Full Release" into the CI/CD pipeline.
3. If the offline evaluation metrics fail to meet the preset threshold, the go-live will be automatically blocked.
4. If the online A/B test performs poorly, it will automatically reduce traffic or roll back to the previous version.
5. **Multi-version Coexistence and Traffic Scheduling**
   In a production environment, multiple model versions (such as `stable` / `canary` / `experimental`) often coexist simultaneously, and online comparisons are conducted on them through traffic allocation strategies (fixed ratio, user dimension, feature dimension).
   1. A/B testing focuses more on stable statistical conclusions;
   2. Multi-armed Bandit automatically balances exploration and exploitation, accelerating convergence to a better-performing version.
6. **Compliance and Audit Support**
   For industries such as finance, healthcare, and government affairs, it is necessary to maintain traceable records for each model version change: who upgraded the model from which version to which version based on what data at what time, and how the impact assessment after the upgrade was. This part is usually linked with the **Security and Compliance ****Infrastructure** in Section 11.5.

In terms of engineering implementation, tools such as MLflow, SageMaker, Vertex AI, and W&B have already provided relatively mature ModelOps capabilities. Most enterprises will build on these capabilities and combine them with their own processes for secondary encapsulation to construct a unified  ** internal model registry and publishing platform ** .

## 11.4 Monitoring, Cost & Reliability

When large models become the core infrastructure of business operations, how to ensure their ** observability, early warning capabilities, scalability, ** ** cost controllability ** becomes the core responsibility of SRE and platform teams. The monitoring, cost, and reliability layer combines the traditional observability system with the unique metrics of large models to build a multi-dimensional view for operations, algorithms, and management.

This layer connects the monitoring and collection, log/link tracing system at one end, and the business KPI and cost analysis platform at the other end, serving as a key pillar to ensure the "stability, speed, and cost-effectiveness" of model services.

* **Scenario**
  * Operations Monitoring Dashboard for Operations / SRE: Unified display of CPU / GPU utilization, QPS, latency, error rate, alerts, etc.
  * Data and Model Quality Monitoring Platform for Algorithm Teams: Monitors input data distribution, model drift, prompt engineering effectiveness, RAG hit rate, etc.
  * Service Health Dashboard for Management: Displays business KPIs (conversion rate, satisfaction, task completion rate) in conjunction with model metrics.
  * AI Cost Analysis and Optimization Platform: Disassemble computing power costs by model, project, and Line of Business, and support budget management and cost optimization strategies.
  * Intelligent Scheduling and Elastic Scaling System: Automatically scales up or down or switches model specifications based on load and budget.
  * External MaaS / API Billing and Cost Accounting System: Supports billing based on dimensions such as call volume, number of tokens, and computing power usage.
* **Principle**
  * Monitoring and Observability:
    * **Multi-layer monitoring** : From the infrastructure layer (CPU / GPU / memory / network / storage) to the service layer (QPS, P50 / P95 / P99 latency, error rate, timeout retry), and then to the model layer (token usage, context length distribution, response length, common error types).
    * **Logging and Tracing** : Record requests/responses (under the premise of desensitization) through structured logging, and carry model version, routing decisions, and tenant information; use distributed tracing tools to record the complete request chain from API gateway → model service → downstream system.
    * **Alerts and Analysis** : Set threshold alerts, anomaly detection, and trend analysis, and integrate with business metrics, costs, and security events to achieve rapid location and recovery.
  * Cost Control and Elastic Scheduling:
    * **Cost Analysis** : Break down GPU/CPU/storage/bandwidth costs by model, project, and Line of Business dimensions, and calculate the average cost per request and the marginal costs of different tasks/customers.
    * **Elastic Scheduling ** : Utilize peak-valley time-sharing strategy to automatically scale up during peak periods and scale down during off-peak periods; stagger offline batch tasks to nighttime or low-load periods.
    * **Strategic Degradation and On-Demand Acceleration** : Automatically switch to smaller models, shorter contexts, or more conservative inference configurations when resources are scarce; automatically use larger models or longer contexts for high-value requests.
* **Model**
  * Monitoring and Visualization:
    * Metrics collection and visualization solutions such as Prometheus + Grafana, VictoriaMetrics, Thanos, etc.
  * Logging System:
    * ELK（Elasticsearch + Logstash + Kibana）、EFK（Fluentd / Fluent Bit）、OpenSearch 等。
  * Link Tracing:
    * OpenTelemetry、Jaeger、Zipkin 等。
  * Model-specific monitoring:
    * WhyLabs, Arize AI, Fiddler, Evidently AI, etc., are used for data/model drift monitoring and output quality assessment.
  * Cost Statistics and Allocation:
    * K8s Metrics / Cost Exporter、Kubecost，以及各云厂商 Cost Management 工具（AWS Cost Explorer / GCP Billing / Azure Cost Management）。
  * Resource Scheduling and Elastic Scaling:
    * K8s HPA / VPA、Cluster Autoscaler、Volcano、Ray Cluster Autoscaler。
  * Task Orchestration:
    * Argo Workflows、Airflow、Prefect、Dagster 等。

### 11.4.1 Monitoring and Observability: From Infrastructure to Model Behavior

In large model systems, traditional CPU / memory / QPS metrics are no longer sufficient; an additional layer of monitoring from a "model perspective" is needed to truly understand the system's health. A complete observability framework typically includes:

1. **Infrastructure and Service Layer Monitoring **
   Collect and visualize through Prometheus / Grafana, VictoriaMetrics, etc.:
   1. CPU, GPU, memory, disk, and network usage at the node/Pod level;
   2. QPS, P50 / P95 / P99 latency, error rate, timeout retry ratio, and number of connections at the service level;
   3. Cluster-level resource utilization and capacity alerts.
2. **Model laye****r m****etric monitoring**
   For large model services, in addition to regular performance metrics, specialized monitoring is also required:
   1. Token consumption (input/output) per request, context length distribution;
   2. Response length and truncation ratio to troubleshoot quality issues caused by context/output length limitations;
   3. Statistics on common error types (such as long input, model timeout, tool call failure, etc.).
3. **Log****gin****g and Distributed Tracing**
   1. Use structured logging to record information such as request parameters (after desensitization), model version, routing decision, tenant identifier, return code, etc.
   2. Trace the entire process of a request in the API gateway → model service → downstream system → callback link using OpenTelemetry, Jaeger, Zipkin, etc., to facilitate the identification of latency bottlenecks and fault points.
4. **Anomaly Detection and Intelligent Alarming**
   Based on traditional threshold-based alarming, simple statistical monitoring or Machine Learning models can be introduced to perform anomaly detection on QPS, latency, error rate, token distribution, etc. When a sudden change occurs, an alarm is automatically triggered, and self-healing strategies (such as automatic scaling, traffic switching, and service degradation) are coordinated.

For the algorithm team, tools such as WhyLabs, Arize, and Evidently AI can also be integrated at this layer to conduct long-term tracking of input distribution, model output features, and drift conditions, providing signals for subsequent data flywheels and retraining.

### 11.4.2 Cost Analysis and Flexible Scheduling: Finding the Balance between "Experience" and "Budget"

One of the most prominent operational and maintenance challenges in large model services is  **high and volatile costs** . Without refined cost analysis and elastic scheduling, it is easy to lose sight of "where the money is being burned" during business growth and difficult to make timely adjustments. A mature cost and resource scheduling system typically includes:

1. **Cost Attribution and Allocation**
   Using Kubecost, cloud provider billing tools, and self-developed ledger, break down GPU/CPU/storage/bandwidth costs by dimensions such as model, project, Line of Business, tenant, etc., so that each team and customer can see their corresponding real resource consumption and costs.
2. **Analysi****s of**** Unit Request Cost and Marginal Cost**
   1. Calculate the average cost per single request (Cost per 1k tokens / per request) for each model/task, and compare the cost-effectiveness across different models and configurations.
   2. Analyze the marginal costs of different customers and different business scenarios to provide a basis for pricing strategies (API billing), SLA classification, and product packaging.
3. **Elastic Scaling and Peak-Valley Utilization**
   1. Automatic scaling is achieved through mechanisms such as K8s HPA / VPA, Cluster Autoscaler, and Ray Autoscaler to ensure that the service does not crash during peak periods and remains idle during off-peak periods.
   2. Schedule offline tasks (such as batch content generation, log replay, and offline evaluation) during nighttime or off-peak hours to improve overall GPU utilization and smooth the cost curve.
4. **Strategic Degradation and On-Demand Acceleration**
   1. Automatically trigger a degradation strategy when resources are scarce or costs exceed the budget: use a smaller model, shorten the context or output, or reduce parallelism.
   2. Automatically use larger models, longer contexts, or more powerful tool invocation capabilities for high-value requests (such as high-paying premium users and critical business processes) to achieve "computing power allocation by value".

In the external API scenario, this layer will also be deeply integrated with the billing system to form  ** the MaaS/API Billing and Cost Accounting Platform ** : Billing is based on token usage, number of calls, model specifications, and request types, and it provides cost and gross profit analysis for operations/sales.

## 11.5 Security, Access Control & Compliance Infrastructure (Security, Access Control & Compliance Infra)

Once the capabilities of large models enter high-sensitivity industries such as finance, healthcare, and government affairs, security and compliance are no longer "added value" but rather preconditions for entry into the scenario. The security, access control, and compliance infrastructure layer is responsible for ** building system-level defenses from access control, data security, privacy protection to compliance auditing ** to ensure that model services operate reliably within the legal and regulatory frameworks.

This layer connects the identity authentication, permission management, key and encryption system at one end, and the model service and log/audit platform at the other end. It is the key to transforming "usable models" into "trustworthy models".

* **Scenario**
  * Localization large model platforms for high-compliance industries such as finance, healthcare, and government affairs: Require data to remain within the domain, be auditable, and traceable.
  * Enterprise Unified AI Access Control and Audit Gateway: Performs unified authentication, permission management, and audit logging for all model calls.
  * Multi-tenant SaaS/Cloud Computing Platform: It is necessary to provide strict security isolation and compliance support for different customers at both logical and physical levels.
  * Open APIs for partners/ecosystems: Require fine-grained permission control and quota limits for API calls, and meet compliance requirements (such as GDPR, etc.).
* **Principle**
  * Access Control and Tenant Isolation:
    * Authenticate using methods such as API Key, Token, OAuth, SSO, etc.
    * Implement refined permission management through RBAC (Role-Based Access Control) and ABAC (Attribute-Based Access Control) across dimensions such as model, function, invocation frequency, and data scope.
    * Implement isolation of**data, logs, configurations, and model weights**in a multi-tenant environment to prevent cross-tenant access and information leakage.
  * Data Security and Privacy Protection:
    * TLS encrypted transmission, storage encryption, and centralized key management (KMS) are used to ensure data security during transmission and storage.
    * Implement desensitization of implementation logs and data minimization strategies, retain only the information necessary for business and optimization, and audit access behavior.
    * Introduce privacy-enhancing technologies (such as data anonymization, differential privacy, FL) in necessary scenarios to further reduce privacy risks.
  * Compliance and Audit:
    * Conduct full-process traceability and approval for key operations such as model release, configuration change, permission change, and routing policy adjustment.
    * Record traceable metadata for each request: request source, model version, decision basis (such as Knowledge Base used / tool invocation status).
    * Ensure that system design and operation comply with regulatory requirements of industries such as finance, healthcare, and government affairs, as well as local and cross-border data compliance regulations.
* **Model**
  * Identity Authentication and Permission Management:
    * Keycloak、Auth0、Okta、各云厂商 IAM（AWS IAM / GCP IAM / Azure AD）。
    * Policy engines such as OPA (Open Policy Agent) + Rego Policy are used for unified policy management and execution.
  * API Security Gateway:
    * Kong, Apigee, Envoy, cloud provider API Gateway, etc.
  * Data and Key Security:
    * KMS（Key Management Service）、HashiCorp Vault。
    * TLS Termination, Confidential Computing, etc.

### 11.5.1 Access Control and Tenant Isolation: Ensure "who can use, what can be used, and how much can be used"

In a large model platform jointly used by multiple Lines of Business, multiple customers, and multiple roles, without fine-grained access control and tenant isolation, serious issues such as abuse of permissions, data leakage, and resource contention are likely to occur. A comprehensive access and isolation system needs to be coordinated in the following dimensions:

1. **Identity ****Auth****enti****cat****ion and Single Sign-On**
   Unified identity authentication for internal employees, external partners, and third-party applications is performed through methods such as API Key / Token, OAuth2 / OIDC, and enterprise SSO. For enterprise users, it can be integrated with existing identity systems (such as AD / LDAP / enterprise IAM) to avoid duplicate account systems.
2. **Fine-grai****ned ****Permissi****on C****ontrol (**  **RBAC** ** / ** **ABAC** **)**
3. RBAC: Configure accessible models, environments (test / production), operations (call / configure / publish), and quotas for roles such as administrators, algorithm engineers, business operators, ordinary users, and partners respectively.
4. ABAC: Based on roles, attributes such as tenant ID, project ID, data domain, and time period are introduced to implement more flexible policies (e.g., "Only allow government tenant A to call the Localization model cluster within the local domain").
5. **Multi-tenant Isolation and Quota Management**
   1. At the logical level, isolate the calls, data, and logs of different customers through the tenant ID;
   2. At the physical level, dedicated clusters or dedicated nodes are provided to high-compliance customers (such as banks/governments) to achieve a higher level of isolation;
   3. Configure QPS limits, concurrent connections, and token quotas for different tenants to prevent "a single tenant from overwhelming the entire system".
6. **Access Audit and Policy Evaluation**
   1. Conduct audit records for critical operations (such as creating/deleting API keys, adjusting permissions, and modifying quotas);
   2. By leveraging policy engines such as OPA / Rego, complex access policies are uniformly evaluated and interpreted before execution, reducing the risk of "policies scattered in code".

Through this mechanism, the platform can open up the capabilities of large models to internal and external users while ensuring the security of resources and data, and at the same time provide basic data for subsequent compliance audits and problem accountability.

### 11.5.2 Data Security, Privacy, and Compliance Audit: Making Models "Useful and Compliant"

Large models often come into contact with a large amount of sensitive data (user conversations, business documents, transaction records, etc.). Once a security or compliance issue occurs, the consequences will be extremely serious. Therefore, "multi-layered protection" is required throughout the entire data lifecycle and the whole-link of model invocation.

1. **Data Transmission and Storage Security**
   1. Uniformly enable TLS encryption for all external and internal interfaces to prevent eavesdropping or tampering during transmission;
   2. Adopt static encryption for storing sensitive data, and cooperate with cloud providers or self-built KMS to manage the key lifecycle;
   3. Use tools such as Vault to centrally manage the keys and credentials required to access databases, object storage, and third-party APIs.
2. **Minimization Principle and Desensitization**
   1. Only collect data fields necessary for business operations, and remove personal identity information (PII) and sensitive fields from logs and training samples as much as possible;
   2. Hash or anonymize identifiers that must inevitably be retained to reduce the risk of leakage;
   3. In RAG / Knowledge Base scenarios, implement permission grading for document access to ensure that the model does not retrieve information from "documents it should not access".
3. **Privacy-Enhancing Technologies and Edge Constraints**
   1. In scenarios where it is necessary to share models without sharing the original data, introduce methods such as differential privacy or FL to balance privacy and efficiency;
   2. For scenarios such as government affairs, finance, and healthcare, adopt the model of "data stays within the domain, model sinks or local deployment" to deploy training/inference capabilities within the compliance domain.
4. **Compliance and Audit Mechanism**
   1. Approve workflows and leave audit trails for operations such as model release, configuration change, and permission adjustment, facilitating post-event traceability;
   2. Record meta information such as model version, caller, routing decision, and data access scope for each request, enabling review in case of disputes or investigation needs;
   3. Regularly output compliance reports (such as data access audits, permission usage records, and abnormal event reports) to meet the requirements of internal risk control and external supervision.

This part of the capabilities works in conjunction with the Data / Model Ops and monitoring platform in 11.3 and 11.4, together forming a model operating environment that is "both capable of continuous iteration and compliant with security requirements".

## 11.6 Upper Application and Mid-Platform Capabilities (Application Enablers)

With a complete infrastructure spanning from training to inference, as well as security and operations, there is still a need for a "capability layer" oriented towards business and developers, which abstracts underlying large models into more user-friendly and business-semantic components and services. This layer is commonly referred to as  **AI Mid-Platform, Application Enablement Layer, or Copilot Platform** , whose responsibility is to encapsulate large models + RAG + Agent + workflows into standardized capabilities, enabling business teams and ecosystem partners to quickly build AI applications.

This layer connects the model API, RAG engine, and Agent Orchestrator at one end, and business systems such as CRM/ERP/OA/ticket at the other end, serving as a key bridge from model capabilities to business scenarios.

* **Scenario**
  * Enterprise AI Mid-Platform / Copilot Platform: Provides unified intelligent capabilities such as dialogue, RAG, and Agent for internal systems including CRM, ERP, OA, customer service, marketing, R&D, etc.
  * Application Development Platform for Developers and Ecosystem Partners: Enables third parties to quickly build and deploy AI applications through SDKs, template projects, and visual orchestration tools.
  * AI Backend of Industry SaaS Products: Such as intelligent customer service cloud, marketing cloud, work collaboration cloud, R&D management cloud, etc., which embed AI capabilities into the existing product system.
  * Vertical scenario assistants: Code Copilot, sales assistant, operations assistant, legal assistant, doctor assistant, etc., quickly combine to create scenario-based solutions through Mid-Platform capabilities.
* **Principle**
  * Dialogue and Agent Capabilities:
    * **Conversation Manag****emen** **t and Memory** : Maintains multi-turn conversation state and long-term memory, supports topic switching, context compression, and personalized profiling.
    * **Tool Use and Workfl****ow **  **Orchestration ** : Connect models with external systems (databases, search, business APIs, third-party services) through function calls or plugin mechanisms; use Workflow/Orchestrator to chain multiple steps in complex tasks.
    * **Multi-Agent Collaboration** : Splits complex tasks into different roles (such as planners, executors, reviewers) to complete task decomposition and result aggregation in a collaborative manner.
  * RAG and Knowledge Base:
    * **Document Parsing and Preprocessing** : Parse, segment, and structure documents such as PDFs, Word files, web pages, and scanned documents.
    * **Vectorization and Retrieval** : Use the Embedding model to vectorize text, tables, code, and other content, and build vector indexes; combine keyword retrieval and vector retrieval to achieve high recall.
    * **Retrieval + Generation (RAG) and Evi****den** **ce Chain** : During inference, relevant content is first retrieved from the Knowledge Base, then the large model generates responses based on the retrieval results, and outputs references and evidence chains to improve accuracy and interpretability.
    * **Know****ledge Graph** **and Structured Know****led** **ge Fusion** : Combine domain knowledge graphs, business data tables, rule systems, and LLMs to improve the ability to handle structured queries and complex constraints.
  * Developer Access and Secondary Development:
    * **Multilingual SDK and ** API ** Desi****gn**: Provide SDKs for languages such as Python / JS / Java / Go, encapsulating call patterns, retry, and idempotence handling.
    * **Templat****es ****and **** Low-Code ** ** / No-Code Building **: Through prefabricated template projects and visual "building block" style tools, even non-professional developers can build RAG / Agent / Workflow.
    * **Plugins and Middle****war** **e** : Provide plugins or middleware for common business systems (CRM / ERP / OA / ticket system, etc.) to reduce system integration costs.
* **Model**
  * Dialogue / Agent Framework:
    * LangChain、LlamaIndex、Haystack、Semantic Kernel 等。
    * Self-developed Orchestration layer: Usually includes Workflow Engine, Tool Router, and Memory management modules.
  * RAG and Vector Retrieval:
    * Vector databases: FAISS, Milvus, Qdrant, Weaviate, Pinecone, etc.
    * Document parsing: unstructured, Textract, pdfplumber, Apache Tika, etc.
  * SDK / Access Layer:
    * Official or self-developed SDKs, front-end component libraries (chat components, prompt template management, conversation record view).
    * Middleware/Plugin for business systems (CRM/ERP/OA/Ticket, etc.).

### 11.6.1 Dialogue and Agent Orchestration: From "Question-and-Answer Robot" to "Task Collaboration Entity"

Compared to early FAQ-style Q&A robots, modern large model-driven applications are more like "intelligent collaborators who can use tools." The goal of dialogue and Agent orchestration is to upgrade large models from "language generators" to intelligent agents capable of **invoking tools, executing plans, and coordinating multiple roles** .

1. **Dialog Management and Memory Mechanism**
   1. Maintain conversation context, user profiles, and long-term memory, ensuring consistency and coherence in multi-turn interactions;
   2. Compress ultra-long conversations using methods such as summarization and retrieval-based memory to avoid context "overflow";
   3. In enterprise internal applications, introduce identity and permission information into the conversation context to ensure that responses and operations comply with the user's permissions in the business system.
2. **Tool Use and Wo****rkf****low Orchestration**
   1. Provide the model with a list of structured tools (such as "Check Order", "Create Ticket", "Query Inventory", "Invoke Search Engine", etc.), and allow the model to actively call them via the function call interface when needed;
   2. Use Orchestrator to coordinate the sequence, data flow, and error handling of multiple tool calls based on the plan proposed by the model;
   3. Workflow modeling is performed on complex business processes (such as approval flow, reimbursement, and after-sales processing), enabling the Agent to play the role of a "process coordinator".
3. **Multi-Agent Collaboration Mode**
   1. Break down complex tasks into multiple roles: such as "Task Planning Agent", "Information Retrieval Agent", "Execution Agent", "Quality Inspection / Audit Agent";
   2. Achieve collaboration between Agents through message channels or shared memory, enhancing the robustness and interpretability of complex tasks;
   3. In an enterprise environment, human roles can also be incorporated into the collaboration loop, such as "AI Draft - Human Review - AI Revision - System Execution".

This layer typically leverages off-the-shelf frameworks such as LangChain, Semantic Kernel, LlamaIndex, etc., and coordinates with self-developed Orchestration services to unify conversations, tools, workflows, permissions, and audits within a single "Agent Platform".

### 11.6.2 RAG, Knowledge Base, and Developer Platform: Connecting Enterprise Knowledge "to the Model's Brain"

No matter how powerful large models are, they cannot inherently master the private knowledge of every enterprise, let alone know the latest policies, products, and business rules in real time. RAG + Knowledge Base + Developer Platform is the ** enterprise knowledge, industry knowledge, and real-time data ** critical path to integrating these into model capabilities in an engineered manner.

1. **Document Parsing and Knowledge Storage into Knowledge Base**
   1. Parse PDF, Office documents, web pages, scanned images into structured text through components such as unstructured, Textract, pdfplumber, Tika, etc.;
   2. Perform "chunking" by chapter, title, semantic block, etc., to provide appropriate granularity for subsequent vectorization and retrieval;
   3. For Structured Information such as tabular data, business databases, and API documentation, construct corresponding schema mappings and access interfaces.
2. **Vectorization, Indexing, and Retrieval Re-ranking**
   1. Use the Embedding model to convert text/code/MultiModal Machine Learning content into vectors and store them in vector databases such as FAISS, Milvus, Qdrant, Weaviate, Pinecone, etc.;
   2. While retaining keyword indexing and metadata filtering capabilities (such as filtering by tenant, department, document type), combine them into a high-precision "pre-retrieval filtering + semantic retrieval + re-ranking" process;
   3. During the query, the retrieval results are fed into the large model together with the original question to implement "Retrieval Augmented Generation (RAG)" and return references and evidence chains.
3. **RAG Application Template and Low-Code Development**
   1. Provides prefabricated RAG templates for common scenarios (knowledge Q&A, policy interpretation, product description, internal document assistant, etc.);
   2. Quickly build a dedicated knowledge assistant through a visual configuration interface (selecting knowledge sources, setting chunking rules, and choosing vector models and large models);
   3. Expose these capabilities to developers in the form of SDKs, supporting quick embedding in Web, mobile, desktop, or business system plugins.
4. **Developer Platform and ****Ecosystem**** Integration**
   1. Provides SDKs for languages such as Python, JS, Java, and Go, as well as front-end components (chat bubbles, document reference areas, feedback buttons, etc.), reducing the integration threshold;
   2. Provide plugins or middleware for mainstream business systems (CRM / ERP / OA / Ticket) to enable them to access AI capabilities with just a few configuration selections;
   3. Open up the application development platform to allow ecosystem partners to build their own industry applications based on the base model, RAG, and Agent capabilities, thus forming a positive cycle of "platform - ecosystem - end customers".

This layer ultimately encapsulates complex models and infrastructure capabilities into "reusable and assemblable business components", helping enterprises ** under the premise of security, compliance, and controllable costs ** to truly transform large models into productivity tools that drive business innovation with lower barriers and at a faster pace.
