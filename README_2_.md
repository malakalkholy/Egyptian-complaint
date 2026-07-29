# 🚀 [Tips Hindawi](https://www.tipshindawi.com/) Challenge (June–July) 2026

> 🏆 This repository is my official submission for the [ **Tips Hindawi** ](https://www.tipshindawi.com/) **Challenge (June–July) 2026**.

## 👤 Participant

| Field            | Value                                |
| ---------------- | ------------------------------------ |
| Full Name        | Malak Hamdi                          |
| Project Name     | Egyptian Arabic Customer Complaint Assistant |
| GitHub Username  | Malakalkholy
| Challenge Batch  | June–July 2026                       |
| Training Program | Large Language Models (LLMs) Program |
| Organization     | [**Edrak for Ai**](https://edrak4ai.com/en)                         |

---

# 📖 Project Overview

An AI system that reads customer complaints written in everyday Egyptian Arabic — slang, sarcasm, and all — classifies them, grounds refund decisions in real company policy, and drafts a natural-sounding reply. Support teams at Egyptian delivery, ride-hailing, and telecom companies are flooded with dialect complaints that are slow to read, classify, and check against policy by hand. This project automates that pipeline end-to-end while keeping every refund decision traceable to an actual policy document, not a guess.

---

# ✨ Features

* Fine-tuned for Egyptian dialect — a small LLM (Qwen, via [Unsloth](https://unsloth.ai)) LoRA fine-tuned on ~450 labeled Egyptian-dialect complaint examples
* RAG-grounded refund decisions — company policies are embedded and retrieved via FAISS, so decisions are backed by an inspectable policy snippet
* Structured, validated output — every response is parsed and validated with LangChain's `StructuredOutputParser`
* Deterministic policy safety net — a rule-based layer double-checks the model's refund decision against the documented policy minimum and corrects it if the model under-delivers
* Live demo via Streamlit — a lightweight frontend that talks to the model over a FastAPI + ngrok tunnel, so the heavy model runs on a free Kaggle GPU while the UI runs anywhere

---

# 🛠️ Technologies Used

| Component | Tool |
|---|---|
| Base model | Qwen (Instruct), via Unsloth |
| Fine-tuning | LoRA, Unsloth `FastLanguageModel` + `SFTTrainer` |
| Model hosting | Hugging Face Hub |
| Structured output | LangChain `StructuredOutputParser` |
| Retrieval (RAG) | FAISS + `paraphrase-multilingual-MiniLM-L12-v2` embeddings |
| Serving | FastAPI + ngrok (tunneled from a Kaggle GPU notebook) |
| Frontend | Streamlit |
| Training/inference compute | Kaggle (free T4 GPU) |

---

# ⚙️ Installation

**1. Fine-tune (or reuse the pushed model)**
Run `training-notebook.ipynb` on Kaggle (GPU enabled) to fine-tune from scratch, or skip straight to step 2 to use the already-pushed model on Hugging Face Hub.

**2. Run the pipeline + serve the API**
In `Egyptian-complaint.ipynb` (Kaggle, GPU enabled):
```python
!pip install faiss-cpu langchain langchain-community langchain-core langchain-huggingface pypdf sentence-transformers transformers torch unsloth fastapi uvicorn pyngrok accelerate -q
```
Run the notebook top to bottom. The final cells start a FastAPI server and print a public ngrok URL.

**3. Run the Streamlit frontend**
```bash
pip install -r requirements.txt
streamlit run app.py
```

**Security note:** don't hardcode your `NGROK_TOKEN` or `API_KEY` directly in a shared notebook — use Kaggle Secrets (`kaggle_secrets.UserSecretsClient`) instead.

---

# 🚀 Usage

1. Start `Egyptian-complaint.ipynb` on Kaggle and let it run to the end — copy the printed ngrok URL.
2. Launch the Streamlit app locally with `streamlit run app.py`.
3. Paste the ngrok URL and your API key into the sidebar.
4. Type a complaint in Egyptian Arabic and click **Process Complaint** to see the category, severity, refund decision, and suggested reply.

Keep the Kaggle notebook tab open and active while demoing — the tunnel dies if the session idles out, and you'll need to re-run the notebook for a fresh URL.

---

# 📸 Demo

*(Add screenshots or a short screen recording of the Streamlit app processing a sample complaint here.)*

---

# 📈 Results

The system reliably classifies Egyptian-dialect complaints into category/subcategory, retrieves the matching company policy, and produces a refund decision that a deterministic enforcement layer guarantees never falls below the documented policy minimum — so every output is auditable against an actual policy line rather than a model guess.

---

# 🔮 Future Improvements

* Expand the fine-tuning set beyond ~450 examples for broader dialect and edge-case coverage
* Improve robustness to non-greedy sampling (currently `do_sample=False` is required to avoid incoherent output)
* Make replies feel less uniform/formal, likely via a larger or more diversely-written training set

---

# 📚 About the Challenge

This project was developed as part of the [**Tips Hindawi**](https://www.tipshindawi.com/) **Challenge (June–July) 2026**.

[Tips Hindawi](https://www.tipshindawi.com/) is the internships department of [**Edrak for Ai**](https://edrak4ai.com/en), and the challenge encourages participants to build real-world projects, apply practical skills, and showcase their work through GitHub.

For more information about the challenge, training programs, and upcoming batches, visit the official [Tips Hindawi](https://www.tipshindawi.com/) website.

---

# 📄 License

This project is shared for educational and portfolio purposes.
