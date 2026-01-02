With the widespread application of Large Language Models (LLMs), enterprises face a practical question: How can models accurately answer questions based on internal documents, real-time data, or professional knowledge? After all, model training data is limited and time-bound, unable to cover enterprise-specific business knowledge and continuously updated information.

An intuitive solution is: Since model context windows are continuously expanding from 8K, 128K to now exceeding millions of tokens, why not simply stuff relevant documents into prompts and let the model generate answers based on these materials?

However, being able to process long contexts is entirely different from delivering correct answers stably, efficiently, and controllably in enterprise scenarios. Blindly relying on long contexts brings a series of severe challenges including skyrocketing costs, scattered attention, and delayed knowledge updates.

It was precisely to address these pain points that a technology called Retrieval-Augmented Generation (RAG) emerged. RAG enables large models to precisely retrieve external knowledge before generating answers. Compared to simply and crudely extending context length, it meets enterprise applications' stringent requirements for factual accuracy and knowledge freshness with lower cost, higher accuracy, and stronger controllability, becoming a key cornerstone for building trustworthy AI applications.

In this tutorial, we will systematically introduce what RAG is, trace its birth background and core principles, and deeply explore its evolution path from basic to advanced levels, as well as future development directions.

# What You Will Learn in This Lesson

* Core value of RAG: Deep understanding of how it solves key challenges of long context in cost, attention, and knowledge updates
* How RAG works: See through specific cases how it completes the closed loop from retrieval to generation
* RAG technology evolution: From basic Naive RAG to Advanced RAG to modular Modular RAG
* RAG model selection recommendations: Master evaluation and selection strategies for the three key models: Embedding, Rerank, and LLM
* RAG enterprise-level practice: Learn the full-chain construction guide from data preprocessing to system deployment evaluation
* RAG effectiveness evaluation and optimization: Understand core evaluation metrics, mainstream frameworks, and continuous optimization methods
* RAG frontier trends: Explore future directions of integration with agents, multimodality, and other technologies

# What You Will Gain from This Lesson

After completing this tutorial, you will establish a systematic introductory-level understanding of RAG technology, not only knowing what it is but why it works. You will gain a clear blueprint, knowing how to evaluate, select, and design an efficient, reliable, and controllable RAG system that meets enterprise-level requirements, laying a solid foundation for developing true enterprise-level RAG applications.

1. # Why RAG is Needed

Retrieval-Augmented Generation (RAG) is a very important technical approach in current generative AI. Its basic idea is: Before having a large model generate an answer, first retrieve information related to the question from an external knowledge base, then give these retrieval results together with the user's question to the model, letting the model answer based on reference to real materials. This external knowledge base can be enterprise internal policy and process documents, product knowledge bases, or industry databases, regulatory standard libraries, etc.

![](images/image1.png)

But at this point we will have a question: Since large models can already "directly answer questions," why do we need to add an additional "retrieval-augmented generation" layer? Especially now that large model context windows are getting larger, it seems that as long as we provide relevant materials to the model and let it understand first then answer, we can solve most needs.

The real difference is: **"Being able to give an answer"** and **"Continuously, stably, and controllably giving correct answers in real business environments"** are two completely different things. If only relying on the "memory" in model parameters, or simply putting large amounts of documents into long context, in actual enterprise applications, at least three types of typical problems will still be exposed:

1. **Cost and efficiency issues**:
   Even though large model contexts continue to expand, the attempt to "stuff all documents in at once" is still impractical in actual applications. The core contradictions focus on two points:
2. Inference cost is strongly positively correlated with context length: The longer the context, the higher the inference cost, rising almost linearly or even super-linearly. Taking a single call as an example, 8K Token vs. 200K Token correspond to completely different orders of magnitude in price and response latency, and the cost threshold for long context is significantly higher;
   ![](images/image2.png)

   > Context (context) in terms of meaning refers to the background information and conversation history that the model "references" when answering the current question; technically it refers to the sum of Token sequences (such as system/user instructions, historical messages, retrieval segments, etc.) input to the model during one inference.
   >
   > "Context window" is the **capacity limit** for this batch of input content: The model can at most "see" this many tokens at one time. In current mainstream large model architectures (such as Transformer), these tokens will perform attention calculations with each other in every layer of the model and repeatedly participate in calculations, so once the window becomes longer and there are more tokens, computational volume and cost will increase multiples or even exponentially.
   >
3. Computational resources are wasted in large quantities: The vast majority of tasks only require a very small amount of information highly relevant to the current question. Putting full documents into context causes serious computational resource idleness and waste, thereby reducing system throughput, slowing response speed, and ultimately affecting user experience.
4. **Attention and focus issues**:
   Although large models can "cover" ultra-long contexts, they cannot achieve equal quality utilization of every piece of information. When context length reaches a certain threshold, the model will show obvious "attention bias":
5. Attention decay: The model's attention to information at the front and middle of context will gradually weaken, more inclined to rely on recently read backend text, causing early key information to be "ignored";
6. Information interference: The model is easily "led astray" by irrelevant, repetitive, or even conflicting information in the context. Even if the final answer seems logically self-consistent, it may actually be disconnected from the core question, making it difficult to guarantee accuracy.
   It can be seen that without a retrieval link for information filtering and relevance sorting, the longer the context, the harder it is to ensure the answer focuses on truly key evidence, and the advantages of long context are completely offset by information interference.
7. **Knowledge update and controllability issues**:
   If all knowledge is completely dependent on model parameter storage, or manually copied into prompts for invocation, there will be two natural defects that are difficult to avoid:
8. Difficult knowledge updates: Once knowledge changes (such as policy adjustments, product iterations, price updates, etc.), either the model needs to be retrained or fine-tuned - high investment and long cycle; or prompt templates need to be manually maintained one by one - not only high cost, but also prone to information bias caused by human operational errors;
9. Poor traceability: When models give answers, it is often difficult to locate core evidence from "black-boxed parameters" or lengthy prompts, making work that requires clear "decision-making basis" such as compliance auditing and risk control explanation face great operational difficulties.

Under these practical constraints, RAG's advantages become clearer. Its core approach is: Before the model generates answers, first precisely locate relevant and reliable information through retrieval, letting the model generate answers based only on necessary knowledge. Knowledge can be stored independently in external knowledge bases, facilitating updates and management; meanwhile, generation results can be accompanied by citation sources, improving answer interpretability and credibility. Even if the model's context window continues to expand in the future, RAG can still achieve efficient knowledge management and utilization at lower cost, thereby supporting an enterprise-level knowledge application system with observable processes and traceable behaviors.

Starting from enterprise needs, compared with traditional LLMs that only rely on the model's own parameters, RAG mainly solves the following practical problems faced by enterprises in landing applications:

1. Timeliness issues:
   Traditional models often don't understand new regulations, new products, and new processes after 2024, while RAG can directly read the latest policy documents, business databases, and knowledge base content, keeping answers synchronized with the latest business without frequent model retraining.
2. Professionalism issues:
   General large models in vertical fields such as medical, chemical, and financial often have the problem of "not understanding deeply enough, not speaking accurately enough." After accessing enterprise proprietary professional documents and industry standards, model answers can be based on authoritative materials, significantly closer to real business practice.
3. "Hallucination" issues:
   By requiring answers to be based as much as possible on retrieved document segments and able to give corresponding source citations, the probability of baseless fabrication can be mechanistically reduced, making "sounding true" closer to "actually being true."
4. Interpretability and auditability issues:
   When pure parameter models give conclusions, it's often difficult to answer "which rule was this deduced from." RAG allows every answer to be traced back to specific policy clauses, business documents, or historical cases, making it convenient for business personnel to spot-check and correct errors, and also providing necessary traceability evidence for audit, risk control, and compliance departments.
5. Computing cost and resource efficiency issues:
   Having large models "memorize" all enterprise knowledge in parameters often means larger models and higher inference costs. RAG stores most knowledge in external vector databases and document libraries through "on-demand retrieval," enabling enterprises to still obtain broader coverage and more detailed and accurate answer capabilities under conditions of smaller models and limited computing power

Therefore, for enterprises hoping to use large models long-term, stably, and controllably in real business scenarios, RAG is not an optional enhancement, but an almost indispensable basic technology for building high-quality enterprise knowledge application systems.

2. # What is RAG

RAG (Retrieval-Augmented Generation)'s core idea is to let large models, when answering questions, not only rely on static knowledge learned during training, but also be able to call the latest, reliable information from external knowledge bases in real-time.

In a typical RAG system, user questions are not directly thrown to the large model. Instead, a retrieval module first finds the most relevant document segments from the enterprise knowledge base, then combines these contents with the original question into a complete context, inputting it to the large model to generate answers. This "retrieve first, then generate" approach allows the model to reason based on real reference materials, rather than speculating only based on knowledge "remembered" in parameters. We can refer to a typical case:

![](images/image3.png)

1. **Indexing Phase**

In the indexing phase, the system first processes raw materials such as enterprise internal documents, web articles, and reports, dividing them into smaller semantic segments (chunks), then uses a vector model to generate vector representations for each segment and establish an index. This way, when subsequently receiving user questions, it can quickly find the "semantically most similar" segments in the vector space.

In the diagram, this phase corresponds to the purple area "Indexing" in the upper right corner. The part from "Documents" through "Chunks / Vectors" to "embeddings" explains the process of documents being chunked and converted to vectors and written into the index. The specific process is as follows:

* Documents are divided into several semantically relatively complete chunks, each chunk possibly corresponding to a small piece of news, an explanation, or an analysis.
* Each chunk is converted to a high-dimensional vector through an embedding model and stored in a vector index.
* This index supports subsequent similarity-based retrieval, preparing a "searchable knowledge base" for answering questions in advance.

2. **Retrieval Phase + Answer Generation Based on Retrieval Results**

When users ask questions, the system first retrieves relevant content from the index, then gives the questions and retrieved text together to the large model to generate answers. The several key areas in the diagram from top to bottom, right to left exactly correspond to this entire process.

(1) User inputs question - yellow area in diagram Input – Query

> "How do you evaluate the fact that OpenAI's CEO, Sam Altman, went through a sudden dismissal by the board in just three days, and then was rehired by the company, resembling a real-life version of 'Game of Thrones' in terms of power dynamics?"

This large text is the content in the "Query" box in the diagram, corresponding to "the user-initiated natural language question." The system will vectorize this text and use it to search for relevant document segments in the index in the upper right corner.

(2) Retrieved relevant documents - pink area in lower right of diagram Relevant Documents

After retrieval is complete, the system obtains several document blocks most relevant to the question, displayed in the diagram as three Chunks:

> "Sam Altman Returns to OpenAI as CEO, Silicon Valley Drama Resembles the 'Zhen Huan' Comedy"
>
> "The Drama Concludes? Sam Altman to Return as CEO of OpenAI, Board to Undergo Restructuring"
>
> "The Personnel Turmoil at OpenAI Comes to an End: Who Won and Who Lost?"

(3) Combine Prompt and generate answer - blue area in diagram LLM / Combine Context and Prompts

The system then combines "user original question + retrieved chunks" into a complete Prompt and sends it to the large model. The dashed box in the lower middle, near the center of the diagram, is the example content of this Prompt:

> "Question:
> How do you evaluate the fact that the OpenAI's CEO, … … dynamics?
>
> Please answer the above questions based on the following information :
> Chunk 1 :
> Chunk 2 :
> Chunk 3 :"

(4) Answer comparison with and without RAG - gray/yellow area in lower left of diagram Output – Answer

Finally, the large model generates answers based on this information, results displayed in the "Answer" area in the lower left of the diagram. Here are shown output examples for both "without RAG" and "with RAG" cases. Without RAG, the model lacks external materials and can only give very vague responses, corresponding to that passage in the gray box:

> "… I am unable to provide comments on future events. Currently, I do not have any information regarding the dismissal and rehiring of OpenAI's CEO …"

With RAG, the model can use the news and analysis just retrieved to give more informative answers, corresponding to that text in the yellow box:

> "… This suggests significant internal disagreements within OpenAI regarding the company's future direction and strategic decisions. All of these twists and turns reflect power struggles and corporate governance issues within OpenAI …"

The above demonstrates the complete process of a typical RAG system, giving us an overall understanding of which core links the system contains and how information flows at each stage. However, how is vector matching performed during retrieval? How should prompts be organized to better enable the model to utilize retrieved content? These technical details that determine RAG's actual effectiveness are currently still "black boxes." Next, we will deeply explore RAG's internal mechanisms, gradually dissecting exactly how RAG works from key links such as vectorization principles, similarity calculation, to prompt engineering.

3. # How RAG Works

We can gradually dissect its key links through a knowledge base Q&A case about "apples."

## 3.1 Document Vectorization Phase

Suppose we have a simplified knowledge base containing the following three document segments:

1. Document segment A: Apple Inc. was founded on April 1, 1976 by Steve Jobs, Steve Wozniak, and Ronald Wayne, headquartered in Cupertino, California.
2. Document segment B: Apple is a fruit rich in vitamin C and dietary fiber, helpful for digestion and immune system health.
3. Document segment C: Apple Inc. launched the first iPhone in 2007, completely changing the smartphone industry.

When we use an embedding model (such as OpenAI's text-embedding-ada-002 or open-source BGE model) to process documents, each document segment is converted to a high-dimensional vector (typically containing 768, 1024, or 1536 dimensions).

> "Vector" is essentially an array composed of multiple numerical values, where each dimension's value corresponds to a semantic feature of the text in a certain dimension. For example, in the vector for "cat," there may be dimensions corresponding to attributes like "mammal," "pet," "has fur," etc. Finally, through the overall numerical combination, it precisely captures the semantic meaning of the text, enabling computers to "understand" associations between texts.

Simplified example (actual vector dimensions are much higher, this is only illustrative):

* Document A vector (about Apple company founding): `[0.85, -0.23, 0.41, -0.56, 0.12, 0.78, ...]`
* Document B vector (about apple fruit): `[-0.12, 0.95, -0.34, 0.67, -0.89, 0.05, ...]`
* Document C vector (about iPhone launch): `[0.79, -0.18, 0.52, -0.61, 0.23, 0.81, ...]`

Relevant vectors need to be stored in a vector database (such as Pinecone, Weaviate, FAISS) for subsequent retrieval recall work.

> A database is a system that stores and manages data according to a specific structure, with core functions of implementing orderly data storage and efficient access, commonly seen in scenarios such as contact lists and e-commerce product catalogs.
>
> A vector database is a subcategory of databases. Unlike traditional databases that store text, tables, and other data, it specializes in storing "vectors" (high-dimensional numerical arrays) and optimizes vector similarity retrieval capabilities to adapt to high-dimensional data management needs in AI scenarios.

## 3.2 User Query Retrieval and Response Phase

After the knowledge base completes vectorization storage, the RAG system can support user real-time query operations. When users ask questions, the system executes a coherent process: first converting the question into a vector, then recalling the most relevant information segments from the knowledge base through similarity calculation, and finally using these segments as the basis for generating answers. We present this complete process through three specific queries.

### Query 1: "When was Apple Inc. founded?"

In the query vectorization phase, this question is converted by the embedding model into a semantic vector, for example `[0.82, -0.21, 0.38, -0.58, 0.15, 0.76, ...]`. This vector is highly similar in numerical pattern to the previously stored "Document A vector" (about company founding) `[0.85, -0.23, 0.41, -0.56, 0.12, 0.78, ...]`.

Next, the system will perform similarity retrieval (Top-K, K=2) operations, calculating the cosine similarity between this query vector and all document vectors in the knowledge base (a metric measuring the closeness of vector directions). Results are as follows:

* Similarity with Document A (company founding): 0.97 (highly relevant)
* Similarity with Document C (iPhone launch): 0.88 (relevant, belongs to same company theme)
* Similarity with Document B (fruit nutrition): 0.12 (almost irrelevant)

> Top-K is a common filtering strategy in vector retrieval scenarios. The core meaning is "from all matching results, after sorting by similarity from high to low, select the top K ranked results"; K=2 is the specific numerical definition of this strategy, explicitly requiring the system to only retain the top 2 ranked document vectors by similarity, filtering out the remaining lower similarity results, ensuring subsequent answers are generated based only on the most relevant 2 document segments.

At this point, the returned results filtered by similarity values are called recall results. The system returns Top-2 document segments as evidence based on similarity scores from high to low:

1. Document A (similarity 0.97): "Apple Inc. was founded on April 1, 1976 by Steve Jobs, Steve Wozniak, and Ronald Wayne, headquartered in Cupertino, California."
2. Document C (similarity 0.88): "Apple Inc. launched the first iPhone in 2007, completely changing the smartphone industry."

In the large model response phase based on retrieval results, the system will construct the following complete dialogue input, putting the recall results into reference information and sending them to the LLM together with system prompts:

```Plain
[System Prompt]
You are a professional Q&A assistant. Please answer questions strictly based on the "Reference Information" provided by the user.
If the reference information contains the answer to the question, please answer directly based on that information.
If the reference information does not contain the answer to the question, please clearly inform the user "Unable to answer this question based on available materials," and do not fabricate information on your own.
Please cite the information points relied upon in your answer.
[Reference Information (Retrieved Context)]
Apple Inc. was founded on April 1, 1976 by Steve Jobs, Steve Wozniak, and Ronald Wayne, headquartered in Cupertino, California.
Apple Inc. launched the first iPhone in 2007, completely changing the smartphone industry.
[User Query]
When was Apple Inc. founded?
```

After receiving the above structured input, the LLM will follow system instructions and treat "Reference Information" as the only credible source for answering the question. Its final response will be similar to: "According to the provided reference information, Apple Inc. was founded on April 1, 1976. [Basis: Information 1]"

### Query 2: "What are the benefits of eating apples?"

In the query vectorization phase, this question is converted by the embedding model into a semantic vector, for example `[-0.08, 0.92, -0.31, 0.71, -0.85, 0.08, ...]`. This vector is highly similar in numerical pattern to the previously stored "Document B vector" (about fruit nutrition) `[-0.12, 0.95, -0.34, 0.67, -0.89, 0.05, ...]`.

Next, the system will perform similarity retrieval (Top-K, K=2) operations, calculating the cosine similarity between this query vector and all document vectors in the knowledge base. Results are as follows:

* Similarity with Document B (fruit nutrition): 0.95 (highly relevant)
* Similarity with Document C (iPhone launch): 0.18 (almost irrelevant)
* Similarity with Document A (company founding): 0.15 (almost irrelevant)

The system returns Top-2 document segments as evidence based on similarity scores from high to low:

1. Document B (similarity 0.95): "Apple is a fruit rich in vitamin C and dietary fiber, helpful for digestion and immune system health."
2. Document C (similarity 0.18): "Apple Inc. launched the first iPhone in 2007, completely changing the smartphone industry." (Extremely weak relevance, may be filtered by threshold in practice)

In the large model response phase based on retrieval results, the system will construct the following complete dialogue input, putting the recall results into reference information and sending them to the LLM together with system prompts:

```Plain
[System Prompt]
 You are a professional Q&A assistant. Please answer questions strictly based on the "Reference Information" provided by the user.
 If the reference information contains the answer to the question, please answer directly based on that information.
 If the reference information does not contain the answer to the question, please clearly inform the user "Unable to answer this question based on available materials," and do not fabricate information on your own.
 Please cite the information points relied upon in your answer.
[Reference Information (Retrieved Context)]
 Apple is a fruit rich in vitamin C and dietary fiber, helpful for digestion and immune system health.
 Apple Inc. launched the first iPhone in 2007, completely changing the smartphone industry.
[User Query]
 What are the benefits of eating apples?
```

After receiving the above structured input, the LLM's final response will be similar to:

> According to the provided reference information, apples are rich in vitamin C and dietary fiber, and eating apples helps with digestion as well as immune system health. [Basis: Information 1]

### Query 3: "What's the weather like today"

In the query vectorization phase, this question is converted by the embedding model into a semantic vector related to meteorology and weather, for example `[0.10, -0.05, 0.30, -0.12, 0.21, 0.08, ...]`. This vector is quite distant in semantic space from all document vectors about "apples (company/fruit)" in the knowledge base in terms of numerical pattern, so no significant similarity will appear.

Next, the system will perform similarity retrieval (Top-K, K=2) operations, calculating cosine similarity. Since the question topic is unrelated to knowledge base content, overall similarity scores are very low. Results are as follows:

* Similarity with Document B (fruit nutrition): 0.18 (extremely low)
* Similarity with Document C (iPhone launch): 0.10 (almost irrelevant)
* Similarity with Document A (company founding): 0.08 (almost irrelevant)

Top-K will still return the top K ranked results by similarity, but in this scenario, these results cannot provide effective evidence. Actual systems often combine a "minimum similarity threshold" to directly return empty recall, meaning no recalled results, reference information is 0, to reduce irrelevant information interference.

1. Document B (similarity 0.18): "Apple is a fruit rich in vitamin C and dietary fiber, helpful for digestion and immune system health."
2. Document C (similarity 0.10): "Apple Inc. launched the first iPhone in 2007, completely changing the smartphone industry."

In the large model response phase based on retrieval results, the system will construct the following complete input:

```Plain
[System Prompt]
 You are a professional Q&A assistant. Please answer questions strictly based on the "Reference Information" provided by the user.
 If the reference information contains the answer to the question, please answer directly based on that information.
 If the reference information does not contain the answer to the question, please clearly inform the user "Unable to answer this question based on available materials," and do not fabricate information on your own.
 Please cite the information points relied upon in your answer.
 [Reference Information (Retrieved Context)]
 Apple is a fruit rich in vitamin C and dietary fiber, helpful for digestion and immune system health.
 Apple Inc. launched the first iPhone in 2007, completely changing the smartphone industry.
 [User Query]
 What's the weather like today?
```

After receiving the above structured input, the LLM will first determine whether the reference information contains direct information such as "weather/meteorology/real-time data"; after confirming the reference information is unrelated to the question, it will follow system instructions to execute "unable to answer." Its final response will be similar to:

> Unable to answer "What's the weather like today" based on available materials, because the reference information only contains content related to apples (fruit nutrition, Apple Inc. products) and does not contain weather information or real-time meteorological data. [Basis: No weather-related information in reference information]

Through the above three examples, it can be seen that in the large model dialogue phase of retrieval-augmented generation, system instructions set the LLM's role and answering rules, retrieval evidence provides specific, credible answering materials, and user questions clarify the task objective. This structured input approach is precisely the key to RAG technology's ability to effectively guide and constrain large models that might otherwise produce "hallucinations," making their output stable and reliable answers. It ensures that large model capabilities are precisely applied to understanding and organizing existing information, rather than creating information without basis.

4. # RAG Technology Evolution History

RAG technology did not emerge in the large model era; prototypes existed in earlier research. From the development perspective, RAG's emergence stemmed from recognizing traditional LLM limitations. Early large language models mainly relied on pre-training data, which was typically fixed after model training completion, unable to access subsequently updated information. For example, knowledge cutoff points for models like GPT-3 usually come after the date of training data collection, unable to access new knowledge. Additionally, retraining or fine-tuning LLMs to adapt to specific domains requires large amounts of resources and professional knowledge, with high costs and difficulty in rapid iteration.

RAG technology's origins can be traced back to the DrQA framework in 2017, which first attempted to combine retrieval mechanisms with language models. Subsequently, Dense Passage Retrieval (DPR) introduced in 2020 marked a major breakthrough in RAG technology, using pre-trained neural network models for semantic retrieval rather than traditional frequency-based methods like TF-IDF or BM25. In 2021, RAG was formally proposed and systematized, becoming a standard method for addressing LLM knowledge cutoff and hallucination problems.

Overall, RAG's evolution can be roughly divided into three stages:

![](images/image4.png)

## 4.1 First Generation RAG: Naive RAG (Basic Retrieval Augmentation)

Naive RAG can be understood as the basic form of RAG. It is very direct in engineering terms, and the typical process can be summarized as "three steps": The first step is document preprocessing and indexing, where raw documents after cleaning are divided into several text blocks (chunks) by fixed length, then each text block is encoded into a vector using an embedding model and written into a vector database; the second step is similarity-based retrieval, where the user's natural language question is encoded into a vector, Top-K similarity search is performed in the vector database, retrieving the text blocks with the highest similarity; the third step is simple concatenated augmented generation, where these retrieved text blocks and the original question are directly concatenated into a long prompt given to the LLM, and the model generates answers based on this context.

The value of this stage lies in validating with a very low threshold that the "retrieve first then answer" approach is indeed effective: compared to completely relying on model internal memory, it can significantly alleviate knowledge cutoff and some hallucination problems, playing an important role in early prototype systems and example projects. This made RAG highly practical from the start, becoming the first choice for numerous demos, prototype systems, and introductory tutorials.

However, the limitations of this generation of RAG are equally obvious. First, text chunking strategies are usually quite crude, mostly using fixed-length segmentation, easily cutting a complete semantic paragraph from the middle, or mixing multiple themes in the same chunk, which both affects retrieval accuracy and brings additional burden to LLM understanding. Second, retrieval signals are very single, often relying only on vector similarity for sorting, without utilizing richer structured clues such as keywords, timestamps, source credibility, access permissions, etc. Third, retrieval results undergo almost no filtering and governance, and noise, repetitive, or even conflicting segments are stuffed into context as-is, making the already tight context window occupied by large amounts of "low-value information."

It can be said that first-generation RAG solved the problem of "whether to retrieve," but remains at a quite primitive stage in the two questions of "how to better retrieve" and "how to more reasonably use retrieved things."

## 4.2 Second Generation RAG: Advanced RAG (Refined Optimization of Retrieval and Context)

As RAG applications move from demos to real business scenarios, system requirements for stability, controllability, and result quality rapidly increase. The second-generation RAG that emerged at this point can generally be called Advanced RAG. It still follows the approach of retrieving first then generating, but introduces systematic refined optimization strategies in both pre-retrieval and post-retrieval links. In other words, no longer satisfied with "whether things can be retrieved," but "store what should be stored well, ask what should be asked clearly, and govern retrieved context well."

Before retrieval, the focus is on handling "what to store" and "how to ask" well:

* At the indexing end, evolve from fixed-length segmentation to semantic-aware chunking and hierarchical indexing, for example segmentation by chapter, section, paragraph, or sentence boundaries, supplemented by sliding windows and multi-granularity index structures.
* Attach rich metadata to each document block, such as source, time, author, topic, document type, etc., providing more dimensions for subsequent filtering and sorting.
* At the query end, rewrite, expand, and split the user's original question, for example through Query Rewrite, Multi-Query, Sub-Query, Step-back Prompting, etc., converting vague or colloquial questions into expressions more conducive to retrieval understanding.
  > 1. Query Rewrite
  >
  > The core is to convert users' vague, colloquial, or non-standard original queries into standardized expressions more easily understood by retrieval systems, supplementing key information and correcting ambiguity.
  >
  > * User's original question is "How to check tomorrow's Beijing weather", will remove colloquial words, supplement key qualifiers like "real-time" and "all-day," rewritten as "Query Beijing city tomorrow all-day real-time weather";
  > * User's original question is "Recommend good movies", if combined with user behavior history showing they often watch suspense films, will supplement information like "2024 high-rated" and "suspense genre," rewritten as "Recommend 2024 high-rated suspense genre movies".
  >
  > 2. Multi-Query
  >
  > Generate multiple queries "semantically related but from different angles" based on the original question, avoiding single queries missing potential results, covering users' unstated potential needs.
  >
  > * User's original question is "How to burp a one-month-old baby", will generate queries focusing on "posture": "Correct posture for burping newborns";
  >   * Generate queries focusing on "preventing spit-up": "Methods for burping one-month-old babies to avoid spit-up";
  >   * Generate queries focusing on "age-appropriate": "Steps for burping infants (0-1 months)";
  >   * Generate queries focusing on "novice scenario": "Tips for novice parents burping one-month-old babies".
  >
  > 3. Sub-Query
  >
  > For composite questions containing multiple demands, split into independent, simple sub-queries, allowing the retrieval system to precisely match data for single demands, avoiding mixed and missing information.
  >
  > * User's original composite question is "High-speed rail from Beijing to Shanghai, what are tomorrow's schedules? How much are tickets? How long does it take?", will split into sub-queries focusing on "schedules": "Beijing city to Shanghai city tomorrow high-speed rail schedule table";
  >   * Split into sub-queries focusing on "ticket prices": "Beijing to Shanghai high-speed rail second-class / first-class ticket prices";
  >   * Split into sub-queries focusing on "duration": "Beijing to Shanghai high-speed rail travel time (fastest / average)".
  >
  > 4. Step-back Prompting
  >
  > First generate a "more macro higher-level question than the original question," then deduce retrieval direction based on higher-level logic, solving understanding bias caused by the original question focusing on details.
  >
  > * User's original question is "Why did a domestic new energy vehicle brand's sales suddenly drop in 2024?", first step generates a macro higher-level question: "What are the core factors affecting short-term sales fluctuations of new energy vehicle brands?" (such as product iteration, competitor moves, policy changes, market demand, etc.);
  > * Second step, based on higher-level question logic, generates specific retrieval directions: "2024 domestic new energy brand product update situation", "2024 new energy vehicle market competitor pricing strategy", "2024 new energy vehicle subsidy policy adjustments".
  >

After retrieval, the focus is on governing well the "retrieved content":

* Use specialized Rerank models or LLMs to re-rank candidate documents, ensuring the most critical, question-relevant content enters context first.
  > Rerank model is a key component in the information retrieval process, mainly used for secondary sorting of candidate results preliminarily filtered in the "recall phase" - it leverages more complex semantic understanding capabilities (often based on deep learning architectures like Transformer) to analyze the deep association between user needs and candidate results, correct possible semantic deviations in preliminary sorting, and ultimately make results better fitting user needs rank higher, improving user efficiency in obtaining effective information.
  >
* Filter, deduplicate, and compress retrieval results, removing obviously irrelevant or highly repetitive segments, alleviating the problem of middle context information being ignored in long contexts.
* When necessary, combine lightweight model fine-tuning to make LLMs more inclined to answer based on retrieval evidence, and attach citation or source information in answers.

Overall, second-generation retrieval-augmented generation technology no longer focuses only on basic questions of "whether retrieval is needed" and "whether information can be retrieved," but further focuses on three greater challenges: "Can we precisely locate truly key paragraph content," "Is the context passed to large models concise, orderly, clearly structured, and easy to use efficiently," and "When facing information noise, content conflicts, or multi-source data retrieval needs, is overall system performance still robust and reliable."

From extensive experimental validation and engineering landing practice, Advanced RAG is significantly superior to Naive RAG in key indicators such as Q&A accuracy, hallucination suppression capability, system robustness, and result interpretability. It is precisely for this reason that Advanced RAG has gradually replaced traditional solutions to become the current mainstream technical paradigm for building RAG systems in industry.

## 4.3 Third Generation RAG: Modular RAG

In enterprise-level complex application scenarios, needs often span multiple domains. In this case, if RAG systems only adopt a single linear processing method like retrieval, reranking, generation, they are often difficult to cope with:

1. The same system needs to support both simple FAQs and generate long reports, perform code retrieval, or call databases.
2. Need to simultaneously connect multiple data sources such as vector databases, full-text retrieval, relational databases, knowledge graphs, and external search engines.
3. Need to maintain memory of user preferences and historical decisions in multi-round interactions, and implement compliance auditing and traceability of output results.

Against this background, RAG's system form began evolving toward modularity. Modular RAG is no longer seen as a fixed pipeline, but composed of a set of pluggable, replaceable, composable functional modules, combined and executed on-demand through orchestration logic. Typical modules include:

1. Query Understanding and Routing Module
   Used for intent recognition, question rewriting, sub-task decomposition, and path selection, deciding whether a request mainly relies on internal knowledge or external retrieval, or needs to call specific tools or databases.
   For example, when users ask "What problem does this error log represent?" the system routes it to the code and log knowledge base; while asking "What are the recent regulatory changes in this industry?" is more suitable for internet search or compliance regulation databases.
2. Multi-source Retrieval and Fusion Module
   Simultaneously connects vector databases, full-text retrieval systems, structured databases, and knowledge graphs, queries different data sources, and uniformly fuses and sorts results.
   For example, when doing "customer annual analysis report," part of the information comes from CRM database (such as customer transaction amounts), part from document library (such as project reviews), and may also need to supplement industry relationships from knowledge graphs, finally this module merges multi-source results into an ordered evidence set.
3. Memory and Personalization Module
   Maintains long-term user profiles, short-term session memory, and domain knowledge caching, enabling systems to continuously accumulate and utilize historical information in long-term interactions.
   For instance, the system remembers a certain user prefers "conclusion first then details," and the business line and common terminology they are in, so next time when answering will automatically adopt the corresponding style and prioritize using cases and data related to that business line.
4. Task Adaptation and Governance Module
   Loads corresponding adapters for different tasks, constrains output format, tone, and style, and combines mechanisms such as fact-checking, risk filtering, and citation alignment to govern generation results.
   For example, based on the same batch of retrieval results, for product managers it generates structured PRD templates, for legal personnel it's formal compliance review opinions; in this process, this module performs secondary verification of key facts and requires giving citation sources.

Overall, traditional RAG often ends after one retrieval paired with one generation, while Modular RAG breaks this single process. When the system discovers insufficient information during generation, it can actively trigger new retrieval rounds, or even multiple round-trip retrievals and generations to complete more complex tasks.

Furthermore, models can also learn self-decision-making: directly answering based on internal knowledge or short context for questions with high confidence; only initiating retrieval or calling external tools when uncertain, thereby improving efficiency and saving resources while ensuring quality. For queries with unclear expressions or severely missing information, systems can even first have a large model generate a hypothetical answer or intermediate document, then use this as a "clue" to retrieve real documents, continuously approaching reliable information sources.

At this stage, RAG is no longer just a simple component that supplements a few reference materials to large models, but gradually evolves into a central knowledge orchestration layer for enterprise-level intelligent applications, responsible for coordination and scheduling among multiple data sources, tools, and tasks.

5. # From Demo to Enterprise-Level RAG System

From the perspective of enterprise engineering practice, building RAG systems cannot be limited to retrieval-augmented generation technology itself. The content mentioned above is more of a demo-level introduction. Because data in actual business scenarios often has issues such as uneven quality and messy formats, more effort needs to be invested in data preprocessing, cleaning, and import links, while making reasonable model selections at various key nodes.

A complete enterprise-level RAG system can usually be divided into three core modules: layout analysis and knowledge acquisition, knowledge base construction, and RAG-based knowledge Q&A services. Throughout the entire technology chain, multiple key model selection decisions are involved, including Embedding models, Rerank models, and LLM models. Only by making reasonable technical choices at each link can we ensure the system achieves optimal results.

1. Layout Analysis and Local Knowledge File Reading

This module is responsible for converting various formats of local knowledge assets into text available for retrieval. Inputs may include documents such as PDF, TXT, HTML, Word, Excel, PPT, as well as image files like PNG, JPG scanned copies, or even voice recordings.

The system needs to parse different formats, perform layout analysis and structure extraction on text documents, distinguishing elements such as titles, body text, tables, headers, and footers, restoring reasonable reading order. For image files, perform OCR recognition, for voice perform speech transcription (ASR), finally uniformly converting to relatively clean knowledge text, while preserving some basic meta-information such as document name, chapters, page numbers, time, etc., laying the foundation for subsequent segmentation and indexing.

2. Knowledge Base Construction (Chunking, Embedding, Indexing)

After obtaining cleaned knowledge text, reasonable text chunking is first needed, dividing long documents into several text blocks with relatively complete semantics and moderate length, usually segmented by paragraph, title structure, or sliding window, while preserving the document source and metadata corresponding to each block.

Then, using a selected Embedding model such as text-embedding-3-small, Sentence Transformers, BGE, etc., calculate vector representations for each text block, and build a vector index based on these vectors, such as using Faiss, Milvus, vector search services, etc., to obtain a knowledge base capable of fast queries by semantic similarity. At this point, we complete the core step of converting knowledge into retrievable vectors.

3. RAG-based Knowledge Q&A (Recall, Ranking, Concatenation, Generation)

In the online Q&A phase, users first issue query requests, the system performs Embedding on queries to obtain query vectors, and retrieves a batch of most similar text blocks (Top N) in the vector index, this is the coarse ranking phase. On this basis, can optionally use Rerank models such as BGE Reranker or LLM as Reranker to perform fine-grained scoring on query-document pairs, selecting Top K truly most relevant documents as knowledge context.

Then, combining carefully designed system prompts such as "Please answer strictly based on the following materials," concatenate user queries and retrieved document segments, send this merged prompt to the LLM, which generates the final answer based on retrieved evidence, and attaches citations or sources when needed.

## 5.1 Model Selection

Next we focus on model selection for each link. A complete RAG system usually involves three core model types: Embedding models, Rerank models, and Large Language Models. These three types of models each perform their own duties, jointly constituting the complete process from knowledge retrieval to answer generation. Among them, Embedding models are responsible for converting text into retrievable semantic vectors, Rerank models perform fine filtering and reordering of preliminary retrieval results, and Large Language Models generate final answers based on filtered knowledge context.

### 5.1.1 Embedding model

In RAG systems, the Embedding model's role is to convert text, such as user queries and knowledge base content, into high-dimensional vectors. Semantically similar text will have vectors that are closer together in space, enabling systems to quickly locate relevant knowledge through vector similarity. Therefore, choosing an appropriate Embedding model is a key step in building high-performance RAG systems, directly determining the quality of the recall phase.

To select good models, we introduce here a systematic evaluation benchmark: MTEB (Massive Text Embedding Benchmark)

MTEB provides a unified, objective evaluation framework for various Embedding models. Through 8 major task categories and 56 datasets, it comprehensively evaluates model performance in retrieval, clustering, classification, reranking, text matching, semantic similarity, and other scenarios. The model's overall score on MTEB can reflect the universality and robustness of its vector representation capability, serving as an important data reference for selection. The latest rankings and detailed results can be viewed through the [HuggingFace MTEB Leaderboard](https://huggingface.co/spaces/mteb/leaderboard).

![](images/image5.png)

Although there are many models on the leaderboard, you can choose according to actual needs and don't need to master all models (generally, choosing the Embedding model that comes with large model manufacturers, or using models deployed on cloud platforms for external use will mostly be correct, as this is the standard verified by most people), you can also select specific categories or languages in the sidebar for filtering:

![](images/image6.png)

Additionally, when filtering Embedding models, need to focus on two core parameters that directly affect RAG performance: dimension and context length. Among them, dimension refers to the number of dimensions of the model's output vector (such as 128 dimensions, 768 dimensions), essentially reflecting the "number of features" used to describe semantic information. Higher dimension means vectors can depict semantic details more richly and strongly, for example a 768-dimensional vector can finely characterize "apple" from hundreds of angles such as variety, taste, origin, etc., thereby more suitable for professional scenarios requiring precise retrieval such as medical and legal; lower dimension means lower calculation and storage costs, faster retrieval speed, suitable for general scenarios with millions of documents, high concurrency, and strong real-time requirements.

Another parameter Context Length refers to the maximum text length an Embedding model can process at one time (in tokens, 1 English token ≈ 0.75 words, 1 Chinese token ≈ 1 Chinese character), excess will be truncated: it directly determines whether the model can completely understand text, if insufficient length causes information loss, will significantly reduce retrieval accuracy. Therefore when processing short text such as user short sentences and Q&A pairs, choosing models with 512-1024 token is sufficient; when processing long text such as papers and reports, need to choose models with 2048 token and above to avoid key information loss.

The following is a horizontal comparison of several common Embedding models. You need to comprehensively consider cost and performance to choose the best model during actual invocation. There is no best model, only the most suitable model selected by comparing effects of multiple models.

| Model Name                      | Model Scale                         | Core Advantages                                       | Applicable Scenarios                                                    |
| ----------------------------- | -------------------------------- | ---------------------------------------------- | ----------------------------------------------------------- |
| OpenAI text-embedding-3-large | Closed-source API                          | Long-term leader on MTEB test set, mature and stable                 | Pursuing ultimate performance with sufficient budget cloud API scenarios, suitable for applications insensitive to latency |
| jina-embeddings-v2            | Supports long text (up to 8K context)       | Asynchronous encoding design, powerful in processing long document retrieval           | Document analysis requiring long context understanding, legal compliance, academic literature retrieval          |
| multilingual-e5-large         | Large scale                        | Classic multilingual backup option                           | Cross-language RAG, international products, multilingual customer service systems                       |
| Qwen/Qwen2-Embedding-8B       | 8B parameters, supports up to 4096-dimension customization     | Once first on MTEB multilingual list, strong in long text, multilingual and code capabilities | High precision Chinese-English RAG, long document analysis, code retrieval                       |
| Qwen/Qwen2-Embedding-4B       | 4B parameters                           | Balance of performance and efficiency                                 | Large-scale production-level RAG systems, high cost-effectiveness                               |
| Qwen/Qwen2-Embedding-0.6B     | 0.6B                             | Suitable for edge devices                                   | Resource-insufficient scenarios, scenarios requiring speed priority                          |
| BAAI/bge-m3                   | Supports hybrid retrieval (dense+sparse+multi-vector) | Leader on cross-language benchmarks like MIRACL                       | Complex multilingual scenarios requiring hybrid retrieval strategies                            |
| BAAI/bge-large-zh-v1.5        | Large scale                        | Stable baseline for Chinese RAG, fully community-verified                | Pure Chinese with shorter documents, projects pursuing stability                          |
| Zhipu AI Embedding-3            | Closed-source cloud API                      | Supports custom dimensions (256-2048 dimensions)                   | Focus on Chinese and prefer cloud API service applications                             |

### 5.1.2 Rerank model

In RAG systems, the Rerank model's role is to perform fine-grained reordering of preliminary retrieval results. It receives user queries and candidate documents as input, calculating precise relevance scores for each (query-document) pair, with higher scores indicating better document-query matching. Therefore, introducing Rerank models on top of Embedding recall is a key step in improving RAG system retrieval precision.

When choosing Embedding models, we can use benchmarks like MTEB. For Rerank models we can refer to Agentset's [Reranker Leaderboard](https://agentset.ai/rerankers), which systematically tests reranking capabilities in RAG scenarios.

| Model Name↑                                                                                        | ELO  | nDCG@10 | Latency (ms) | Price / 1M | License      |
| --------------------------------------------------------------------------------------------------- | ---- | ------- | ------------ | ---------- | ------------ |
| [BAAI/BGE Reranker v2 M3](https://agentset.ai/rerankers/baaibge-reranker-v2-m3)                        | 1314 | 0.201   | 2383         | $0.02      | Apache 2.0   |
| [Cohere Rerank 3.5](https://agentset.ai/rerankers/cohere-rerank-35)                                    | 1452 | 0.2     | 392          | $0.05      | Proprietary  |
| [Cohere Rerank 4 Fast](https://agentset.ai/rerankers/cohere-rerank-4-fast)                             | 1506 | 0.216   | 447          | $0.05      | Proprietary  |
| [Cohere Rerank 4 Pro](https://agentset.ai/rerankers/cohere-rerank-4-pro)                               | 1627 | 0.219   | 614          | $0.05      | Proprietary  |
| [Contextual AI Rerank v2 Instruct](https://agentset.ai/rerankers/contextual-ai-rerank-v2-instruct)     | 1461 | 0.23    | 3333         | $0.05      | cc-by-nc-4.0 |
| [Jina Reranker v2 Base Multilingual](https://agentset.ai/rerankers/jina-reranker-v2-base-multilingual) | 1306 | 0.193   | 746          | $0.05      | cc-by-nc-4.0 |
| [Voyage AI Rerank 2.5](https://agentset.ai/rerankers/voyage-ai-rerank-25)                              | 1547 | 0.235   | 613          | $0.05      | Proprietary  |
| [Voyage AI Rerank 2.5 Lite](https://agentset.ai/rerankers/voyage-ai-rerank-25-lite)                    | 1528 | 0.226   | 616          | $0.02      | Proprietary  |
| [Zerank 1](https://agentset.ai/rerankers/zerank-1)                                                     | 1574 | 0.192   | 266          | $0.03      | cc-by-nc-4.0 |
| [Zerank 1 Small](https://agentset.ai/rerankers/zerank-1-small)                                         | 1541 | 0.202   | 248          | $0.03      | Apache 2.0   |
| [Zerank 2](https://agentset.ai/rerankers/zerank-2)                                                     | 1644 | 0.195   | 265          | $0.03      | cc-by-nc-4.0 |

When evaluating Rerank model performance, Agentset benchmarks use the following process: First retrieve the top 50 candidate results most relevant to queries from large-scale document libraries based on the vector database FAISS, then have the Rerank model being evaluated re-rank these 50 documents. The evaluation process simultaneously focuses on two key dimensions: sorting quality and inference latency. In actual application scenarios, only pursuing high precision while ignoring response speed will harm user experience, while only pursuing speed but sacrificing sorting quality will lead to decreased result practicality.

To further compare model capabilities, Agentset benchmarks additionally introduce an ELO scoring mechanism: For each query, GPT-5 serves as an objective "judge," performing pairwise comparison on the sorting results output by two different Rerank models, with the core criterion being which model can arrange truly relevant documents more reasonably and higher. After continuous comparison across massive queries, models with higher winning frequencies obtain higher ELO scores, thereby intuitively reflecting differences in model comprehensive performance.

On this basis, the benchmark also designs two sets of complementary indicators for multi-dimensional comprehensive evaluation of models:

* nDCG@5/10: Focuses on sorting precision, emphasizing whether relevant documents are reasonably placed at the front of results, directly reflecting "ranking accuracy" capability;
* Recall@5/10: Focuses on result coverage, core evaluating whether the system can identify all documents relevant to the query, corresponding to "finding comprehensively" capability.

These two sets of indicators complement each other, jointly building a complete evaluation system for Rerank models, ensuring evaluation results have greater comprehensiveness and reference value.

However in actual use, we don't necessarily need to only refer to LeaderBoard for model selection. Besides ranking factors, mainly because industrial usability and high scores aren't necessarily the same thing. We can choose based on Rerank models recommended by various cloud service providers (such as large model manufacturers' default Rerank APIs, or can try Qwen's corresponding Rerank model, in the current 2025 situation as a multi-parameter-supported Rerank model the effect is decent.)

### 5.1.3 LLM

After semantic retrieval by Embedding models and precise filtering by Rerank models, relevant document segments are integrated with the user's original question into a prompt, and finally the LLM completes reading comprehension, information integration, and natural language generation, outputting coherent, accurate, and context-appropriate answers to users.

At the implementation level, LLM usage in RAG is mainly divided into two types:

1. Privately deployed large models. Suitable for scenarios emphasizing data privacy, controllable costs, or needing deep customization. Current mainstream open-source LLMs such as Qwen series, Llama series, GLM series, etc. perform excellently in RAG tasks. Taking Qwen2.5 as an example, 7B or 14B parameter versions maintain smaller resource occupation while showing good instruction-following and Chinese understanding capabilities, particularly suitable for enterprise-level RAG application local deployment. KIMI, Minimax, DeepSeek, and other models also show their respective advantages in different languages and domains, and can be flexibly selected according to specific business needs.
2. Large models as cloud API services. Suitable for scenarios pursuing rapid launch, elastic scaling, and continuous model iteration. Mainstream providers such as OpenAI (GPT-4 series), Anthropic (Claude series), Google (Gemini series), and domestic Alibaba (Tongyi Qianwen), Zhipu AI (GLM series), etc. all provide stable API services. These models generally have powerful language understanding and generation capabilities, capable of high-quality completion of RAG scenario answer synthesis tasks.
   When choosing cloud models, need to focus on several key points: whether answer quality is accurate and fluent, whether pricing is reasonable, whether response speed is fast enough, whether context window is large enough (can hold retrieved multiple documents). In actual use, can first take several candidate models for comparative testing, seeing which answers more accurately and completely. If cost-sensitive, can use "large and small model pairing": use cheap small models for simple questions, only call expensive large models for complex questions, saving money while ensuring effectiveness. Additionally, large models update quickly, suggest regularly testing new models, timely replacing with better-performing versions.

For comprehensive capability evaluation of large language models in dialogue and Q&A scenarios, [LMSYS Chatbot Arena (LMArena)](https://lmarena.ai/) provides an industry-recognized gold evaluation benchmark. The platform uses an innovative "blind test battle" mechanism - human evaluators, without knowing model identities, compare the quality of responses from two anonymous models to the same prompt, ranking models through a large number of such pairwise comparisons.

The following is an example of arena rankings (as of December 15, 2025):

| Rank | Model                                                                                    | Score | Votes  | Organization | License     |
| ---- | ---------------------------------------------------------------------------------------- | ----- | ------ | ------------ | ----------- |
| 1    | [gemini-3-pro](http://aistudio.google.com/app/prompts/new_chat?model=gemini-3-pro-preview)  | 1492  | 15,871 | Google       | Proprietary |
| 2    | [grok-4.1-thinking](https://x.ai/news/grok-4-1)                                             | 1478  | 16,660 | xAI          | Proprietary |
| 3    | [claude-opus-4-5-20251101-thinking-32k](https://www.anthropic.com/news/claude-opus-4-5)     | 1470  | 9,879  | Anthropic    | Proprietary |
| 4    | [claude-opus-4-5-20251101](https://www.anthropic.com/news/claude-opus-4-5)                  | 1467  | 10,659 | Anthropic    | Proprietary |
| 5    | [grok-4.1](https://x.ai/news/grok-4-1)                                                      | 1465  | 16,501 | xAI          | Proprietary |
| 6    | [gpt-5.1-high](https://openai.com/index/gpt-5-1/)                                           | 1457  | 13,953 | OpenAI       | Proprietary |
| 7    | [gemini-2.5-pro](http://aistudio.google.com/app/prompts/new_chat?model=gemini-2.5-pro)      | 1451  | 76,975 | Google       | Proprietary |
| 8    | [claude-sonnet-4-5-20250929-thinking-32k](https://www.anthropic.com/news/claude-sonnet-4-5) | 1450  | 28,019 | Anthropic    | Proprietary |
| 9    | [claude-opus-4-1-20250805-thinking-16k](https://www.anthropic.com/news/claude-opus-4-1)     | 1448  | 43,836 | Anthropic    | Proprietary |
| 10   | [claude-sonnet-4-5-20250929](https://www.anthropic.com/news/claude-sonnet-4-5)              | 1445  | 23,185 | Anthropic    | Proprietary |

LMArena's unique value lies in its evaluation approach being closer to real user experience, rather than purely relying on automated metrics. The leaderboard not only shows overall rankings but also subdivides into different capability dimensions (such as reasoning ability, creative ability, multilingual support, etc.), helping developers choose the most suitable models according to actual application scenarios. As of 2025, the platform has accumulated over 1 million human evaluations, covering 50+ mainstream open-source and closed-source models, becoming an important reference for LLM selection.

Visit the LMArena official website to view real-time leaderboards, detailed capability analysis, and direct comparison data between models. However in actual selection, suggest using LMArena rankings as a preliminary screening basis, then combining enterprise-specific data for A/B testing. Especially in professional domains (such as medical, legal, financial), there may be large differences between general leaderboard rankings and actual performance, and targeted testing is particularly important.

The best practice for LLM selection is to build a small but representative test set containing 20-30 typical business questions, performing end-to-end RAG process evaluation on candidate models, rather than only evaluating LLM single-point performance, such as using reasoning models or non-reasoning models, using what parameter model can balance RAG effect and speed; these all need to be tested in actual use to obtain optimal conclusions.

## 5.2 Running Frameworks

In actual engineering practice, usually no need to build the entire RAG system from scratch. Currently multiple mature open-source frameworks are available in industry for selection, each with characteristics in architectural design, module integration, and development efficiency. Enterprises can choose appropriate frameworks to quickly build systems based on their own technical reserves and business scenarios. Common framework types include:

 **Low-code** **/Visual Platforms**

* [Dify](https://dify.ai): Provides intuitive visual interface, supports rapid RAG application construction, suitable for non-technical teams or rapid prototype validation scenarios. Built-in multi-model access, workflow orchestration, and prompt management functions.
* [Coze](https://www.coze.com/): AI Bot development platform launched by ByteDance, providing zero-code visual construction capability. Feature is deep integration with ByteDance series large models like Doubao, supports plugin marketplace, scheduled tasks, and multi-channel publishing (Feishu, WeChat, etc.), suitable for rapidly building dialogue applications facing C-end users or enterprise internal intelligent assistants.
* [n8n](https://n8n.io/): An open-source, node-based workflow automation platform. It visually connects various applications, APIs, and data sources. In RAG scenarios, can use n8n to orchestrate complex business logic, connecting data preprocessing, vector database operations, large model invocation, and subsequent actions (such as sending emails, updating tickets) into an automated process.
* [RAGFlow](https://ragflow.io/): Focuses on deep layout analysis and knowledge extraction capabilities, better at processing complex documents (such as multi-column PDFs, table-intensive documents), suitable for enterprise knowledge base scenarios with complex document structures.
* [FastGPT](https://fastgpt.io/en): Domestic open-source solution, integrating knowledge base management, dialogue flow orchestration, and application publishing functions, with complete Chinese documentation, suitable for rapidly deploying Chinese RAG applications.

**Code Frameworks/Development Libraries**

The software introduced below usually has implementations for different platforms (frontend/backend languages). You can choose the corresponding language version of the following software based on the current application's language (such as Python or Java versions).

* [LlamaIndex](https://www.llamaindex.ai/): Python framework specifically designed for RAG scenarios, providing rich data connectors, index structures, and query engines, high modularity, suitable for scenarios needing deep customization of retrieval strategies or integrating multiple data sources.
* [LangChain](https://www.langchain.com/): General LLM application development framework, RAG is just one application direction. Advantage lies in rich ecosystem and complete components, supporting complex Agent and workflow orchestration, but steeper learning curve, suitable for building complex multi-module LLM applications.

If team technical reserves are limited and pursuing rapid launch, can prioritize low-code platforms like Dify, Coze, or FastGPT; if need deep customization of retrieval frameworks, connecting special data sources, or optimizing performance details, LlamaIndex and LangChain provide greater flexibility. In actual projects, can also use "hybrid solutions": use low-code platforms to quickly verify feasibility, then use code frameworks for production-level deployment and performance optimization. Additionally, these frameworks mostly support rapid access to mainstream Embedding, Rerank, and LLM models, can flexibly combine ultimately used models based on the model selection criteria mentioned earlier.

## 5.3 Effect Evaluation

The biggest challenge enterprises face in RAG system landing is often not construction but optimization, for large enterprises. Production-level large RAG systems need measurable and quantifiable effect evaluation. RAG involves two non-deterministic links: retrieval and generation, traditional software testing methods no longer apply, and establishing scientific evaluation systems (RAG Evaluation) is crucial. We need to understand how to systematically evaluate RAG effects.

### 5.3.1 Introductory Example: LLM-based RAG Effect Evaluation

To help everyone quickly establish intuitive understanding of RAG effect evaluation, this section will illustrate with an LLM-based RAG effect automated evaluation process. The core of this solution is "LLM-as-a-judge," that is, using large models themselves as judges to quantitatively evaluate RAG system output quality https://huggingface.co/learn/cookbook/rag_evaluation.

Specifically, this process usually contains three key steps:

* First, synthesize evaluation dataset, need to sample documents from knowledge base and instruct LLM to generate corresponding high-quality "question-reference answer" pairs, then filter through relevance, fact groundedness, etc., forming a benchmark test set;
* Second, run RAG system and collect answers, have the system being evaluated process each question in the test set, obtaining its generated answers;
* Third, perform automated scoring, call another LLM serving as "judge" to compare the system-generated answers with reference answers, giving quantitative scores from dimensions such as accuracy and completeness.

Can use a simple example to demonstrate its process:

1. Question generation (synthesize evaluation set): We have a knowledge base, for example a product manual segment: "This device supports wireless charging, battery capacity is 5000mAh." We let a large model (such as GPT-4) act as "question setter," automatically generate a test question based on this text, for example: "What is the battery capacity of this device?" and record the standard answer: "5000mAh." This constitutes one evaluation data.
2. Answering (run RAG system): Input this question into the RAG system being evaluated. The system retrieves relevant information from the knowledge base and generates an answer. Suppose it answers: "This device battery capacity is 5000mAh."
3. Grading (LLM-as-a-Judge): We ask another large model (such as Claude 3) to act as "grading teacher." Give the "question," "RAG-generated answer," and "standard answer" to it together, and instruct: "Please determine whether the generated answer is correct, only need to output 'correct' or 'incorrect'." The "grading teacher" after comparison outputs: "correct."

Through automated batch testing, we can obtain specific metrics such as RAG system accuracy. This forms a practical cycle of "evaluate → discover problems → adjust strategies → re-evaluate": first look at data to find problems, then adjust retrieval methods or optimize models, then re-test to verify effects. The system achieves continuous improvement and performance enhancement through such iterations.

You already know what evaluation means in RAG, next we will focus on the core components of RAG evaluation: common evaluation metrics (such as Recall@K in retrieval phase, Faithfulness in generation phase), mainstream evaluation frameworks (such as RAGAS, ARES) and benchmark datasets (such as WikiEval, MedRAG). Given these contents cover a wide range and complex details, here we first give an overview introduction to help you establish an overall cognitive framework.

If you need to deeply master specific details (such as mathematical calculation logic of metrics, practical deployment steps of frameworks, applicable scenarios of different benchmark datasets, etc.), suggest referring to the following two papers in RAG evaluation field:

* [https://arxiv.org/pdf/2504.14891](https://arxiv.org/pdf/2504.14891) ("Retrieval Augmented Generation Evaluation in the Era of Large Language Models: A Comprehensive Survey"): Systematically reviews internal and external evaluation methods for RAG in LLM era, covering component-level and system-level evaluation, also summarizes massive evaluation datasets and frameworks, and analyzes current research trends and challenges.
* [https://arxiv.org/pdf/2405.07437](https://arxiv.org/pdf/2405.07437) ("Evaluation of Retrieval-Augmented Generation: A Survey"): Proposes a unified RAG evaluation process (Auepora), dissects evaluation logic from three dimensions of "evaluation objectives, datasets, metrics," while comparing pros and cons of different benchmarks, providing clear guidance for practice.

### 5.3.2 Evaluation Metrics

RAG system evaluation essentially revolves around two core questions: Can the retrieval module accurately find relevant materials, and can the generation module give high-quality answers based on these materials? Therefore, the evaluation system correspondingly divides into two major modules: retrieval effect evaluation and generation quality evaluation, supplemented by LLM judges for comprehensive scoring. Let's unfold each one.

#### Retrieval Effect Evaluation: Recall Accuracy and Sorting Quality

The retrieval module is the first gateway of RAG systems, and its evaluation focus lies in three dimensions: whether it finds accurately, whether it finds comprehensively, whether it sorts well.

**Basic Recall Quality Metrics**

First is a set of classic metrics measuring basic recall quality: Recall@K, Precision@K, and F1.

* **Recall@K** measures the proportion of relevant documents recalled among the top K retrieval results. For example, if there are 5 relevant documents in the knowledge base and 3 are found in the top 10 results, then Recall@10 is 60%. This metric tells us the "coverage" of retrieval.
* **Precision** **@K** measures the proportion of truly relevant documents among the top K results. Similarly for top 10 results, if 3 are relevant and 7 irrelevant, then Precision@10 is 30%. This metric reflects retrieval "accuracy."
* **F1** is the harmonic mean of Recall and Precision, seeking balance between the two.

This set of metrics is suitable for quickly discovering basic problems in the recall phase, such as whether vectorization models are effective, whether retrieval strategies are reasonable, whether Query rewriting is in place, etc. If Recall is very low, it means relevant documents aren't being found at all; if Precision is very low, it means retrieval noise is too large.

**Sorting Quality Metrics**

Finding relevant documents is just the first step; more important is placing the most relevant documents at the front. This requires attention to sorting quality metrics: MRR, NDCG@K, and MAP.

* **MRR** **(**  **Mean Reciprocal Rank** **)** calculates the reciprocal mean of the position where the first relevant document appears. If the first relevant document appears at position 3, that query's RR is 1/3. MRR is suitable for scenarios that only need one correct answer, such as Q&A systems.
* **NDCG@K (Normalized Discounted Cumulative Gain)** considers both relevance grading and position decay factors. It not only focuses on whether documents are relevant but also the degree of relevance; meanwhile, the more relevant documents are ranked higher, the higher the score. This makes NDCG one of the most comprehensive metrics for measuring sorting quality.
* **MAP (Mean ** **Average Precision** **)** comprehensively considers positions of all relevant documents, more sensitive to overall sorting quality.

In actual engineering, we usually use the combination of Recall@K + MRR@K, ensuring both recall coverage and sorting quality. For example, if finding Recall@10 reaches 80% but MRR@10 is only 0.3, it means although relevant documents are found they're buried behind, at this point need to optimize reranking strategies, such as introducing cross-encoders or adjusting multi-path recall weight allocation.

When necessary, can also supplement Coverage metrics to monitor knowledge base coverage, discovering systematic recall blind spots. For example, if questions related to certain professional terms consistently have poor recall effects, need to consider whether to specifically optimize document segmentation or vectorization methods in that field.

#### Generation Quality Evaluation: Accuracy and Fact Faithfulness

Retrieval provides "raw materials" for generation, next to evaluate is: Based on these materials, can the generation module give high-quality answers? The core dimensions of generation quality evaluation are two: Whether the answer is accurate, and whether it's faithful to retrieved evidence.

**Exact Match and Text Similarity**

The most direct evaluation method is **EM (Exact Match)**, requiring generated answers to exactly match reference answers. This metric is suitable for scenarios with unique answers and fixed forms, such as factual Q&A like "When was it established?" "Where is headquarters located?" But EM is too strict; equally correct "January 1, 2020" and "2020-01-01" would be judged as not matching.

Therefore, more commonly used are similarity metrics based on n-gram overlap: **ROUGE** **,**  **BLEU** **, METEOR**. They score by calculating vocabulary overlap between generated content and reference answers. Among them, ROUGE-L focuses on longest common subsequence, more sensitive to answer fluency; BLEU originates from machine translation field, focusing on exact matching; METEOR adds synonym and stem considerations. The advantage of these metrics is simple calculation and easy understanding, but also has obvious limitations - they only look at surface vocabulary matching, not deep enough into semantic understanding.

To make up for this deficiency, can introduce **BertScore** or direct **vector similarity**. They use pre-trained model vector representations to calculate semantic similarity, more tolerant of expression differences. For example, "this product is very popular" and "this device is widely praised" have almost no vocabulary overlap, but vector similarity will be high. This is particularly effective for generation tasks requiring rewriting, summarization, and explanation.

**Fact Faithfulness and Hallucination Detection**

For RAG systems, merely evaluating answer similarity to reference standards is not enough; a more critical question is: Is the generated answer based on retrieved documents, are there "baseless" hallucinations?

This requires specialized Hallucination rate and Faithfulness metrics. Specific approach is to have another LLM act as "fact checker," checking generated answers sentence by sentence, judging whether each sentence can find basis in retrieved documents. For example, retrieved document says "product weight is 500 grams," but generated answer writes "this product is lightweight and portable, weighing only 300 grams," this is a typical hallucination. By counting the proportion of statements with basis, we can quantify system faithfulness.

This metric is crucial for monitoring factual errors, especially in fields with extremely high accuracy requirements such as medical, legal, and financial. In practice, many enterprises set hallucination rate thresholds as launch standards, such as requiring accuracy must reach above 95%.

#### LLM Judge: Multi-dimensional Comprehensive Scoring

The metrics introduced above each have their focus, but all have certain limitations: automated metrics often only look at surface features, difficult to grasp deep semantic meaning and overall quality. At this time, **LLM-as-a-Judge** mechanism becomes particularly important.

Specific approach is: Input the question, retrieved documents, system answer, and reference answer together into an independent large model (usually choose a powerful model such as GPT-4 or Claude), letting it score comprehensively across multiple dimensions:

* **Question relevance**: Does the answer truly respond to the user's question, is there evading the question?
* **Information completeness**: Are all points that should be covered mentioned, any missing key information?
* **Fact faithfulness**: Does the answer contain content not existing in retrieved documents, are there hallucinations?
* **Overall correctness**: Compared to reference answers, how is the quality of generated answers?

The advantage of LLM judges is being able to make more human-like holistic judgments - it can understand context, grasp semantics, identify logic, even discover subtle issues that automated metrics can't capture, such as inappropriate tone, logical contradictions, vague expressions, etc. Of course, judges themselves also need carefully designed prompts and calibration with human-labeled samples to ensure consistency and reliability of scoring standards.

#### Building Practical Evaluation Combinations

Facing so many evaluation metrics, enterprises often feel confused when landing: Which metrics to choose? How to combine them?

A pragmatic suggestion is **start with a streamlined combination, gradually improve**:

* **Retrieval evaluation**: Use the core combination of Recall@K + MRR@K to quickly grasp recall coverage and sorting quality
* **Generation evaluation**: According to task characteristics, choose one or two from EM, ROUGE-L, BertScore as baseline
* **Comprehensive evaluation**: Introduce LLM judge, focusing on three dimensions of relevance, completeness, and faithfulness

On this basis, adopt the cycle iteration of "evaluation → discover problems → adjust strategies → re-evaluate." For example, finding good recall rate but very low MRR, focus on optimizing reranking; finding high hallucination rate, strengthen faithfulness constraints to retrieved documents; finding poor answer quality for certain question types, specifically supplement detailed indicators.

This progressive building approach allows teams to quickly start, establish basic cognition of system effects, and gradually improve the evaluation system as understanding deepens, ultimately forming an evaluation solution suitable for their business scenario.

### 5.3.3 Evaluation Frameworks

With the rapid development of RAG technology, a large number of excellent evaluation frameworks have emerged in academia and industry. They not only encapsulate common evaluation metrics but also provide standardized datasets, benchmarks, and end-to-end evaluation processes. This section will systematically review current mainstream RAG evaluation frameworks, helping you quickly select evaluation tools suitable for your scenario.

#### **Evaluation Framework Classification System**

According to evaluation objectives and usage scenarios, we can divide RAG evaluation frameworks into three major categories: research frameworks, benchmark frameworks, and tool frameworks.

**Research frameworks** mainly serve academic research and frontier exploration, characterized by detailed evaluation dimensions and strong method innovation. Representative examples include FiD-Light and Diversity Reranker, which focus on fine-grained evaluation of the retrieval phase, the former focuses on recall latency, the latter emphasizes result diversity. Such frameworks usually dive deep into specific links of RAG systems, providing refined diagnostic capabilities.

**Benchmark** **frameworks** provide standardized test sets and evaluation processes for horizontal comparison of different RAG system performance. This type has the largest quantity and widest influence. For example:

* **RAGAS** (2023.09) is one of the earliest comprehensive RAG evaluation frameworks, adopting LLM-as-a-Judge mode, simultaneously evaluating retrieval and generation links
* **ARES** (2023.11) introduces classifier-assisted evaluation methods, combining LLM judgment and traditional classifiers to evaluate Context relevance and Answer relevance
* **RGB** (2023.12) focuses on generation phase evaluation, proposing detailed dimensions such as Info Integration, NoiseRobust, NegRejection, Counterfact
* **MultiHop-RAG** (2024.01) targets multi-hop reasoning scenarios, focusing on evaluating retrieval relevance (Retrieval C) and answer correctness (Response C), using metrics such as MAP, MRR, Hit@K
* **CRUD-RAG** (2024.02) simulates real knowledge management scenarios, evaluating system performance under four operations of Create, Read, Update, Delete, introducing RAGQuerEval scoring system

Entering 2024, evaluation frameworks show obvious professionalization and segmentation trends. Medical field has MedRAG, legal field has LegalBench-RAG, financial field has related domain-specific frameworks. These domain frameworks not only provide professional datasets but also design customized evaluation metrics according to industry characteristics, for example medical scenarios especially focus on accuracy, legal scenarios emphasize document-level precision and citation relevance.

**Tool frameworks** focus on engineering practice, providing easy-to-use evaluation tools and integration solutions. TruEra RAG Triad, LangChain Benchmarks, RECALL, etc. all belong to this category. They are usually deeply integrated with mainstream RAG development frameworks, supporting rapid access to existing systems, some also providing visualized evaluation reports and monitoring panels.

Above we introduced various different RAG evaluation frameworks, but how to choose in actual combat? Might first select several with more GitHub stars for preliminary testing; when enterprises face rich framework choices and need landing decisions, can start from the following aspects.

* Quick start needs: If need to quickly build baseline evaluation, can choose comprehensive frameworks like RAGAS, RAGEval, they provide complete out-of-the-box processes; if need to deeply diagnose problems in a certain link, need to use targeted frameworks: for example when retrieval effect is poor can use MultiHop-RAG, when hallucination problem is prominent can use CoURAGE or RAG Unfairness.
* Combine industry for selection: If applied to professional fields such as medical, legal, financial, should prioritize choosing frameworks adapted to that field. Such frameworks often have built-in key capabilities such as professional terminology processing and compliance checking. General frameworks though fully functional, easily show "acclimatization issues" in professional scenarios.
* Choose according to integration cost: Frameworks like LangChain Benchmarks, TruEra RAG Triad are deeply integrated with mainstream development frameworks, can quickly access existing systems; while some academic frameworks though technically advanced, need additional engineering adaptation work; finally need to pay attention to maintenance status, should prioritize choosing frameworks with active communities, complete documentation, and continuous updates, avoiding discontinued projects, can specifically refer to GitHub stars, update frequency, Issue response speed, etc.

Besides, a batch of tools are also commonly recognized and recommended in the community, some frameworks already mentioned above: Ragas provides rich metrics and doesn't bind to specific frameworks; Continuous Eval characterized by lightweight and low cost, supports building evaluation pipelines with mathematical guarantees; TruLens‑Eval integrates well with mainstream frameworks like LangChain and Llama‑Index, providing visualized analysis; Llama‑Index's own ecosystem also integrates evaluation and synthetic data generation functions, facilitating closed-loop testing of applications built with it. Tools like Phoenix, DeepEval, LangSmith, and OpenAI Evals are also continuously iterating, you can further choose based on comprehensive consideration of your own needs and corresponding tools' reputation.

### 5.3.4 Evaluation Benchmarks

The importance of evaluation benchmarks in practice is often underestimated. Many teams when building RAG systems, often rush to start evaluation based only on a small amount of human-written test questions, leading to significant gaps between actual online effects and test phase performance. The root cause of this problem is the lack of representative and systematic evaluation data, difficult to truly reflect complex and changing business scenarios.

An evaluation benchmark that can effectively support system iteration usually has three core characteristics. First is representativeness, test data need to comprehensively cover various scenarios in real business, including high-frequency common questions, complex boundary cases, and abnormal inputs, etc.; second is standardization, format, difficulty coefficient, and scoring standards of questions and answers need unified norms, ensuring evaluation results have comparability and repeatability; third is evolvability, benchmarks should be able to continuously update with system capability improvement and business demand changes, avoiding evaluation distortion caused by fixed "test-taking" data.

For most enterprises, due to business scenario uniqueness, ultimately often need to build their own evaluation datasets.

* The construction process can start by extracting real user questions from business logs, and performing stratified sampling according to type, frequency, and difficulty to ensure data representativeness. For simple questions, domain experts can directly label; for complex questions, can first use high-quality LLM to generate candidate answers, then have experts review and modify. This "machine generation + human calibration" approach can significantly reduce labeling costs.
* Besides answers themselves, label metadata such as relevant documents, answer types, difficulty levels, etc., providing support for subsequent fine analysis. Establish labeling norms, perform multi-person cross-validation, calculate labeling consistency (such as Kappa coefficient), ensure data quality.
* Regularly supplement new test cases from online feedback, especially questions the system answers poorly, letting evaluation data evolve synchronously with system capability. This continuous iteration mechanism keeps evaluation benchmarks always sensitive and effective to business scenarios.

Of course, if team resources are limited or hope to quickly establish baseline, referring to industry mature public evaluation benchmarks is also a feasible starting point. As of 2025, numerous benchmarks covering general domains and vertical industries are available for selection (see chart).

![](images/image7.png)

When choosing, should first clarify evaluation purpose: is it establishing capability baseline or making final verification for launch? Second, need to evaluate whether benchmark data covers concerned scenarios, question types, and difficulties. For time-sensitive scenarios such as news and finance, must examine whether benchmarks include real-time data testing; for historical knowledge processing, static benchmarks may be sufficient. Finally, also need to weigh labeling costs, whether to directly use fully labeled benchmarks or use original data for self-labeling.

Combining self-built data with public benchmarks both ensures evaluation is close to business actuality and enables horizontal comparison using public standards, being a pragmatic path to building robust evaluation systems.

6. # Deep Research: Learning from Competitions and Open Source Tutorials (Optional)

The RAG system principles and basic implementation introduced above, although helping you quickly build a usable prototype, are still quite far from truly solving complex problems in production environments. If you want to deeply understand more landing and combat-valuable RAG techniques, referring to major competitions' winning solutions and high-quality open-source tutorials is the most efficient learning path. These solutions often concentrate best practices from excellent teams' repeated attempts in real scenarios.

But it needs emphasis that the cases listed in this section are not exhaustive, but select several representative solutions. When you encounter specific problems in practice, suggest adopting this learning strategy: first search related competitions according to problem type (keywords such as "PDF parsing," "multimodal retrieval," "low latency optimization," etc.), then deeply study winning teams' technical reports or open-source code, often able to find directly usable solution ideas.

## 6.1 Semantic Cache: Optimizing High-frequency Query Scenarios

Hugging Face provides a semantic cache implementation solution based on Chroma vector database, this tutorial's address is:

[https://huggingface.co/learn/cookbook/semantic_cache_chroma_vector_database](https://huggingface.co/learn/cookbook/semantic_cache_chroma_vector_database)

![](images/image8.png)

Background: Most tutorial-built RAG systems are only suitable for single-user testing. When systems are deployed to production environments, facing dozens to thousands of repeated queries (such as users repeatedly asking "how to refund" in customer service scenarios), each time executing vector database retrieval and LLM calls will significantly increase response time and costs will also rise quickly. By introducing a semantic cache layer, can greatly reduce access pressure on original data sources while ensuring answer quality.

This solution adopts a dual-layer retrieval architecture. The base layer uses Chroma vector database to store original knowledge base (using MedQuad medical Q&A dataset as example), adding unique IDs to each data for precise citation. The cache layer is built based on FAISS, choosing FlatL2 index to handle small datasets and high-dimensional vectors. Semantic cache is placed between user queries and Chroma, not caching LLM's final answers - this design is important, because directly caching answers will cause users' personalized requirements (such as "explain in simple language") to fail.

The cache system uses SentenceTransformer's all-mpnet-base-v2 model to generate query vectors, judging query similarity through Euclidean distance (setting threshold to 0.35). When cache is full (max_response parameter controls capacity), uses FIFO strategy to delete earliest entries. To support cross-session use, cache data is saved to JSON file.

In small-scale testing, first query "How do vaccines work?" takes 0.057 seconds to get results from Chroma, while similar query "Briefly explain me what is a Sydenham chorea." takes only 0.016 seconds from cache, retrieval time halved. In large-scale production environments, this solution can achieve 90%-95% performance optimization, effectively reducing vector database access pressure and API call costs.

## 6.2 Unstructured Data Processing: Unified Multi-format Document Parsing

Another Hugging Face tutorial shows how to use the Unstructured library to build complete unstructured data processing flow, tutorial address is:

[https://huggingface.co/learn/cookbook/rag_with_unstructured_data](https://huggingface.co/learn/cookbook/rag_with_unstructured_data)

![](images/image9.png)

Background: Knowledge in enterprise scenarios is often scattered in PDF, PowerPoint, EPUB, HTML, and other formats. Traditional data preprocessing methods either can only handle single format (for example only supporting PDF), or lose key information during format conversion (especially structured content like tables, title hierarchies, etc.), causing RAG systems to unable to accurately understand and retrieve this information.

This solution first downloads multi-format test documents as examples, including real documents such as Canadian Environment Department pesticide manual PDF (containing large amounts of table data), University of Florida citrus IPM PowerPoint (containing charts and multi-level titles), etc. Then uses Unstructured library's Local Runner to complete parsing. Configuration is divided into three parts: ProcessorConfig specifies output directory and number of parallel processes (2 processes), PartitionConfig can choose API partition mode (requires Unstructured key, better OCR effect, especially suitable for scanned PDFs), SimpleLocalConfig defines document input paths. Parsed documents are converted to JSON format, containing element types such as body text, titles, tables, etc.

The system uses chunk_by_title method for chunking, setting maximum characters to 512, and merging consecutive segments under 200 characters to maintain semantic integrity. When converting to LangChain Document format, filters complex metadata fields to adapt to Chroma vector database. The vectorization phase adopts BAAI/bge-base-en-v1.5 embedding model, combining 4-bit quantized Llama-3-8B-Instruct model and LangChain's RetrievalQA chain to build complete RAG system.

The system can accurately process multi-format documents. When testing questions like "Are aphids a pest?", can extract key information such as aphid hazards, attracting ants, etc. from parsed documents, generating answers meeting requirements. This solution successfully achieves complete conversion from unstructured data to RAG-usable data, particularly suitable for enterprise knowledge base scenarios needing to process multiple document formats.

## 6.3 Enterprise-level Document Q&A: High-precision Traceable RAG Implementation

Enterprise RAG Challenge champion solution shows how to build production-grade RAG systems under strict time and precision requirements, related technical article address is:

[https://abdullin.com/ilya/how-to-build-best-rag/](https://abdullin.com/ilya/how-to-build-best-rag/)

[https://hustyichi.github.io/2025/07/03/rag-complete/](https://hustyichi.github.io/2025/07/03/rag-complete/)

Background: Participants need to complete parsing of 100 real enterprise annual report PDFs within 2.5 hours, these reports are up to 1000 pages each, containing complex financial tables, multi-column layouts, charts, etc. After parsing completion, the system needs to answer 100 precise business questions. These questions require clear answer types (such as Yes/No judgment, company names, specific numerical indicators, executive position titles, etc.), and must give page number citations of answer sources for business personnel verification. The entire process simulates the actual work scenarios of investment analysts or financial auditors.

The champion team chose IBM open-source Docling as PDF parsing tool, because it performs best in processing complex tables (such as cross-page tables, nested tables) and multi-column text. The team improved Docling code to make it generate JSON and Markdown+HTML formats containing metadata, specifically fixing table structure parsing issues (such as cell merging, header recognition, etc.). To accelerate processing, the team rented RTX 4090 GPU, completing parsing of 100 reports in 40 minutes.

Text chunking adopts 300 token length, overlapping 50 tokens, using recursive splitting strategy to maintain semantic integrity. To avoid cross-company information confusion (such as when querying Company A's CEO retrieving Company B's information), built separate FAISS vector libraries for each company, using IndexFlatIP index (no compression to ensure precision). The retrieval phase adopts a three-step strategy: first find Top30 text blocks through vector retrieval, then extract parent pages where these blocks are located and deduplicate (because multiple blocks may come from same page), finally use GPT-4o-mini to re-rank pages. Vector retrieval scores and LLM reranking scores are mixed by 0.3:0.7 weight.

The generation phase uses different prompt templates according to answer type (number/boolean/string, etc.). For numerical questions (such as "what is 2023 revenue"), designed a 5-step analysis process to ensure indicator matching accuracy: identify indicator type in question, locate relevant tables in documents, extract values, verify unit consistency, cross-validate. System output adopts structured format, containing analysis process, relevant page numbers, etc., ensuring answers are traceable. For questions involving multi-company comparison (such as "which company has highest revenue"), splits into single-company sub-queries then merges results.

This solution won double awards and first place on leaderboard in the competition. Notably, even using small models (such as Llama 8B) can exceed over 80% of participants, using Llama 3.3 70B is only slightly worse than GPT-4o-mini, successfully achieving balance of accuracy, efficiency, and cost.

## 6.4 AIOps Scenario: Intelligent Processing of Image-Text Mixed Data

AIOps RAG competition's EasyRAG project focuses on Q&A tasks in operations scenarios, technical article address is:

[http://blog.csdn.net/hustyichi/article/details/143323746](http://blog.csdn.net/hustyichi/article/details/143323746)

![](images/image10.png)

Background: Operations engineers in daily work need to consult large amounts of technical documents. These documents not only contain text explanations but also image information such as monitoring charts, system architecture diagrams, performance curves, etc. For example, when system performance problems occur, engineers need to quickly query "how to handle when CPU usage exceeds 80%," answers may be scattered in text explanations and monitoring charts. Traditional RAG systems can only process text, unable to understand trends and values in charts, leading to incomplete answers. This project ultimately won first place in preliminaries and second place in finals.

The indexing phase uses improved SentenceSplitter (fixed original version's block size calculation problem), chunking by 1024 tokens, overlapping 200 tokens. Key innovation lies in adding metadata information such as knowledge base path and file path for each text block. This improvement increased recall rate by 2%. For image data, first use PaddleOCR to extract text in images (such as chart titles, axis labels), then call GLM-4V-9B multimodal model to generate natural language descriptions of images (such as "this line chart shows CPU usage reaches peak 90% at 3 PM"), storing text and descriptions together in database, achieving unified retrieval of image-text information.

The retrieval phase uses a "dual-path BM25 + vector retrieval" strategy for extensive recall. BM25 includes document block retrieval (recalls 192 items) and path retrieval (filters irrelevant documents through file paths, such as only retrieving operation manuals not development documents), using Harbin Institute of Technology stop word list for denoising. Vector retrieval uses gte-Qwen2-7B-instruct model, recalling 288 candidate results. The reranking phase uses bge-reranker-v2-minicpm-layerwise model, through testing finding 28-layer configuration has best effect.

Answer generation adopts a two-step strategy - first generate preliminary results based on Top6 documents (covering multiple relevant knowledge points), then combine Top1 most relevant document for secondary optimization (highlighting most core answers). This design ensures answers have both sufficient information coverage and highlight most core content.

To cope with long text scenarios (such as a complete operation manual may be hundreds of pages), the system implements BM25-based context compression method. This method splits documents into sentence level, calculates each sentence's similarity to query, then concatenates high-relevance sentences proportionally. Experiments show that at 50% compression rate, this method takes only 7.7 seconds, accuracy reaches 86.48%, superior to existing compression tools like LLMLingua.

Compared to basic solution, after adding metadata information and answer secondary optimization, system accuracy improved by 2% respectively. BM25 compression method maintains high accuracy while ensuring efficiency, well adapting to AIOps scenario's image-text data processing and real-time response needs.

## 6.5 Multi-source Data Fusion: Synergy of Structured and Unstructured Knowledge

KDD Cup 2024 Meta RAG challenge champion solution shows how to integrate unstructured web data and structured knowledge graphs, technical article address is:

[https://blog.csdn.net/m0_59164520/article/details/143694213](https://blog.csdn.net/m0_59164520/article/details/143694213)

https://arxiv.org/pdf/2410.00005

![](images/image11.png)

Background: Task 1 requires retrieval summary based on 5 web pages, for example when user searches "who directed Interstellar," the system needs to extract answers from given web pages. Task 2 adds Mock API (simulating access to structured knowledge graphs) on top of task 1, the system can call APIs to query structured information such as movie databases and character relationships. Task 3 further increases difficulty, handling complex queries based on 50 web pages and Mock APIs, for example "which Nolan-directed films have box office over 500 million dollars," this requires simultaneously querying knowledge graphs (director-work relationships) and web pages (box office data). Each query needs to complete within 30 seconds, core objective is improving multi-source data integration accuracy and reducing hallucinations.

Peking University db3 team designed refined web data processing flow for task 1. Uses BeautifulSoup to extract web page text, ParentDocumentRetriever manages parent-child chunk relationships (child chunks 200 tokens for retrieval, parent chunks 500-2000 tokens for generation), ensuring retrieval accuracy and generation completeness. Embedding model chooses bge-base-en-v1.5, vector library uses Chroma, reranking adopts bge-reranker-v2-m3. The team also supplements public data in fields such as movies and finance (such as IMDB movie data, listed company reports), converting to standard format before storing in database. At model level uses LoRA to fine-tune Llama-3-8B-instruct, training data includes invalid question labels (such as "how's the weather today" type questions beyond knowledge base scope), correct answers, etc.

Tasks 2-3's key innovation lies in prioritizing knowledge graphs. The team designed standardized API calling mechanisms, including interfaces such as get_person (query character information), get_movie (query movie information), etc., supporting conditional filtering (such as cmp operator filtering movies with box office > 500 million) and sorting (by box office descending). API call generation uses GPT-4 for preliminary labeling then manual optimization for fine-tuning. During system execution, first calls knowledge graph APIs, only falls back to web retrieval when knowledge graph results are invalid (such as queried movie not in database), this design greatly improves query efficiency and answer accuracy.

Through knowledge graph priority strategy and structured output format, the system significantly reduces LLM hallucination phenomena. When knowledge graphs can provide definitive answers (such as "Nolan's birth year"), directly outputs without going through generation step; when needing to retrieve from web (such as "Nolan's latest interview content"), ensures answers are verifiable through strict document citation and step-by-step reasoning.

This solution won first place in all three tasks, scores respectively reaching 28.4%, 42.7%, and 47.8%, successfully balancing multi-source data integration accuracy and real-time performance. The core inspiration of this case lies in that for enterprise scenarios containing both structured and unstructured data, should design different retrieval strategies according to data characteristics, prioritize using deterministic structured data, use unstructured data as supplement.

Deeply analyzing these practical cases, we can summarize several common principles for building high-quality RAG systems: in architectural design, should choose appropriate cache, retrieval, and generation strategies according to business scenarios; in data processing, need to design specialized parsing and indexing schemes for different formats and modalities; in retrieval optimization, hybrid retrieval plus reranking has become standard configuration; in answer generation, typed prompts and structured output can significantly improve accuracy and traceability.

These experiences from real competitions and open-source projects provide valuable references for building better enterprise-level RAG systems. You can search for corresponding competitions based on actual problems, finding mature existing solutions to try.

7. # Breadth Exploration: Future Evolution of RAG (Optional)

After deeply mastering RAG's practical techniques and optimization methods, you can already effectively improve system performance in specific scenarios. However, to fully grasp RAG technology, only deep diving into parts is not enough, we also need to broaden horizons, understanding its evolution direction and expansion space from broader dimensions.

Currently, RAG technology is rapidly breaking through the traditional retrieval-generation paradigm based on document chunking, developing in more diverse directions. This section will focus on discussing the following evolution paths: from simple chunking retrieval to graph data structure retrieval; fusing multimodal information such as images and audio to enhance RAG retrieval capabilities; using vectorization technology to optimize long document chunking strategies; and how RAG gradually evolves into Agent systems.

## 7.1 Graph RAG: Reshaping Deep Retrieval with Relational Networks

Related research: [https://arxiv.org/pdf/2410.05779](https://arxiv.org/pdf/2410.05779), [https://arxiv.org/pdf/2502.11371](https://arxiv.org/pdf/2502.11371), https://arxiv.org/pdf/2404.16130

![](images/image12.png)

Traditional RAG works by finding text passages similar to the question, like picking out the most relevant passages from a pile of materials. For directly finding specific information, this method is very effective. But if a question needs to link multiple documents and combine different clues to answer, its performance will suffer.

For example, a doctor might want to ask: "Based on these cases and the latest treatment guidelines, how to evaluate the benefits and risks of a certain drug for elderly patients?" Or a project team might care: "Considering past two years of requirement documents, review records, and online problem reports, which part of our system architecture most often has problems?" The key to such questions is not finding a certain sentence, but finding the people, things, objects mentioned in various scattered materials and the connections between them, sorting out clues, forming a complete panoramic view.

Graph RAG's approach is to proactively draw this panoramic view first. The system uses large models to identify key elements from text (such as characters, institutions, functional modules, events, data, etc.) and their relationships (such as who caused what, what depends on what, how to change, what conflicts, etc.), thereby building a knowledge network that continuously enriches as materials increase. Then, through automatic grouping, elements and relationships with close connections are classified into different themes, and for each theme, a summary description is generated in advance. This way, when users ask questions, the system no longer merely finds semantically most similar passages, but first finds elements and local structures most relevant to the question in the knowledge network, then extends along connection lines to relevant theme groups, finally giving these analysis paths, node explanations, and corresponding original text segments together to the large model for reasoning and organizing answers.

Under this framework, Graph RAG and traditional RAG form good division and collaboration: traditional RAG is still good at answering direct, one-step detail questions; while Graph RAG is more like human thinking when doing research or writing reports - first sort out overall structure and themes (build networks and grouping), then fill in specific evidence (cite original text), finally give logical, conditional conclusions. Existing system comparisons also show that in tasks requiring linking multiple information points for reasoning, Graph RAG can usually cover more key content, provide more comprehensive perspectives; and according to specific question characteristics, flexibly combining both methods, overall effect is often better than using only one.

## 7.2 Multimodal RAG

Related research: https://arxiv.org/pdf/2502.08826

![](images/image13.png)

Real-world data is never single-format text. When engineers troubleshoot server failures, they need to simultaneously look at temperature monitoring curves, device panel screenshots, and system logs; when doctors make diagnoses, they need to view CT/MRI images, examination reports, and electronic records together. Traditional text RAG can at most retrieve text descriptions such as "temperature abnormal," "suspected pulmonary nodules," but difficult to correspond these descriptions to specific curve trends and image lesion forms, let alone using "images/audio/video" to reversely retrieve relevant documents and knowledge.

Multimodal RAG solves this problem of "modalities not seeing each other." Its core lies in cross-modal semantic alignment: configuring appropriate encoders for images, video, audio, text respectively (such as ViT/CLIP encoding images and video frames, Whisper encoding audio, BGE-M3, etc. encoding text), combining tools such as OCR, ASR, layout analysis, extracting key information from visuals and audio, then mapping representations of different modalities into a shared semantic space through models, building unified multimodal index.

In retrieval and generation phases, whether users ask "find a chart showing 2023 Q3 sales peak" or upload a product sketch or operation video to initiate query, the system first finds a batch of most similar multimodal content in this unified space, then filters out obviously irrelevant results based on signals such as text similarity and image similarity, keeping the few most useful pieces of evidence. Finally, gives these filtered images, text, tables, etc. together to multimodal large models, which synthesize information from different modalities to give answers, and try to mark information sources or highlight relevant positions in screenshots and documents. This way, compared to text-only RAG, the system can both utilize more modality clues and more easily reduce hallucinations, making answers more complete and easier to verify.

## 7.3 Late Chunking: Preserving Complete Context for Long Documents

Related introduction: https://jina.ai/news/late-chunking-in-long-context-embedding-models/

![](images/image14.png)

Imagine you are reading a Wikipedia article about Berlin. Traditional RAG systems first cut it into independent paragraphs then generate vectors. When the first sentence mentions "Berlin is Germany's capital," subsequent paragraphs' pronouns like "the city," "its population" lose connection to "Berlin." At this point, if querying "what is Berlin's population," the system fails retrieval because "Berlin" and "population data" never appear in the same text block. This problem is more serious in long document scenarios: a 200-page insurance contract might have "deductible" definition on page 5, specific applicable conditions on page 30, traditional fixed-length chunking (such as 512 tokens per block) would scatter this relevant information across 40+ independent text blocks. Experimental data shows this fragmentation causes semantic similarity to plummet from 0.85 to 0.71.

Late Chunking subverts the traditional "chunk first then encode" process, changing to "encode first then chunk": using long-context embedding models supporting 8192 tokens (about 10 pages of text) such as Jina Embeddings v2, first input the entire document into Transformer layers, generating vector representations for each token - at this point each token's embedding has already "seen" full text information, capturing cross-paragraph referential relationships and concept associations. Then, perform chunk-wise mean pooling on these token vectors with global awareness, generating final chunk embeddings. The text blocks generated this way are no longer isolated islands of independent identical distribution, but "conditionally dependent" context chains: when processing the sentence "the city has 3.85 million residents," the vector already contains semantic information of "Berlin" from earlier text, improving similarity from 0.71 to 0.83. The key difference lies in the timing of boundary marker usage: traditional methods apply boundary markers such as periods and paragraph breaks in the preprocessing phase, while Late Chunking only applies boundary clues for intelligent chunking after obtaining global token embeddings.

On the 5 datasets of BEIR benchmark testing, Late Chunking comprehensively surpasses traditional chunking methods. The most significant case is NFCorpus dataset (average document length 1590 characters), retrieval accuracy surges from 23.46% to 29.98%, relative increase of 27.8%; while in short text scenarios (such as Quora's 62-character questions) both perform the same, verifying a key pattern: document length is positively correlated with Late Chunking's advantage. From the technical comparison table, we can see core differences: traditional chunking directly applies boundary markers in preprocessing phase, producing independent identically distributed chunk embeddings, losing context information; Late Chunking applies boundary markers only after obtaining token embeddings, producing conditionally dependent chunk embeddings, with long-context models preserving complete context information.

This method has now been integrated into Jina Embeddings v3 API. Although needing to encode the entire long document first, increasing inference time by 10-20%, in scenarios such as medical records (diagnostic basis across chapters), legal documents (cross-references between definitions and clauses), technical manuals (concept explanations scattered across multiple chapters), the significant improvement in retrieval accuracy far exceeds this performance overhead. Late Chunking not only proves the practical value of 8K+ long-context models - not "over-engineering," but a necessary condition for achieving high-quality chunk embeddings, but also provides RAG systems with an optimization path having theoretical guarantees, breaking away from "hit-or-miss" heuristic techniques like sliding windows and multiple scans, representing a paradigm shift from "chunk first then encode" to "encode first then chunk."

## 7.4 From RAG to RAG in the Agent Era

Related discussions: [https://ragflow.io/blog/rag-at-the-crossroads-mid-2025-reflections-on-ai-evolution](https://ragflow.io/blog/rag-at-the-crossroads-mid-2025-reflections-on-ai-evolution), [https://arxiv.org/pdf/2501.09136](https://arxiv.org/pdf/2501.09136), [https://www.letta.com/blog/rag-vs-agent-memory](https://www.letta.com/blog/rag-vs-agent-memory), [https://www.linkedin.com/posts/richmondalake_100daysofagentmemory-rag-memorizz-activity-7348281860843577346-LM7Y/](https://www.linkedin.com/posts/richmondalake_100daysofagentmemory-rag-memorizz-activity-7348281860843577346-LM7Y/), https://www.llamaindex.ai/blog/rag-is-dead-long-live-agentic-retrieval

RAG technology has evolved from the initial retrieval-augmented generation tool to becoming a key part of building Agent cognitive architecture. Traditional RAG systems are based on the simple mode of question, retrieve, answer, essentially passively accepting queries, without active action capability. To break through this passivity and handle more complex cognitive tasks, RAG has deeply integrated with Agent capabilities, giving birth to the new paradigm of Agentic RAG. In this paradigm, RAG's role has fundamentally changed: it is no longer merely a passive provider of external knowledge, but under the drive of Agents' active planning, goal guidance, and reflection capabilities, becomes a core processing unit supporting intelligent behavior. This fusion gives the overall system goal-oriented, iterative optimization, and autonomous decision-making capabilities, significantly improving the depth and quality of human-computer interaction. Specifically, Agentic RAG can understand complex tasks, autonomously decompose problems, plan retrieval strategies, and after obtaining preliminary information, evaluate result quality, decide whether to explore deeper, thereby competent for multi-step complex tasks that traditional RAG struggles with.

![](images/image15.png)

Agentic RAG's key to achieving such complex task processing lies in establishing a multi-level active cyclic working mechanism. Facing complex queries, the Agent first analyzes the question's essence, decomposes it into sub-questions, and designs precise retrieval strategies for each sub-question. After obtaining preliminary results, the Agent performs evaluation and reflection, judging information completeness and relevance, identifying knowledge gaps, and dynamically generating more precise new queries. This iterative process often contains multi-hop retrieval, that is, discovering new retrieval directions based on previous round results, forming a knowledge exploration chain similar to human researchers. However, to support this continuous, iterative intelligent behavior, especially achieving personalization and knowledge accumulation in long-term interactions, relying solely on single-session short-term context (short-term memory) is far from enough. This leads to the demand for long-term, structured memory capabilities.

It is precisely to meet this demand that RAG is endowed with the role of Agent's long-term memory system, building a complete external memory architecture. This system complements the short-term memory responsible for maintaining current session context. The core operation of this long-term memory system relies on three key mechanisms:
 First, structured indexing capability: enabling Agents to establish multi-dimensional index systems for massive unstructured data (such as by time, topic, or entity relationships), supporting multi-angle efficient retrieval, simulating the way human brains recall information through different clues.
 Second, intelligent forgetting mechanism: through value evaluation algorithms, the system performs weight decay or selective removal on information with low usage frequency, weak relevance, or outdated content, maintaining the memory system's refinement and efficiency, preventing information overload.
 Third, knowledge consolidation process: the system refines fragmented conversations and interaction experiences into structured knowledge, using techniques such as entity recognition, relation extraction, and semantic clustering to integrate and connect fragment information into knowledge graphs, completing the transformation and sedimentation from short-term experience to long-term knowledge.

This external memory system built by RAG not only greatly expands Agents' cognitive boundaries, more importantly gives them continuous learning and knowledge evolution capabilities. It enables Agents to accumulate experience in long-term interactions, forming personalized processing patterns and domain professional knowledge systems, thereby providing a solid foundation for executing more complex and longer-lasting tasks.

# Summary

Retrieval-augmented generation is not only a technical solution to compensate for large model hallucinations and knowledge lag, but also a key bridge for converting general AI capabilities into deep enterprise business value. From basic Naive RAG evolving to modular, Agent-collaborative Advanced RAG, this process reflects that RAG needs continuous deepening in every link - whether more refined data processing, more scientific model selection (Embedding, Rerank, LLM), or more systematic effect evaluation, are all necessary paths for building controllable, trustworthy, efficient enterprise-level knowledge systems. Meanwhile, drawing experience and techniques from various competitions and practice cases can also further deepen understanding of technical details.

With the fusion and development of frontier directions such as graph structure retrieval (Graph RAG), multimodal understanding, and Late Chunking, RAG is continuously breaking through traditional retrieval-generation boundaries, gradually possessing deeper semantic associations and sustainable memory capabilities. Hope that through studying this overview article, you can master the full-chain methodology from principle to practice, from evaluation to evolution, thereby in the rapidly iterating technology wave, creating truly landing, high-quality intelligent applications capable of coping with complex business challenges.

# Reference

[1] Ask in Any Modality: A Comprehensive Survey on Multimodal Retrieval-Augmented Generation.

https://arxiv.org/pdf/2502.08826

[2] Retrieving Multimodal Information for Augmented Generation: A Survey.

https://arxiv.org/pdf/2303.10868

[3] A Survey on RAG Meeting LLMs: Towards Retrieval-Augmented Large Language Models.

https://arxiv.org/pdf/2405.06211

[4] Retrieval-Augmented Generation for Large Language Models: A Survey.

https://arxiv.org/pdf/2312.10997

[5] LightRAG: Simple and Fast Retrieval-Augmented Generation.

https://arxiv.org/pdf/2410.05779

[6] Agentic Retrieval-Augmented Generation: A Survey on Agentic RAG.

https://arxiv.org/pdf/2501.09136

[7] ERAGent: Enhancing Retrieval-Augmented Language Models with Improved Accuracy, Efficiency, and Personalization.

https://arxiv.org/pdf/2405.06683

[8] Graph Retrieval-Augmented Generation: A Survey.

https://www.arxiv.org/pdf/2408.08921

[9] Evaluation of Retrieval-Augmented Generation: A Survey.

https://arxiv.org/pdf/2405.07437

[10] Retrieval Augmented Generation Evaluation in the Era of Large Language Models: A Comprehensive Survey.

https://arxiv.org/pdf/2504.14891

[11] From Local to Global: A Graph RAG Approach to Query-Focused Summarization.

https://arxiv.org/pdf/2404.16130

[12] RAG vs. GraphRAG: A Systematic Evaluation and Key Insights.

https://arxiv.org/pdf/2502.11371

[13] Introduction to RAG | LlamaIndex Python Documentation.

https://developers.llamaindex.ai/python/framework/understanding/rag/

[14] All-in-RAG | LLM Application Development in Practice: RAG Technology Full Stack Guide.

https://datawhalechina.github.io/all-in-rag/#/en/

[15] Ilya Rice: How I Won the Enterprise RAG Challenge.

https://abdullin.com/ilya/how-to-build-best-rag/

[16] RAG Research Table – Awesome Generative AI Guide (GitHub).

https://github.com/aishwaryanr/awesome-generative-ai-guide/blob/main/research_updates/rag_research_table.md

[17] RAG is dead, long live agentic retrieval.

https://www.llamaindex.ai/blog/rag-is-dead-long-live-agentic-retrieval

[18] LLM/RAG Zoomcamp Extra Supplement 5: RAG Evolution Common Evaluation Methods and Market Preferences.

https://vip.studycamp.tw/t/llmrag-zoomcamp-%E8%AA%B2%E5%A4%96%E8%A3%9C%E5%85%A85%EF%BC%9Arag-evolution-%E5%B8%B8%E8%A6%8B%E8%A9%95%E4%BC%A6%E6%96%B9%E6%B3%95%E5%92%8C%E5%B8%82%E5%A0%B4%E5%81%8F%E5%A5%BD/8185

[19] How to Evaluate Retrieval Augmented Generation (RAG) Applications.

https://zilliz.com.cn/blog/how-to-evaluate-rag-zilliz

[20] RAG is not Agent Memory.

https://www.letta.com/blog/rag-vs-agent-memory

[21] Richmond Alake. LinkedIn post on #100DaysOfAgentMemory, RAG and MemoRizz.

https://www.linkedin.com/posts/richmondalake_100daysofagentmemory-rag-memorizz-activity-7348281860843577346-LM7Y/
