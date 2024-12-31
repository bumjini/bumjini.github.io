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
img: assets/img/bp.png
title: '[Thinking] What is role of Language in thinking?'
category: 'AI'
description: 'What is role of Language in thinking?'
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


## 생각 (thinking) 은 무엇인가? 

생각이라는 것은 포괄적인 의미를 담고 있는 것 같다. 목적을 달성하기 위해서 할 수도 있고, 목적 없이 자유연상을 할 수도 있다. 


언어는 다른 이들과 생각을 공유하여 의사소통을 가능하게 하며, 생각을 전달하고 생각을 받는 역할을 한다. 
인간의 언어라는 것은 생각의 내부 표현에 대해서 심볼 시스템으로 내보내는 것이다. 

언어는 의사소통이고 아래와 같은 연결고리를 가지고 있다. 
* 생각의 관점에서는 Thought -> Language -> Thought 
* 통신의 관점에서는 Language -> Thought -> Language 

즉, 언어라는 요소는 배출이고 통신이며, 여기에는 대화를 하는 대상들이 존재한다는 가정이 있다. 즉, 의사소통을 위한 분리이다.

따라서 언어라는 것은 생각을 위해 필요조건이 아니다. 
> infants are born equipped with a powerful toolkit for modeling and thinking about
> the world, including an understanding of physical objects and events, and the goals and actions of agents
> (Spelke, 2022; Spelke & Kinzler, 2007)

물론, 언어를 통해서 생각들은 전달되고 더 폭넓은 사고를 지닐 수 있다. 

*Language of thought* (Fodor, 1975), a structured symbolic
substrate for representing conceptual knowledge that provides a general interface to algorithms for problem
solving and reasoning.

These symbolic systems are not merely logic engines; they support our probabilistic
inferences, and rich intuitive simulations (Goodman, Tenenbaum, & Gerstenberg, 2014; Oaksford & Chater,
2007; Russell & Norvig, 2021).

논리적으로만 동작하는 것은 아니며, 확률적이고 시뮬레이션적인 요소들을 포함하여 동작한다. 

**문장의 의미(semantic)**를 **구조화(parse)**

Within linguistics and natural language processing, in turn, this paradigm underlies *semantic parsing systems* designed to map from human language into symbolic computational representations.

Semantic parsing은 문장의 의미적 구조를 컴퓨터가 이해할 수 있는 형태로 변환한다. 

```sql
// What is the weather in New York?
SELECT weather FROM database WHERE location = "New York"
```

probabilistic language of thought

probabilistic programs


We take a broadly rational perspective on language—we consider language to be a system of goal-directed actions for
externalizing and communicating thoughts to other intelligent beings (Chater & Manning, 2006; Gibson,
2014; Goodman & Frank, 2016)

In this context, we frame the problem of deriving meaning as inferring the
mappings between a language’s system of external communicative signals into the representations of rational
thought.


It is worth highlighting that thought does not require language and is distinct from language in the human brain (Mahowald et al., 2023). Non-human species, and pre-verbal infants (Spelke, 2022), are clearly capable of modeling the world towards their inferences and goals without language. But for humans, language clearly plays a profound role in determining the problems we think about, and how we think about them.


humans are resource-rational thinkers—under finite constraints of time and memory, we rationally allocate computational resources in order to make useful inferences and plans (S. J. Gershman, Horvitz, & Tenenbaum, 2015; Lieder & Griffiths, 2019).
Resource rational agents amortize computational effort across prior experience and problems, storing and reusing prior computation towards similar new problems that we encounter in the future (S. Gershman & Goodman, 2014; Le, Baydin, & Wood, 2017). 

Certain domains of inferences share more structure than others, and evidence suggests that we therefore heavily amortize them. Prior work, for instance, suggests that computations involved in basic perceptual activities (Brooke-Wilson, 2023; Dasgupta & Gershman, 2021; Fodor, 1983), such as object recognition under common lighting conditions, are highly amortizable from reusable patterns in computation that are learnable and shared across a background distribution of perceptual instances. This view suggests why fast, bottom-up pattern recognition models have made great advances in modeling perception in recent years, while it has proved much more challenging to amortize the wide range of flexible inferences required for arbitrary problem solving.

But while we take the view that a resource-rational agent should intelligently learn and reuse prior computation when possible, we do not view language-informed thinking, or thinking in general, as solely a matter of learning and interpolating over statistical patterns from prior experience. When we think, including when we think about the meanings we recover from language—to update our beliefs, to follow instructions, or to answer questions posed in language—we must be able to flexibly model arbitrary situations and support capacities for general problem solving, including inference, planning, and simulation, under a wide range of new and unencountered circumstances.

The efficient learnability of human language also highlights that, in many senses, the computational relationship between language and thought in humans is almost the inverse of that in today’s LLMs. For humans, language could be characterized as an emergent property of thinking. Infants can model the world and draw inferences well before they know language (Gopnik, 1996; Spelke, 2022), and reliably acquire complete linguistic capabilities from exposure to relatively tiny amounts of language (R. Brown, 1973). Congenitally-Deaf humans born with no language input spontaneously develop languages to communicate their thoughts, with the same basic hallmarks of mature natural languages (Goldin-Meadow, 2012; Pyers, Shusterman, Senghas, Spelke, & Emmorey, 2010; Senghas, Kita, & Ozyurek, 2004). This paper seeks to understand and model the cognitive and computational structures underlying this human scaling route to intelligence and language use

probabilistic language of thought (PLoT)

we then propose that large language models trained on language and code can be used to implement meaning functions in a resource-rational architecture – they can implement learned, broad-coverage mappings between language and code; and they can be understood as part of a human-like, resource-rational system that efficiently infers these mappings using stored patterns amortized from the prior joint distribution over language and code.

a generic inference query motif (Goodman, Mansinghka, Roy, Bonawitz, & Tenenbaum, 2008)

* Symbolic 하다는 것은 Symbol의 의미를 찾아야 한다. 이 때 프르토타입 등 활용 
* 연산 이후로 나타난 심볼이 반드시 의미가 명확하지 않을 있다..
* Amortization은 비용을 절감한다. 
* Translation과 Inference는 구분된다. 
* Symbolic 하다는 것은 Translation적인 요소가 없고 inference만 진행한다. 
* Subsymbolic 
* 통계적인 연산과 룰 기반, operation기반으로 연산
* In-context learning등은 수많은 Amortization으로부터 연산을 진행한다. feature를 형성하는 것은 amortization으로 고려될 있다. 
* Symbolic은 추론 과정에서 해석적인 과정을 추가하지 않는다. 그러나, LLM의 경우는 inference 과정에서 기존 추론의 결과가 
* Rule-based inference vs data-driven inference
* Working memory는 amortization하는 것들을 좀 더 강조하는 효과가 있다. 
* PLoT의 경우, 확률적인 연산을 추가하는 효과가 있다. 그러나, world model을 만드는 것은 쉽지 않을 것 같으며, LLM으로 만든 world model은 데이터를 기반으로 형성한 것일 가능성이 있다. 이후에 만들어진 world model로부터 연산을 진행하는 것이다. 물론 symbolic 또한 amortization을 활용할 수 있을 것이다. 
* Neurosymbolic에서 symbolization을 하는 것은 어떤 위험을 가지고 있는가? context 를 기반으로 심볼을 형성하는 것이다. 따라서 심볼 자체의 의미를 정확하게 파악하기 어려울 수 있다. 
* 모델에 심볼을 사용하는 것은 candidate set등을 지속적으로 평가할 필요가 있다. 즉, 의미라는 것을 나타내야 한다. 
* translation, inference, rational meaning construction, 
* resource-rational decision making  
* Language understanding and generation 
* Language translation and inference 
* Contextual amortization / In-context amortization 

이해란 무엇인가?
주어진 쿼리에 대한 어떤 알고리즘 A를 동작하려고 할 떄, 
이 알고리즘을 동작하도록 만드는 준비상태이다.
이해를 했다는 것은 정보가 준비상태로 있다는 것을 나타낸다. 
어떤 알고리즘을 선택하는지도 고려하였음

---

## 4 가지 용어에 대해서 

아키텍처의 한계, 심볼릭, 서브심볼릭, 통계적 추론, 연역적 추론, 알고리즘, 생각, 번역, 언어, 벡터 표현 등 다양한 요소들이 있다. 의미를 적확하게 이해하는 것은 LLM의 한계를 이해하고 필요한 모듈을 설계하기 위해서 필요한 과정이다. 이를 위해서 각 요소들이 나타내는 바를 명확히 하고 그들이 어떤 역할을 지니며, 한계점이 무엇이고, 그 한계점은 다른 어떤 모듈에 의해서 해소되어야 하는지 이야기 한다. 이 과정은 모델이 지닌 복잡적인 인지과정 혹은 알고리즘에 대한 전반적인 과정에 대한 해석이다.



### 이해라는 것은 무엇인가? (Understanding)

무언가를 이해한다는 것은 대상에 대한 처리 과정을 나타내며, 그 과정의 정확성은 질문으로부터 파악된다. 주어진 정보 $I$에 대해서 이 정보를 처리하여 $I$ 내부에 있는 정보를 정리하거나, 외부의 정보들을 준비하여 sufficient set $S$ 를 만든다. 이후 주어진 질문 $Q$에 대해서 $S$와 알고리즘 $F$를 통해서 정답 $A$를 생성한다. 따라서 대상에 대해서 이해한다는 것은 주어진 $I$에 대해서 정보 집합 $S$를 만드는 것이다. 

주어진 집합 $S$는 질문 $Q$에 의존적일수도 있고, 독립적으로 존재할 수도 있다. 더욱이 주어진 정보를 이해하는 것과, 정보와 질문을 동시에 이해하는 것은 차이가 있다. 혹은 정보는 없고 질문만 존재할 수도 있다. 이 모든 경우를 고려해서, 이해하는 과정은 sufficient set $S$를 만드는 것, 알고리즘 $F$를 만드는 것이다. 이후에 알고리즘 $F$에 의해서 정답 $A$를 얻는 과정은 이해의 영역이 아니다. 이해는 정보처리에 대한 선택의 과정이지, 도출하는 과정이 아니기 때문이다. 실행하는다는 것은, decision making 과정이며, 이 과정은 정보들을 알고리즘으로 어떻게 처리할지 결정하는 과정이다. 즉, $F$ 자체는 이해의 영역에서 어떤 것으로 구현하는지와는 상관없다. 
이는 Marr’s Three Levels of Analysis를 모두 포함하는 과정으로, Computational Level, Algorithmic Level, Implementation Level로 알고리즘을 생각한다. 
계획적인 단계이며, 실행 결과는 이해가 정확한지 평가하는 것이다. 

1. $I \rightarrow S$ : 정보만 있고, 정보를 처리하는 과정 
2. $(I, Q) \rightarrow F \rightarrow S \rightarrow A$ : 정보와 질문이 있고, 순서대로 알고리즘, 정보처리, 정답 도출
3. $(I, Q) \rightarrow S \rightarrow F \rightarrow A$ : 정보와 질문이 있고, 순서대로 정보처리, 알고리즘, 정답 도출
4. $(I, Q) \rightarrow (S, F) \rightarrow A$ : 정보와 질문이 있고, 순서대로 정보처리와 알고리즘, 정답 도출
5. $Q \rightarrow S \rightarrow F \rightarrow A$ : 질문만 있고, 순서대로 정보처리 (필요한 외부 정보 활용), 알고리즘, 정답 도출
6. $Q \rightarrow F \rightarrow S \rightarrow A$ : 질문만 있고, 순서대로 알고리즘, 정보처리 (필요한 외부 정보 활용), 정답 도출   
7. $Q \rightarrow (S, F) \rightarrow A$ : 질문만 있고, 순서대로 정보처리 (필요한 외부 정보 활용)와 알고리즘, 정답 도출

#### LLM이 이해했는가? 

이해라는 관점에서 LLM이 특정 정보 혹은 (정보와 질문)을 이해했는지 분석해야 한다. 
LLM은 subsymbolic 표현으로 주어진 정보들을 처리하며, Query 토큰에 대해서 다음 토큰을 생성하는 모델이다. 
따라서, (2,3,4) 번에 해당하며, 연산과정에서 정보처리 $S$와 알고리즘 $F$는 동시에 진행된다. 
LLM이 무엇을 이해했다고 말한다면, 이는 정보처리 $S$와 알고리즘 $F$를 통해서 정답 $A$를 도출할 수 있다는 점을 의미한다. 

Subsymbolic한 방식에 대해서 문제가 되는 것은 sufficient set $S$를 만드는지, 어떤 알고리즘 $F$를 사용하는지 명확하지 않다는데 있다. 
이는 통계기반 모델의 특징인데, Set에 필요한 정보들은 미리 계산된 amortized 형태로 존재하며, 그들에 대한 추가적인 변형과 조합을 통해서 연산을 하는 것이다. 
문제는 주어진 context에 대해서 sufficient set 자체를 매번 다르게 만든다는 점이고, 원소들은 symbolic 하기보다 vector형태의 표현들이다. 이로부터 유연적인 연산이 가능하지만, 
만일 알고리즘 $F$가 명시적이라면, 비명시적인 원소들로부터 하는 연산은 명확하지 않다. 한 가지 대안법은 function $F$와 symbolized 된 원소들을 활용해서 연산 자체를 해석가능하게 만드는 것이다. 
이러한 모델은 알고리즘 $F$와 원소들을 명확하게 하는 효과가 있으며, subsymbolic에 대한 명확한 symbolization 연산으로 봐야 한다. 
그러나 이 연산을 transformer architecture를 이용해서 구현하는 것은 다음과 같은 이유로 비효율적이다. 

1. Representation Superposition: 서로 겹치는 표현들에 대해서 모델이 명확하게 구분하지 못하며, 기존 다른 알고리즘 F, 정보처리 S를 바꿀 가능성이 있다. 
2. Flexibility of Implementation: Softmax 연산 등으로 어떤 것이 구현 가능한지 명확하지 않다. Family Relation 과 같은 문제에 대해서 이를 transformer 내부에 구현하는 것이 가능하지 않을 수 있다. 
3. Depth of Algorithm: 레이어를 지나면채서 표현을 바꾸는 방식이다. 알고리즘을 구현할 수 있을지라도, 알고리즘 자체가 많은 변형을 요구한다면, 현실적으로 불가능할 가능성이 있다. 이전과 마찬가지로 amortization을 통해서 연산을 효율화 시킬 수 있겠지만, distributed representation에 대해서 top-down 방식으로 amortization을 시키는 것은 어렵다. 

Bottom-up은 모델이 스스로 amortization을 만든다. 여기에 외부 힘에 의해서 amortization을 추가하는 연구는 진행되었지만, 일반화 성능 등 여전히 어려운 문제로 남는다. 또한 Feature engineering과 같은 요소들은 amortization된 표현을 선택하는 방식을 바꾸는 것이다. 궁극적으로 LLM은 amortization을 통해서 세계에 필요한 정보를 선택하여 $S$를 만들고 알고리즘 $F$를 모델 내부 연산으로 구현한다. 두 가지 연산 모두 transformer의 장점으로 볼 수 있으나, 이 연산들이 모든 종류의 $(I, S, F, Q)$에 대해서 동작하지 않는다는 한계가 있다. 따라서 LLM은 모든 종류의 지식을 이해할 수 없는 본질적인 한계가 있다. 

#### Symbolic Cognitive Architecture는 이해했는가? 



### 번역이라는 것은 무엇인가? (Translation)


### 생성이라는 것은 무엇인가? (Generation)


### 추론이라는 것은 무엇인가? (Inference)


### 언어라는 것은 무엇인가? (Language)


### 생각 이라는 것은 무엇인가? (Thinking)