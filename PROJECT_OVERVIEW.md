# 📄 Project Overview: TableTap

## 🧩 Problem Statement  
Insurance policy documents often include **complex tables** with essential information—like deductibles, copays, dental coverage, and plan totals. These tables are difficult to read, vary in structure, and make automated processing challenging.

For analysts, underwriters, or app developers, there's a need for a **simple script-based tool** that can automatically extract key coverage values and present them in a human-readable format, without needing to manually inspect the PDF.

---

## 🎯 Goal  
To build a Python tool that:
1. **Extracts tables** from insurance PDFs using layout-aware tools  
2. **Automatically finds answers** to a set of **predefined, common questions** (e.g., deductible, total, dental coverage)  
3. **Prints results in the terminal** in a clean, labeled format  
4. Defaults to a test file (`test.pdf`), but allows the user to specify another file if desired

---

## 🛠️ Tools & Technologies

| Component           | Tool/Library                         | Purpose                             |
|---------------------|--------------------------------------|-------------------------------------|
| Table Extraction    | `Camelot` or `pdfplumber`            | Pull tables from PDFs into DataFrames  
| QA Model            | `Hugging Face Tapas`                 | Answer preset questions from table data  
| Language            | Python                               | All processing and model code  
| CLI Input           | `argparse` / `input()`               | Prompt for PDF path (optional)  

---

## 🧭 Approach

### Step 1: Table Extraction  
Use Camelot (or pdfplumber) to extract tabular data from the given PDF file.

### Step 2: Default PDF Fallback  
The script will try to run on `test.pdf` in the project root. If the user provides a file name/path via prompt, that file will be used instead.

### Step 3: Predefined Questions  
The script will run a fixed set of questions like:
- "What is the deductible?"
- "What is the total cost of the plan?"
- "What is the dental coverage?"

Each question will be sent to the Tapas model, and the answer will be extracted.

### Step 4: Result Display  
Answers will be printed to the terminal in the format:

```bash
Deductible: $500
Total Cost: $15,000
Dental Coverage: Included

No user interaction beyond choosing the file.
```
---

## ✅ Deliverables
- A single command-line Python script (`main.py`) that runs end-to-end  
- Test file: `test.pdf` placed in the root folder  
- Table extraction, question answering, and formatted print output  
- README and documentation

---

## Example Output

```bash
$ python main.py
No PDF file provided. Using default: test.pdf

Deductible: $1,000  
Total Cost: $12,500  
Dental Coverage: Yes, up to $2,000/year 
```