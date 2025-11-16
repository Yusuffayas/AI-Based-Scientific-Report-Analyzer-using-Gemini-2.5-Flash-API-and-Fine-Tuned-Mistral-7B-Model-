# AI-Based-Scientific-Report-Analyzer-using-Gemini-2.5-Flash-API-and-Fine-Tuned-Mistral-7B-Model-
Scientific research papers are rich in structured equations, variables, tables, and quantitative results but extracting and analyzing that manually is tedious. AI-Based Scientific Report Analyzer automatically reads research PDFs, identifies mathematical equations and tabular data, computes results, and generates a structured author-ready output. 

# Chapter 1 – Introduction

## 1.1 Background
Modern research output is overwhelmingly digital and data-intensive. Scientific reports, especially in domains such as cryptography, IoT, and medical engineering, contain structured information embedded in text and mathematical expressions. Manual extraction of these elements for comparative or computational analysis is time-consuming.

Advances in Large Language Models (LLMs) and multimodal AI have opened pathways for automating the reading, understanding, and mathematical processing of such documents. This internship focused on building a system that bridges document intelligence with symbolic reasoning—an AI tool capable of parsing complex scientific papers, identifying all mathematical entities, performing relevant computations, and delivering structured analytical outputs for authors and reviewers.

## 1.2 Problem Statement
Researchers often need to verify equations, recompute performance metrics, or cross-reference variable definitions from PDFs. Existing AI tools are limited to text summarization or OCR-based extraction without mathematical reasoning.

The problem addressed here is to design and develop an AI model that can automatically extract, interpret, and solve equations from scientific research papers and produce accurate, human-readable results.

## 1.3 Objectives
- Automate extraction of equations, variables, and tables from research PDFs.
- Compute results and classify variable types and bit sizes.
- Compare cloud-based (Gemini API) and fine-tuned local LLM (Mistral 7B LoRA) performance.
- Design a modular architecture deployable via cloud and local inference.
- Generate structured output suitable for publication or validation.

## 1.4 Scope and Significance
The analyzer targets domains where reproducibility and computational verification are essential—cryptography, IoT security, biomedical signal processing, etc.

It enables reviewers and researchers to validate reported formulas and results without manual effort, thus improving transparency and accuracy in scientific publication.

## 1.5 Internship Environment
- **Organization:** National Institute of Technology Puducherry  
- **Team:** Yusuf Fayas, Sabareesh K S, and Nandhagopalan S  
- **Tools & Frameworks:** Python, Gemini 2.5 Flash API, LLaMA Factory, LoRA, Hugging Face Hub, Firebase, AWS Cloud, React Native  
- **Computing Setup:** GPU-enabled AI server for fine-tuning experiments

# Chapter 2 – Literature Review

## 2.1 Scientific Document Understanding
Early document-analysis systems relied on OCR and rule-based parsing. Modern AI models like LayoutLM, DocFormer, and Gemini’s multimodal variants combine textual, visual, and spatial features, allowing direct reasoning over PDF structures.

## 2.2 Equation Extraction and Computation
Techniques such as MathPix OCR and LaTeX tokenizers convert mathematical regions into structured markup. Recent LLMs (GPT-4, Gemini 2.5, Claude 3) can interpret equations and perform symbolic reasoning. Fine-tuned models (Mistral, LLaMA 2 Math, DeepSeek) show improved accuracy for scientific tasks.

## 2.3 Fine-Tuning LLMs with LoRA and LLaMA Factory
Low-Rank Adaptation (LoRA) adds small trainable matrices to existing model weights, reducing GPU memory usage. LLaMA Factory provides structured interfaces for supervised fine-tuning and experiment tracking.

## 2.4 Gemini 2.5 Flash API
Gemini 2.5 Flash is a multimodal model optimized for reasoning over text, images, and PDFs using fast streaming inference.

## 2.5 Related Work Analysis
Reference paper: “An Efficient ECC and Fuzzy Verifier-Based User Authentication Protocol for IoT-Enabled WSNs” (Sudhakar et al., 2025).  
Contains elliptic curve equations, hash functions, and cost tables—ideal for validating extraction and computation modules.

# Chapter 3 – System Analysis and Design

## 3.1 Functional Requirements
- **Input:** PDF document.
- **Process:** Extract text, tables, equations → symbolic parsing → computation.
- **Output:** Structured table (equation, result, operators, operands).
- **Modes:** Gemini API vs. Fine-Tuned Mistral 7B.
- **Storage:** Firebase + AWS S3.

## 3.2 Non-Functional Requirements
- Accuracy ≥ 95%.
- Latency < 10 sec for 5-page PDF.
- Scalable and secure.
- Portable across cloud/local GPU.

## 3.3 Architecture (5 Layers)
1. Input Handler  
2. Pre-Processor  
3. Analyzer Core  
4. Computation Engine  
5. Report Generator  

## 3.4 Data Flow
1. User uploads PDF  
2. Gemini → Cloud / Mistral → Local  
3. Store results in Firebase  
4. Compare metrics  

## 3.5 Module Description
| Module | Purpose | Tech |
|--------|----------|--------|
| PDF Pre-Processor | Extract text/tables/equations | pdfminer, PyMuPDF |
| Gemini Analyzer | Cloud multimodal extraction | Google AI API |
| Mistral Analyzer | Local symbolic reasoning | LoRA + Transformers |
| Comparator | Compare outputs/time | Python |
| Formatter | Build JSON/CSV dashboards | React + Firebase |

## 3.6 System Specifications
- NVIDIA A100 GPU  
- Python 3.10, PyTorch, Node.js  
- Custom dataset (~15k equation–solution pairs)

# Chapter 4 – Implementation Details

## 4.1 Workflow
Two pipelines:
1. **Gemini Flash (cloud)** for multimodal extraction  
2. **Mistral 7B LoRA (local GPU)** for symbolic math

## 4.2 Module Implementation

### 4.2.1 PDF Pre-Processing
- pdfminer.six, PyMuPDF, OpenCV  
- Steps:
  1. Convert PDF to images  
  2. Segment text/equations  
  3. OCR → LaTeX  
  4. Save JSON tokens  


# Chapter 4 – Implementation Details

## 4.1 System Workflow Overview
The AI Scientific Report Analyzer follows a two-pipeline architecture:

1. **Gemini 2.5 Flash Pipeline (Cloud-Based)**  
   - Optimized for multimodal PDF analysis (text + images).  
   - Fast extraction with structured JSON output.

2. **Fine-Tuned Mistral 7B Pipeline (Local GPU)**  
   - Specialized for symbolic reasoning and equation solving.  
   - Built using LoRA fine-tuning with LLaMA Factory.

Each PDF passes through pre-processing, content extraction, model analysis, computation, and report generation.

## 4.2 Module Implementation Details

### 4.2.1 PDF Pre-Processing and Extraction
**Libraries Used:** `pdfminer.six`, `PyMuPDF`, `OpenCV`, `Pandas`

**Steps:**
1. Convert PDF pages into image frames.  
2. Detect text, tables, and equation blocks using layout segmentation.  
3. OCR mathematical regions and convert them into LaTeX / MathML tokens.  
4. Store structured outputs into JSON.

4.2.2 Gemini 2.5 Flash Integration

Uses Google AI Studio with API key + secure endpoints.

Batch uploads PDF content through streaming mode.

Prompt Example:

Extract all equations and variables from this research paper.
For each equation, compute the result, operators, and operands.


Output Format:
A JSON object containing:

equation

operators

operands

result

confidence score

Advantages:

Fast processing (< 6 seconds for 5 pages)

Handles image-based PDFs well

Limitations:

Sometimes truncates long tables

Has limited control over decoding parameters (temperature, beams)

4.2.3 Fine-Tuned Mistral 7B Model with LoRA

Fine-tuned using LLaMA Factory on a GPU server.

Dataset (≈ 15,000 entries)

Algebraic equations

Cryptographic cost functions

Scientific formula evaluation tasks

Example Training Pair:

Input:
Compute the result of: E = mc^2 for m=2, c=3

Output:
E = 18; Operators: *, ^; Operands: 2, 3

Training Parameters
Parameter	Value
Base Model	Mistral-7B-v0.1
LoRA Rank (r)	8
Alpha	16
Dropout	0.05
Batch Size	4
Learning Rate	2e-4
Epochs	3
Max Seq Length	4096
Optimizer	AdamW 8-bit
Scheduler	Cosine with warmup
Precision	bfloat16
GPU	A100 80GB

After training, the LoRA adapter was merged, and the final checkpoint was uploaded to Hugging Face.

4.2.4 Computation Engine

Uses SymPy for symbolic and numeric evaluation.

For each extracted equation, the engine determines:

Numeric result

Operators used

Operands extracted

Variable bit sizes (cryptographic parameters)

Example:

expr = sympify("E = m * c**2")
result = expr.subs({"m": 2, "c": 3})

4.2.5 Output Formatting and Storage

Final results are converted into a structured table:

| Equation | Result | Operators | Operands | Bit Size |

Outputs are:

Saved to Firebase Firestore

Archived in AWS S3

Displayed in a React dashboard

4.3 User Interface Prototype

A cross-platform UI was built using React Native.

Features:

Upload PDF from device

View extracted equations and variables

Compare outputs from Gemini and Mistral pipelines

Real-time progress bar

Latency & accuracy graphs

4.4 Cloud Deployment

Deployment was implemented using a hybrid multi-cloud approach:

Gemini API called through Google Cloud Functions

Firebase for authentication and database sync

AWS S3 to store processed result files

Hugging Face Inference Endpoint serves the fine-tuned Mistral 7B model

This architecture ensures:

Fast cloud extraction

Accurate local symbolic computation

Scalable storage

Modular deployment design


---

# Chapter 5 – Results and Discussion

## 5.1 Dataset
Reference paper contained:
- 50+ equations  
- 10+ computational tables

## 5.2 Gemini 2.5 Flash Results
- 84% extraction accuracy  
- ~6 sec per PDF  
- Minor notation mismatches  

## 5.3 Fine-Tuned Mistral 7B Results
- 95% extraction accuracy  
- ~12 sec per PDF  
- Strong symbolic precision  

## 5.4 Comparative Performance
| Metric | Gemini Flash | Mistral 7B |
|--------|--------------|------------|
| Equation Accuracy | 84% | 95% |
| Table Extraction | Excellent | Good |
| Computation Accuracy | 90% | 93% |
| Latency | 6s | 12s |

## 5.5 Discussion
Gemini → strong multimodal extraction  
Mistral → strong symbolic reasoning  
Combined → best pipeline

# Chapter 6 – Comparison and Evaluation

## 6.1 Technical Evaluation
- Gemini: fast OCR + multimodal processing  
- Mistral: fully customizable + stable symbolic math  
- LoRA boosts accuracy while reducing training cost  

## 6.2 Cost Analysis
| Component | Gemini Cloud | Local Mistral |
|----------|--------------|---------------|
| Infra | API Billing | One-time GPU |
| Cost/run | ₹0.15/page | Negligible |

## 6.3 Scalability
Hybrid model:
- Gemini → extraction  
- Mistral → computation  

# Chapter 7 – Conclusion and Future Work

## 7.1 Conclusion
The system successfully automates extraction, interpretation, and computation of equations from scientific PDFs using Gemini 2.5 Flash and a fine-tuned Mistral 7B model. Achieved ~93% overall accuracy.

## 7.2 Future Enhancements
- Add more LLMs (Claude 3, GPT-4 Turbo).  
- Expand dataset to biomedical, chemistry, physics.  
- Deploy as a public web portal (rights reserved).  
- Export to LaTeX/IEEE templates (rights reserved).  

# Appendix A – Folder Structure


research-analyzer

│

├── src

│   ├── __pycache__

│   ├── database

│   │   └── app.db

│   ├── models

│   │   └── user.py

│   ├── routes

│   │   ├── analysis.py

│   │   └── user.py

│   ├── static

│   │   ├── favicon.ico

│   │   └── index.html

│   ├── __init__.py

│   ├── main.py

│   └── test.py

│

├── requirements.txt

└── trained model


# Appendix B – Hardware and Software Environment

- **Processor:** Intel Xeon 64-bit  
- **GPU:** NVIDIA A100 80 GB  
- OS: Ubuntu 22.04 LTS 
- IDE: VS Code, Jupyter Lab 
- Libraries: Transformers, SymPy, Torch, LLaMA Factory, Firebase SDK
