# AI Engineering Personal Learning Path

## 1. Prompt Engineering

### Task & Framing
- **Task Framing** – define the task precisely.
- **Role Assignment** – specify the model’s role.
- **Output Schema** – enforce structured output (JSON, tables, lists).

### Context & Information Flow
- **Context Injection** – provide only relevant context.
- **Few-shot Examples** – include high-quality input/output examples.
- **Meta-instructions** – specify how to use context, ask questions, or handle errors.

### Reasoning & Execution
- **Step-by-step Reasoning** – require explicit reasoning steps.
- **Task Decomposition** – break tasks into substeps.
- **Delegation Prompts** – decide when to use tools or other agents.

### Safety, Quality & Validation
- **Guardrails** – define allowed/forbidden behaviors.
- **Validation Prompts** – make the model check its own output.
- **Self-Eval Criteria** – evaluate responses against specific criteria.

### Reusability & Modularity
- **Modular Prompts** – reusable prompts for analysis, synthesis, verification.

---

## 2. Context Engineering

### RAG
- **Retrieval Quality**
- **Chunking Strategies**
- **Re-ranking**
- **Context Filtering**
- **Query Transformation**
- **Grounding & Fact Checking**
- **Multi-step Retrieval**
- **Evaluation (Evals for RAG)**

### Tools
- **Model Context Protocol (MCP)**
- **Tool Schemas (Inputs/Outputs)**
- **Permission Scopes**
- **Tool Selection Logic**
- **Action Validation**
- **Observability & Logging**
- **Error Recovery / Retries**
- **Safety & Guardrails for Tools**

### Anthropic Skills
- **Capability Modularization**
- **Skill Invocation Logic**
- **Skill Chaining**
- **Specialization vs. General Reasoning**
- **Reusability Across Agents/Models**
- **Safety Boundaries Per Skill**
- **Versioning & Governance of Skills**

---

## 3. Memory Management

### Models
- **Semantic & Episodic Memory**  
  Stores factual knowledge and lived interaction history.
- **Salience & Recency Weighting**  
  Prioritizes important or recent memories for better retrieval.
- **Automatic Decay**  
  Removes outdated/low-value memories to prevent drift.
- **Multiple Embeddings (optional)**  
  Captures different semantic angles of a memory.
- **Explainable Recall Paths**  
  Shows why a memory was retrieved for transparency/debugging.

### Cognitive Operations
- **Pattern Clustering**  
  Groups similar memories to reduce noise.
- **Memory Consolidation**  
  Merges duplicates and strengthens consistent information.
- **Context Summaries**  
  Compresses interaction history into compact summaries.
- **Sector-aware Retrieval**  
  Retrieves only memories relevant to the task domain.
- **Associative Recall**  
  Connects memories across sectors to generate insights.

### Essential Additions
- **Memory Permissions**  
  Controls which agents/tools may access memory sectors.
- **Memory Versioning**  
  Tracks memory changes over time for audits.
- **Conflict Resolution**  
  Handles contradictory or competing memories.
- **Memory Validity Scoring**  
  Scores memories by reliability, freshness, and source quality.
