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
title: '[Logic] Horn Logic'
category: 'AI'
description: '조건의 disjunction으로부터 결론을 유도하는 논리'
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

<img src="/assets/img/bp.png" width="40%" height="auto" class="styled-image"/>

## Horn Logic

Horn Logic는 1951년 Horn에 의해서 제안되었다.  
Horn Clause는 다음과 같은 형태를 가진다. 

Horn Clause에서는 Body에 나열된 **predicate(전제)**들이 모두 참임을 만족해야 **Head(결론)**이 참으로 도출될 수 있다. 

$$
B_1 \wedge B_2 \wedge \cdots \wedge B_n \rightarrow H 
$$

이를 논리식으로 다시 쓰면

$$
\neg B_1 \vee \neg B_2 \vee \cdots \vee \neg B_n \vee H
$$

---

## 유형 

Horn Clause는 다음과 같은 유형으로 분류된다. 

- **True**: 사실. 객체(object) 기반의 진술.
  $$
  \text{parent}(alice, bob)
  $$

- **Rule**: 규칙. 변수(variable)를 기반으로 일반화된 관계를 정의.
  $$
  \text{parent}(X, Y) \wedge \text{parent}(Y, Z) \rightarrow \text{grandparent}(X, Z)
  $$

- **Query**: 질의. 결론을 유도하기 위해 변수를 찾는 과정.
  $$
  \text{grandparent}(alice, Z)?
  $$

사실에서는 **객체(object)**가 주어진다.  
Rule에서는 **변수(variable)**가 주어진다.  
Query에서는 모두 주어진 후 **변수의 값을 찾는다.**  

---

## Horn Clause의 요소

- **Head**: 규칙의 결론 부분. Body가 만족되었을 때 도출되는 결과.
- **Body**: 규칙의 조건 부분. 전제들로 이루어지며 AND 연산으로 결합된 형태로 주어진다.

> #### 예시
> **만약 A이고, B라면, C이다.**
> 
> $$
> A \wedge B \rightarrow C
> $$
> 
> 여기서 $A \wedge B$ 는 Body이고, $C$는 Head이다.

---

## Decision Tree와의 비교

Horn Logic는 **Decision Tree**와 유사한 구조적 흐름을 가진다.  
- Horn Logic에서는 각 규칙들을 만족하는지 여부를 토대로 추론을 진행한다.  
- Decision Tree에서는 각 노드들을 순차적으로 방문하여 만족하는 조건을 찾아내는 방식으로 추론한다.

### 차이점
- **학습 과정**:
  - Horn Logic은 Horn Clause를 정의하는 방식으로 진행된다.
  - Decision Tree는 데이터를 토대로 학습한다.
- **표현 방식**:
  - Decision Tree는 **subsymbolic 표현**을 활용하여 데이터를 분류하지만,  
    이를 symbolic한 규칙으로 해석할 수도 있다.

결과적으로, 두 방식 모두 규칙 기반으로 작동하지만 다루는 대상과 학습 방식에는 차이가 있다.

---

## 규칙 선택 문제

특히 **RuleFit**의 경우 Horn Logic과 일치도가 높다.  
하지만 RuleFit은 **만족하는 규칙들에 대해 가중치**를 두고 최종 값을 예측한다는 점에서 차이가 있다.

### Horn Logic에서의 규칙 선택 문제
Horn Logic에서도 만족하는 여러 규칙이 있을 경우, 이를 해결하는 방안이 필요하다:
1. **규칙 접근 순서**:
   - 규칙의 순서를 고정하여 우선 탐색한다.
2. **규칙 충돌 해소**:
   - 다음과 같은 전략을 통해 해결:
     - **규칙의 우선순위** 설정
     - **결과 가중치**를 기반으로 선택
     - **전제 증거 신뢰도**를 반영
     - **일관성 확인**을 통해 충돌을 제거

Horn Logic과 Decision Tree는 모두 **조건 기반 추론**에 초점이 맞춰져 있지만,  
각 규칙의 선택 문제와 학습 방식에서 차이가 있다.  
이를 해결하기 위한 다양한 접근법이 활용될 수 있다.


## Prolog 예시

<d-code block language="python">

% 사실 (Facts)
parent(alice, bob).
parent(bob, charlie).
parent(alice, dave).
parent(dave, emily).


% 규칙 (Rules)
grandparent(X, Z) :- parent(X, Y), parent(Y, Z).
sibling(X, Y) :- parent(Z, X), parent(Z, Y), X \= Y.
ancestor(X, Z) :- parent(X, Z).
ancestor(X, Z) :- parent(X, Y), ancestor(Y, Z).


% 질의 (Queries)
% Example queries you can run in Prolog:
% 1. ?- grandparent(alice, charlie).    % alice는 charlie의 조부모인가?
% 2. ?- sibling(bob, dave).            % bob과 dave는 형제인가?
% 3. ?- ancestor(alice, emily).        % alice는 emily의 조상인가?
% 4. ?- parent(bob, Who).              % bob의 자식은 누구인가?
% 5. ?- grandparent(Who, charlie).     % charlie의 조부모는 누구인가?

</d-code>
