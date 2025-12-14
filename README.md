# Secure Code Generation with Multi-Agent Collaboration

**Re-evaluation of INDICT Using SALLM and Introduction of Methodological Enhancements**

---

## Overview

This project revisits the reliability of multi-agent LLM frameworks for secure code generation.
We re-evaluate **INDICT**, a representative multi-agent framework, using **SALLM**, a vulnerability-grounded security evaluation pipeline based on static and dynamic analysis.

Our analysis reveals that INDICT’s originally reported security performance was **overstated due to its reliance on LLM-based evaluators**.  
Based on this finding, we introduce methodological enhancements to INDICT—most notably **step-based planning** and **step-level security notes**—to enforce more disciplined reasoning and targeted critique throughout the generation process.

Experiments across two models demonstrate that the revised framework:
- Eliminates functional performance degradation observed in the original design
- Achieves higher functional correctness and security robustness
- Improves combined functional-and-secure success rates

---

## Introduction

Large Language Models (LLMs) are increasingly used for code generation, including security-sensitive tasks.  
While recent multi-agent frameworks aim to improve reliability by distributing roles (planning, generation, critique), **how security is evaluated** remains a critical concern.

INDICT reports improved security and helpfulness through internal dialogues among agents.  
However, its original evaluation relies on **another LLM acting as a security evaluator**, raising concerns about validity and overestimation of real-world safety.

To address this issue, this work applies **SALLM**, a systematic security evaluation framework, to reassess INDICT-generated code under vulnerability-grounded criteria.

---

## Background

### INDICT: Code Generation with Internal Dialogues of Critiques

INDICT improves code generation through iterative interaction among:
- **Actor**: generates code
- **Executor**: executes and tests code
- **Critics**: review security and helpfulness

Although this design enhances reasoning and refinement, the original study evaluates security using **LLM-as-an-evaluator**, which may fail to detect practical vulnerabilities.

### SALLM: Security Assessment of Generated Code

SALLM is a framework designed to systematically evaluate whether LLMs generate secure code.  
It uses:
- A curated dataset of security-centric Python prompts
- **CodeQL-based static analysis**
- **Docker-based dynamic test execution**

This enables detection of concrete vulnerabilities rather than relying on functional correctness or subjective LLM judgments.

---

## Methods and Results

### ① Re-evaluating INDICT with SALLM

We reassess INDICT-generated code using SALLM, replacing the original LLM-as-evaluator approach with:
- CodeQL static rules
- Containerized dynamic testing

This provides a **more practical and vulnerability-grounded measurement** of security properties.

The reassessment reveals a substantial gap between previously reported “safety/helpfulness” metrics and actual vulnerability-based results.

---

### ② Methodological Enhancements to INDICT

To mitigate these limitations, we revise INDICT with the following enhancements:

- **Step-based Planning Layer**
  - Before code generation, the system produces a functional *Step Plan*
- **Step-level Security Notes**
  - Security considerations are explicitly attached to each step
- **Prompt Redesign**
  - Actor writes code strictly following the Step Plan
  - Safety/Helpful critics perform step-aligned reviews against corresponding security notes

These changes enforce structured reasoning and focused security critique throughout the generation process.

---

### ③ Experimental Comparison

We evaluate three approaches:
- Direct generation
- Original INDICT
- Revised INDICT

Experiments are conducted on two models.  
Relative to Original INDICT, the revised framework consistently improves:
- Functional correctness
- Security robustness
- Combined functional-and-secure success

Notably, the revised design eliminates the functional degradation observed in the original INDICT and surpasses direct generation, demonstrating that **integrating step-level planning and security reasoning strengthens reliability without sacrificing performance**.

---

## Conclusions

This work demonstrates that:
- LLM-based evaluators can overestimate the security of generated code
- Vulnerability-grounded evaluation is necessary for trustworthy assessment
- Explicit step planning and security considerations can meaningfully improve both functionality and security in multi-agent LLM systems

Overall, the results suggest that **incorporating structured reasoning and security-aware constraints may help multi-agent code generation systems produce code that is both functional and secure**.

---

## References

1. H. Le, Y. Zhou, C. Xiong, S. Savarese, and D. Sahoo,  
   *INDICT: Code Generation with Internal Dialogues of Critiques for Both Security and Helpfulness*,  
   NeurIPS 2024.

2. M. L. Siddiq, J. C. da Silva Santos, S. Devareddy, and A. Muller,  
   *SALLM: Security Assessment of Generated Code*,  
   ASE Workshops 2024.

---
