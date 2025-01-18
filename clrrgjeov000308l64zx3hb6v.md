---
title: "How to develop superior AI application with RAG?"
seoTitle: "How to develop superior AI application with RAG?"
seoDescription: "Understanding the concepts of Retrieval-Augmented Generation for building AI applications."
datePublished: Wed Jan 24 2024 07:22:15 GMT+0000 (Coordinated Universal Time)
cuid: clrrgjeov000308l64zx3hb6v
slug: how-to-develop-superior-ai-application-with-rag
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706080760055/88d05934-19c2-4205-8f36-f54b01517666.png
tags: ai, artificial-intelligence, javascript, python, data-science, machine-learning, chatgpt

---

### Story so far

Last year, the tech industry was abuzz with the exciting developments in artificial intelligence! If the title of this blog piqued your interest, it's likely that you've been captivated by the AI revolution and have already experimented with remarkable tools like ChatGPT!

ChatGPT is a based on GPT, an acronym for Generative Pre-trained Transformer, which is currently the market leader among large language models (LLMs). LLMs are machine learning models specifically designed to understand and process natural human language. These models are trained on extensive datasets that act as their knowledge base. Therefore, the range of ChatGPT's responses is determined by the information included in these datasets. To keep up with evolving language and information about the world, these models are periodically updated with fresh datasets.

1. ### What ChatGPT doesn't know?
    

ChatGPT, like any Large Language Model (LLM), is inherently constrained by the information present in the datasets it was trained on. Let's consider a scenario where you are the CEO of a company with over 100 employees. Your team diligently compiles an annual company report, which encapsulates a wealth of information including quarterly performance reports of employees, financial data, management insights, and strategic roadmaps. The performance report is meticulously crafted based on more than 20 parameters. Now, you wish to find which employee outperformed others in the previous year.

While it's a complex task to calculate all the parameters for each quarter of the previous year and determine the top-performing employee, AI can certainly assist in this process. However, it's important to note that AI models like ChatGPT don't have the ability to access or process real-time data, such as employee performance reviews. They can't perform tasks that require access to specific databases or proprietary information.

If you were to ask ChatGPT, "Can you rank the employees based on their performance review last year?" it would likely show you something like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706031691899/bb96702d-bc10-444d-bc10-f3cf079d1ef1.png align="center")

This is because the GPT model was not trained to know about your company and its annual reports. It broke!

![](https://media1.giphy.com/media/kE6xCyOOHoxlS/giphy.gif?cid=ecf05e47cv7i1i0mhop2lni81icmszs6o1fqxast5ls6wzza&ep=v1_gifs_search&rid=giphy.gif&ct=g align="center")

How can we approach this problem? How can we use AI models to retrieve private information about a business or domain using natural human language?

1. ### Method 1: Fine Tuning
    

If you've ever conversed with a car enthusiast, you're likely familiar with the concept of tuning. While the engine of your favorite car may be highly capable, its performance is often limited by the manufacturer to ensure the engine's reliability and longevity. That's why enthusiasts often have their cars professionally tuned to optimize performance to their liking.

Similarly, fine-tuning in Language Learning Models (LLMs) involves training a pre-existing model with additional data. In our scenario, this new data could be a company's annual report. Once the model is trained with this new dataset, it's equipped to answer company-specific questions.

However, when a new report is generated in the subsequent quarter, the model will need to be retrained with this updated data. This process repeats every three months. Training a model requires substantial computational resources and potentially specialized hardware like high-end GPUs or TPUs. Additionally, it demands a deep understanding of deep learning, Natural Language Processing (NLP), and expertise in data preprocessing, model configuration, and evaluation.

1. ### Method 2: Retrieval-Augmented Generation (RAG)
    

RAG introduces an intermediary layer between the user and the Language Learning Model (LLM). In a traditional setup, a user poses a question to the LLM as a prompt and receives a response that is generated based on the model's training dataset. However, with RAG, the LLM isn't directly trained on new data. Instead, this data is incorporated into the prompt itself.

For instance, when inquiring about the best performing employee, the performance metrics are integrated into the question and passed along as part of the prompt. The prompt might look something like this.

```plaintext
........Long data about performance of employees...........
........Long data about performance of employees...........
........Long data about performance of employees...........
........Long data about performance of employees...........

Can you rank the employees based on their performance review last year?
```

Now, the model has context about the question because the query was augmented with relevant data.

You might wonder, if this approach is so straightforward, why not feed the model with the entire report every time a question is asked? For instance, in the example above, why not provide the full report instead of just the performance review section? The challenge lies in the size of the dataset. Language Learning Models (LLMs) can only process a limited number of tokens (words) at a time. They cannot process an entire business's knowledge base for every query. This would be highly resource-intensive and costly.

The solution lies in the **Retrieval** component of Retrieval-Augmented Generation (RAG).

The goal is to retrieve the most relevant chunk of data from the entire knowledge base. This chunk should be small enough to be processed by the LLM. But how do we determine which part of the comprehensive company report is most relevant to the asked question? This is where 'Embeddings' come into play. Embeddings capture the 'relatedness' of text, images, videos, or other types of information. They compress discrete information (like words and symbols) into distributed, continuous-valued data (like vectors).

For example, consider these three phrases:

1. "I am hungry"
    
2. "I need to eat something"
    
3. "I love the smell of napalm in the morning"
    

![](https://media0.giphy.com/media/9xgCMjSM56TFm/giphy.gif?cid=ecf05e47jdyttbz71x1tiohduk1eou4fshet23g1trvgu8m9&ep=v1_gifs_related&rid=giphy.gif&ct=g align="center")

As a human, it's easy to discern that the first two phrases have somewhat similar meanings, while the third phrase significantly deviates in meaning from the first two. If we were to represent these three phrases as vectors on a 2D graph, the visualization might look something like this.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706078043137/b7a526b6-23c2-4c83-89ed-b338e87ebcd9.png align="center")

"Phrases 1 and 2 would likely be plotted close to each other in the vector space, given their similar meanings. In contrast, we would expect Phrase 3 to be positioned further away due to its unrelated content. For simplicity, we're considering a two-dimensional example here, but most embedding models operate in hundreds of dimensions to capture the complexity of human language.

These vectors are stored in a searchable vector database. When we decompose our entire company knowledge base into such embeddings, we end up with millions of these vectors.

Here's how the process works:

1\. **Vector Storage**: The vectors are stored in a structure known as a Vector Database.

2\. **Question Embedding**: Our question, "Can you rank the employees based on their performance review last year?", is also transformed into a one-time embedding.

3\. **Retrieval**: This embedding is then used to query the vector database, searching for the most relevant chunks of data. This process is known as Retrieval.

4\. **Augmentation**: The retrieved relevant data is then combined with the question to create a prompt.

5\. **Generation**: Finally, the answer is generated based on this prompt."

**Retrieval + Augmentation = Generation**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706079401430/4360e58c-d211-4ef7-8d90-3d047998386e.png align="center")

This technique is more cost effective then fine-tuning and is friendly towards ever-changing and ever-updating dynamic data. You just have to store new data in a vector database.

Generating embeddings and building a reliable retrieval mechanism is necessary for a performant AI application. You can use tools like [MindsDB](https://mindsdb.com/) or [Supabase's Vector Database](https://supabase.com/docs/guides/ai) to build such systems.

If you like this article, drop a hi [here](https://twitter.com/devcodesthings)!