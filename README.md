
# 🕵️ CitationSleuth: The Fact-Checking RAG System

**CitationSleuth** is an advanced Retrieval-Augmented Generation (RAG) system designed to detect and prevent hallucinations in Large Language Models. It employs a "Trust but Verify" architecture, combining Vector Search with Knowledge Graphs to audit AI answers against source documents.

---

## 📂 Repository Contents

* **`CitationSleuth_final_project.ipynb`**: The complete project pipeline (Ingestion, RAG, Verification, and UI).
* **`demo-file.pdf`**: The research paper (*SayNav*) used to demonstrate and test the system.
* **`Secret Keys.txt`**: Contains the necessary API credentials for testing.

---

## ⚡ Execution Guide (Google Colab)

Follow these steps to set up and run the project.

### 1. Open the Notebook
Upload `CitationSleuth_final_project.ipynb` to Google Colab.

### 2. Configure Keys (Notebook Step 2)
Navigate to the code cell labeled **Step 2: Imports, Auth, & Model Initialization**.
1.  Open the `Secret Keys.txt` file provided in this repository.
2.  Copy **ALL** the values (`HF_TOKEN`, `GOOGLE_API_KEY`, `NEO4J_URI`, `NEO4J_PASSWORD`, and `NGROK_TOKEN`).
3.  Paste them directly into the corresponding variables in the notebook code.

> **ℹ️ Model Selection**: The system is configured to use **`gemini-2.5-flash`** by default for high speed and efficiency.
> * **Quota Limits**: If you encounter a `429 Resource Exhausted` error, it means the free tier quota for this model has been reached.
> * **Fix**: You can modify the model name in Step 2 to use other variants such as `gemini-1.5-flash` or `gemini-2.5-flash-exp`.

> **⚠️ Troubleshooting `HF_TOKEN`**: If you receive a `401 Unauthorized` error, the provided Hugging Face token may have expired. You can generate a free "Read" token at [Hugging Face Settings](https://huggingface.co/settings/tokens) and use that instead.

### 3. Upload Demo File (Notebook Step 3)
Run **Step 3: PDF Ingestion**.
* The cell will display a "Choose Files" button.
* Upload the `demo-file.pdf` provided in this repository.
* The system will extract text and chunk the document for the database.

### 4. Run Verification Logic (Notebook Steps 4-12)
Run the cells from **Step 4** through **Step 12** to build the Knowledge Graph and run the backend benchmarks.

> **⚠️ Troubleshooting Verification (Step 10)**: If Step 10 fails due to API limits:
> * Ensure you are using your own personal Google API Key.
> * Try switching the model in Step 2 (e.g., to `gemini-1.5-flash`).

### 5. Configure App Secrets (Notebook Step 13)
**Crucial Step:** The User Interface runs as a separate application script (`app.py`), so it cannot access the variables from Step 2. You must manually inject the keys again here.

1.  Look inside the code block for **Step 13** (under `%%writefile app.py`).
2.  Find the section marked `# ⚠️ PASTE YOUR REAL KEYS HERE`.
3.  Paste the following keys from your `Secret Keys.txt` file:
    * `GOOGLE_API_KEY`
    * `NEO4J_URI`
    * `NEO4J_PASSWORD`
4.  Run the cell to generate the `app.py` file.

### 6. Launch Application (Notebook Step 14)
Run the final step. It will start the Streamlit server using the `NGROK_TOKEN` you provided in Step 2.
* Wait for the output to display a public URL (e.g., `https://....ngrok-free.app`).
* Click this link to open the CitationSleuth UI.

---

## 🖥️ User Interface Instructions

Once the app is open in your browser, follow this workflow:

1.  **Ingest Data:**
    * In the sidebar, upload the same PDF file (`demo-file.pdf`).
    * Click the **"Ingest"** button. Wait for the green success message.

2.  **View Global Graph:**
    * **Before asking any questions**, switch to the **"Graph"** tab.
    * You will see the **Global Knowledge Graph**, visualizing the entire document's concepts and connections.

3.  **Ask & Verify:**
    * Switch to the **"Chat"** tab.
    * Type a question (e.g., *"What are the three modules?"*) and press Enter.
    * The AI will generate an answer with a **Verification Badge** (Green for Supported, Red for Flagged).

4.  **View Context Graph:**
    * **After getting an answer**, switch back to the **"Graph"** tab.
    * The view will automatically update to show the **Context Graph**—visualizing *only* the entities and relationships relevant to your last question.

---

## 📊 Performance

Based on the **HaluEval** benchmark (1,000 samples), CitationSleuth achieves:
* **Accuracy:** 80.7%
* **Precision:** 72.2%
* **Recall:** 99.7% (Extremely effective at catching hallucinations)
* **F1-Score:** 83.7%

---

## 👥 Authors

**Presented By:**
* Koushik Vasa
* Kavya Shivakumar
* Sehaj Gill
