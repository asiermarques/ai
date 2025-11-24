# AI Engineering Personal Learning Path

## 1. Prompt "Engineering"

```mermaid
---
config:
  layout: tidy-tree
---

mindmap
  root((Prompt Writing))
      Task & Framing
        Task Framing
        Role Assignment
        Output Schema
  
      Context & Information Flow
        Context Injection
        Few-shot Examples
        Meta-instructions
  
      Reasoning & Execution
        Step-by-step Reasoning
        Task Decomposition
        Delegation Prompts
  
      Safety, Quality & Validation
        Guardrails
        Validation Prompts
        Self-Eval Criteria
  
      Reusability & Modularity
        Modular Prompts

    
```

## 2. Context Engineering
```mermaid
---
config:
  layout: tidy-tree
---

mindmap
  root((Context Engineering))
      (RAG)
        Retrieval Quality
        Chunking Strategies
        Re-ranking
        Context Filtering
        Query Transformation
        Grounding & Fact Checking
        Multi-step Retrieval
        Evaluation (Evals for RAG)
  
      (Tools)
        Model Context Protocol (MCP)
        Tool Schemas (Inputs/Outputs)
        Permission Scopes
        Tool Selection Logic
        Action Validation
        Observability & Logging
        Error Recovery / Retries
        Safety & Guardrails for Tools
  
      (Anthropic Skills)
        Capability Modularization
        Skill Invocation Logic
        Skill Chaining
        Specialization vs. General Reasoning
        Reusability Across Agents/Models
        Safety Boundaries Per Skill
        Versioning & Governance of Skills
    
```

## 3. Memory Management

```mermaid
---
config:
  layout: tidy-tree
---
mindmap
  root((Memory Management — Key Concepts 2025))

    Models
      Semantic & Episodic Memory
        Desc("Stores factual knowledge (semantic) and lived interactions/events (episodic).")
      Salience & Recency Weighting
        Desc("Prioritizes important or recent memories for higher-quality retrieval.")
      Automatic Decay
        Desc("Gradually removes outdated or low-value memories to prevent drift.")
      Multiple Embeddings (optional)
        Desc("Uses several embeddings to capture different semantic angles of the same memory.")
      Explainable Recall Paths
        Desc("Shows why a memory was retrieved, improving transparency and debugging.")

    Cognitive Operations
      Pattern Clustering
        Desc("Groups similar memories to reduce noise and enhance retrieval.")
      Memory Consolidation
        Desc("Merges duplicates and strengthens consistent information.")
      Context Summaries
        Desc("Compresses interaction history into compact, efficient summaries.")
      Sector-aware Retrieval
        Desc("Retrieves only memories relevant to the task’s sector (technical, contextual, personal, etc.).")
      Associative Recall
        Desc("Connects related memories across sectors to generate useful insights.")

    Essential Additions
      Memory Permissions
        Desc("Controls which agents or tools can access specific memory sectors.")
      Memory Versioning
        Desc("Tracks changes in memories over time for audits and rollbacks.")
      Conflict Resolution
        Desc("Detects and resolves contradictory or competing memories.")
      Memory Validity Scoring
        Desc("Scores memories by reliability, freshness, and source quality.")
```

