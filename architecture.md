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
