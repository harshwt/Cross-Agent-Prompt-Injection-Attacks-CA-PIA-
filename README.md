# Cross-Agent-Prompt-Injection-Attacks-CA-PIA-
Cross-LLM Infection explores a novel attack vector in multi-agent AI systems where malicious instructions propagate between trusted LLM agents via internal communication. 
The research exposes inter-model trust vulnerabilities and highlights the need for secure-by-design multi-agent architectures. 
Author: Harshwardhan Tiwari

Cross-LLM Infection: A Novel Attack Vector Exploiting Trust and Inter-Model Communication in Multi-Agent AI Systems

Author: Harshwardhan Tiwari
Category: C1 – Cybersecurity / AI Safety
Event: Inter-University Avishkar Research Convention 2025–26
Group No.: 64

📌 Overview
This research introduces Cross-LLM Infection, a previously underexplored attack vector in multi-agent AI systems where multiple Large Language Models (LLMs) collaborate through shared memory, summaries, and inter-agent communication. 
The work demonstrates how malicious instructions embedded in one agent’s output can propagate through trusted internal channels, ultimately compromising downstream agents without direct external interaction.
The study highlights a critical inter-model trust vulnerability, showing that failures arise not from weak LLM capabilities, but from system-level design assumptions where internal outputs are implicitly trusted.

 Motivation & Problem Statement:
Modern AI systems increasingly rely on multi-agent architectures to perform complex tasks through coordination and delegation. These systems assume that:
Internal agent communications are safe by default
Summaries and shared memory are trustworthy
Validation is primarily needed only for external inputs
This research challenges those assumptions by demonstrating how internal trust itself becomes the attack surface, enabling cascading failures across agents.

 Key Concepts:
Cross-LLM Infection
A scenario where:

One LLM generates a malicious but well-structured output
The output passes through summarization or transformation
Downstream LLMs interpret it as a valid system-level command
The entire system becomes compromised without explicit prompt injection at each step

 Vulnerability Background:
The research is grounded in a Cybersecurity Vulnerability Hierarchy, illustrating how:
Hidden Weaknesses – Adversarial instructions embedded in untrusted data
Root Vulnerabilities – Lack of validation for internal outputs
Visible Symptoms – System-level sabotage, incorrect actions, or operational disruption
These vulnerabilities accumulate and escalate, culminating in observable failures.

 Research Objectives:
The study explores multiple dimensions of Cross-LLM Infection:
Prompt Propagation Analysis – How malicious intent survives summarization
Experimental Testing – Simulated multi-agent pipelines
Defense Evaluation – Assessing current mitigation strategies
Attack Classification – Categorizing infection stages
Security-by-Design Measures – Proposing architectural safeguards

 Methodology:
A two-agent LLM pipeline was designed and tested:

                       ┌───────────────────────────────────── ┐
                       │        External Untrusted Data       │
                       │  (e.g., webpage content / input text)│
                       └─────────────────────────────────────┘
                                        |
                                        ▼
                          ┌─────────────────────────────┐
                          │         LLM1 (Summarizer)   │
                          │ - Reads untrusted data      │
                          │ - Produces a summary        │
                          │ - MAY contain hidden        │
                          │   embedded instructions     │
                          └─────────────────────────────┘
                                        |
                                        ▼
                         ┌──────────────────────────────┐
                         │   Summary with hidden cmds    │
                         │   (treated as output text)    │
                         └──────────────────────────────┘
                                        |
                                        ▼
                          ┌─────────────────────────────┐
                          │      LLM2 (Executor)        │
                          │ - Receives the summary      │
                          │ - Trusts it as a command    │
                          │ - Executes hidden directives│
                          └─────────────────────────────┘
                                        |
                                        ▼
                         ┌──────────────────────────────┐
                         │      Executed actions        │
                         │ (possibly malicious/unsafe)  │
                         └──────────────────────────────┘


The experiment evaluates whether malicious instructions:
-Survive summarization
-Bypass validation layers
-Trigger harmful downstream actions

Results & Findings:
Infection Lifecycle
Layer	Description	Observation
Layer 1: Upstream Injection	Attacker inserts structured authoritative payload	Injection persists due to recency bias
Layer 2: Midstream Failure	Sanitizer follows injected instruction	Contamination spreads
Layer 3: Downstream Execution	Trusted agent executes payload	System fully compromised

Key Insights:
Multi-agent LLM systems are highly vulnerable when internal outputs are trusted without verification
This is an inter-trust model vulnerability, not a prompt-engineering flaw
Malicious instructions propagate because agents are designed to cooperate and trust each other
Standard defenses focus on external input sanitization, leaving internal channels exposed

 Conclusion:
Cross-LLM Infection reveals a fundamental architectural weakness in collaborative AI systems. As LLMs increasingly act as autonomous agents, internal communication must be treated as untrusted by default.

The study emphasizes that:
-Trust boundaries must be explicitly defined
-Internal outputs require validation and isolation
-Security must be embedded at the system design level, not patched at the prompt level


 Impact & Future Work:
This research contributes to:
-AI safety
-Secure multi-agent system design
-Prompt injection and indirect attack mitigation

Future work includes:
-Automated detection of malicious intent in summaries
-Trust-boundary enforcement mechanisms
-Secure inter-agent communication protocol
