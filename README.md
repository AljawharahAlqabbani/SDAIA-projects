
*Student:* Aljawharah Alsubaie  
*Program:* SDAIA Academy — Data Engineering for AI Systems (DAICO)  
*Session dates:* 19 July 2026 – 23 July 2026  
*Trainer:* Mohammed Albeladi  




# End-to-End Data Engineering & RAG Pipeline — Capstone Project

## Project Overview
An end-to-end data pipeline built to ingest, validate, and structure retail transaction data, storing it across a multi-layered Delta Lake architecture, and powering an intelligent semantic retrieval system using a Retrieval-Augmented Generation (RAG) pipeline.

---

## Dataset & Data Type
* **Dataset Name:** UCI Online Retail Dataset.
* **Data Type:** Real transactional and e-commerce invoice records from a UK-based online retail shop covering the period from 2010 to 2011.
* **Key Attributes Used:** 
  * `InvoiceNo`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `UnitPrice`, `CustomerID`, and `Country`.

---

## Tools & Tech Stack
* **Environment:** Google Colab (Python / Jupyter Notebook)
* **Data Processing & Validation:** Pandas, Pydantic 
* **Delta Lakehouse:** `deltalake` 
* **RAG & Vector Search:** LangChain (`CharacterTextSplitter`), HuggingFaceEmbeddings (`sentence-transformers/all-MiniLM-L6-v2`), ChromaDB

---

## Implementation Stages & Results

### 1. Data Ingestion & Contract (Pydantic)
* **What was done:** Defined strict data contracts and validation schemas using Pydantic to check data boundaries and types.
* **Results & Outputs:** 
  * Successfully validated the incoming transaction stream.
  * Isolated corrupted, malformed, or invalid records (such as negative quantities or missing critical fields) and routed them safely into a separate **Quarantine DataFrame/Table** to prevent data pollution.

### 2. Delta Lakehouse Layers
* **Bronze Layer (Raw):** 
  * *Action:* Ingested the raw transactional dataset directly into a Delta table without modifications.
  * *Result:* Preserved an immutable, exact copy of the original source data as a single source of truth.
* **Silver Layer (Cleaned):** 
  * *Action:* Filtered out the quarantined records, cleaned missing values, and standardized data types.
  * *Result:* A clean, reliable, and standardized dataset ready for downstream analytics.
* **Gold Layer (Analytics-Ready):** 
  * *Action:* Aggregated the clean data using grouping operations.
  * *Result:* Generated analytics-ready metrics including **Total Sales** (Quantity $\times$ Unit Price), total quantities, and average prices grouped by product `StockCode` and `Country`.

### 3. RAG Pipeline & Semantic Search
* **What was done:** 
  * Extracted unique product descriptions and chunked them using `CharacterTextSplitter`.
  * Generated dense semantic embeddings using the HuggingFace model (`sentence-transformers/all-MiniLM-L6-v2`).
  * Stored the embeddings inside a **ChromaDB** vector database.
* **Results & Outputs:** 
  * Enabled intelligent semantic search queries (e.g., searching for product descriptions using keywords like "WHITE").
  * Successfully retrieved the most relevant product matches and context insights based on vector similarity scores.

---

## How to Run
Open the Jupyter Notebook (`.ipynb`) in Google Colab and run all cells sequentially from top to bottom.
