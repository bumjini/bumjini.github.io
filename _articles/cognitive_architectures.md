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
img: assets/img/cognitive_architecture.png
title: 'Cognitive Architectures'
category: 'AI'
description: 'Cognitive Architectures'
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


## ACT-R


## Soar ㅡㅡ

### Components

* **Working Memory**: 현재 상태와 목표를 저장한다.  $\operatorname{WM}_t = \{ S_t, G_t \}$
* **Long-term Memory**: 규칙들을 저장한다. $\operatorname{LTM} = \{ R_i \mid  R_i = C_i \rightarrow A_i ,i \in [1, \mathbb{N}] \}$
* **MatchedRules** : A set of rules whose conditions are satisfied in working memory. $$\operatorname{MatchedRules}_t = \{ R_i \mid C_i \subseteq \operatorname{WM}_t \}$$
* **Preference**: $\operatorname{Preference}(R_i)$: 규칙에 대한 선호도. 
* **Solution**: $A^* = \operatorname{Solution}(G_i)$: 해당 목표를 달성하기 위한 행동. 이건 확실하게 추측하기 어렵다. 환경의 복잡성과 행동이 미치는 영향을 정확하게 파악하기 쉽지 않기 때문이다. 

### Processes 

* **Matching Process**: Given a set of matched rules and conditions in working memory, determine the rules that satisfy the conditions. 
* **Condition Matching**: Given a set of matched rules and conditions in working memory, determine the rules that satisfy the conditions. 
* **Evaluation of Goal Achievement Process**: $Distance(S_t, G_t) > Distnace(S_{t+1}, G_t)$ 와 같이 상태가 더 멀어지게 되는 경우는 해당 규칙으로 달성할 수 없는 상태라고 판단한다. 이에 subgoal 을 만들어서, $G_{sub} = f(S_t, G_t)$, 목표 상태를 현실적으로 가능하게 만든다. 이후 working memory 는 $$S\operatorname{WM}_{t+1} = \{ S_{t}, G_{t} G_{sub}, \operatorname{Conctext}_{sub} \}$$ 로 업데이트 된다.  WM에 들어있는 목표들 중에서 subgoal들을 우선적으로 처리하며, $\operatorname{Conctext}_{sub}$의 경우, 상위와 하위 목표에 대한 정보를 포함한 메타정보가 제공된다. 이로부터 메모리를 효율적으로 관리하여 최종 목표 $G$를 달성하기 위한 행동을 수행한다. 
* **New Rule**: 새로운 규칙을 학습하는 방법은 condition이 주어졌을 때, 어떤 행동을 할 것인지를 나타낸다. 
* **Preference Process**: Determine which rule to execute. 


* 하위 목표 생성과 재사용: 기존에 하위목표를 풀었다면, 이 방식을 다시 사용하면 목표에 도달할 수 있다. 
* 규칙이라는 것은 생각보다 간단한 존재이다. 조건에 따라서 행동을 한다. 문제는 조건과 행동이라는 것이 다양한 방식으로 정의될 수 있다는 것이다. 
* 조건은 현재 상태, 목표 상태, 메타 정보 등 다양한 것을 고려한다. 이는 기존에 봤던 것일수도 있고, 완전히 새로운 것일 수도 있다. 주어진 상태와 목표에 대해서 어떤 규칙에 매칭되는지는 한편으로 모호할 수 있다. 
* 행동이라는 것은 입력에 대해서 가능한 모든 절차들을 포괄한다. 실제 물리적인 행동, 새로운 정보에 대한 사용, 상태에 대한 업데이트, 하위 목표 생성등 다양한 행위적인 것을 포괄한다. 
* Goal 풀기: 현재 목표를 달성하기 위해서 조건 중 사용가능한 규칙을 찾는다. Soar는 규칙 기반 모델이기 때문에, 가용한 규칙이 없다면 목표를 변경해야 한다. 또한 가용한 규칙이 있더라도, 이들이 현재 상태를 더 안 좋게 만든다면, 사용가능한 규칙이 없는 것과 동일하다. 따라서 목표 자체를 변경해야 한다. 
* Subgoal 생성하기: 내 생각에 subgoal을 생성하기 위해서는 Impasse 상태라는 점과, 현재 정보가 모두 주어져야 한다. 이를 바탕으로 어떤 subgoal을 만들지 결정할 수 있는데, 이 과정 또한 rule에 의해서 동작하는 것이다. 
* Subgoal 달성하기: 주어진 규칙내에서 해당 subgoal은 여러 행위들을 토대로 달성될 수 있다. 해당 subgoal이 달성되는 경우, 해당 상태에서 추가적인 규칙을 적용하여 문제를 해결할 수 있다. 
* Chunking: 입출력에 대한 새로운 방식이 주어지는 경우, 이 정보는 기억되고, 이후에 동일한 문제가 봉착되는 경우 동일한 방식으로 해결된다. 여기서 입력은 풀었던 방식에서 필요한 상태들을 나타내며, 행동은 풀었던 방식의 시퀀스를 나타낸다.  **Soar가 규칙을 생성할 때 모든 정보를 "범용적"이고 "재사용 가능"한 방식으로 저장하기 때문입니다.**

* 심볼은 생각보다 모호한 것이다. 추상적이며 지칭하는 대상이 명확하지 않다. 현실의 정보는 벡터표현보다 심볼표현이 정보를 잃어버린다. 마치 threshold를 기반으로 유무를 판단하는 것과 유사하다. 따라서, Soar에서 하는 symbolic rule 기반 방식은 모호성과 추상성을 기반으로 동작하며, 하위 목표 생성 및 새로운 규칙을 저장하는 것도 이러한 모호성들을 포괄하여 저장하는 것이다. 

가장 큰 문제는 추상적으로 정보를 저장한다는 것이다. 특정한 상황에서 얻은 기억 정보들은 명확하게 일치하기보다 공통된 특징을 뽑아내서 정의되어야 한다. 이는 추론 과정에서 필요한 path를 저장하는 방식과 유사하다. 즉, 규칙이라는 것은 특정 대상에서 다른 대상으로 가는 것이고 이 때, 대상은 상태, 정보, 목표 등을 범용적이고 추상적이며 포괄적으로 저장한다. 
따라서, 정보의 사용은 대단히 모호하기에 condition이 일치하는지, 어떻게 행동을 구현해야 하는지 모호성을 지니고 있다. 
