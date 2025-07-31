---
layout: distill
title: 'Circumscription'
description: Nonmonotonic Reasoning
gradient: linear-gradient(135deg, #0064e1 0%, #5bd3ff 100%)
hover-gradient: linear-gradient(135deg, #00c6fb 0%, #005bea 100%)
background_color: rgb(255, 231, 214)
---

## Motivation: When Classical Logic Falls Short

In classical logic, a conclusion that is once derived remains valid regardless of additional information. This property, known as monotonicity, often fails to reflect how real-world reasoning works.

Consider the following two statements:

- "Birds can fly."  
- "Penguins are birds that cannot fly."

Classical logic has no built-in mechanism for accommodating exceptions like penguins. Once you accept the rule that all birds can fly, the system cannot revise this conclusion without contradiction. This is where non-monotonic logic — and in particular, default logic — becomes useful.


<img src="https://d2acbkrrljl37x.cloudfront.net/bumjini-blog/study_post/penguine.png" width="100%" height="auto" class="styled-image"/>


## What Is Default Logic?

Default logic, introduced by Raymond Reiter (1980), is a formalism that extends classical logic with the ability to draw conclusions tentatively — that is, as long as no contradictory evidence is discovered. The core idea is to express generalizations in a way that allows for exceptions, without requiring explicit enumeration of every exception.

Default logic introduces a new construct: the default rule, written in the following form:

$$
\frac{\phi : \psi_1, \dots, \psi_n}{\chi}
$$

Where:
- $\phi$ is the prerequisite: what must be known or assumed true.
- $\psi_1, \dots, \psi_n$ are the justifications: assumptions we are allowed to make if they are not contradicted.
- $\chi$ is the conclusion (or consequent): what we infer if the above conditions hold.

## Example: Birds and Tweety

Let’s encode the assumption that Tweety is a bird by default, unless evidence to the contrary is known.

We can express this as a default rule:

$$
\frac{\text{true} : \text{Bird}(\text{Tweety})}{\text{Bird}(\text{Tweety})}
$$

- The prerequisite is $\text{true}$, meaning the rule is always applicable.
- The justification is $\text{Bird}(\text{Tweety})$, which must be consistent with known information.
- The conclusion is $\text{Bird}(\text{Tweety})$, which we infer as long as the justification is not contradicted.

This rule says:  
"Assume Tweety is a bird, unless you know otherwise."

## Comparison with Circumscription

In circumscription, exceptions are managed using explicit abnormality predicates:

$$
\text{Bird}(x) \land \neg \text{Abnormal}(x) \rightarrow \text{Flies}(x)
$$

The abnormal predicate $\text{Abnormal}(x)$ is then circumscribed (minimized), so that as few things as possible are considered exceptions.

In contrast, default logic does not require introducing abnormal predicates. Instead, exceptions are handled using the justification part of the default rule. A default rule may apply if its justification is consistent — but it is not forced to be evaluated unless challenged.

### Key Difference:

| Aspect | Circumscription | Default Logic |
|--------|------------------|----------------|
| Mechanism | Minimize exception predicate (e.g., $\text{Abnormal}(x)$) | Use justification to check consistency |
| Exception handling | Must be explicitly represented | Implicitly blocked by contradictory evidence |
| Evaluation | Mandatory evaluation of abnormality | Conditional: justification only evaluated when contradicted |

Circumscription is more syntactic — requiring abnormality conditions to be embedded in logical form. Default logic is more procedural — applying inference only when no contradiction arises.

## Optionality of Justifications

One of the key insights in default logic is that justifications are not mandatory evaluations. A rule with justification $\psi$ can be applied as long as $\neg \psi$ is not provable — not necessarily that $\psi$ is provable.

This mirrors human reasoning:  
"I will assume this is true unless I see a reason to doubt it."

If a later statement contradicts the justification, then the rule is rejected.

If you want the justification to be strictly enforced, you can include it directly in the prerequisite, turning the default rule:

$$
\frac{\phi : \psi}{\chi}
$$

into a classical rule:

$$
\phi \land \psi \rightarrow \chi
$$

This collapses the non-monotonic behavior into classical inference.

## Integration with Classical Logic

Another advantage of Reiter’s framework is that default logic does not discard classical logic. Instead, it builds on top of it.

Given a set of known facts $W$, the classical consequences are defined as:

$$
Th(W)
$$

— the deductive closure under classical first-order logic.

Default rules are applied only when needed, and their conclusions are added to $Th(W)$ only if their justifications remain consistent.

This preserves the modularity and reliability of classical inference while introducing non-monotonic flexibility through default rules.

## Caution: Conceptual Gaps and Intuition

While default logic adds expressive power, it can also lead to results that diverge from human intuition. A system might apply a default rule that is formally valid but semantically misleading.

For example, if a default applies in an unintended context (e.g., due to missing exceptions), it might derive a conclusion that seems obviously wrong to a human observer, yet is consistent in the logic.

This highlights the importance of carefully crafting default rules, especially in systems that aim to align with human expectations.

## Historical Notes and Development

Default logic was first proposed by Raymond Reiter in 1980 and has since inspired extensive work in:

- Extensions: constrained defaults, prioritized defaults
- Semantics: extensions, fixpoints, skeptical vs. credulous reasoning
- Applications: planning, knowledge representation, explanation, and logic programming

It also relates to other non-monotonic frameworks such as:

- Circumscription (McCarthy)
- Autoepistemic Logic (Moore)
- Answer Set Programming (Gelfond & Lifschitz)

## Conclusion

Default logic offers a flexible and powerful framework for encoding real-world knowledge that is inherently defeasible. It enables systems to reason in the presence of incomplete information, handle exceptions gracefully, and revise beliefs when contradictions arise.

By separating prerequisites, justifications, and conclusions, default logic allows for structured and robust inference that aligns more closely with human commonsense reasoning. Its ongoing development continues to shape the field of AI reasoning and logic-based knowledge systems.


## Reference 

- A logic for default reasoning. Artificial Intelligence, R. Reiter, 1980.
- A Tutorial on Default Logics, G. Antoniou, 1999