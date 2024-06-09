# AI-Powered-Document-Reader

## Part 1: Document Conversion, OCR, and Preprocessing

### Document Conversion: 
I used the pypdf library to convert PDF documents into text. The Document_Conversion function takes a PDF file path as input, extracts text from each page, and concatenates it into a single string. pypdf was chosen for its simplicity and efficiency in handling PDF files without the need for additional dependencies.

### OCR Integration
For OCR (Optical Character Recognition), I use the pdf2image library to convert PDF pages into images and pytesseract to extract text from these images. The OCR_Integration function converts each page of the PDF to an image, applies OCR using pytesseract, and combines the extracted text into a single string. pytesseract was chosen for its accuracy and wide language support, making it suitable for documents in various languages.

### Preprocessing
The preprocess function performs several steps to clean and prepare the text for LLM processing:
* Removing repeating lines to reduce redundancy.
* Cleaning text by removing newlines, tabs, and non-ASCII characters.
* Language detection using the langdetect library, which supports a wide range of languages.
* Sentence segmentation and tokenization using spaCy, a powerful NLP library.
* I prioritize web-based models (_core_web_sm) over news-based models (_core_news_sm) for better general-purpose text handling.

## Part 2: LLM-Powered Understanding and Actions

### LLM Integration
I used a combination of pre-trained models for various tasks, leveraging the power of transfer learning. This approach allows me to benefit from models trained on large datasets without the need for extensive fine-tuning.

### Information Extraction
* Named Entity Recognition (NER): I used the flair library with the flair/ner-german-large model for robust NER. Although this model is German-specific, it was chosen for its high accuracy and can be easily replaced with language-specific models.
* Relationship Extraction: Also using flair, I extract relationships between entities. The pre-trained relations classifier was chosen for its ability to identify semantic relationships.
* Summarization: I use the bert-extractive-summarizer library, which leverages BERT for extractive summarization. This model was chosen for its ability to identify key sentences without the need for fine-tuning.

### Document Classification
For document classification, I used the SetFitModel from the setfit library, specifically the luis-cardoso-q/kotodama-multilingual-v3 model. This model is pre-trained to classify documents into categories like "buying," "invoice," "refund," etc. The multilingual aspect makes it suitable for my diverse language requirements.

### Internal Translation
I used the transformers library from Hugging Face for translation. The google/bert2bert_L-24_wmt_de_en model is used for German to English translation. This model was chosen for its high-quality translations and the ability to handle long texts (up to 4000 tokens). For other languages, similar models can be integrated.

## Part 3: User Interaction via a Chatbot Interface

### Chatbot UI
I used streamlit to create a web-based chatbot interface. streamlit was chosen for its simplicity in creating interactive web apps with Python. The interface allows users to:
* Upload PDF documents.
* View document language, summary, and English translation (if applicable).
* Ask questions about entities, relationships, summary, or document category.
* Provide feedback on the chatbot's responses.

### Pipeline Integration
The process_document function integrates all the pipeline components:
* Convert PDF to text and apply OCR.
* Clean and preprocess the text.
* Translate if not in English.
* Extract entities, relationships, and generate summary.
* Classify the document.

The chatbot then uses this processed information to answer user queries.

### Technical Requirements
Libraries and Frameworks

* Document Processing: pypdf, pdf2image, pytesseract
* NLP and Preprocessing: spacy, langdetect, flair
* LLM and Information Extraction: bert-extractive-summarizer, setfit, transformers
* Chatbot UI: streamlit
