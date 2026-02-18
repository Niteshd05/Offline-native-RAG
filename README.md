# 🧠 Offline Edge RAG – React Native  
### A 100% Offline, Privacy-First Retrieval-Augmented Generation System Running Fully On-Device

![React Native](https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Offline First](https://img.shields.io/badge/100%25_Offline-Success?style=for-the-badge)
![Zero APIs](https://img.shields.io/badge/Zero_API_Calls-blue?style=for-the-badge)
![MIT License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

---

## 📖 Overview

Most AI applications today are thin wrappers around cloud APIs.

**Offline Edge RAG is different.**

This project is a fully self-contained Retrieval-Augmented Generation (RAG) pipeline that runs entirely on mobile hardware using React Native — no backend, no API calls, no cloud vector database.

It ingests local documents, performs semantic chunking, generates high-dimensional embeddings, executes vector similarity search, and augments a local LLM — all on-device.

After the initial model download, the system runs 100% offline.

Built and engineered by **Nitesh Domal** as an exploration into pushing Edge AI to its limits on constrained mobile architectures.

---

## ✨ Key Features

### 🔒 Absolute Privacy
- Zero API calls
- No OpenAI
- No Pinecone
- No cloud vector DB
- All data remains on the device

### 🧠 Dual-Model Architecture
- Separate local LLM for text generation
- Dedicated embedding model for semantic mapping
- Both models loaded simultaneously on mobile

### 🗂 Custom JavaScript Vector Database
- Flat-file JSON vector index
- Brute-force cosine similarity search
- No SQLite vector extensions
- No native DB complexity

### 📄 On-Device Document Ingestion
- Reads `.txt` files directly from device storage
- Uses `RecursiveCharacterTextSplitter`
- Optimized for mobile context limits

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|------------|
| Framework | React Native (0.73+) |
| Inference Engine | `llama.rn` (C++ bindings for `llama.cpp`) |
| LLM | Qwen 2.5 (1.5B, Q4_K_M GGUF) |
| Embeddings | Nomic Embed Text v1.5 (GGUF) |
| Vector Search | Pure JavaScript cosine similarity |
| Storage | Flat JSON file index |

---

## ⚙️ Architecture & Engineering Challenges

Running two ML models on a mobile device requires aggressive optimization.  
This system was benchmarked on mid-range Android hardware and tuned for memory safety and UI stability.

---

### 1️⃣ The Vector Search Bottleneck

Instead of using SQLite vector extensions or FAISS, a custom flat-file JSON database was engineered.

Search complexity:


Cosine Similarity formula:  similarity = (A · B) / (||A|| ||B||)


Why brute force?

- Dataset size is manageable on-device
- Eliminates heavy native dependencies
- Keeps architecture simple and portable

---

### 2️⃣ Context Window Management

Mobile LLMs have strict token limits (2048 tokens).

Optimizations:
- `chunkSize` reduced to 500 characters
- Top 2–3 most similar chunks selected
- Prompt dynamically constructed
- System prompt + chat history + retrieved context carefully packed

This prevents:
- Token overflow crashes
- OS memory kills
- Context truncation issues

---

Here is your section in **clean, properly formatted, paste-ready Markdown**:

````markdown
---

### 3️⃣ RAM Headroom Management

Loading two `.gguf` models simultaneously is volatile on mobile unified memory.

#### Key Optimizations
- Quantized models (`Q4_K_M`)
- `use_mlock: true`
- Reduced batch size
- Strict inference settings

**Final footprint:** ~1.2GB RAM usage  

Leaves safe headroom for:
- React Native UI thread
- Smooth 60fps rendering
- Stable background processing

---

## 🚀 Setup Instructions

### 2️⃣ Install Dependencies

```bash
npm install
````

For iOS:

```bash
cd ios
pod install
cd ..
```

---

### 3️⃣ Run the App

For Android:

```bash
npx react-native run-android
```

For iOS:

```bash
npx react-native run-ios
```

---

## 📥 First Launch Behavior

On first launch:

* The app automatically downloads the required `.gguf` models
* Models are stored in the device's document directory
* This is the only time internet access is required

After that:

* The system runs completely offline
* No network requests are made
* All inference happens locally

---

## 📊 Performance Benchmarks (Mid-Range Android)

| Metric             | Result                |
| ------------------ | --------------------- |
| Embedding Time     | ~150–250ms            |
| Vector Search      | <50ms (small dataset) |
| Generation Latency | 1–3s                  |
| RAM Usage          | ~600MB                |
| Offline Capability | 100%                  |

---

## 🔮 Future Improvements

* ANN search (HNSW in JS or WASM)
* Streaming token output
* PDF ingestion support
* Persistent chat memory
* On-device quantization selection
* iOS memory tuning

---

## 📜 License

MIT License

---

## 👨‍💻 Author

**Nitesh Domal**
Exploring Edge AI, Generative Systems, and Privacy-First Architectures.

```

If you want, I can also format this into a **visually stronger GitHub-style README section hierarchy** with consistent numbering and no duplication between RAM usage values (currently 1.2GB vs 600MB mismatch).
```

