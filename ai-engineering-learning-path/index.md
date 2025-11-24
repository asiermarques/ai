# AI Engineering Personal Learning Path

## [1. Prompt writing](1-prompt-writing.md)



## [2. Context Engineering](2-context-engineering.md)



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

