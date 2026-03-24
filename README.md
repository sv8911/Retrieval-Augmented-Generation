# 📚 Local RAG System (Retrieval-Augmented Generation)

This project implements a fully local Retrieval-Augmented Generation (RAG) system that allows users to query PDF documents and receive context-aware answers using a local language model.
The goal of this project was to understand how modern AI systems like ChatGPT work with documents, and to build a complete pipeline from scratch without relying on external APIs.

## Overview

This system allows you to load a PDF, process it into searchable chunks, and ask questions that are answered based only on the document content. Everything runs locally, including the language model.
It supports semantic search, meaning it understands the intent behind a query rather than relying on keyword matching.

## Tech Stack

Python  
PyMuPDF for extracting text from PDFs  
Sentence Transformers for generating embeddings using the all-MiniLM-L6-v2 model  
ChromaDB as the vector database  
Ollama for running a local LLM such as Gemma or Mistral  

## How it works

The pipeline is built step by step.
First, the PDF is loaded and text is extracted using PyMuPDF. Since raw PDF text can be messy, a cleaning step removes unnecessary noise such as formatting issues, headers, and irrelevant front pages.
The cleaned text is then split into smaller overlapping chunks. This ensures that context is preserved and improves retrieval quality.
Each chunk is converted into a vector representation using a sentence transformer model. These embeddings are stored in ChromaDB, which allows fast similarity-based search.
When a user asks a question, the query is also converted into an embedding. The system retrieves the most relevant chunks from the database and sends them, along with the question, to a local LLM running via Ollama.
The model then generates an answer grounded only in the retrieved context.

## Architecture

PDF → Text Extraction → Cleaning → Chunking → Embeddings → Vector Database → Query → Retrieval → LLM → Answer

## Features

Runs completely locally with no API usage  
Works with any PDF document  
Uses semantic search instead of keyword matching  
Produces context-aware answers  
Modular design that can be extended easily  

## Installation

Clone the repository and navigate into the project folder.

Install the required dependencies:
pip install pymupdf sentence-transformers chromadb ollama tf-keras
Install Ollama from the official website and make sure it is running.

Download a lightweight model such as:
ollama pull gemma3:1b

## Usage

Place your PDF file in the project directory.
Run the notebook and execute all cells in order.
Once everything is loaded, you can ask questions such as:
query = "Explain Law 7"
The system will retrieve relevant sections and generate an answer based on them.

## Example

The system is able to retrieve relevant passages and generate answers that reflect the intent of the document, rather than just matching keywords.

## Limitations

Answer quality depends on the model being used. Smaller models may produce less refined outputs.
PDF formatting can affect how well the text is chunked and retrieved.
The system currently requires manual tuning for preprocessing and chunking.

## Future Improvements

Add a Streamlit interface for a chat-based experience  
Improve chunking using paragraph or semantic boundaries  
Support multiple documents in a single index  
Display source references alongside answers  
Implement hybrid search combining keyword and vector methods  

## Author

Shreya Abraham Varghese

## Acknowledgements

This project builds on tools and libraries such as Sentence Transformers, ChromaDB, and Ollama.
