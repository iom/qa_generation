# qa_generation

This notebook demonstrates how to use the `qa_generation` library to generate question-answer pairs from a given text. 

It uses Azure OpenAI API  configure within a .env file. As much as possible, the code is designed to be modular and reusable. It uses parallel processing to speed up the generation of question-answer pairs.
The library is designed to be used in conjunction with a vector database (LanceDB) to store the generated question-answer pairs and retrieve them later for further processing or analysis.

Steps:

 1. Build a library a PDF documents based on Google Search

 2. Download each PDF document locally

 3. Review each document page by page and generate questions using an LLM configured with high temperature settings (aka creative)

 4. Convert each page of the PDF to embeddings using OpenAI API and load them into a vector database (LanceDB) - and set a retriever to retrieve the most relevant pages based on the question asked.

 5. Use the retriever to find the most relevant pages and generate answers using the LLM configured with low temperature settings (aka factual)

 6. Save the question-answer pairs to a json file that can be used for:
    
    * Perform human __data-labeling - use [Label Studio](https://api.labelstud.io/tutorials/tutorials/evaluate-llm-responses) for subject matter expert to assess the quality of the generated questions and answers.
    * Implement __fine-tuning__ a small open model that will be less costly to run while keeping accuracy - the dataset is pushed to Hugging Face as a public good
    * Create a __knowledge base__ - for instance within an agentic system like [CrewAI](https://docs.crewai.com/concepts/knowledge)
    

This capacity can be used in multiple context, for instance:

- Policy Development for instance to compare similar policies in different countries using a consistent set of questions.
- Chatbots to answer questions from Migrants on Migration Pathways.
- Agentic models to inform the development of project proposals