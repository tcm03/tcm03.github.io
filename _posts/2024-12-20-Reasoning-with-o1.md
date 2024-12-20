---
layout: post
title: "Reasoning with O1"
date: 2024-12-20
categories: today-i-learn
---

# Reasoning with O1

Link: [Reasoning with O1](https://www.deeplearning.ai/short-courses/reasoning-with-o1/)

## Outline
- Introduction to the o1 Models
- Prompting o1
- Planning with o1
- Coding with o1
- Reasoning with Images
- Meta-Prompting

## 1. Introduction to o1

- Reasons through complex tasks
- Use CoT to explore all possible paths and verify its answers
- Require less context and prompting in order to produce an answer
e.g. Identify problem and solution space -> Develop hypotheses -> Test hypotheses -> Reject ideas and backtrack -> Identify most promising path

Completion tokens
- Two distinct categories of completion tokens
    - Reasoning tokens
        - count toward context length and price that you pay
        - not passed from one turn to the next (need to do this ourselves)
    - Output tokens

- Verification in LLMs via Consensus/ Majority Vote (Large Language Monkey paper)
    - Generate a bunch of solutions and take the most common one: similar to sampling at low temperature (flatlines before 100 samples)

- How does OpenAI o1 work? (Wei et al. NeurIPS-2022)
    - Uses large-scale RL to generate a CoT before answering
    - CoT is longer and high-quality than what is attained via prompting
    - CoT contains behavior like:
        - Error correction
        - Try multiple strategies
        - Break down problems into smaller steps
    - Abstract reasoning: emergent capabilities (different from maths, coding, ...)
