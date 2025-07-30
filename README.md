# RD Sharma Math Question Extraction Pipeline

This project provides an end-to-end pipeline to **automatically extract and generate LaTeX-formatted math questions** from RD Sharma textbooks in PDF format. It leverages open-source tools and models including PyMuPDF, SentenceTransformers, FAISS, and instruction-tuned GPT-like LLMs via HuggingFace Transformers.

---

## Project Folder Structure
```markdown
rdsharma_extractor/
├── data/
│ └── rd.pdf # Place your RD Sharma PDF here
├── src/
│ ├── pdf_extraction.py # PDF text extraction and cleaning
│ ├── chunking.py # Chunking and noise filtering
│ ├── retrieval.py # Semantic search module using FAISS
│ ├── llm_extract.py # LLM question extraction from chunks
│ ├── batch_llm_extract.py # Batch question extraction script
│ ├── validate_latex.py # LaTeX validation and cleaning
│ └── (other helper scripts)
├── tests/ # Unit tests for each module
│ ├── test_chunking.py
│ ├── test_retrieval.py
│ ├── test_llm_extract.py
│ └── test_validate_latex.py
├── extracted_topic_text.txt # Extracted and cleaned text output
├── filtered_chunks.txt # Filtered and chunked text output
├── extracted_questions.tex # Aggregated LaTeX questions output
├── cleaned_questions.tex # Validated and cleaned LaTeX file
├── requirements.txt # Python dependencies list
└── README.md # This file

```


## Setup & Installation

1. **Clone this repository:**

git clone https://github.com/yourusername/your-repo-name.git
cd your-repo-name

python -m venv .venv

Windows
..venv\Scripts\activate

Linux/Mac
source .venv/bin/activate


2. **Install required packages:**

Install dependencies listed in `requirements.txt` (example content below):

pymupdf
regex
sentence-transformers
faiss-cpu
numpy
transformers
torch
pylatexenc
pytest

Install with:

pip install -r requirements.txt


---

## Running the Pipeline

Follow these steps in sequence to perform extraction and question generation:

### Step 1: Extract Text from PDF

python src/pdf_extraction.py

- This extracts specified chapter/topic text from `data/rd.pdf` and saves cleaned text to `extracted_topic_text.txt`.

### Step 2: Chunk and Filter Text

python src/chunking.py

- Splits `extracted_topic_text.txt` into manageable chunks.
- Filters out noisy artifacts.
- Saves filtered chunks to `filtered_chunks.txt`.

### Step 3: Run Retrieval (Optional for focused queries)

python src/retrieval.py

- Use this module to embed chunks and retrieve relevant ones for a query.
- For ad-hoc queries, import `Retriever` class from `src/retrieval.py` in your scripts.

### Step 4: Batch LLM Extraction of LaTeX Questions

python src/batch_llm_extract.py

- Processes all filtered chunks via the instruction-tuned local LLM.
- Extracts LaTeX math questions.
- Saves output to `extracted_questions.tex`.

### Step 5: Validate and Clean LaTeX Output


- Checks LaTeX syntax validity.
- Cleans prompt echoes.
- Writes clean LaTeX to `cleaned_questions.tex`.

---

## Running Tests

To run the unit tests and ensure everything works:

pytest tests/

- Tests cover chunking, retrieval, LLM extraction (mocked), and LaTeX validation.

---

## Notes & Recommendations

- The LLM extraction step can be slow on CPU; using a GPU accelerates generation substantially.
- Adjust chunk size and filtering heuristics in `chunking.py` to optimize context vs speed.
- Customize the prompt in `llm_extract.py` for your desired extraction style.
- Always review and lightly clean the generated LaTeX before using in production documents.
- Extract the zip folders and follow the same structure and following the steps will give correct output

---


