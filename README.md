
# 🕵️ CitationSleuth: The Fact-Checking RAG System

**CitationSleuth** is an advanced Retrieval-Augmented Generation (RAG) system designed to detect and prevent hallucinations in Large Language Models. It employs a "Trust but Verify" architecture, combining Vector Search with Knowledge Graphs to audit AI answers against source documents.

---

## 📂 Repository Contents

* **`CitationSleuth_final_project.ipynb`**: The complete project pipeline (Ingestion, RAG, Verification, and UI).
* **`demo-file.pdf`**: The research paper (*SayNav*) used to demonstrate and test the system.
* **`Secret Keys.txt`**: Contains the necessary API credentials for testing.

---

## ⚡ Quick Start Guide (Google Colab)

Follow these steps to set up and run the project.

### 1. Open the Notebook
Upload `CitationSleuth_final_project.ipynb` to Google Colab.

### 2. Configure Keys (Notebook Step 2)
Navigate to the code cell labeled **Step 2: Imports, Auth, & Model Initialization**.
1.  Open the `Secret Keys.txt` file provided in this repository.
2.  Copy the values for `HF_TOKEN`, `GOOGLE_API_KEY`, `NEO4J_URI`, and `NEO4J_PASSWORD`.
3.  Paste them directly into the corresponding variables in the notebook code.

> **⚠️ Troubleshooting `HF_TOKEN`**: If you receive a `401 Unauthorized` or "Expired Token" error in Step 2, the provided Hugging Face token may have expired.
> * **Fix:** Create a free account at [Hugging Face](https://huggingface.co/settings/tokens), generate a new "Read" token, and replace the `HF_TOKEN` in the code.

### 3. Upload Demo File (Notebook Step 3)
Run **Step 3: PDF Ingestion**.
* The cell will display a "Choose Files" button.
* Upload the `demo-file.pdf` provided in this repository.
* The system will then extract text and chunk the document for the database.

### 4. Run Verification Logic (Notebook Steps 4-12)
Run the cells from **Step 4** through **Step 12** to build the Knowledge Graph and run the backend benchmarks.

> **⚠️ Troubleshooting Gemini Quota (Step 10)**: If Step 10 fails with a `429 Resource Exhausted` error, you have hit the rate limit for the free Gemini API.
> * **Fix 1:** Use your own personal Google API Key in Step 2.
> * **Fix 2:** Change the model in Step 2 from `gemini-2.0-flash` to `gemini-1.5-flash` (it has higher limits).
> * **Fix 3:** Add `time.sleep(10)` inside the test loop in Step 10 to slow down requests.

### 5. Configure App Secrets (Notebook Step 13)
**Crucial Step:** Before running **Step 13: Streamlit App Generation**, you must manually add your keys to the application code.
1.  Look inside the code block for Step 13 (under `%%writefile app.py`).
2.  Find the section marked `# ⚠️ PASTE YOUR REAL KEYS HERE`.
3.  Paste your `GOOGLE_API_KEY`, `NEO4J_PASSWORD`, and `NGROK_TOKEN` into this cell.
    * *Note:* The app runs as a separate process, so it cannot "see" the keys you set in Step 2. You must paste them here again.
4.  Run the cell to generate the `app.py` file.

### 6. Launch Application (Notebook Step 14)
Run the final step. It will start the Streamlit server and provide a public URL (e.g., `https://....ngrok-free.app`). Click this link to open the UI.

---

## 🖥️ User Interface Instructions

Once the app is open in your browser, follow this workflow:

1.  **Ingest Data:**
    * In the sidebar, upload a PDF file (e.g., `demo-file.pdf`).
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
