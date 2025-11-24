# 2. Context Engineering

## RAG

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


## Tools

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


## Anthropic Skills
- **Capability Modularization**
- **Skill Invocation Logic**
- **Skill Chaining**
- **Specialization vs. General Reasoning**
- **Reusability Across Agents/Models**
- **Safety Boundaries Per Skill**
- **Versioning & Governance of Skills**
