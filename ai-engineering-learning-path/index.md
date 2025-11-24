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


## 4. Agents (with LangChain & Spring AI integration points)

### Agent Architecture
- **Agent Definition**
  - Clear task boundaries
  - Explicit goals, constraints, and allowed behaviors
  - Guardrails for reasoning and execution
  - **LangChain:** LCEL (LangChain Expression Language) to define declarative agent flows.
  - **Spring AI:** configuration-driven agents via Spring configuration (properties/beans) and Java abstractions.

- **Agent Loop Design**
  - Plan → Act → Observe → Reflect → Repeat
  - Interruptibility (stop conditions)
  - Step limits to avoid runaway behavior
  - Self-checks at each iteration
  - **LangChain:** Agent Executors, ReAct-style agents, Plan-and-Execute agents.
  - **Spring AI:** agent-like flows implemented as Spring services calling AI models and tools in orchestrated methods.

- **Role & Capability Assignment**
  - Single-agent vs. multi-agent setups
  - Specialized vs. general-purpose roles
  - Capability routing based on task type
  - **LangChain:** multi-agent orchestration, router chains for routing tasks.
  - **Spring AI:** different `ChatClient` configurations / beans per role or capability.



### Tool & Skill Integration
- **Tool Use Policies**
  - When the agent should call a tool
  - Multi-tool fallback logic
  - Avoiding overuse of tools
  - **LangChain:** `Tool` / `StructuredTool` abstractions, `@tool` decorator.
  - **Spring AI:** tools exposed as Spring beans and wired into AI flows via method calls around the model.

- **Skill Invocation**
  - Selecting the right cognitive skill for each step
  - Switching between base-model reasoning and specialized skills
  - Composing reasoning through skill chaining
  - **LangChain:** Chains as reusable “skills” (RetrievalQA, summarization chains, translation chains, etc.).
  - **Spring AI:** reusable service methods / components wrapping AI calls for specific capabilities (e.g. summarization, classification, code review).



### Planning & Reasoning
- **Structured Planning**
  - Breaking tasks into actionable steps
  - Long-term vs. short-term planning
  - Replanning after unexpected outcomes
  - **LangChain:** planner agents, LCEL pipelines with explicit steps.
  - **Spring AI:** orchestration implemented via Spring services / workflows (e.g. Spring Batch, Spring Integration, or custom orchestrators) that call AI in each stage.

- **Reflection Mechanisms**
  - Self-evaluation before continuing loops
  - Detecting failed assumptions
  - Corrective actions on faulty reasoning
  - **LangChain:** self-critique / self-correction chains, reflection patterns.
  - **Spring AI:** explicit “reflection” steps coded as additional AI calls that review previous outputs.

- **Task Decomposition**
  - Dynamic splitting of complex tasks
  - Delegating subproblems to other agents
  - Maintaining coherence across steps
  - **LangChain:** task-decomposition chains, router chains.
  - **Spring AI:** decomposition implemented in Java/Kotlin logic, delegating to different AI-powered components.



### Safety & Control
- **Safety Rails**
  - Allowed action lists
  - Forbidden operations
  - Sandbox execution for risky actions
  - **LangChain:** guarded tools, pre-checks before tool execution.
  - **Spring AI:** Spring Security, validation layers, and policy checks around AI and tool-invoking services.

- **Permission Model**
  - Granular access to tools, data, and APIs
  - Escalation requests for higher permissions
  - Revocation and expiration of permissions
  - **LangChain:** permission logic in tool wrappers / custom middleware.
  - **Spring AI:** permission/business rules via Spring Security, method-level security, and scoped beans.

- **Autonomy Limits**
  - Maximum number of reasoning steps
  - Maximum depth of tool/action chains
  - Cost ceilings per execution
  - **LangChain:** max iterations in Agent Executors, callbacks to monitor cost.
  - **Spring AI:** limits implemented via configuration, interceptors or circuit breakers (Resilience4j / Spring Cloud).



### Observability & Monitoring
- **Execution Tracing**
  - Log each reasoning step
  - Log each tool invocation and parameters
  - Correlate logs across multi-agent workflows
  - **LangChain:** LangSmith tracing and run trees.
  - **Spring AI:** standard Spring observability stack (Micrometer, logs, traces) + custom logging around AI calls.

- **Metrics**
  - Success rate
  - Error rate
  - Cost per task
  - Average reasoning steps
  - Time-to-completion
  - **LangChain:** LangSmith metrics and dashboards.
  - **Spring AI:** Micrometer metrics, Prometheus/Grafana, etc.

- **Anomaly Detection**
  - Detect loops, stalls, or runaway behavior
  - Spot incorrect tool usage
  - Alert when tasks exceed thresholds
  - **LangChain:** custom callbacks, guards, and anomaly handlers.
  - **Spring AI:** Spring-based monitoring + alerting rules (e.g., via Spring Boot Actuator, Prometheus alerts).



### Error Recovery & Robustness
- **Retry Logic**
  - Intelligent retries for recoverable errors
  - Escalate to another agent or tool on repeated failure
  - **LangChain:** retry wrappers, `Runnable.retry()`, error-handling chains.
  - **Spring AI:** Spring Retry / Resilience4j policies over AI calls and tool interactions.

- **Fallback Strategies**
  - Use safer or cheaper tools as alternatives
  - Short-circuit reasoning when confidence is low
  - **LangChain:** fallback chains, router chains with backup routes.
  - **Spring AI:** multiple AI providers / models configured and selected based on errors or cost.

- **Human Handoff**
  - Trigger human-in-the-loop review
  - Provide a clear state snapshot
  - Resume workflows after human intervention
  - **LangChain:** patterns for human approval steps integrated via callbacks or external UI.
  - **Spring AI:** handoff to human via standard Spring web flows, queues, or workflow engines (e.g. Camunda, Temporal).


### Multi-Agent Systems
- **Collaboration Models**
  - Coordinator + specialists
  - Peer-to-peer reasoning
  - Negotiation between agents
  - **LangChain:** multi-agent patterns, supervisor agents.
  - **Spring AI:** multiple AI-enabled services acting as independent agent roles.
  - **LangGraph:** orchestrating structured collaboration between agents with explicit state transitions.

- **Communication Protocols**
  - Structured message passing
  - Task assignment and status updates
  - Conflict resolution mechanisms
  - **LangChain:** chat message abstractions, agent message protocol.
  - **Spring AI:** Spring Messaging / events / RPC between agent services.
  - **LangGraph:** graph-based routing of messages between nodes (agents), ensuring deterministic flow.

- **Shared State & Memory**
  - Multi-agent shared context
  - Local vs. global state boundaries
  - Consistency across agent steps
  - **LangChain:** limited shared memory via external stores.
  - **Spring AI:** explicit state stored in DB / cache managed by Spring services.
  - **LangGraph:** built-in stateful graph nodes with history, snapshots, and resumable execution.

- **Emergent Behavior Control**
  - Prevent agent drift
  - Avoid over-coordination loops
  - Constraint-aware multi-agent planning
  - **LangChain:** supervisor agents controlling other agents.
  - **Spring AI:** enforcing constraints with rules/validation layers in the orchestration layer.
  - **LangGraph:** guardrails embedded in graph edges + policies that block unsafe or cyclical paths.

- **Workflow & Execution Engine**
  - Deterministic execution order
  - Resumability / check-pointing
  - Long-running processes
  - **LangChain:** LCEL pipelines for simple workflows.
  - **Spring AI:** Spring Batch / Spring Integration / state workflows outside AI layer.
  - **LangGraph:** full workflow engine for agents, with node-by-node execution, retries, and state recovery.



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


## 5. Evaluation & Governance

### Model-Level Evaluation
- **Accuracy & Relevance**
  - Compare model outputs against ground truth or expert answers.
  - Measure task completion success.

- **Hallucination Rate**
  - Detect fabricated facts or unsupported reasoning.
  - Evaluate grounding quality (truthfulness vs. creativity).

- **Consistency Across Runs**
  - Ensure repeatability under identical inputs.
  - Track variability with and without temperature changes.

- **Adversarial Robustness**
  - Test model resistance to prompt injection or jailbreaks.
  - Evaluate safe-mode performance under hostile inputs.



### RAG Evaluation
- **Retrieval Precision & Recall**
  - Measure relevance of retrieved documents.
  - Detect under-retrieval (missing info) and over-retrieval (noise).

- **Coverage Tests**
  - Ensure all key facts exist in the retrieved context.
  - Validate that chunking and indexing are effective.

- **Grounding Checks**
  - Verify that generated answers strictly reference retrieved text.
  - Highlight ungrounded claims.

- **End-to-End Task Evaluation**
  - Score quality of the final output, not only retrieval.
  - Use human or synthetic judges for scoring.



### Agent Evaluation
- **Agent Success Rate**
  - How often the agent completes tasks correctly.
  - Track results by task type and complexity.

- **Execution Efficiency**
  - Average reasoning steps.
  - Time-to-completion.
  - Cost per task.

- **Error Classification**
  - Tool misuse
  - Planning failures
  - Reflection errors
  - Infinite loops / runaway agents

- **Drift Detection**
  - Detect changes in agent behavior over time.
  - Identify emerging unsafe or inefficient patterns.



### Behavioral Evaluation (Safety & Ethics)
- **Harmful Output Detection**
  - Bias
  - Toxicity
  - Safety policy violations

- **Alignment Testing**
  - Whether the model or agent follows rules and constraints.
  - Stress-test with edge cases.

- **Privacy Leakage Tests**
  - Check for memorization of sensitive inputs.
  - Validate that memory systems don’t leak old data.

- **Policy Compliance**
  - GDPR / internal compliance rules
  - Data minimization checks



### Governance & Control
- **Auditability**
  - Full logs of reasoning steps, tool calls, and decisions.
  - Traceability from input → agent → output.

- **Version Control**
  - Track versions of:
    - Prompts
    - Tools
    - Skills
    - Memory schemas
    - Agent configurations

- **Approval Workflow**
  - Review changes to agents, tools, skills before deployment.
  - Human in the loop for high-risk workflows.

- **Access Control**
  - Granular permissions for tools, APIs, datasets.
  - Escalation procedures for restricted actions.

- **Guardrail Enforcement**
  - Automatic rejection of unsafe outputs.
  - Policies for allowed / forbidden behaviors.
  - Runtime monitors for violations.



### Monitoring & Observability
- **Operational Metrics**
  - Latency
  - Error rates
  - Model usage
  - Cost per user / per job

- **Agent Telemetry**
  - Number of steps per task
  - Tool usage statistics
  - Failure patterns

- **Alerting**
  - High error rates
  - Unexpected tool usage
  - Model drift indicators

- **Longitudinal Tracking**
  - Track model and agent performance over weeks/months.
  - Early detection of regressions.



### Evaluation Infrastructure (Tech Examples)
- **LangSmith** (LangChain) – tracing, evaluation harness, datasets  
- **OpenAI Evals** – standardized benchmarking  
- **DeepEval** – automated eval suite for LLM outputs  
- **RAGA** – evaluation toolkit for RAG systems  
- **Weights & Biases** – experiment tracking and model monitoring  
- **Custom Eval Pipelines** – for domain-specific tasks  



### Governance Frameworks (Industry-Level)
- **NIST AI Risk Management Framework**
- **ISO/IEC 42001 (AI Management System Standards)**
- **GDPR compliance for AI**
- **Internal policy guidelines (permissions, red-teaming, approvals)**

