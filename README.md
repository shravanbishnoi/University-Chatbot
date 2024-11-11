# University-Chatbot
This project is a university chatbot designed to answer common questions about Sitare University. It uses a Retrieval-Augmented Generation (RAG) approach combined with a Llama model to retrieve relevant information from a pre-collected dataset and generate contextually appropriate responses.

By leveraging FAISS for fast embedding search and Grok API with Llama for generating human-like answers, the chatbot provides students with quick and relevant responses.

## Requirements
Ensure you have the following packages installed to run this chatbot:
- `pandas`
- `numpy`
- `faiss-cpu`
- `sentence-transformers`
- `transformers`
- `google.generativeai`
- `grok`

To install all dependencies, you can run:
- `pip install pandas numpy faiss-cpu sentence-transformers transformers google-generativeai grok`

## Data Preparation
Upload the pre-collected dataset, containing questions and answers about the university, to your Colab environment. Specify the file path in the script to load the dataset:

`csv_file_path = '/content/chatbot-combined.csv'
df = pd.read_csv(csv_file_path)`
## Setup for Grok API
- Sign up or log in to Grok's Console.
- Create a new API key and copy it.
- Paste the generated key in the code where specified:
- `grok_api_key = "YOUR_API_KEY"`
  
## Techniques Used
### Retrieval with FAISS
- Sentence Embeddings: Using SentenceTransformer('all-MiniLM-L6-v2'), embeddings are generated for each question in the dataset.
- FAISS Indexing: Embeddings are stored in a FAISS L2-distance index, enabling fast similarity-based retrieval of relevant answers.

### Generation with Llama and Grok API
- Prompt-Based Generation: Using the Grok API and Llama model, the chatbot combines retrieved answers with prompt-based generation to provide coherent responses.
- Query Handling: If the retrieved context is relevant, a direct answer is generated. If not, the model defaults to "I don’t have an appropriate answer."

## How to Use
- Initialize the Dataset and Model: Upload your CSV file and load it as shown in the code. Set up FAISS indexing and embedding model.
- Start Asking Questions: Run the chatbot, which will prompt you to enter questions. Type your question, and it will return an answer generated based on the relevant retrieved documents.
- Exit: Type "exit" to stop the chatbot.
Example interaction:
`Enter your query here: What is Sitare University?
Llama Answer: Sitare University provides high-quality Computer Science education to students from underprivileged backgrounds, covering all expenses.`

Key Functions
- `get_top_answer(query, model, faiss_index, df, top_k=3)`: Retrieves top matching answers for the user query.
- `GroqChat(question)`: Queries the Llama model through the Grok API to generate an answer based on retrieved content.
- `generate_answer_from_docs(query, retrieved_docs)`: Compiles the final answer using both retrieved documents and generated content from the Llama model.

## Future Improvements
- Expanding the dataset to cover more university topics
- Integrating additional language models for diverse queries
  
This chatbot provides a foundation for answering university-related queries with speed and accuracy, ensuring students receive reliable and accessible information.
