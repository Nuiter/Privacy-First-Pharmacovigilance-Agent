# 💊 Privacy-First Pharmacovigilance Agent

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) [![Status: Prototype](https://img.shields.io/badge/Status-Prototype-blue)](https://github.com/Nuiter) [![Built with n8n](https://img.shields.io/badge/Built%20with-n8n-XR?logo=n8n)](https://n8n.io)

An automated, **air-gapped AI agent** designed to streamline the extraction and triage of Adverse Event (AE) reports from unstructured clinical notes.

Built on top of the **[n8n-API-unleashed](https://github.com/Nuiter/n8n-API-unleashed)** stack, this project demonstrates a flexible architecture that can leverage efficient **Small Language Models (SLMs)** for speed and privacy, or scale up to massive **Large Language Models (LLMs)** for complex reasoning tasks.

**Zero data egress. Zero API costs. Maximum privacy.**

---

## 🏥 The Clinical Problem

**Pharmacovigilance** teams are overwhelmed by unstructured data. Reviewing clinical notes to identify suspected drugs, adverse events, and severity grades is a manual, error-prone, and slow process.

**The Challenge:** Cloud-based AI solutions offer power but pose significant **privacy and compliance risks** when handling raw patient data (RWD).

## 💡 The Solution

A local, autonomous agentic workflow that processes data entirely within your infrastructure:

1.  **Ingests** raw clinical notes from a database (simulated via local Sheets).
2.  **Extracts** structured entities (Drug, Event, Grade) using prompt engineering.
3.  **Analyzes** risk and determines the protocol action based on severity.
4.  **Reports** structured data back to the system.

### 🧠 Flexible Intelligence: From Efficiency to Genius

This architecture is model-agnostic. You choose the brain that fits the mission:

*   **⚡ The Efficient Path (Default):** Uses **SLMs** like `Microsoft Phi-3 Mini` (3.8B). Perfect for standard extraction tasks, running on consumer CPUs with minimal latency and energy cost.
*   **🧠 The "Beautiful Mind" Path:** For complex causality analysis or rare disease detection, the stack supports swapping the engine for high-parameter **LLMs** (e.g., `Llama-3-70B`, `Mixtral 8x22B`, or `DeepSeek-Coder-33B`). If you provide the GPU hardware, this system delivers GPT-4 class reasoning power while maintaining 100% data sovereignty.

---

## 🛠️ Technical Architecture

-   **Orchestrator:** n8n (Self-hosted).
-   **Inference Engine:** Llama.cpp server (Dockerized).
-   **Current Model:** `Microsoft Phi-3 Mini 4k Instruct` (GGUF Quantized).
-   **Data Storage:** Local Google Sheets integration.

### Workflow Logic

1.  **Agent 1 (The Extractor):** Parses natural language notes into structured JSON.
2.  **Agent 2 (The Safety Officer):** Applies business logic to determine the required action based on the extracted Severity Grade.

---

## 🚀 How to Run

### 1. Prerequisites
You need Docker and Docker Compose installed.

### 2. Setup the Infrastructure
This project relies on the infrastructure defined in the `docker-compose.yml`.

```bash
# Clone this repository
git clone https://github.com/Nuiter/Privacy-First-Pharmacovigilance-Agent.git
cd Privacy-First-Pharmacovigilance-Agent

# Download the model (Phi-3 Mini) to ./model-cache/
# (Check n8n-API-unleashed for detailed model setup instructions)

# Start the stack
docker-compose up -d

### 3. Import the Workflow
1.  Open n8n at `http://localhost:5678`.
2.  Import the workflow file located at `./workflows/pharmacovigilance_agent.json`.
3.  Configure your Google Sheets credentials.
4.  Use the sample data in `./data/dummy_patients.csv` to test the extraction logic.

---

## 📜 License

This project is licensed under the MIT License. See the `LICENSE` file for details.

## ✍️ How to Cite

If you find this project useful for your research or work, please consider citing it. 
While a `CITATION.cff` file is provided for automated tools, we recommend using the following formats for accuracy.

### APA

```text
Pérez-Santiago, Á. I. (Nuiter). (2025). Privacy-First Pharmacovigilance Agent (Version 1.0.0) [Software]. Zenodo. https://doi.org/10.5281/zenodo.[DOI_ID]
```

### BibTeX

```bibtex
@software{Perez-Santiago_2025_pharmacovigilance,
  author       = {Pérez-Santiago, Ángel Ignacio (Nuiter)},
  title        = {{Privacy-First-Pharmacovigilance-Agent}},
  month        = dec,
  year         = 2025,
  publisher    = {Zenodo},
  version      = {1.0.0},
  doi          = {10.5281/zenodo.[DOI_ID]},
  url          = {https://doi.org/10.5281/zenodo.[DOI_ID]}
}
```