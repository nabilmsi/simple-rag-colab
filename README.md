# Simple RAG: Ask Questions About a PDF

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nabilmsi/simple-rag-colab/blob/main/simple_rag_colab.ipynb)

A small Retrieval-Augmented Generation (RAG) system that answers questions using a PDF document and cites the source page numbers.

## How it works

1. **Extract** text from the PDF page by page (PyMuPDF)
2. **Chunk** the text (900 characters, 150 overlap)
3. **Embed** the chunks (`paraphrase-multilingual-MiniLM-L12-v2`)
4. **Index** the vectors (FAISS, exact cosine search)
5. **Retrieve** the top-4 chunks for a question
6. **Generate** an answer from those chunks only (`Qwen2.5-3B-Instruct`)

## Document used

"Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks" (Lewis et al., 2020), arXiv:2005.11401.

## Run it

1. Click the **Open in Colab** badge above
2. Set Runtime → Change runtime type → **T4 GPU**
3. Run all cells (Runtime → Run all)

## Example

**Question:** Which retriever does RAG use?

**Answer:** RAG uses a retriever that is initialized using DPR's retriever, which uses retrieval supervision on Natural Questions and TriviaQA.

**Sources:**   [1] rag_paper.pdf p.5 (score 0.637)
  [2] rag_paper.pdf p.7 (score 0.565)
  [3] rag_paper.pdf p.2 (score 0.442)
  [4] rag_paper.pdf p.9 (score 0.415)

## Limitations

- Answers depend on retrieval quality, so a wrong passage can lead to a wrong answer.
- A small 3B model can misread context, so check answers against the cited pages.
- Works best on text-based PDFs; scanned PDFs and complex tables need extra handling.

## Tools

PyMuPDF, Sentence Transformers, FAISS, Hugging Face Transformers, PyTorch
