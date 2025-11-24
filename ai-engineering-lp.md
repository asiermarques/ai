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



## 2. Context Engineering

### RAG

- **Retrieval Quality**
  - High-recall vs. high-precision tradeoffs
  - Semantic vs. keyword vs. hybrid search
  - Top-k vs. dynamic retrieval thresholds
  - Evaluating noise vs. relevance

- **Chunking Strategies**
  - Semantic chunking (LLM-aware)
  - Overlapping windows to preserve context
  - Adaptive chunk sizes based on document type
  - Sentence/paragraph boundary respect

- **Re-ranking**
  - Cross-encoder re-ranking
  - LLM-based relevance scoring
  - Penalizing redundancy
  - Domain-specific ranking boosts

- **Context Filtering**
  - Remove irrelevant or noisy chunks
  - Deduplicate overlapping information
  - Apply metadata filters (author, type, timestamp)
  - Enforce max-context size budgets

- **Query Transformation**
  - Expand/correct ambiguous queries
  - Semantic query rewriting
  - Multi-query generation (n variations)
  - Intent classification before retrieval

- **Grounding & Fact Checking**
  - Verify retrieved facts against source docs
  - Highlight conflicts or contradictions
  - Confidence scoring
  - Reject ungrounded LLM responses

- **Multi-step Retrieval**
  - Retrieve → read → refine → retrieve again
  - Iterative narrowing of context
  - Agent-based exploration of sources
  - Multi-agent voting for relevance

- **Evaluation (Evals for RAG)**
  - Retrieval precision/recall benchmarks
  - Coverage tests (missing info)
  - Hallucination detection evals
  - End-to-end task performance scoring


### Tools

- **Model Context Protocol (MCP)**
  - Standardized interface between models and tools
  - Auto-discovery of capabilities
  - Structured request/response format
  - Tool permission negotiation
  - Vendor-agnostic integration layer

- **Tool Schemas (Inputs/Outputs)**
  - Strong typing of parameters
  - Validation rules for inputs
  - Clear definition of side effects
  - Idempotency requirements
  - Error format standardization

- **Permission Scopes**
  - Least-privilege access for each tool
  - Read vs. write vs. destructive actions
  - Temporary vs. persistent permissions
  - Sensitive-data separation
  - Auditable permission changes

- **Tool Selection Logic**
  - Matching task → tool based on intent
  - Multi-tool fallback logic
  - Prioritization (cheapest, safest, fastest)
  - Avoiding tool misfires (incorrect tool usage)
  - Self-checks before calling a tool

- **Action Validation**
  - Pre-execution validation (sanity checks)
  - Post-execution verification (did it work?)
  - Result conformity to schema
  - Detecting unintended side effects
  - Rejecting unsafe or incomplete outputs

- **Observability & Logging**
  - Log each tool invocation with parameters
  - Latency, cost, and success metrics
  - Tracing across tool chains
  - Agent/tool correlation IDs
  - Monitoring anomalous tool usage

- **Error Recovery / Retries**
  - Retry policies (exponential backoff, max retries)
  - Fallback tools or alternative strategies
  - State rollback mechanisms
  - Human handoff when recovery fails
  - Classification of recoverable vs. fatal errors

- **Safety & Guardrails for Tools**
  - Allowlist of safe actions
  - Blocklist of forbidden operations
  - Rate limits & quotas
  - Safe-mode execution for high-risk tools
  - Continuous security auditing


### Anthropic Skills
- **Capability Modularization**
- **Skill Invocation Logic**
- **Skill Chaining**
- **Specialization vs. General Reasoning**
- **Reusability Across Agents/Models**
- **Safety Boundaries Per Skill**
- **Versioning & Governance of Skills**


## 3. Agents (with LangChain integration points)

### Agent Architecture
- **Agent Definition**
  - Clear task boundaries, goals, constraints.
  - LangChain: *LCEL (LangChain Expression Language)* para definir flujos declarativos.

- **Agent Loop Design**
  - Plan → Act → Observe → Reflect.
  - LangChain: *Agent Executors*, *Plan-and-Execute Agent*, *ReAct Agent*.

- **Role & Capability Assignment**
  - Single-agent vs multi-agent roles.
  - LangChain: *Multi-agent workflows*, *Agent orchestration*.



### Tool & Skill Integration
- **Tool Use Policies**
  - When to call tools, fallback logic.
  - LangChain: *Tool interface*, `@tool` decorator, *StructuredTool*, *Bound tools*.

- **Skill Invocation**
  - Switch between base model reasoning and specialized capabilities.
  - LangChain: *Chains* como “skills”: SummarizationChain, RetrievalQAChain, TranslationChain, etc.


### Planning & Reasoning
- **Structured Planning**
  - Decompose tasks, build actionable steps.
  - LangChain: *Planner agents*, *ReAct + LCEL pipelines*.

- **Reflection Mechanisms**
  - Self-evaluation per iteration.
  - LangChain: *Self-critique prompts*, *Self-correction chains*.

- **Task Decomposition**
  - Split complex tasks dynamically.
  - LangChain: *Task Decomposition Chain*, *RouterChain*.



### Safety & Control
- **Safety Rails**
  - Allowed/forbidden actions.
  - LangChain: *Tool permissions*, *guarded tool wrappers*, *sandboxed tools*.

- **Permission Model**
  - Granular access to tools and data.
  - LangChain: *Tool authentication/authorization middleware*.

- **Autonomy Limits**
  - Max reasoning steps



## 4. Memory Management

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
