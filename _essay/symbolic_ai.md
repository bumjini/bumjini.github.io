---
layout: distill
bibliography: all.bib
giscus_comments: false
disqus_comments: false
date: 2025-07-02
featured: true
background_color: rgb(246, 255, 248)
title: 'Towards Understanding Symbolic AI'
category: 'AI'
description: 'All the baselines and Results'
_styles: >
    .table {
        padding-top:200px;
        margin-bottom: 2.5rem
        border-bottom: 2px;
    }
    .p {
        font-size:20px;
        font-weight: 250;
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
    .td .th {
        font-size: 1.10rem;
        font-family: 'Times New Roman', Times, serif;
    }
---


## Towards Symbolic AI

With the rapid advancement of artificial intelligence, there is a growing interest in symbolic reasoning. This resurgence is particularly significant because humans tend to learn extensively by understanding, identifying, and forming relationships between symbols. Symbolic AI aims to model such processes by examining the relations among symbols and using formal systems—such as logical or probabilistic inference—to discover new symbolic connections.

However, a persistent challenge in symbolic AI lies in the complexity of integrating benchmarks and hypotheses that arise from the study of symbols into modern AI systems. Rather than being clearly defined and embedded, these symbolic components are often entangled within broader architectures. For instance, the grounding problem—how to ensure that symbols carry meaning—offers crucial insight into the semantics and relational structures of symbols, including metaphysical grounding. Analogical reasoning, another key area, involves mapping relationships between symbols metaphorically. This is exemplified by vector-based relational models, such as those found in WordNet or word embedding spaces. In such models, semantic relationships can be captured by vector arithmetic (e.g., the vector from *king* to *queen* can be applied to *gorilla* to yield a new conceptual direction): $P = P_{\text{gorilla}} + V_{\text{queen}}$. This illustrates how symbolic meaning can emerge through transformations in a vector space.

These approaches offer a path toward mapping abstract concepts to symbols. Prior AI systems have explored how internal vector representations may acquire meaning through learning processes (e.g., via toy models), contributing to a deeper understanding of how vectors encode and manipulate conceptual directions.

In contrast, humans have developed rich traditions of dealing with symbols, informed by centuries of philosophical, linguistic, and cognitive research. Symbolic AI can benefit from integrating these traditions, helping large-scale systems like LLMs to better handle symbolic reasoning. This, in turn, could lead to safer, more interpretable, and more efficient model architectures, improved algorithms, and more robust data representations.

Accordingly, the goal of this post is to provide a comprehensive overview of symbolic AI systems, exploring their foundations and offering insights into how they might evolve to support future research and practical applications.



## Two Branches of Symbolic AI 


<img src="https://d2acbkrrljl37x.cloudfront.net/bumjini-blog/study_post/symbolicAI_overview.png" width="100%" height="auto" class="styled-image"/>

### Symbol Grounding (Perception to Symbol Mapping) 

Harnad (1990) famously posed the symbol grounding problem:
“How can the meanings of words be grounded in anything other than other words?”

What are differences between the symbol grounding problem and classification tasks? (See the footnote<d-footnote> Symbol Grounding is about how symbols get their meaning, especially from the world and experience. Classification is about how systems assign labels to data, based on patterns in training data.</d-footnote>.)


<strong> Algorithm Examples </strong>

- **DeepProbLog** (Manhaeve et al., 2018) [[go below](#-algorithm-deepproblog)]: The input is processed by a neural predicate `digit(Img, Digit)`, which uses a neural network to produce probabilistic outputs. The error is computed after symbolic reasoning via Prolog, and only the neural network parameters are trained.

Symbolic logic systems must search over all possible instantiations of symbols, even when the rules are known.

- **Neuro-Symbolic Concept Learner (NS-CL, Mao, 2019)** [[go below](#-algorithm-ns-cl)]:  
  Given an image and a natural language question, the system first extracts object-level feature vectors from the image. These features are processed through various **neural operators** (e.g., `ShapeOf(obj)`, `ColorOf(obj)`) to generate **soft attribute estimates**. In parallel, the natural language question is parsed into a structured program represented in a **domain-specific language (DSL)**,  
  which defines a sequence of symbolic operations (e.g., Filter, Relate, Query).  The extracted soft facts—probabilistic evaluations of visual concepts—are then used as inputs to execute the **DSL program**. This execution is performed not by a traditional symbolic engine, but by a **quasi-symbolic executor**, also referred to as a **neuro-symbolic program executor**. This executor evaluates the symbolic program over soft neural outputs,  
  enabling differentiable reasoning and end-to-end learning.

- **LOGIC-LM** (Pan et al., 2023) [[go below](#-algorithm-logic-lm)]
A neuro-symbolic reasoning system that combines LLMs with symbolic solvers for faithful logical inference. Shift reasoning execution from LLM to symbolic solvers, leveraging LLMs only for translation (symbol grounding).
1. **Problem Formulator** – LLM converts a natural language problem into a symbolic representation (FOL, LP, CSP, SAT).
2. **Symbolic Reasoner** – Deterministic symbolic solver (e.g., Prover9, Pyke, Z3) performs logical inference.
3. **Result Interpreter** – Maps symbolic result back to natural language.
4. **Self-Refiner** – Uses solver error messages to revise invalid symbolic forms via iterative prompting.

### Which Symbolic Engine the LLMs use? 
An LLM gets a prompt describing the a dedicated task. 

* Deductive reasoning → Logic Programming (LP) → Pyke
* First-order logic → FOL → Prover9
* Constraint satisfaction → CSP → python-constraint
* Analytical reasoning → SAT → Z3

### Inductive Logic Program (Rule Learning)


- **Inductive Logic Programming**, Muggleton, S. (1991)

- **FOIL**: Learning logical definitions from relations, Quinlan, J. R. (1990)

- **Progol** (Muggleton, 1995) 

- **Metagol** system for learning meta-interpreted programs, Cropper, A., & Muggleton, S. (2016)

- Ultra-strong machine learning: comprehensibility of programs learned with ILP, Muggleton et al. (2014)

- **∂ILP (Differentiable ILP)** – Evans & Grefenstette, 2018

- **Neural Logic Machines**, Dong, 2019

- **Neural Theorem Provers**, Rocktäschel & Riedel, 2017

- Inductive Logic Programming via Differentiable Forward Chaining, Payani & Fekri (2019)

- Differentiable Learning of Logical Rules for Knowledge Base Reasoning, Yang, Z. et al. (2017)

- Logical neural networks, Campero, A. et al. (2018)

- Learning explanatory rules from noisy data, Evans, R., & Grefenstette, E. (2018)

- Learning Big Logical Rules by Joining Small Rules, Hocquette, 2024 







--- 

### 🧠 ALGORITHM: DeepProbLog

Mahaeve proposed Probabilistic Logic Programming (DeepProbLog) in 2018. The algorithm trains a **neural predicate** which is defined by the following format.
```
nn(m, InputArgs, OutputVar, OutputDomain) :: Predicate.
```

For example, the digit predicate for an image and symbol digit could be defined by: 

```
nn(mnist_net, [Img], Digit, [0,1,2,3,4,5,6,7,8,9]) :: digit(Img, Digit).
```

```
nn(digit_net, [Img], Digit, [0..9]) :: digit(Img, Digit).
nn(op_net, [Img], Op, [+,-,*,/]) :: operator(Img, Op).

solve(E1, E2, E3, Result) :-
    digit(E1, D1),
    digit(E3, D2),
    operator(E2, Op),
    eval(Op, D1, D2, Result).

eval(+, A, B, R) :- R is A + B.
eval(-, A, B, R) :- R is A - B.
```

### 🧠 ALGORITHM: NS-CL

Mao proposed Neuro-Symbolic Concept Learner in 2019. 
* The natural language question is mapped to a structured symbolic program.
* Execution is performed through differentiable neural operators like `ColorOf()` and `PositionOf()`.
* The result is a probabilistic symbolic reasoning trace that is fully trainable end-to-end.

Consider a color vectors:
```python 
# Assume 3 color concepts: Red, Blue, Green
v_red   = torch.tensor([0.9, 0.1, 0.0])
v_blue  = torch.tensor([0.2, 0.8, 0.0])
v_green = torch.tensor([0.1, 0.2, 0.9])
concepts = torch.stack([v_red, v_blue, v_green])  # (3, d)
```

```python
# Object feature (from ResNet)
f_obj = torch.tensor([0.85, 0.15, 0.1])  # example object feature

# Predict color distribution
color_probs = ColorOf(f_obj, concepts)
print(color_probs)  # e.g., tensor([0.81, 0.15, 0.04])
```

We have a question in the form of natural language: 
"What is the color of the right object?" It is converted into a DSL form: 
```python
# DSL Program:
Program = Query(Color, Filter(Rightmost))
``` 

```python
# Step 2: Apply Filter(Rightmost) - select the rightmost object
right_scores = [PositionOf(obj).x for obj in object_features]  # Get x-coordinate
rightmost_index = argmax(right_scores)                        # Index of rightmost object
mask = one_hot(len(object_features), rightmost_index)         # Binary mask for that object
```


```python
# Step 3: Apply Query(Color) - predict the color of the selected object
selected_feat = weighted_sum(object_features, mask)       # Soft selection
color_probs = ColorOf(selected_feat, color_concepts)      # Probability over color concepts

# Final Answer:
predicted_color = argmax(color_probs)  # e.g., "Red"
```

* **Question**: Why this algorithm is called Neuro-Symbolic? <d-footnote>  From the visual scene, the algorithm extracts the probability of each symbolic concept, and the natural language question is transformed into a domain-specific language (DSL). This program directly evaluates symbolic conditions, although the evaluation itself is probabilistic.   </d-footnote>

---


### 🧠 ALGORITHM: LOGIC-LM 

Pan et al. introduced LOGIC-LM in 2023.  A neuro-symbolic framework that decouples reasoning from language generation by having LLMs generate symbolic representations, and symbolic solvers execute logical inference.
LOGIC-LM delegates:
- **Language understanding → LLM**
- **Symbolic inference → External solver**
- Ensures logical **faithfulness**, **robustness**, and **interpretability**

#### **Input:**

- Natural language problem (e.g., multiple-choice or free-form question)

```text
"Stranger Things" is a popular Netflix show.
If a Netflix show is popular, Karen will binge-watch it.
If and only if Karen binge-watches a Netflix show, she will download it.
Karen does not download "Black Mirror".
"Black Mirror" is a Netflix show.
If Karen binge-watches a Netflix show, she will share it to Lisa.

Question: Is the following statement true, false, or uncertain?  
"Black Mirror" is popular. (A) True  (B) False  (C) Uncertain
```

#### **Problem Formulator (LLM-generated symbolic form):**

```prolog
Predicates:
NetflixShow(x)        # x is a Netflix show
Popular(x)            # x is popular
BingeWatch(x, y)      # x binge-watches y
Download(x, y)        # x downloads y
Share(x, y, z)        # x shares y to z

Facts:
NetflixShow(strangerThings) ∧ Popular(strangerThings)
∀x (NetflixShow(x) ∧ Popular(x) → BingeWatch(karen, x))
∀x (NetflixShow(x) ∧ BingeWatch(karen, x) ↔ Download(karen, x))
NetflixShow(blackMirror) ∧ ¬Download(karen, blackMirror)
∀x (NetflixShow(x) ∧ BingeWatch(karen, x) → Share(karen, x, lisa))

Query:
Popular(blackMirror)
```

#### **Symbolic Reasoner Output:**

```text
Result: false
```

#### **Result Interpreter Output:**

```text
Answer: (B) False
```

#### **Self-Refiner (if symbolic execution fails):**

- Receives error from symbolic solver (e.g., "unbound variable")
- LLM revises symbolic form using in-context error correction examples
- Retries execution until success or max attempts

---






## References 

- Mahaeve, DeepProbLog: Neural Probabilistic Logic Programming, 2018

- Mao, The Neuro-Symbolic Concept Learner: Interpreting Scenes, Words, and Sentences From Natural Supervision, 2019

- PAN, LOGIC-LM: Empowering Large Language Models with Symbolic Solvers for Faithful Logical Reasoning, 2023