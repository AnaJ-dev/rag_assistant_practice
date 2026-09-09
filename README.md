# Document RAG Assistant

An n8n RAG workflow that answers questions from a PDF employee handbook using vector retrieval and Gemini. Questions that cannot be answered from the retrieved context are routed to manual review.

## How It Works

1. Upload a PDF document.
2. Extract and split the document into chunks.
3. Create embeddings and store the chunks in a vector store.
4. Embed the user question and retrieve the most relevant chunks.
5. Aggregate the retrieved context and send it to Gemini.
6. Return a source-grounded answer when the information is found.
7. Route unanswered questions to a manual-review Data Table.

## Key Features

- PDF document ingestion
- Document chunking and embeddings
- Vector similarity retrieval
- Gemini-based question answering
- Source-grounded responses
- `FOUND` / `NOT_FOUND` handling
- Manual-review fallback for unanswered questions

## Example Tests

**Found**
- Meal allowance
- Annual leave entitlement
- Working abroad policy

**Not found**
- Company pension contribution percentage → routed to `needs_review`


# Workflow Architecture

```mermaid
flowchart TD

    subgraph DOCUMENT_STORAGE["Document storage"]
        A["Upload Document"] --> B["Store Document Vectors"]
        C["Embeddings -Embed Document Chunks"] --> B
        D["Split Document into Chunks"] --> E["Extract PDF Text"]
        E --> B
    end

    subgraph RETRIEVAL["Retrieve info from document"]
        F["Ask Question"] --> G["Set Question"]
        G --> H["Retrieve Relevant Text Chunks"]
        I["Embeddings - Embed Question"] --> H
        H --> J["Aggregate text"]
        J --> K["Basic LLM Chain"]
        L["Google Gemini Chat Model"] --> K
        K --> M{"If Answer Found?"}
        M -->|True| N["Format Answer for true"]
        M -->|False| O["Review Case For False"]
        O --> P["Manual Review"]
    end

    B -. "employee_handbook" .-> H
```
