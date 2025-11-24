# 1. Prompt Writing

## Task & Framing
- **Task Framing** – define the task precisely.
- **Role Assignment** – specify the model’s role.
- **Output Schema** – enforce structured output (JSON, tables, lists).

## Context & Information Flow
- **Context Injection** – provide only relevant context.
- **Few-shot Examples** – include high-quality input/output examples.
- **Meta-instructions** – specify how to use context, ask questions, or handle errors.

## Reasoning & Execution
- **Step-by-step Reasoning** – require explicit reasoning steps.
- **Task Decomposition** – break tasks into substeps.
- **Delegation Prompts** – decide when to use tools or other agents.

## Safety, Quality & Validation
- **Guardrails** – define allowed/forbidden behaviors.
- **Validation Prompts** – make the model check its own output.
- **Self-Eval Criteria** – evaluate responses against specific criteria.

## Reusability & Modularity
- **Modular Prompts** – reusable prompts for analysis, synthesis, verification.
