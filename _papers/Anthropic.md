---
layout: default
title: 'Anthropic Research'
img: /assets/img/logos/anthropic.png
description: Human-oriented AI company
gradient: linear-gradient(135deg, #0064e1 0%, #5bd3ff 100%)
hover-gradient: linear-gradient(135deg, #00c6fb 0%, #005bea 100%)
---

|Tag | Title | Year |
|----|----|----|
| | Values in the wild: Discovering and analyzing values in real-world language model interactions | 2025 [url](https://www.anthropic.com/research/values-wild) |
| | Progress on Attention [url](https://transformer-circuits.pub/2025/attention-update/index.html) | 2025 



- QK 는 토큰이 어떤 곳을 볼지 결정한다. Head들은 서로 다른 곳을 보며, superposition hypothesis 는 그들이 독립적으로 보는 것이 아니라 다 같이 보는 것을 나타낸다. (Progress on Attention)
- OV에서는 value 에 대한 값의 변환이 이루어진다. Value들을 여러 key 들에서 모아서 섞는 연산을 진행하는 것이다. (Progress on Attention)
- Head loading vectors는 특정 개념을 전달할 때, 각 헤드들이 얼마나 기여하는지 측정한 벡터이다 (합을 1로 하면 좋을 듯)