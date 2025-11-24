# AI Engineering Personal Learning Path

## [1. Prompt writing](1-prompt-writing.md)



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


## [3. Agents (with LangChain & Spring AI integration points)](3-agents-learning-path.md)


## [4. Memory Management](4-memory-management.md)


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

