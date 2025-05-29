# 📄 Project Overview: TableTap

## 🧩 Problem Statement  
Insurance policy documents often contain **dense tables** listing critical coverage details—deductibles, exclusions, plan types, and limits. These documents are difficult for users (and even analysts) to read, interpret, and search through.  

Manual extraction of this information is:  
- Time-consuming  
- Prone to human error  
- Not scalable across thousands of documents

There is a clear need for a tool that can automatically extract tabular data from PDFs and allow users to **ask natural-language questions** about the information contained within them.

---

## 🎯 Goal  
To build a lightweight, AI-powered application that:
1. **Extracts tables** from insurance PDFs using OCR and layout-aware tools  
2. **Transforms them into structured data**  
3. **Enables users to ask questions** (e.g., “What is the deductible for Plan B?”) and get accurate, contextual answers

---

## 🛠️ Tools & Technologies

| Component           | Tool/Library                         | Purpose                             |
|---------------------|--------------------------------------|-------------------------------------|
| Table Extraction    | `Camelot` or `pdfplumber`            | Pull tables from PDFs into DataFrames  
| QA Model            | `Hugging Face Tapas`                 | Answer questions from table data  
| PDF Samples         | Insurance policy documents           | Realistic, complex documents for testing  
| Interface (optional)| CLI or Streamlit                     | Interact with the system easily  
| Language            | Python                               | All processing and model code  

---

## 🧭 Approach

### Step 1: PDF Table Extraction  
Use Camelot (preferred for structured tables) to extract tabular data from PDFs. If Camelot fails on certain layouts, pdfplumber will be used as fallback.

### Step 2: Table Cleaning & Normalization  
Convert extracted tables into Pandas DataFrames and clean them:
- Fix headers, merge rows if split
- Normalize numeric values (e.g., remove "$", "%", etc.)

### Step 3: Question Answering  
Use the `transformers` library to run a table-aware QA model (e.g., `google/tapas-large-finetuned-wtq`) on the cleaned DataFrame:
- Input: user’s question (text)
- Output: model-generated answer based on table data

### Step 4: User Interaction  
Simple CLI for now:
- Show list of extracted tables
- Let user select a table and ask questions
- Print the answer

(Optional: A web app using Streamlit can be built later for better UX.)

---

## ✅ Deliverables
- Python package with modular structure: `extractor.py`, `qa.py`, `main.py`
- At least one working example with a sample insurance PDF
- CLI that allows users to select a table and ask questions
- README and documentation

---