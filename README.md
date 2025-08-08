# Smart Igbo Idiom Translator 

## 1. Introduction

This repo presents a Smart Igbo Idiom Translator that utilizes a Retrieval-Augmented Generation (RAG) approach to provide both literal and figurative meanings of Igbo idioms within a given sentence. The application is built using Python and libraries like Langchain, Hugging Face Transformers, FAISS, and Gradio.

## 2. How to Use the App

The application provides a user-friendly interface powered by Gradio. To use the translator:

1.  **Run the entire notebook:** Ensure all code cells in the notebook are executed successfully.
2.  **Access the Gradio interface:** Once the last code cell (containing the Gradio app) is executed, a public URL will be provided. Click on this URL to open the translator in your web browser.
   OR
Simply copy this <a href ="https://6f73c14d9fd9f57c1f.gradio.live/">url</a> and paste on a browser
4.  **Enter your Igbo sentence:** In the "Enter Igbo sentence" textbox, type the Igbo sentence containing the idiom you want to translate.
5.  **Select Meaning Type:** Choose whether you want to see the "Literal" or "Actual" (figurative) meaning of the idiom using the radio buttons.
6.  **Click "Translate":** Click the "Translate" button to get the translation. The result will appear in the "Meaning" textbox.

## 3. Replicating the Work

To replicate this work, you will need to set up your environment and obtain the necessary data and API keys.

1.  **Clone the repository :** You can clone this repo to your local machine or a cloud environment like Google Colab.
2.  **Install dependencies:** Install the required Python libraries by running the pip install commands provided in the requirements.txt file.
3.  **Obtain OpenAI API Key:** This project uses the OpenAI API. You will need to obtain an API key from the OpenAI <a href="https://platform.openai.com/">website.</a> In your local or cloud environment, safely store your OpenAI API key to avoid exposure. 
4.  **Idioms Dataset:** The application relies on an Excel file named `Idioms.xlsx` containing Igbo idioms and their translations. You will need to have this file available in the `/content/` directory or update the code to load it from a different location or create your own dataset of idioms translations. The expected columns in the Excel file are "Phrase", "Literal Translation", and "Actual Meaning".
5.  **Run the notebook:** Execute all code cells sequentially. Make changes as desired.

## 4. Preprocessing Explanation

In this project, the primary preprocessing step involves creating embeddings of the idiom data using a Sentence Transformer model. Unlike some natural language processing tasks, extensive text cleaning such as removing punctuation, stop words, or lowercasing was intentionally omitted.

The reason for this approach is that idioms are highly context-dependent and their meaning is often derived from the specific words used and their arrangement, including punctuation. Removing these elements through aggressive cleaning stripped away crucial contextual information necessary for accurately identifying and interpreting the idioms. The chosen embedding model is capable of handling the nuances of the text with punctuation and casing, preserving the richness of the original data for better retrieval.

## 5. Code Explanation

The notebook is structured into several key parts:

-   **Library Imports:** Imports all necessary libraries.
-   **API Key Configuration:** Securely loads the OpenAI API key from Colab's Secrets Manager.
-   **Data Loading:** Reads the Igbo idioms from the `Idioms.xlsx` file into a pandas DataFrame.
-   **Embedding Creation:** Defines a function to create embeddings using a Hugging Face Sentence Transformer model and prepares the data for FAISS by concatenating the phrase, literal, and actual meanings.
-   **FAISS Vector Store:** Creates a FAISS index from the embeddings, allowing for efficient similarity search.
-   **Language Model and Prompting:** Initializes the ChatOpenAI model and defines the prompt template for the language model, including a placeholder for chat history to enable conversational context.
-   **RAG Chain Implementation:** Sets up a RAG chain using Langchain's components: a history-aware retriever to handle conversational context, a document chain to combine retrieved documents with the user's query, and a retrieval chain to orchestrate the process.
-   **Session History Management:** Implements a simple in-memory system to manage chat history for conversational turns.
-   **Response Generation Function:** Defines a function `generate_response` that invokes the conversational RAG chain with user input and session history.
-   **Meaning Extraction Function:** Defines a function `get_meaning` that calls `generate_response` and then parses the output to extract the literal and actual meanings.
-   **Gradio Interface:** Sets up the web-based user interface using Gradio, connecting the input and output components to the `get_meaning` function.

## 6. Evaluation

Evaluation is done manually.

## 7.Future Improvements

Several areas could be explored to improve this project:

-   **Expand the Idiom Dataset:** Including more Igbo idioms would enhance the translator's coverage and accuracy.
-   **Containerization:** Package the application using Docker for easier deployment and reproducibility.
-   **Add support for other languages:** Extend the framework to support idiom translation for other languages.

