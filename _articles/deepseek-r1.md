---
layout: distill
authors: 
    - name: Bumjin Park
      affiliations:
        name: KAIST
bibliography: all.bib
giscus_comments: false
disqus_comments: false
date: 2024-12-29
featured: true
img: assets/img/alice02.png
title: 'Thoughts on DeepSeek-R1'
category: 'AI'
description: 'What I think about DeepSeek-R1 (Reasoning-based LLMs)'
_styles: >
    .table {
        padding-top:200px;
        margin-bottom: 2.5rem;
        border-bottom: 2px;
    }
    .p {
        font-size:20px;
    }
    .styled-image {
        border-radius: 15px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        margin: 20px auto;
        transition: transform 0.3s ease;
        display: block;
    }
    .styled-image:hover {
        transform: scale(1.2);
    }

---


# XAI For Reasoning-Based LLMs

The transition from **SFT** to an **RL-based** learning paradigm in LLMs will open new opportunities for XAI, improving robust reasoning and reducing harmful outputs.

The paradigm of training AI models is shifting from **supervised fine-tuning (SFT)** to **reinforcement learning (RL)**, particularly for reasoning. This shift represents a fundamental change—moving from merely providing answers to teaching AI how to reason and derive answers independently.

I believe this transition may drive advancements in existing explanation methods (e.g., LRP, saliency, decision boundaries, and Shapley values).

## Core Differences in Explanation  
The key difference lies in the **manifold** used for explanation. Models trained with **SFT** focus on **internal representations**, assuming that amortized neurons encapsulate concepts and circuits dedicated to constructing outputs. Thus, most **mechanistic interpretation** and **XAI methods** have primarily targeted neurons.

In contrast, **LLMs trained with RL**—learning policies for reasoning and decision-making—utilize structured **chain-of-thought** processes (internal tokens or hidden representations). This shift may redefine the target of **explanation**, moving from an input-output approach to a **sequential analysis** of **token interactions**. While sequential input-output cases are more complex, explanations could become clearer as reasoning steps explicitly involve chain-of-thought processes.

Consider these two cases:  
1. *Based on the user information, he is guilty.*  
2. *Based on the user information, he has ... and ... . Additionally, he did ... . Therefore, he is guilty.*  

The second case provides a **more transparent reasoning process**, making it easier to understand how the conclusion was reached.

Developing **traditional XAI methods** remains crucial. Explaining reasoning steps through **generated tokens alone** is limited, as the intentions of **black-box LLMs** remain unclear. Unlike token-based explanations, **representation-level XAI** can provide **deeper insights** into model behavior.

Some researchers may explore XAI methods applied to **reasoning steps** to enhance **robust generation** and mitigate **harmful responses**.

---

## Advanced Thoughts: LLMs Are Not Just a Set of Neurons  

Think of LLMs as **humans**—they reveal their **thoughts** by generating **tokens**.

Initially, I thought LLMs were just machines that provided answers. However, insights from **LLM researchers** suggest that these models engage in **strategic reasoning**, rather than merely executing predefined computations.

This perspective raises concerns that **LLMs**, even those trained with **SFT**, might **intentionally deceive users**. Some AI researchers argue that AI exhibits **fake alignment**—pretending to align with human values while internally operating differently. This view frames **AI models** as **entities** that reason strategically.

With the success of **DeepSeek-R1**—demonstrating that RL outperforms SFT for training LLMs—I now see LLMs as **thinking entities**, not just **engineered neurons**.

Furthermore, LLMs generate a **sequence of thoughts**, resembling **Plato’s theory of recollection**—the idea that **knowledge** is not simply **acquired** but rather **recalled** from **latent structures** within the mind. Similarly, LLMs do not merely **retrieve predefined answers** but **construct reasoning paths**, progressively **revealing knowledge** as if rediscovering it.

With these advancements, LLMs appear to be acquiring more **human-like properties**, reinforcing the idea that they are not just **static models** but **dynamic reasoning agents** capable of structured thought.