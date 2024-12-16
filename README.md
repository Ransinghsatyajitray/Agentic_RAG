# Agentic_RAG
This application is for looking into the Agentic RAG and uses Chroma 

## This codes implement a Q&A system that uses RAG. This means it retrieves relevant information from the kb to help answer the questions. 

Here is the Breakdown of the code and a flowchart that illustrate the process:

**1. Fetching Web Content:**

fetch_url_content(url): Fetches content from a given URL. It uses requests.get() to make an HTTP request and retrieves the content if the request is successful (status code 200).

**2. Splitting and Cleaning Text:**

RecursiveCharacterTextSplitter: Splits the fetched web content into smaller chunks of a specified size (token_size). This is important for managing the input to the language model.
clean_text(text): Removes newline characters and extra spaces to clean up the text.

**3. Generating Embeddings:**

get_embeddings(texts): Uses the OpenAI API to generate embeddings for each text chunk. Embeddings are numerical representations of text that capture semantic meaning.

**4. Storing in ChromaDB:**

chromadb.Client(): Initializes a ChromaDB client for vector storage.
collection.add(): Stores the text chunks and their corresponding embeddings in a ChromaDB collection. This allows for efficient similarity search.

**5. Searching for Relevant Context:**

search(text, top_k): Searches the ChromaDB collection for chunks that are most semantically similar to the input question. It retrieves the top_k most relevant chunks.

**6. Answering the Question:**

decision_system_prompt: This prompt is used to ask a large language model (LLM) to determine if the retrieved context is relevant to the question.
system_prompt: This prompt instructs the LLM to answer the question based on the provided context.
user_prompt: This prompt structures the question for the LLM.
The code uses litellm.completion() to send the prompts and context to the LLM (gpt-4o-mini).
If the LLM determines the context is relevant, it answers the question.
If the context is not relevant, the code performs a web search using duckduckgo_search and then uses the search results as context to answer the question.

