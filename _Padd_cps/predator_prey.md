---
layout: distill
authors: 
    - name: Bumjin Park
      affiliations:
        name: KAIST
giscus_comments: true
disqus_comments: true
date: 2022-11-20
featured: true
title: 'Predator Prey (Simple Tag)'
description: 'We study the message passing performance in MARL '
importance: 2
img: https://pettingzoo.farama.org/_images/mpe_simple_tag.gif
---

## Predator Prey Environment 

* [v23.11.21.1](https://github.com/fxnnxc/marl_xai/tree/v23.11.21.1)

최근 메시지 기반 멀티에이전트 강화학습으 심층공간의 표현력에 힘업어 높은 성능을 보였다. 
사람이 명시적인 언어로 메시지를 전달하는 것, 혹은 암호처럼 의미가 명확한 메시지를 전달하는 것과 다르게, 
심층 표현 메시지는 벡터형태로 명확한 메시지가 명확하지 않다. 

본 연구는 메시지에 대해서 고민해야 하는 다양한 주제에 대해서, 그 중 몇 가지에 대한 해답을 제시하고 추가적인 연구 방향에 대해서 논한다. 

1. 메시지 형성에 더 도움이 되는 activation은 무엇인가? (ReLU or Sigmoid) : **Sigmoid** 
2. 메시지를 공유하지 않은 모델보다 메시지 공유 모델은 더 빠르게 학습하는가? : **환경마다 다르지만, 에이전트가 3개 이상인 경우, 메시지 공유가 더 성능이 좋다** 
3. 메시지를 공유하지 않은 모델보다 메시지 공유 모델은 더 높은 성능으로 학습되는가? **환경마다 다르지만, 에이전트가 2개인 경우 더 높은 성능을 보일 때도 있다.** 
4. 메시지를 공유하면 에이전트 수가 늘어남에 따라 성능도 증가하는가? **모델마다 다르지만, 단순한 메시지 전달 모델은 증가한다** 
5. 메시지의 차원의 크기는 모델 성능에 긍정적으로 작용하는가? **일반적으로 차원이 클수록 성능은 향상된다. 그러나 너무 큰 경우, 더 성능이 낮은 경우가 있었다**


포식자 개수 및 장애물 개수에 따른 모델별 성능은 다음과 같다. 여러 포식자가 하나의 에이전트를 쫓는 환경에서 메시지 공유는 포식자들간의 위치를 결정하는데 중요한 역할을 하기에 통신하지 않는 (v1)보다 v2가 더 높은 성능을 지니고 있다. 


<img src="https://drive.google.com/uc?export=view&id=1DbXfME3gHf_OFAIB1Tj_jXoTFVw942Pw" style='width:100%'>  
<figcaption>
모델, 에이전트 개수, 장애물 개수에 따른 성능차이. X: 에이전트 수, Y: 성능, legend: 장애물 수. V2모델이 선형적으로 증가하는 성능을 보였으며, 장애물 개수에 따른 성능 저하를 명확하게 보여줬다. 이 결과는 환경 복잡도-에이전트 통신 수에 따른 직관적인 상관관계를 그대로 보여줬다. 어텐션 기반인 V3의 경우, V2보다 성능이 낮은데, 통신을 위한 표현학습이 오래걸리기 때문으로 추정된다. 
</figcaption>

## Training Dynamics 


학습 과정에서 성능 그래프는 다음과 같다. 해당 그래프는 모든 하이퍼파라미터에 대해서 평균을 낸 점수이다. 
해당 그래프를 기반으로 학습과정에서 성능이 어떻게 변화하는지 확인할 수 있다. 
대표적으로 기울기를 측정하는 경우, 메시지가 발생하는 시점을 특정할 수 있을 것이라는 기대가 있다.  


#### Predator 개수 : 2


<div style="display:grid;grid-template-columns: 1fr 1fr;border:1px solid #000000;" >
<div style="border:1px solid #000000; text-align:center;">
Obstacle 0 
</div>
<div style="border:1px solid #000000;  text-align:center;">
Obstacle 2
</div>
<div style="border:1px solid #000000;">
<img src="https://drive.google.com/uc?export=view&id=19WrFUcBKIIYf0Bjc6v1m0Q0KtlrACwmL" style='width:100%'>
</div>
<div style="border:1px solid #000000;">
 <img src="https://drive.google.com/uc?export=view&id=15ypRtqA1aFdNsZjszIcgXadcqJb74hLm" style='width:100%'>  
</div>
</div>

#### Predator 개수 : 3

<div style="display:grid;grid-template-columns: 1fr 1fr;border:1px solid #000000;" >
<div style="border:1px solid #000000; text-align:center;">
Obstacle 0 
</div>
<div style="border:1px solid #000000;  text-align:center;">
Obstacle 2
</div>
<div style="border:1px solid #000000;">
<img src="https://drive.google.com/uc?export=view&id=1Iz3rURcmZIYI76SrnGEB70vQvh_xg2cn" style='width:100%'>
</div>
<div style="border:1px solid #000000;">
 <img src="https://drive.google.com/uc?export=view&id=1APSohTZjA-vIc6FQFUYKHO21N7HKVLtN" style='width:100%'>  
</div>
</div>

#### Predator 개수 : 4



<div style="display:grid;grid-template-columns: 1fr 1fr;border:1px solid #000000;" >
<div style="border:1px solid #000000; text-align:center;">
Obstacle 0 
</div>
<div style="border:1px solid #000000;  text-align:center;">
Obstacle 2
</div>
<div style="border:1px solid #000000;">
<img src="https://drive.google.com/uc?export=view&id=1bih9MnHHCs7fK8jZPfRxcyOLHAD6o2eQ" style='width:100%'>
</div>
<div style="border:1px solid #000000;">
 <img src="https://drive.google.com/uc?export=view&id=1mhze42N5HchE-VLC9EXnna7-sToeR5q2" style='width:100%'>  
</div>
</div>


 --- 

## 세부적인 하이퍼파라미터 테스트 

Predator Prey 환경에서 Sigmoid 는 ReLU보다 월등하게 높은 성능을 보이며, 메시지 dimension도 증가하면 성능이 증가하는 경향성을 보인다. 
그러나 몇몇 실험의 경우, message dimension이 증가할수록 성능이 저하되는 경우도 존재하였다. 이는 메시지 공간 자체의 불안정성 때문으로 판단되는데, 
최적의 bottleneck 사이즈에 대해서 고민이 필요한 부분이다. **너무 넢은 공간의 경우, 노이즈 dimension은 없는지, 노이즈 representation은 없는지 연구할 필요성이 느껴진다.**

물론 reward를 기준으로 dimension을 고를 수 있지만, 이는 메시지 공간에 대한 해석 및 특징을 기반으로 고른 것이 아니기에 
추후 안정적인 사용과 메시지에 대한 분석을 어렵게 만든다. 

### ENV: 2_1_0 Enemies / Goods / Obstacles

model | 0 | 1 | 2 | 
|---|---|---|---
('v1', 'ReLU', 1) |     5 |     5 |    -8 | 
('v1', 'ReLU', 2) |     5 |     5 |    -8 | 
('v1', 'ReLU', 4) |     5 |     5 |    -8 | 
('v1', 'ReLU', 8) |     5 |     5 |    -8 | 
('v1', 'ReLU', 16) |     5 |     5 |    -8 | 
('v1', 'Sigmoid', 1) |    44 |    44 |   -54 | 
('v1', 'Sigmoid', 2) |    44 |    44 |   -54 | 
('v1', 'Sigmoid', 4) |    44 |    44 |   -54 | 
('v1', 'Sigmoid', 8) |    44 |    44 |   -54 | 
('v1', 'Sigmoid', 16) |    44 |    44 |   -54 | 
('v2', 'ReLU', 1) |     4 |     4 |    -6 | 
('v2', 'ReLU', 2) |     5 |     5 |    -7 | 
('v2', 'ReLU', 4) |     9 |     9 |   -12 | 
('v2', 'ReLU', 8) |    10 |    10 |   -14 | 
('v2', 'ReLU', 16) |    13 |    13 |   -18 | 
('v2', 'Sigmoid', 1) |    39 |    39 |   -68 | 
('v2', 'Sigmoid', 2) |    37 |    37 |   -56 | 
('v2', 'Sigmoid', 4) |    47 |    47 |   -79 | 
('v2', 'Sigmoid', 8) |    65 |    65 |   -88 | 
('v2', 'Sigmoid', 16) |    37 |    37 |   -41 | 
('v3', 'ReLU', 1) |     7 |     7 |    -9 | 
('v3', 'ReLU', 2) |     6 |     6 |   -11 | 
('v3', 'ReLU', 4) |     5 |     5 |   -10 | 
('v3', 'ReLU', 8) |     6 |     6 |    -8 | 
('v3', 'ReLU', 16) |    17 |    17 |   -23 | 
('v3', 'Sigmoid', 1) |    58 |    58 |   -72 | 
('v3', 'Sigmoid', 2) |    54 |    54 |   -64 | 
('v3', 'Sigmoid', 4) |    40 |    40 |   -57 | 
('v3', 'Sigmoid', 8) |     9 |     9 |   -10 | 
('v3', 'Sigmoid', 16) |    18 |    18 |   -21 | 

 --- 

### ENV: 2_1_2 Enemies / Goods / Obstacles

model | 0 | 1 | 2 | 
|---|---|---|---
('v1', 'ReLU', 1) |     5 |     5 |    -9 | 
('v1', 'ReLU', 2) |     5 |     5 |    -9 | 
('v1', 'ReLU', 4) |     5 |     5 |    -9 | 
('v1', 'ReLU', 8) |     5 |     5 |    -9 | 
('v1', 'ReLU', 16) |     5 |     5 |    -9 | 
('v1', 'Sigmoid', 1) |    53 |    53 |   -75 | 
('v1', 'Sigmoid', 2) |    53 |    53 |   -75 | 
('v1', 'Sigmoid', 4) |    53 |    53 |   -75 | 
('v1', 'Sigmoid', 8) |    53 |    53 |   -75 | 
('v1', 'Sigmoid', 16) |    53 |    53 |   -75 | 
('v2', 'ReLU', 1) |    10 |    10 |   -13 | 
('v2', 'ReLU', 2) |     3 |     3 |    -6 | 
('v2', 'ReLU', 4) |     7 |     7 |   -10 | 
('v2', 'ReLU', 8) |    13 |    13 |   -18 | 
('v2', 'ReLU', 16) |    10 |    10 |   -17 | 
('v2', 'Sigmoid', 1) |    23 |    23 |   -32 | 
('v2', 'Sigmoid', 2) |    14 |    14 |   -17 | 
('v2', 'Sigmoid', 4) |    29 |    29 |   -36 | 
('v2', 'Sigmoid', 8) |    32 |    32 |   -43 | 
('v2', 'Sigmoid', 16) |    47 |    47 |   -62 | 
('v3', 'ReLU', 1) |     5 |     5 |    -7 | 
('v3', 'ReLU', 2) |     2 |     2 |    -5 | 
('v3', 'ReLU', 4) |     8 |     8 |   -12 | 
('v3', 'ReLU', 8) |     7 |     7 |   -10 | 
('v3', 'ReLU', 16) |     5 |     5 |    -7 | 
('v3', 'Sigmoid', 1) |     9 |     9 |   -11 | 
('v3', 'Sigmoid', 2) |    10 |    10 |   -12 | 
('v3', 'Sigmoid', 4) |    51 |    51 |   -64 | 
('v3', 'Sigmoid', 8) |    27 |    27 |   -33 | 
('v3', 'Sigmoid', 16) |    67 |    67 |   -79 | 

 --- 

###  ENV: 2_1_4 Enemies / Goods / Obstacles

|model | 0 | 1 | 2 | 
|---|---|---|---|
('v1', 'ReLU', 1) |     5 |     5 |    -8 | 
('v1', 'ReLU', 2) |     5 |     5 |    -8 | 
('v1', 'ReLU', 4) |     5 |     5 |    -8 | 
('v1', 'ReLU', 8) |     5 |     5 |    -8 | 
('v1', 'ReLU', 16) |     5 |     5 |    -8 | 
('v1', 'Sigmoid', 1) |    12 |    12 |   -14 | 
('v1', 'Sigmoid', 2) |    12 |    12 |   -14 | 
('v1', 'Sigmoid', 4) |    12 |    12 |   -14 | 
('v1', 'Sigmoid', 8) |    12 |    12 |   -14 | 
('v1', 'Sigmoid', 16) |    12 |    12 |   -14 | 
('v2', 'ReLU', 1) |    14 |    14 |   -22 | 
('v2', 'ReLU', 2) |     5 |     5 |    -8 | 
('v2', 'ReLU', 4) |     6 |     6 |    -9 | 
('v2', 'ReLU', 8) |     6 |     6 |    -7 | 
('v2', 'ReLU', 16) |     5 |     5 |    -7 | 
('v2', 'Sigmoid', 1) |     6 |     6 |    -8 | 
('v2', 'Sigmoid', 2) |     9 |     9 |   -11 | 
('v2', 'Sigmoid', 4) |     6 |     6 |    -8 | 
('v2', 'Sigmoid', 8) |     9 |     9 |   -14 | 
('v2', 'Sigmoid', 16) |    29 |    29 |   -33 | 
('v3', 'ReLU', 1) |     7 |     7 |    -9 | 
('v3', 'ReLU', 2) |     3 |     3 |    -5 | 
('v3', 'ReLU', 4) |     5 |     5 |   -11 | 
('v3', 'ReLU', 8) |     5 |     5 |    -7 | 
('v3', 'ReLU', 16) |     9 |     9 |   -11 | 
('v3', 'Sigmoid', 1) |     6 |     6 |    -7 | 
('v3', 'Sigmoid', 2) |     8 |     8 |   -10 | 
('v3', 'Sigmoid', 4) |    11 |    11 |   -13 | 
('v3', 'Sigmoid', 8) |    12 |    12 |   -14 | 
('v3', 'Sigmoid', 16) |    14 |    14 |   -17 | 

 --- 

### ENV: 2_2_0 Enemies / Goods / Obstacles

model | 0 | 1 | 2 | 3 | 
|---|---|---|---|---
('v1', 'ReLU', 1) |    10 |    10 |    -8 |    -6 | 
('v1', 'ReLU', 2) |    10 |    10 |    -8 |    -6 | 
('v1', 'ReLU', 4) |    10 |    10 |    -8 |    -6 | 
('v1', 'ReLU', 8) |    10 |    10 |    -8 |    -6 | 
('v1', 'ReLU', 16) |    10 |    10 |    -8 |    -6 | 
('v1', 'Sigmoid', 1) |    16 |    16 |    -8 |   -10 | 
('v1', 'Sigmoid', 2) |    16 |    16 |    -8 |   -10 | 
('v1', 'Sigmoid', 4) |    16 |    16 |    -8 |   -10 | 
('v1', 'Sigmoid', 8) |    16 |    16 |    -8 |   -10 | 
('v1', 'Sigmoid', 16) |    16 |    16 |    -8 |   -10 | 
('v2', 'ReLU', 1) |     7 |     7 |    -5 |    -6 | 
('v2', 'ReLU', 2) |     6 |     6 |    -4 |    -4 | 
('v2', 'ReLU', 4) |     6 |     6 |    -3 |    -5 | 
('v2', 'ReLU', 8) |     6 |     6 |    -4 |    -3 | 
('v2', 'ReLU', 16) |     8 |     8 |    -7 |    -4 | 
('v2', 'Sigmoid', 1) |    13 |    13 |    -8 |    -7 | 
('v2', 'Sigmoid', 2) |    30 |    30 |   -22 |   -16 | 
('v2', 'Sigmoid', 4) |    15 |    15 |   -12 |    -8 | 
('v2', 'Sigmoid', 8) |    22 |    22 |   -19 |    -8 | 
('v2', 'Sigmoid', 16) |    35 |    35 |   -27 |   -24 | 
('v3', 'ReLU', 1) |    11 |    11 |    -7 |    -6 | 
('v3', 'ReLU', 2) |     5 |     5 |    -3 |    -5 | 
('v3', 'ReLU', 4) |     5 |     5 |    -3 |    -5 | 
('v3', 'ReLU', 8) |     8 |     8 |    -7 |    -5 | 
('v3', 'ReLU', 16) |     6 |     6 |    -3 |    -4 | 
('v3', 'Sigmoid', 1) |    20 |    20 |    -5 |   -17 | 
('v3', 'Sigmoid', 2) |    18 |    18 |   -12 |   -11 | 
('v3', 'Sigmoid', 4) |    39 |    39 |   -21 |   -23 | 
('v3', 'Sigmoid', 8) |    20 |    20 |   -13 |   -10 | 
('v3', 'Sigmoid', 16) |    14 |    14 |    -8 |    -9 | 

 --- 

### ENV: 2_2_2 Enemies / Goods / Obstacles

model | 0 | 1 | 2 | 3 | 
|---|---|---|---|---
('v1', 'ReLU', 1) |     7 |     7 |    -4 |    -5 | 
('v1', 'ReLU', 2) |     7 |     7 |    -4 |    -5 | 
('v1', 'ReLU', 4) |     7 |     7 |    -4 |    -5 | 
('v1', 'ReLU', 8) |     7 |     7 |    -4 |    -5 | 
('v1', 'ReLU', 16) |     7 |     7 |    -4 |    -5 | 
('v1', 'Sigmoid', 1) |    29 |    29 |   -20 |   -16 | 
('v1', 'Sigmoid', 2) |    29 |    29 |   -20 |   -16 | 
('v1', 'Sigmoid', 4) |    29 |    29 |   -20 |   -16 | 
('v1', 'Sigmoid', 8) |    29 |    29 |   -20 |   -16 | 
('v1', 'Sigmoid', 16) |    29 |    29 |   -20 |   -16 | 
('v2', 'ReLU', 1) |    10 |    10 |    -6 |    -8 | 
('v2', 'ReLU', 2) |     4 |     4 |    -2 |    -4 | 
('v2', 'ReLU', 4) |     8 |     8 |    -5 |    -6 | 
('v2', 'ReLU', 8) |     7 |     7 |    -5 |    -4 | 
('v2', 'ReLU', 16) |    10 |    10 |    -7 |    -6 | 
('v2', 'Sigmoid', 1) |    18 |    18 |   -13 |    -9 | 
('v2', 'Sigmoid', 2) |    46 |    46 |   -30 |   -23 | 
('v2', 'Sigmoid', 4) |    40 |    40 |   -29 |   -35 | 
('v2', 'Sigmoid', 8) |    43 |    43 |   -31 |   -33 | 
('v2', 'Sigmoid', 16) |    12 |    12 |    -5 |    -8 | 
('v3', 'ReLU', 1) |     9 |     9 |    -5 |    -7 | 
('v3', 'ReLU', 2) |     8 |     8 |    -3 |    -7 | 
('v3', 'ReLU', 4) |     6 |     6 |    -3 |    -5 | 
('v3', 'ReLU', 8) |     9 |     9 |    -7 |    -5 | 
('v3', 'ReLU', 16) |     6 |     6 |    -6 |    -4 | 
('v3', 'Sigmoid', 1) |    29 |    29 |   -18 |   -17 | 
('v3', 'Sigmoid', 2) |    42 |    42 |   -27 |   -26 | 
('v3', 'Sigmoid', 4) |    38 |    38 |   -23 |   -25 | 
('v3', 'Sigmoid', 8) |    19 |    19 |   -12 |   -11 | 
('v3', 'Sigmoid', 16) |    66 |    66 |   -56 |   -59 | 

 --- 

###  ENV: 2_2_4 Enemies / Goods / Obstacles

model | 0 | 1 | 2 | 3 | 
|---|---|---|---|---
('v1', 'ReLU', 1) |    11 |    11 |    -6 |   -10 | 
('v1', 'ReLU', 2) |    11 |    11 |    -6 |   -10 | 
('v1', 'ReLU', 4) |    11 |    11 |    -6 |   -10 | 
('v1', 'ReLU', 8) |    11 |    11 |    -6 |   -10 | 
('v1', 'ReLU', 16) |    11 |    11 |    -6 |   -10 | 
('v1', 'Sigmoid', 1) |     7 |     7 |    -4 |    -4 | 
('v1', 'Sigmoid', 2) |     7 |     7 |    -4 |    -4 | 
('v1', 'Sigmoid', 4) |     7 |     7 |    -4 |    -4 | 
('v1', 'Sigmoid', 8) |     7 |     7 |    -4 |    -4 | 
('v1', 'Sigmoid', 16) |     7 |     7 |    -4 |    -4 | 
('v2', 'ReLU', 1) |     8 |     8 |    -6 |    -5 | 
('v2', 'ReLU', 2) |    10 |    10 |    -9 |    -7 | 
('v2', 'ReLU', 4) |     8 |     8 |    -7 |    -5 | 
('v2', 'ReLU', 8) |     5 |     5 |    -4 |    -4 | 
('v2', 'ReLU', 16) |     6 |     6 |    -5 |    -5 | 
('v2', 'Sigmoid', 1) |    12 |    12 |    -8 |    -8 | 
('v2', 'Sigmoid', 2) |    15 |    15 |    -9 |   -10 | 
('v2', 'Sigmoid', 4) |     7 |     7 |    -2 |    -7 | 
('v2', 'Sigmoid', 8) |     9 |     9 |    -5 |    -6 | 
('v2', 'Sigmoid', 16) |    14 |    14 |    -7 |   -10 | 
('v3', 'ReLU', 1) |     7 |     7 |    -5 |    -5 | 
('v3', 'ReLU', 2) |     8 |     8 |    -6 |    -5 | 
('v3', 'ReLU', 4) |     9 |     9 |    -6 |    -9 | 
('v3', 'ReLU', 8) |    12 |    12 |    -9 |    -6 | 
('v3', 'ReLU', 16) |     8 |     8 |    -8 |    -4 | 
('v3', 'Sigmoid', 1) |    15 |    15 |    -9 |   -10 | 
('v3', 'Sigmoid', 2) |    15 |    15 |    -8 |    -9 | 
('v3', 'Sigmoid', 4) |    24 |    24 |   -15 |   -16 | 
('v3', 'Sigmoid', 8) |    29 |    29 |   -18 |   -17 | 
('v3', 'Sigmoid', 16) |    26 |    26 |   -13 |   -19 | 

 --- 

###  ENV: 3_1_0 Enemies / Goods / Obstacles

model | 0 | 1 | 2 | 3 | 
|---|---|---|---|---
('v1', 'ReLU', 1) |    18 |    18 |    18 |   -22 | 
('v1', 'ReLU', 2) |    18 |    18 |    18 |   -22 | 
('v1', 'ReLU', 4) |    18 |    18 |    18 |   -22 | 
('v1', 'ReLU', 8) |    18 |    18 |    18 |   -22 | 
('v1', 'ReLU', 16) |    18 |    18 |    18 |   -22 | 
('v1', 'Sigmoid', 1) |    22 |    22 |    22 |   -24 | 
('v1', 'Sigmoid', 2) |    22 |    22 |    22 |   -24 | 
('v1', 'Sigmoid', 4) |    22 |    22 |    22 |   -24 | 
('v1', 'Sigmoid', 8) |    22 |    22 |    22 |   -24 | 
('v1', 'Sigmoid', 16) |    22 |    22 |    22 |   -24 | 
('v2', 'ReLU', 1) |    12 |    12 |    12 |   -15 | 
('v2', 'ReLU', 2) |    11 |    11 |    11 |   -16 | 
('v2', 'ReLU', 4) |    12 |    12 |    12 |   -17 | 
('v2', 'ReLU', 8) |    14 |    14 |    14 |   -18 | 
('v2', 'ReLU', 16) |    23 |    23 |    23 |   -30 | 
('v2', 'Sigmoid', 1) |    57 |    57 |    57 |   -76 | 
('v2', 'Sigmoid', 2) |    62 |    62 |    62 |   -88 | 
('v2', 'Sigmoid', 4) |    89 |    89 |    89 |  -104 | 
('v2', 'Sigmoid', 8) |    97 |    97 |    97 |  -128 | 
('v2', 'Sigmoid', 16) |    28 |    28 |    28 |   -34 | 
('v3', 'ReLU', 1) |    14 |    14 |    14 |   -21 | 
('v3', 'ReLU', 2) |    23 |    23 |    23 |   -29 | 
('v3', 'ReLU', 4) |     5 |     5 |     5 |   -11 | 
('v3', 'ReLU', 8) |    10 |    10 |    10 |   -15 | 
('v3', 'ReLU', 16) |    17 |    17 |    17 |   -22 | 
('v3', 'Sigmoid', 1) |    48 |    48 |    48 |   -60 | 
('v3', 'Sigmoid', 2) |    50 |    50 |    50 |   -56 | 
('v3', 'Sigmoid', 4) |    47 |    47 |    47 |   -56 | 
('v3', 'Sigmoid', 8) |    44 |    44 |    44 |   -51 | 
('v3', 'Sigmoid', 16) |    65 |    65 |    65 |   -73 | 

 --- 

###  ENV: 3_1_2 Enemies / Goods / Obstacles

model | 0 | 1 | 2 | 3 | 
|---|---|---|---|---
('v1', 'ReLU', 1) |    16 |    16 |    16 |   -22 | 
('v1', 'ReLU', 2) |    16 |    16 |    16 |   -22 | 
('v1', 'ReLU', 4) |    16 |    16 |    16 |   -22 | 
('v1', 'ReLU', 8) |    16 |    16 |    16 |   -22 | 
('v1', 'ReLU', 16) |    16 |    16 |    16 |   -22 | 
('v1', 'Sigmoid', 1) |     7 |     7 |     7 |    -9 | 
('v1', 'Sigmoid', 2) |     7 |     7 |     7 |    -9 | 
('v1', 'Sigmoid', 4) |     7 |     7 |     7 |    -9 | 
('v1', 'Sigmoid', 8) |     7 |     7 |     7 |    -9 | 
('v1', 'Sigmoid', 16) |     7 |     7 |     7 |    -9 | 
('v2', 'ReLU', 1) |    13 |    13 |    13 |   -20 | 
('v2', 'ReLU', 2) |    15 |    15 |    15 |   -21 | 
('v2', 'ReLU', 4) |    12 |    12 |    12 |   -18 | 
('v2', 'ReLU', 8) |     9 |     9 |     9 |   -13 | 
('v2', 'ReLU', 16) |    10 |    10 |    10 |   -15 | 
('v2', 'Sigmoid', 1) |    59 |    59 |    59 |   -72 | 
('v2', 'Sigmoid', 2) |    58 |    58 |    58 |   -70 | 
('v2', 'Sigmoid', 4) |    36 |    36 |    36 |   -44 | 
('v2', 'Sigmoid', 8) |    45 |    45 |    45 |   -51 | 
('v2', 'Sigmoid', 16) |    38 |    38 |    38 |   -43 | 
('v3', 'ReLU', 1) |    15 |    15 |    15 |   -21 | 
('v3', 'ReLU', 2) |    14 |    14 |    14 |   -20 | 
('v3', 'ReLU', 4) |     6 |     6 |     6 |   -13 | 
('v3', 'ReLU', 8) |    14 |    14 |    14 |   -21 | 
('v3', 'ReLU', 16) |    16 |    16 |    16 |   -27 | 
('v3', 'Sigmoid', 1) |    55 |    55 |    55 |   -65 | 
('v3', 'Sigmoid', 2) |    28 |    28 |    28 |   -32 | 
('v3', 'Sigmoid', 4) |    20 |    20 |    20 |   -21 | 
('v3', 'Sigmoid', 8) |    24 |    24 |    24 |   -31 | 
('v3', 'Sigmoid', 16) |    51 |    51 |    51 |   -69 | 

 --- 

###  ENV: 3_1_4 Enemies / Goods / Obstacles

model | 0 | 1 | 2 | 3 | 
|---|---|---|---|---
('v1', 'ReLU', 1) |    12 |    12 |    12 |   -19 | 
('v1', 'ReLU', 2) |    12 |    12 |    12 |   -19 | 
('v1', 'ReLU', 4) |    12 |    12 |    12 |   -19 | 
('v1', 'ReLU', 8) |    12 |    12 |    12 |   -19 | 
('v1', 'ReLU', 16) |    12 |    12 |    12 |   -19 | 
('v1', 'Sigmoid', 1) |    55 |    55 |    55 |   -65 | 
('v1', 'Sigmoid', 2) |    55 |    55 |    55 |   -65 | 
('v1', 'Sigmoid', 4) |    55 |    55 |    55 |   -65 | 
('v1', 'Sigmoid', 8) |    55 |    55 |    55 |   -65 | 
('v1', 'Sigmoid', 16) |    55 |    55 |    55 |   -65 | 
('v2', 'ReLU', 1) |    13 |    13 |    13 |   -17 | 
('v2', 'ReLU', 2) |     8 |     8 |     8 |   -12 | 
('v2', 'ReLU', 4) |     9 |     9 |     9 |   -15 | 
('v2', 'ReLU', 8) |     8 |     8 |     8 |   -16 | 
('v2', 'ReLU', 16) |    14 |    14 |    14 |   -20 | 
('v2', 'Sigmoid', 1) |    46 |    46 |    46 |   -68 | 
('v2', 'Sigmoid', 2) |    27 |    27 |    27 |   -33 | 
('v2', 'Sigmoid', 4) |    10 |    10 |    10 |   -11 | 
('v2', 'Sigmoid', 8) |    38 |    38 |    38 |   -44 | 
('v2', 'Sigmoid', 16) |    59 |    59 |    59 |   -80 | 
('v3', 'ReLU', 1) |    13 |    13 |    13 |   -18 | 
('v3', 'ReLU', 2) |    12 |    12 |    12 |   -23 | 
('v3', 'ReLU', 4) |    25 |    25 |    25 |   -34 | 
('v3', 'ReLU', 8) |    13 |    13 |    13 |   -17 | 
('v3', 'ReLU', 16) |    14 |    14 |    14 |   -19 | 
('v3', 'Sigmoid', 1) |    33 |    33 |    33 |   -42 | 
('v3', 'Sigmoid', 2) |    34 |    34 |    34 |   -41 | 
('v3', 'Sigmoid', 4) |    59 |    59 |    59 |   -71 | 
('v3', 'Sigmoid', 8) |    49 |    49 |    49 |   -73 | 
('v3', 'Sigmoid', 16) |    46 |    46 |    46 |   -55 | 

 --- 

###  ENV: 3_2_0 Enemies / Goods / Obstacles

model | 0 | 1 | 2 | 3 | 4 | 
|---|---|---|---|---|---
('v1', 'ReLU', 1) |    13 |    13 |    13 |    -8 |    -9 | 
('v1', 'ReLU', 2) |    13 |    13 |    13 |    -8 |    -9 | 
('v1', 'ReLU', 4) |    13 |    13 |    13 |    -8 |    -9 | 
('v1', 'ReLU', 8) |    13 |    13 |    13 |    -8 |    -9 | 
('v1', 'ReLU', 16) |    13 |    13 |    13 |    -8 |    -9 | 
('v1', 'Sigmoid', 1) |    19 |    19 |    19 |   -11 |   -13 | 
('v1', 'Sigmoid', 2) |    19 |    19 |    19 |   -11 |   -13 | 
('v1', 'Sigmoid', 4) |    19 |    19 |    19 |   -11 |   -13 | 
('v1', 'Sigmoid', 8) |    19 |    19 |    19 |   -11 |   -13 | 
('v1', 'Sigmoid', 16) |    19 |    19 |    19 |   -11 |   -13 | 
('v2', 'ReLU', 1) |    18 |    18 |    18 |   -12 |    -9 | 
('v2', 'ReLU', 2) |    14 |    14 |    14 |    -8 |   -10 | 
('v2', 'ReLU', 4) |    12 |    12 |    12 |    -9 |   -12 | 
('v2', 'ReLU', 8) |    12 |    12 |    12 |    -9 |    -8 | 
('v2', 'ReLU', 16) |    11 |    11 |    11 |    -8 |   -11 | 
('v2', 'Sigmoid', 1) |    24 |    24 |    24 |   -13 |   -15 | 
('v2', 'Sigmoid', 2) |    44 |    44 |    44 |   -27 |   -25 | 
('v2', 'Sigmoid', 4) |    25 |    25 |    25 |   -14 |   -13 | 
('v2', 'Sigmoid', 8) |    38 |    38 |    38 |   -34 |   -29 | 
('v2', 'Sigmoid', 16) |    29 |    29 |    29 |   -19 |   -17 | 
('v3', 'ReLU', 1) |     9 |     9 |     9 |    -8 |    -6 | 
('v3', 'ReLU', 2) |    10 |    10 |    10 |    -9 |    -6 | 
('v3', 'ReLU', 4) |    12 |    12 |    12 |   -12 |    -6 | 
('v3', 'ReLU', 8) |    14 |    14 |    14 |    -8 |   -10 | 
('v3', 'ReLU', 16) |    10 |    10 |    10 |    -6 |    -8 | 
('v3', 'Sigmoid', 1) |    40 |    40 |    40 |   -27 |   -27 | 
('v3', 'Sigmoid', 2) |    27 |    27 |    27 |   -11 |   -19 | 
('v3', 'Sigmoid', 4) |    48 |    48 |    48 |   -33 |   -28 | 
('v3', 'Sigmoid', 8) |    61 |    61 |    61 |   -44 |   -42 | 
('v3', 'Sigmoid', 16) |    39 |    39 |    39 |   -18 |   -26 | 

 --- 

###  ENV: 3_2_2 Enemies / Goods / Obstacles

model | 0 | 1 | 2 | 3 | 4 | 
|---|---|---|---|---|---
('v1', 'ReLU', 1) |    13 |    13 |    13 |   -11 |    -7 | 
('v1', 'ReLU', 2) |    13 |    13 |    13 |   -11 |    -7 | 
('v1', 'ReLU', 4) |    13 |    13 |    13 |   -11 |    -7 | 
('v1', 'ReLU', 8) |    13 |    13 |    13 |   -11 |    -7 | 
('v1', 'ReLU', 16) |    13 |    13 |    13 |   -11 |    -7 | 
('v1', 'Sigmoid', 1) |    58 |    58 |    58 |   -46 |   -43 | 
('v1', 'Sigmoid', 2) |    58 |    58 |    58 |   -46 |   -43 | 
('v1', 'Sigmoid', 4) |    58 |    58 |    58 |   -46 |   -43 | 
('v1', 'Sigmoid', 8) |    58 |    58 |    58 |   -46 |   -43 | 
('v1', 'Sigmoid', 16) |    58 |    58 |    58 |   -46 |   -43 | 
('v2', 'ReLU', 1) |    13 |    13 |    13 |   -12 |    -7 | 
('v2', 'ReLU', 2) |    12 |    12 |    12 |   -10 |   -12 | 
('v2', 'ReLU', 4) |    15 |    15 |    15 |   -12 |    -8 | 
('v2', 'ReLU', 8) |    13 |    13 |    13 |   -10 |    -8 | 
('v2', 'ReLU', 16) |    11 |    11 |    11 |    -6 |    -8 | 
('v2', 'Sigmoid', 1) |    27 |    27 |    27 |   -14 |   -16 | 
('v2', 'Sigmoid', 2) |    28 |    28 |    28 |   -14 |   -20 | 
('v2', 'Sigmoid', 4) |    47 |    47 |    47 |   -28 |   -24 | 
('v2', 'Sigmoid', 8) |    43 |    43 |    43 |   -33 |   -33 | 
('v2', 'Sigmoid', 16) |    15 |    15 |    15 |   -10 |    -8 | 
('v3', 'ReLU', 1) |    14 |    14 |    14 |   -13 |    -9 | 
('v3', 'ReLU', 2) |    16 |    16 |    16 |   -12 |    -9 | 
('v3', 'ReLU', 4) |    12 |    12 |    12 |   -10 |    -9 | 
('v3', 'ReLU', 8) |    14 |    14 |    14 |   -11 |   -11 | 
('v3', 'ReLU', 16) |    16 |    16 |    16 |   -11 |   -11 | 
('v3', 'Sigmoid', 1) |    46 |    46 |    46 |   -35 |   -32 | 
('v3', 'Sigmoid', 2) |    22 |    22 |    22 |   -10 |   -16 | 
('v3', 'Sigmoid', 4) |    27 |    27 |    27 |   -16 |   -18 | 
('v3', 'Sigmoid', 8) |    38 |    38 |    38 |   -21 |   -30 | 
('v3', 'Sigmoid', 16) |    28 |    28 |    28 |   -16 |   -16 | 

 --- 

###  ENV: 3_2_4 Enemies / Goods / Obstacles

model | 0 | 1 | 2 | 3 | 4 | 
|---|---|---|---|---|---
('v1', 'ReLU', 1) |    17 |    17 |    17 |   -13 |   -10 | 
('v1', 'ReLU', 2) |    17 |    17 |    17 |   -13 |   -10 | 
('v1', 'ReLU', 4) |    17 |    17 |    17 |   -13 |   -10 | 
('v1', 'ReLU', 8) |    17 |    17 |    17 |   -13 |   -10 | 
('v1', 'ReLU', 16) |    17 |    17 |    17 |   -13 |   -10 | 
('v1', 'Sigmoid', 1) |    54 |    54 |    54 |   -33 |   -35 | 
('v1', 'Sigmoid', 2) |    54 |    54 |    54 |   -33 |   -35 | 
('v1', 'Sigmoid', 4) |    54 |    54 |    54 |   -33 |   -35 | 
('v1', 'Sigmoid', 8) |    54 |    54 |    54 |   -33 |   -35 | 
('v1', 'Sigmoid', 16) |    54 |    54 |    54 |   -33 |   -35 | 
('v2', 'ReLU', 1) |    16 |    16 |    16 |   -11 |   -17 | 
('v2', 'ReLU', 2) |    15 |    15 |    15 |   -11 |   -11 | 
('v2', 'ReLU', 4) |    13 |    13 |    13 |   -10 |   -12 | 
('v2', 'ReLU', 8) |    17 |    17 |    17 |   -13 |   -10 | 
('v2', 'ReLU', 16) |    17 |    17 |    17 |   -10 |   -15 | 
('v2', 'Sigmoid', 1) |    18 |    18 |    18 |    -7 |   -14 | 
('v2', 'Sigmoid', 2) |    23 |    23 |    23 |   -18 |   -13 | 
('v2', 'Sigmoid', 4) |    20 |    20 |    20 |   -13 |   -13 | 
('v2', 'Sigmoid', 8) |    35 |    35 |    35 |   -16 |   -25 | 
('v2', 'Sigmoid', 16) |    23 |    23 |    23 |   -11 |   -16 | 
('v3', 'ReLU', 1) |    13 |    13 |    13 |    -9 |   -10 | 
('v3', 'ReLU', 2) |     9 |     9 |     9 |    -7 |    -9 | 
('v3', 'ReLU', 4) |    16 |    16 |    16 |   -12 |   -10 | 
('v3', 'ReLU', 8) |    11 |    11 |    11 |    -8 |   -11 | 
('v3', 'ReLU', 16) |    17 |    17 |    17 |   -12 |   -14 | 
('v3', 'Sigmoid', 1) |    23 |    23 |    23 |   -11 |   -15 | 
('v3', 'Sigmoid', 2) |    25 |    25 |    25 |   -18 |   -13 | 
('v3', 'Sigmoid', 4) |    27 |    27 |    27 |   -16 |   -20 | 
('v3', 'Sigmoid', 8) |    28 |    28 |    28 |   -18 |   -23 | 
('v3', 'Sigmoid', 16) |    29 |    29 |    29 |   -21 |   -22 | 

 --- 

###  ENV: 4_1_0 Enemies / Goods / Obstacles

model | 0 | 1 | 2 | 3 | 4 | 
|---|---|---|---|---|---
('v1', 'ReLU', 1) |    22 |    22 |    22 |    22 |   -29 | 
('v1', 'ReLU', 2) |    22 |    22 |    22 |    22 |   -29 | 
('v1', 'ReLU', 4) |    22 |    22 |    22 |    22 |   -29 | 
('v1', 'ReLU', 8) |    22 |    22 |    22 |    22 |   -29 | 
('v1', 'ReLU', 16) |    22 |    22 |    22 |    22 |   -29 | 
('v1', 'Sigmoid', 1) |    53 |    53 |    53 |    53 |   -60 | 
('v1', 'Sigmoid', 2) |    53 |    53 |    53 |    53 |   -60 | 
('v1', 'Sigmoid', 4) |    53 |    53 |    53 |    53 |   -60 | 
('v1', 'Sigmoid', 8) |    53 |    53 |    53 |    53 |   -60 | 
('v1', 'Sigmoid', 16) |    53 |    53 |    53 |    53 |   -60 | 
('v2', 'ReLU', 1) |    22 |    22 |    22 |    22 |   -30 | 
('v2', 'ReLU', 2) |    24 |    24 |    24 |    24 |   -32 | 
('v2', 'ReLU', 4) |    35 |    35 |    35 |    35 |   -44 | 
('v2', 'ReLU', 8) |    22 |    22 |    22 |    22 |   -30 | 
('v2', 'ReLU', 16) |    24 |    24 |    24 |    24 |   -34 | 
('v2', 'Sigmoid', 1) |    24 |    24 |    24 |    24 |   -28 | 
('v2', 'Sigmoid', 2) |    48 |    48 |    48 |    48 |   -63 | 
('v2', 'Sigmoid', 4) |    75 |    75 |    75 |    75 |   -95 | 
('v2', 'Sigmoid', 8) |    73 |    73 |    73 |    73 |   -91 | 
('v2', 'Sigmoid', 16) |   105 |   105 |   105 |   105 |  -144 | 
('v3', 'ReLU', 1) |    21 |    21 |    21 |    21 |   -29 | 
('v3', 'ReLU', 2) |    15 |    15 |    15 |    15 |   -23 | 
('v3', 'ReLU', 4) |    13 |    13 |    13 |    13 |   -21 | 
('v3', 'ReLU', 8) |    15 |    15 |    15 |    15 |   -23 | 
('v3', 'ReLU', 16) |    25 |    25 |    25 |    25 |   -35 | 
('v3', 'Sigmoid', 1) |    47 |    47 |    47 |    47 |   -62 | 
('v3', 'Sigmoid', 2) |    21 |    21 |    21 |    21 |   -26 | 
('v3', 'Sigmoid', 4) |    12 |    12 |    12 |    12 |   -14 | 
('v3', 'Sigmoid', 8) |    56 |    56 |    56 |    56 |   -95 | 
('v3', 'Sigmoid', 16) |    29 |    29 |    29 |    29 |   -36 | 

 --- 

###  ENV: 4_1_2 Enemies / Goods / Obstacles

model | 0 | 1 | 2 | 3 | 4 | 
|---|---|---|---|---|---
('v1', 'ReLU', 1) |    15 |    15 |    15 |    15 |   -23 | 
('v1', 'ReLU', 2) |    15 |    15 |    15 |    15 |   -23 | 
('v1', 'ReLU', 4) |    15 |    15 |    15 |    15 |   -23 | 
('v1', 'ReLU', 8) |    15 |    15 |    15 |    15 |   -23 | 
('v1', 'ReLU', 16) |    15 |    15 |    15 |    15 |   -23 | 
('v1', 'Sigmoid', 1) |    23 |    23 |    23 |    23 |   -28 | 
('v1', 'Sigmoid', 2) |    23 |    23 |    23 |    23 |   -28 | 
('v1', 'Sigmoid', 4) |    23 |    23 |    23 |    23 |   -28 | 
('v1', 'Sigmoid', 8) |    23 |    23 |    23 |    23 |   -28 | 
('v1', 'Sigmoid', 16) |    23 |    23 |    23 |    23 |   -28 | 
('v2', 'ReLU', 1) |    14 |    14 |    14 |    14 |   -23 | 
('v2', 'ReLU', 2) |    20 |    20 |    20 |    20 |   -28 | 
('v2', 'ReLU', 4) |    14 |    14 |    14 |    14 |   -21 | 
('v2', 'ReLU', 8) |    13 |    13 |    13 |    13 |   -22 | 
('v2', 'ReLU', 16) |    14 |    14 |    14 |    14 |   -23 | 
('v2', 'Sigmoid', 1) |    24 |    24 |    24 |    24 |   -31 | 
('v2', 'Sigmoid', 2) |    28 |    28 |    28 |    28 |   -42 | 
('v2', 'Sigmoid', 4) |    60 |    60 |    60 |    60 |   -85 | 
('v2', 'Sigmoid', 8) |    35 |    35 |    35 |    35 |   -45 | 
('v2', 'Sigmoid', 16) |    55 |    55 |    55 |    55 |   -71 | 
('v3', 'ReLU', 1) |    17 |    17 |    17 |    17 |   -31 | 
('v3', 'ReLU', 2) |    20 |    20 |    20 |    20 |   -30 | 
('v3', 'ReLU', 4) |    14 |    14 |    14 |    14 |   -22 | 
('v3', 'ReLU', 8) |    14 |    14 |    14 |    14 |   -26 | 
('v3', 'ReLU', 16) |    24 |    24 |    24 |    24 |   -35 | 
('v3', 'Sigmoid', 1) |    61 |    61 |    61 |    61 |   -82 | 
('v3', 'Sigmoid', 2) |    10 |    10 |    10 |    10 |   -13 | 
('v3', 'Sigmoid', 4) |    26 |    26 |    26 |    26 |   -32 | 
('v3', 'Sigmoid', 8) |    36 |    36 |    36 |    36 |   -71 | 
('v3', 'Sigmoid', 16) |    43 |    43 |    43 |    43 |   -53 | 

 --- 

### ENV: 4_1_4 Enemies / Goods / Obstacles

model | 0 | 1 | 2 | 3 | 4 | 
|---|---|---|---|---|---
('v1', 'ReLU', 1) |    15 |    15 |    15 |    15 |   -31 | 
('v1', 'ReLU', 2) |    15 |    15 |    15 |    15 |   -31 | 
('v1', 'ReLU', 4) |    15 |    15 |    15 |    15 |   -31 | 
('v1', 'ReLU', 8) |    15 |    15 |    15 |    15 |   -31 | 
('v1', 'ReLU', 16) |    15 |    15 |    15 |    15 |   -31 | 
('v1', 'Sigmoid', 1) |    15 |    15 |    15 |    15 |   -23 | 
('v1', 'Sigmoid', 2) |    15 |    15 |    15 |    15 |   -23 | 
('v1', 'Sigmoid', 4) |    15 |    15 |    15 |    15 |   -23 | 
('v1', 'Sigmoid', 8) |    15 |    15 |    15 |    15 |   -23 | 
('v1', 'Sigmoid', 16) |    15 |    15 |    15 |    15 |   -23 | 
('v2', 'ReLU', 1) |    21 |    21 |    21 |    21 |   -30 | 
('v2', 'ReLU', 2) |    17 |    17 |    17 |    17 |   -25 | 
('v2', 'ReLU', 4) |    12 |    12 |    12 |    12 |   -23 | 
('v2', 'ReLU', 8) |    19 |    19 |    19 |    19 |   -32 | 
('v2', 'ReLU', 16) |    11 |    11 |    11 |    11 |   -17 | 
('v2', 'Sigmoid', 1) |    28 |    28 |    28 |    28 |   -36 | 
('v2', 'Sigmoid', 2) |    50 |    50 |    50 |    50 |   -79 | 
('v2', 'Sigmoid', 4) |    12 |    12 |    12 |    12 |   -16 | 
('v2', 'Sigmoid', 8) |    33 |    33 |    33 |    33 |   -38 | 
('v2', 'Sigmoid', 16) |    22 |    22 |    22 |    22 |   -34 | 
('v3', 'ReLU', 1) |    16 |    16 |    16 |    16 |   -28 | 
('v3', 'ReLU', 2) |    10 |    10 |    10 |    10 |   -17 | 
('v3', 'ReLU', 4) |    23 |    23 |    23 |    23 |   -46 | 
('v3', 'ReLU', 8) |    15 |    15 |    15 |    15 |   -22 | 
('v3', 'ReLU', 16) |    22 |    22 |    22 |    22 |   -36 | 
('v3', 'Sigmoid', 1) |    47 |    47 |    47 |    47 |   -76 | 
('v3', 'Sigmoid', 2) |    36 |    36 |    36 |    36 |   -57 | 
('v3', 'Sigmoid', 4) |    13 |    13 |    13 |    13 |   -19 | 
('v3', 'Sigmoid', 8) |    32 |    32 |    32 |    32 |   -45 | 
('v3', 'Sigmoid', 16) |    13 |    13 |    13 |    13 |   -18 | 

 --- 

### ENV: 4_2_0 Enemies / Goods / Obstacles

model | 0 | 1 | 2 | 3 | 4 | 5 | 
|---|---|---|---|---|---|---
('v1', 'ReLU', 1) |    20 |    20 |    20 |    20 |   -10 |   -15 | 
('v1', 'ReLU', 2) |    20 |    20 |    20 |    20 |   -10 |   -15 | 
('v1', 'ReLU', 4) |    20 |    20 |    20 |    20 |   -10 |   -15 | 
('v1', 'ReLU', 8) |    20 |    20 |    20 |    20 |   -10 |   -15 | 
('v1', 'ReLU', 16) |    20 |    20 |    20 |    20 |   -10 |   -15 | 
('v1', 'Sigmoid', 1) |    46 |    46 |    46 |    46 |   -30 |   -30 | 
('v1', 'Sigmoid', 2) |    46 |    46 |    46 |    46 |   -30 |   -30 | 
('v1', 'Sigmoid', 4) |    46 |    46 |    46 |    46 |   -30 |   -30 | 
('v1', 'Sigmoid', 8) |    46 |    46 |    46 |    46 |   -30 |   -30 | 
('v1', 'Sigmoid', 16) |    46 |    46 |    46 |    46 |   -30 |   -30 | 
('v2', 'ReLU', 1) |    14 |    14 |    14 |    14 |    -8 |   -14 | 
('v2', 'ReLU', 2) |    15 |    15 |    15 |    15 |    -9 |   -13 | 
('v2', 'ReLU', 4) |    15 |    15 |    15 |    15 |    -9 |   -10 | 
('v2', 'ReLU', 8) |    23 |    23 |    23 |    23 |    -8 |   -21 | 
('v2', 'ReLU', 16) |    20 |    20 |    20 |    20 |   -17 |   -16 | 
('v2', 'Sigmoid', 1) |    38 |    38 |    38 |    38 |   -21 |   -33 | 
('v2', 'Sigmoid', 2) |    25 |    25 |    25 |    25 |   -14 |   -16 | 
('v2', 'Sigmoid', 4) |    50 |    50 |    50 |    50 |   -34 |   -30 | 
('v2', 'Sigmoid', 8) |    35 |    35 |    35 |    35 |   -26 |   -26 | 
('v2', 'Sigmoid', 16) |    32 |    32 |    32 |    32 |   -30 |   -20 | 
('v3', 'ReLU', 1) |    16 |    16 |    16 |    16 |   -13 |   -11 | 
('v3', 'ReLU', 2) |    19 |    19 |    19 |    19 |   -11 |   -14 | 
('v3', 'ReLU', 4) |    19 |    19 |    19 |    19 |   -10 |   -15 | 
('v3', 'ReLU', 8) |    14 |    14 |    14 |    14 |   -12 |    -6 | 
('v3', 'ReLU', 16) |    19 |    19 |    19 |    19 |   -13 |   -12 | 
('v3', 'Sigmoid', 1) |    35 |    35 |    35 |    35 |   -29 |   -26 | 
('v3', 'Sigmoid', 2) |    34 |    34 |    34 |    34 |   -17 |   -21 | 
('v3', 'Sigmoid', 4) |    20 |    20 |    20 |    20 |   -10 |   -11 | 
('v3', 'Sigmoid', 8) |    43 |    43 |    43 |    43 |   -27 |   -21 | 
('v3', 'Sigmoid', 16) |    43 |    43 |    43 |    43 |   -22 |   -28 | 

 --- 

ENV: 4_2_2 Enemies / Goods / Obstacles


model | 0 | 1 | 2 | 3 | 4 | 5 | 
|---|---|---|---|---|---|---
('v1', 'ReLU', 1) |    19 |    19 |    19 |    19 |   -16 |   -17 | 
('v1', 'ReLU', 2) |    19 |    19 |    19 |    19 |   -16 |   -17 | 
('v1', 'ReLU', 4) |    19 |    19 |    19 |    19 |   -16 |   -17 | 
('v1', 'ReLU', 8) |    19 |    19 |    19 |    19 |   -16 |   -17 | 
('v1', 'ReLU', 16) |    19 |    19 |    19 |    19 |   -16 |   -17 | 
('v1', 'Sigmoid', 1) |    34 |    34 |    34 |    34 |   -26 |   -20 | 
('v1', 'Sigmoid', 2) |    34 |    34 |    34 |    34 |   -26 |   -20 | 
('v1', 'Sigmoid', 4) |    34 |    34 |    34 |    34 |   -26 |   -20 | 
('v1', 'Sigmoid', 8) |    34 |    34 |    34 |    34 |   -26 |   -20 | 
('v1', 'Sigmoid', 16) |    34 |    34 |    34 |    34 |   -26 |   -20 | 
('v2', 'ReLU', 1) |    20 |    20 |    20 |    20 |    -9 |   -21 | 
('v2', 'ReLU', 2) |    17 |    17 |    17 |    17 |   -14 |   -11 | 
('v2', 'ReLU', 4) |    19 |    19 |    19 |    19 |   -11 |   -16 | 
('v2', 'ReLU', 8) |    24 |    24 |    24 |    24 |   -16 |   -18 | 
('v2', 'ReLU', 16) |    22 |    22 |    22 |    22 |   -15 |   -19 | 
('v2', 'Sigmoid', 1) |    60 |    60 |    60 |    60 |   -43 |   -44 | 
('v2', 'Sigmoid', 2) |    57 |    57 |    57 |    57 |   -40 |   -41 | 
('v2', 'Sigmoid', 4) |    39 |    39 |    39 |    39 |   -19 |   -26 | 
('v2', 'Sigmoid', 8) |    55 |    55 |    55 |    55 |   -37 |   -44 | 
('v2', 'Sigmoid', 16) |    58 |    58 |    58 |    58 |   -36 |   -41 | 
('v3', 'ReLU', 1) |    14 |    14 |    14 |    14 |    -9 |   -13 | 
('v3', 'ReLU', 2) |    14 |    14 |    14 |    14 |   -10 |   -13 | 
('v3', 'ReLU', 4) |    14 |    14 |    14 |    14 |    -8 |   -13 | 
('v3', 'ReLU', 8) |    20 |    20 |    20 |    20 |   -17 |   -16 | 
('v3', 'ReLU', 16) |    20 |    20 |    20 |    20 |   -15 |   -16 | 
('v3', 'Sigmoid', 1) |    28 |    28 |    28 |    28 |   -16 |   -16 | 
('v3', 'Sigmoid', 2) |    17 |    17 |    17 |    17 |   -10 |   -13 | 
('v3', 'Sigmoid', 4) |    18 |    18 |    18 |    18 |   -12 |   -13 | 
('v3', 'Sigmoid', 8) |    47 |    47 |    47 |    47 |   -28 |   -30 | 
('v3', 'Sigmoid', 16) |    50 |    50 |    50 |    50 |   -29 |   -29 | 

 --- 

### ENV: 4_2_4 Enemies / Goods / Obstacles


model | 0 | 1 | 2 | 3 | 4 | 5 | 
|---|---|---|---|---|---|---
('v1', 'ReLU', 1) |    26 |    26 |    26 |    26 |   -26 |   -20 | 
('v1', 'ReLU', 2) |    26 |    26 |    26 |    26 |   -26 |   -20 | 
('v1', 'ReLU', 4) |    26 |    26 |    26 |    26 |   -26 |   -20 | 
('v1', 'ReLU', 8) |    26 |    26 |    26 |    26 |   -26 |   -20 | 
('v1', 'ReLU', 16) |    26 |    26 |    26 |    26 |   -26 |   -20 | 
('v1', 'Sigmoid', 1) |    21 |    21 |    21 |    21 |   -15 |   -16 | 
('v1', 'Sigmoid', 2) |    21 |    21 |    21 |    21 |   -15 |   -16 | 
('v1', 'Sigmoid', 4) |    21 |    21 |    21 |    21 |   -15 |   -16 | 
('v1', 'Sigmoid', 8) |    21 |    21 |    21 |    21 |   -15 |   -16 | 
('v1', 'Sigmoid', 16) |    11 |    11 |    11 |    11 |    -8 |   -11 | 
('v2', 'ReLU', 1) |    23 |    23 |    23 |    23 |   -18 |   -19 | 
('v2', 'ReLU', 2) |    21 |    21 |    21 |    21 |   -15 |   -16 | 
('v2', 'ReLU', 4) |    22 |    22 |    22 |    22 |   -19 |   -18 | 
('v2', 'ReLU', 8) |    19 |    19 |    19 |    19 |   -14 |   -15 | 
('v2', 'ReLU', 16) |    23 |    23 |    23 |    23 |   -15 |   -17 | 
('v2', 'Sigmoid', 1) |    45 |    45 |    45 |    45 |   -43 |   -31 | 
('v2', 'Sigmoid', 2) |    60 |    60 |    60 |    60 |   -43 |   -46 | 
('v2', 'Sigmoid', 4) |    37 |    37 |    37 |    37 |   -24 |   -27 | 
('v2', 'Sigmoid', 8) |    49 |    49 |    49 |    49 |   -31 |   -33 | 
('v2', 'Sigmoid', 16) |    31 |    31 |    31 |    31 |   -18 |   -22 | 
('v3', 'ReLU', 1) |    22 |    22 |    22 |    22 |   -15 |   -16 | 
('v3', 'ReLU', 2) |    21 |    21 |    21 |    21 |   -17 |   -19 | 
('v3', 'ReLU', 4) |    16 |    16 |    16 |    16 |   -12 |   -14 | 
('v3', 'ReLU', 8) |    15 |    15 |    15 |    15 |    -8 |   -13 | 
('v3', 'ReLU', 16) |    18 |    18 |    18 |    18 |   -13 |   -16 | 
('v3', 'Sigmoid', 1) |    24 |    24 |    24 |    24 |   -12 |   -16 | 
('v3', 'Sigmoid', 2) |    25 |    25 |    25 |    25 |   -17 |   -13 | 
('v3', 'Sigmoid', 4) |    36 |    36 |    36 |    36 |   -21 |   -26 | 
('v3', 'Sigmoid', 8) |    25 |    25 |    25 |    25 |   -12 |   -18 | 
('v3', 'Sigmoid', 16) |    30 |    30 |    30 |    30 |   -19 |   -22 | 