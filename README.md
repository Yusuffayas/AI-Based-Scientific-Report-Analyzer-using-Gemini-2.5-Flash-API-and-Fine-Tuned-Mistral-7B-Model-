# AI-Based-Scientific-Report-Analyzer-using-Gemini-2.5-Flash-API-and-Fine-Tuned-Mistral-7B-Model-
Scientific research papers are rich in structured equations, variables, tables, and quantitative results but extracting and analyzing that manually is tedious. AI-Based Scientific Report Analyzer automatically reads research PDFs, identifies mathematical equations and tabular data, computes results, and generates a structured author-ready output. 

Chapter 1 – Introduction
1.1 Background

Modern research output is overwhelmingly digital and data-intensive. Scientific reports, especially in domains such as cryptography, IoT, and medical engineering, contain structured information embedded in text and mathematical expressions. Manual extraction of these elements for comparative or computational analysis is time-consuming.

Advances in Large Language Models (LLMs) and multimodal AI have opened pathways for automating the reading, understanding, and mathematical processing of such documents.
This internship focused on building a system that bridges document intelligence with symbolic reasoning—an AI tool capable of parsing complex scientific papers, identifying all mathematical entities, performing relevant computations, and delivering structured analytical outputs for authors and reviewers.

1.2 Problem Statement

Researchers often need to verify equations, recompute performance metrics, or cross-reference variable definitions from PDFs. Existing AI tools are limited to text summarization or OCR-based extraction without mathematical reasoning.

The problem addressed here is to design and develop an AI model that can automatically extract, interpret, and solve equations from scientific research papers and produce accurate, human-readable results.

1.3 Objectives

Automate extraction of equations, variables, and tables from research PDFs.

Compute results and classify variable types and bit sizes.

Compare cloud-based (Gemini API) and fine-tuned local LLM (Mistral 7B LoRA) performance.

Design a modular architecture deployable via cloud and local inference.

Generate structured output suitable for publication or validation.

1.4 Scope and Significance

The analyzer targets domains where reproducibility and computational verification are essential—cryptography, IoT security, biomedical signal processing, etc.

It enables reviewers and researchers to validate reported formulas and results without manual effort, thus improving transparency and accuracy in scientific publication.

1.5 Project Environment

Organization: National Institute of Technology Puducherry

Team: Yusuf Fayas, Sabareesh K S, and Nandhagopalan S

Tools & Frameworks: Python, Gemini 2.5 Flash API, LLaMA Factory, LoRA, Hugging Face Hub, Firebase, AWS Cloud, React Native

Computing Setup: GPU-enabled AI server for fine-tuning experiments

Chapter 2 – Literature Review
2.1 Scientific Document Understanding

Early systems used OCR and rule-based parsing. Modern models such as LayoutLM, DocFormer, and Gemini multimodal variants combine text, visual, and spatial reasoning to analyze PDFs with higher accuracy.

2.2 Equation Extraction and Computation

Systems like MathPix and LaTeX tokenizers convert math regions into structured markup.

Recent LLMs (GPT-4, Gemini 2.5, Claude 3, DeepSeek) can directly interpret equations and perform symbolic reasoning.
Fine-tuned models such as Mistral, LLaMA-2-Math demonstrate domain-specific improvements.

2.3 Fine-Tuning LLMs with LoRA and LLaMA Factory

Low-Rank Adaptation (LoRA) injects small trainable matrices into existing weights, reducing GPU memory cost.

LLaMA Factory enables structured supervised fine-tuning and experiment management.
Fine-tuning Mistral 7B v0.1 on equation–solution datasets improves scientific reasoning.

2.4 Gemini 2.5 Flash API

Gemini 2.5 Flash is a fast multimodal model capable of reasoning over text, images, and PDFs.
Streaming inference enables fast extraction of structured outputs from documents.

2.5 Related Work

The reference paper “An Efficient ECC and Fuzzy Verifier-Based User Authentication Protocol for IoT-Enabled WSNs” (Sudhakar et al., 2025) contains well-structured cryptographic equations, hash functions, and cost tables—ideal for validating the system.

Chapter 3 – System Analysis and Design
3.1 Functional Requirements

Input: Scientific PDF

Process: Extract text, tables, equations → symbolic reasoning

Output: Structured table with equation, operators, operands, and computed value

Comparison: Gemini API vs. Mistral 7B

Storage: Firebase (metadata), AWS S3 (archives)

3.2 Non-Functional Requirements

Accuracy: ≥ 95% equation identification

Latency: < 10s for a 5-page PDF

Scalability: Batch processing support

Security: Encrypted data, authenticated API keys

Portability: Cloud + Local GPU support

3.3 System Architecture

Five main layers:

Input Handler

Pre-Processor

Analyzer Core (Gemini / Mistral)

Computation Engine

Report Generator

3.4 Data Flow

User uploads PDF

Gemini → Cloud analysis
Mistral → Local GPU inference

Results stored in Firebase

Metrics evaluated (accuracy, latency, tokens)

3.5 Module Description

PDF Pre-Processor :	Extract text, tables, equations	- pdfminer, PyMuPDF

Gemini Analyzer :	Multimodal extraction & JSON parsing - Google AI API

Mistral Analyzer :	Local inference via fine-tuned model - Transformers + LoRA

Comparator :	Compare outputs, timing - Custom Python

Output Formatter :	Generate CSV/JSON and dashboard display - React + Firebase

3.6 System Specifications

Hardware: NVIDIA A100, 64 GB RAM

Software: Ubuntu 22.04, PyTorch, Node.js

APIs: Gemini Flash, Hugging Face

Dataset: ~15,000 equation–solution pairs

Chapter 4 – Implementation Details
4.1 Workflow

Two pipelines:

Gemini 2.5 Flash (Cloud) – handles multimodal extraction

Fine-Tuned Mistral 7B (Local) – performs symbolic computation

4.2 Module Details
4.2.1 PDF Pre-Processing

Libraries: pdfminer.six, PyMuPDF, OpenCV
Steps:

Convert PDF to images

Detect text & equations

OCR math regions

Store tokens as JSON

for page in document:
    text = page.get_text("text")
    equations = detect_equations(page)
    save_to_json({"text": text, "equations": equations})

4.2.2 Gemini Flash Integration

Batch upload

Prompt engineering

Receives JSON with equation, operators, operands, result

Advantages: Fast, multimodal
Limitations: Occasional truncation, limited control

4.2.3 Fine-Tuned Mistral 7B (LoRA)

Dataset: 15k equation–solution pairs
Training Parameters:

Base Model	Mistral-7B-v0.1

LoRA r	8

α	16

LR	2e-4

Epochs	3

Max Seq Len	4096

GPU	A100 80GB

4.2.4 Computation Engine

Uses SymPy to compute:

Result

Operators

Operands

Bit sizes

4.2.5 Output Formatting

Tabular result:

| Equation | Result | Operators | Operands | Bit Size |

Stored in Firebase, shown on React dashboard.

4.3 UI Prototype

React Native

PDF upload

Equation viewer

Comparison mode

4.4 Cloud Deployment

Gemini on Google Cloud

Firebase Auth + DB

AWS S3 storage

Hugging Face inference endpoint for Mistral

Chapter 5 – Results and Discussion

5.1 Dataset

Reference paper with 50+ equations, 10+ tables.

5.2 Gemini Results

84% extraction accuracy

Output under 6 seconds

Minor errors in notation

5.3 Mistral Results

95% extraction accuracy

12 seconds per PDF

Strong symbolic consistency

5.4 Comparison
Metric            | Gemini Flash | Mistral 7B

Equation Accuracy | 84%	         |95%

Table Recognition | Excellent    |Good

Computation	  | 90%	         |93%

Latency	          | 6s	         |12

Cloud Dependency	High	Low

Cost	Higher	Minimal

5.5 Discussion

Gemini excels in multimodal extraction;


Mistral excels in symbolic accuracy.

The combined architecture gives the best results.

Chapter 6 – Comparison and Evaluation

6.1 Technical Evaluation

Gemini: fast OCR + multimodal

Mistral: customizable, stable symbolic math

LoRA improved precision and reduced forgetting

6.2 Cost Analysis
Component  | Gemini Cloud | Local Mistral
Infra	   | API Billing  | One-time GPU
Cost/run   | ₹0.15/page	  | Negligible

6.3 Scalability

Hybrid architecture:
Gemini → Extraction
Mistral → Computation

Chapter 7 – Conclusion & Future Work
7.1 Conclusion

The system successfully extracts, interprets, and solves scientific equations with ~93% accuracy, combining Gemini Flash and fine-tuned Mistral 7B.

7.2 Future Enhancements

Add GPT-4 / Claude 3 integrations

Expand datasets

Release as public portal (rights reserved)

Export to LaTeX / IEEE formats

Appendix A – Folder Structure
research-analyzer

│

├── src

│   ├── __pycache__

│   │   ├── __init__.cpython-310.pyc

│   │   ├── __init__.cpython-311.pyc

│   │   ├── __init__.cpython-313.pyc

│   │

│   ├── database

│   │   └── app.db

│   │

│   ├── models

│   │   ├── __pycache__

│   │   └── user.py

│   │

│   ├── routes

│   │   ├── __pycache__

│   │   ├── analysis.cpython-310.pyc

│   │   ├── analysis.cpython-311.pyc

│   │   ├── analysis.cpython-313.pyc

│   │   ├── user.cpython-310.pyc

│   │   ├── user.cpython-311.pyc

│   │   ├── user.cpython-313.pyc

│   │   ├── analysis.py

│   │   └── user.py

│   │

│   ├── static

│   │   ├── favicon.ico

│   │   └── index.html

│   │

│   ├── __init__.py

│   ├── main.py

│   └── test.py

│

├── requirements.txt

├── trained model

Appendix B – Hardware & Software Environment

Processor: Intel Xeon 64-bit

GPU: NVIDIA A100 80GB
• OS: Ubuntu 22.04 LTS 
• IDE: VS Code, Jupyter Lab 
• Libraries: Transformers, SymPy, Torch, LLaMA Factory, Firebase SDK
