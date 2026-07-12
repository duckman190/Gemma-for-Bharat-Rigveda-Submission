Dataset File too large to upload extracted(25MB limit reached)

Overview: Rigveda HyDE RAG Bot (Viprah Vadanti)

This notebook implements a state-of-the-art Retrieval-Augmented Generation (RAG) pipeline designed to serve as a Vedic Scripture scholar. Named "VIPRAH VADANTI", the system allows users to interactively query the ancient text of the Rigveda and receive highly precise, cited answers directly rooted in the scripture.Key Technical HighlightsPowered by Google Gemma 3

The project leverages the Gemma 3 1B IT (Instruction-Tuned) model as its primary reasoning and generation engine. Despite its lightweight and efficient size (1 Billion parameters), Gemma 3 excels at:
Contextual Synthesis: Adhering strictly to provided scriptural context while blocking outside hallucinations.

Multilingual Translation: Translating complex Sanskrit verses directly into modern languages (like Hindi, French, Spanish, etc.) by leveraging existing English scholarly text as context.Advanced HyDE RAG Pipeline
Rather than relying on basic vector search which can suffer from keyword mismatch, this notebook introduces a Hypothetical Document Embeddings (HyDE) workflow combined with semantic search:

Embedding Model: Uses all-MiniLM-L6-v2 to vectorize and map text into a semantic space.


The RAG Workflow:
        User Query: The user inputs a natural language question about the Rigveda.
        Hypothetical Verse: Gemma generates a "hypothetical" English verse that would ideally answer the query.
        Vector Search: The embedding of this generated hypothetical text is calculated and cross-referenced against the precomputed embeddings of 10,402 original Rigveda verses.
        Context Retrieval: The top-matching actual verses (Sanskrit, English, Mandala/Hymn metadata) are extracted.
        Grounded Generation: Gemma receives the true scripture as context, delivering a citation-aware response complete with Mandala, Hymn, and Verse markers.Production-Grade Safety and Security
        
Because Large Language Models are prone to prompt injection and rate abuse in public deployments, the notebook builds custom safety utilities directly into the pipeline:
       Prompt Injection Blocker: Regex-based filtering prevents users from bypassing instructions or utilizing standard "jailbreak" patterns.
       Input/Output Sanitization: Strips out structural markers, HTML tags, and malicious syntax to ensure clean interface outputs.
       Rate Limiting: Implements a token/call bucket mechanism to avoid model overloading during user hosting.Interactive Gradio Interface

The notebook wraps the entire system into a polished, front-end Gradio interface featuring two core operational modes:
      Seek Knowledge: The chatbot query terminal where users chat directly with Gemma to find scriptural answers.
      Read the Rigveda: A structured exploration deck allowing users to browse through Mandalas and Suktas manually, displaying Devanagari Samhita text, Padapatha transliterations, and triggering translations on demand.
