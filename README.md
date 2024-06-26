# Lithuanian-Legal-Q-A-Chatbot-with-RAG-LangChain
### This project presents a locally deployable Question and Answer (Q&amp;A) chatbot system built using LangChain, Chroma as vector database and the pre-trained LLM (Large Language Model) model "l3utterfly/phi-2-layla-v1".

# Motivation:

### Navigating legal documents can be challenging for individuals unfamiliar with legal terminology. This chatbot offers a user-friendly interface to access information within Lithuanian legal documents, potentially empowering citizens and legal professionals with easier access to relevant legal information.

# Benefits:

### * Improved Access to Legal Information: The chatbot provides a user-friendly way to access information within Lithuanian legal documents, potentially empowering individuals and legal professionals.
### * Natural Language Interaction: Users can ask questions in natural English language, enhancing accessibility compared to traditional search methods.
### * Offline Functionality (Potential): Local deployment offers the possibility of offline use, potentially beneficial in situations where internet access is limited or where user doesn't want it's data to be shared.

# RAG LLm Chain explanation:

![Chat Bot RAG chain](https://github.com/ArturasGrygelis/Lithuanian-Legal-Q-A-Chatbot-with-RAG-LangChain/blob/main/assets/447725144_3827899717441033_3841956047829821436_n.png)

#### 1. Loading Documents and Text Splitting:

The  function load_documents  retrieve the documents used as the knowledge base.
These documents are then split into smaller chunks using RecursiveCharacterTextSplitter. This helps the system process information more efficiently.
#### 2. Building a Document Vector Database:

Chroma.from_documents creates a vector database from the split documents.
Each document is represented as a vector using the provided  pre-trained Huggingface word embeddings.
This allows for efficient retrieval of similar documents based on their content.
#### 3. Retriever for Relevant Documents:

The vectordb.as_retriever method creates a retriever object from the vector database.
This retriever uses a technique called "Minimum Mutual Regret (MMR)" to find the most relevant documents to a given query, considering both relevance and diversity.
The parameter k controls the number of documents retrieved for each query.
#### 4. Contextualizing User Questions:

The contextualize_q_system_prompt variable defines a prompt for a large language model (LLM) like me.
This prompt instructs the LLM to reformulate a user question into a standalone format, independent of the chat history.
#### 5. History-Aware Retriever:

create_history_aware_retriever combines the original retriever with the LLM's ability to understand context.
This allows the system to consider both the user's current question and the conversation history when searching for relevant documents.
#### 6. Building the RAG Chain:

qa_system_prompt defines a prompt for the LLM to use for question answering.
Similar to the contextualization prompt, this prompt includes placeholders for chat history and user input.
create_stuff_documents_chain  creates a chain for processing the user's question and answer using the LLM and the qa_prompt.
create_retrieval_chain combines the question answering chain with the history-aware retriever, forming the core RAG functionality.
#### 7. Conversational RAG Chain:

RunnableWithMessageHistory wraps the RAG chain to manage conversation history.
It defines functions to retrieve and update the chat history for each user session.
This allows the system to track the conversation and use past information to inform future responses.

# Example:
Example of how RAG Q&A bot  works:
#### Legal Q&A Chatbot input output and how context looks like:
![Chat Bot RAG Conversation example](https://github.com/ArturasGrygelis/Lithuanian-Legal-Q-A-Chatbot-with-RAG-LangChain/blob/main/assets/448079728_446779294635176_33098728519908288_n.png
)

#### Legal Q&A Chatbot Conversation Example:
![Chat Bot RAG Input Output](https://github.com/ArturasGrygelis/Lithuanian-Legal-Q-A-Chatbot-with-RAG-LangChain/blob/main/assets/448144203_1132798198026457_5805972757956745459_n.png)

# Disclaimer:

#### Important Information:

##### * Data Currency: The legal information used by this chatbot system may not reflect the absolute latest redactions of Lithuanian law. Legal documents are subject to change over time, and this chatbot's knowledge base might not always be fully up-to-date.
##### * Resource Constraints: This project was developed using freely available resources. For a more comprehensive and reliable legal chatbot system, it's recommended to utilize Large Language Models (LLMs) with a larger context size to handle complex legal inquiries.

##### * By using this chatbot, you acknowledge and agree to the following:

*The information provided by this chatbot is for general informational purposes only and should not be construed as legal advice.
*You should always consult with a qualified legal professional for any specific legal issues or concerns.
*The developers of this project cannot be held liable for any actions or decisions taken based on the information provided by the chatbot.


## Attribution
#### Big thanks to huggingface and langchain comunities!
This project incorporates the "l3utterfly/phi-2-layla-v1" model from Hugging Face under the MIT License.


**Copyright [2024], Layla, l3utterfly** 

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**Link to Repository:** [l3utterfly/phi-2-layla-v1](https://huggingface.co/l3utterfly/phi-2-layla-v1)
