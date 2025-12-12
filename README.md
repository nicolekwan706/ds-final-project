<h1>Movie RAG System</h1>

Group members: Nishita Koya(vfj8ba), Yuhan Liu(yl7gk), Nicole Kwan(ypt2vj)

---
<p>This project implements a Retrieval-Augmented Generation (RAG) system using:</p>
<ul>
  <li>A cleaned CSV dataset (<code>etl_cleaned_dataset.csv</code>)</li>
  <li>A film box-office PDF (https://www.researchgate.net/publication/281730174_The_determinants_of_box_office_performance_in_the_film_industry_revisited) </li>
</ul>

<p>The system performs:</p>
<ul>
  <li>Document ingestion and chunking</li>
  <li>Embedding with <code>bge-small-en-v1.5</code></li>
  <li>FAISS vector search</li>
  <li>Local LLM generation using <code>Phi-3-mini-4k-instruct</code></li>
  <li>A Flask API endpoint at <code>/api/ask</code></li>
  <li>A simple optional HTML user interface</li>
</ul>

<h2>Folder Structure</h2>

<pre>
ds-final-project-nyn/
│
├── api/
│   ├── app.py
│   └── requirements.txt
│
├── rag_pipeline/
│   ├── ingest.py
│   ├── embeddings.py
│   ├── vector_store.py
│   ├── retriever.py
│   └── rag.py
│
├── data/
│   ├── etl_cleaned_dataset.csv
│   └── additional_documents/
│
├── ui/
│   └── chat.html
│
├── README.md
└── reflection.pdf
</pre>

<h2>How to Run (Under 2 Minutes)</h2>

<h3>1. Navigate to the API folder</h3>
<pre>
cd api
</pre>

<h3>2. Install dependencies</h3>

<p><strong>Important:</strong> Several project artifacts (such as <code>texts.pkl</code>, <code>metadatas.pkl</code>, and the FAISS index) were generated using <strong>Python 3.12</strong>.  
To ensure compatibility, install the requirements using Python 3.12:</p>

<pre>
python3.12 -m pip install -r requirements.txt
</pre>

<p><em>These serialized files are not guaranteed to load correctly under different Python versions.</em></p>

<h3>3. Start the server</h3>

<pre>
python3.12 app.py
</pre>

<p>The API will be available at:</p>
<pre>
http://127.0.0.1:8000
</pre>


<h2>API Usage</h2>

<h3>POST /api/ask</h3>

<p>Example CURL request:</p>

<pre>
curl -X POST http://127.0.0.1:8000/api/ask \
  -H "Content-Type: application/json" \
  -d '{"question": "Which movie has the highest IMDb rating?"}'
</pre>

<p>Example JSON response:</p>

<pre>
{
  "answer": "Based on the context ...",
  "sources": [
    { "id": "file.pdf", "page": 7, "snippet": "..." },
    { "id": "etl_cleaned_dataset.csv", "snippet": "..." }
  ]
}
</pre>


<h2>Bonus UI</h2>

<p>Open <code>ui/chat.html</code> in a browser to use a very simple chat interface that sends queries to <code>/api/ask</code>.</p>
